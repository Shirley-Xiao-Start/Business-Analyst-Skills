---
name: gherkin-bdd-writer
description: Takes any requirement description, meeting note, user-story draft or code file and runs a structured analysis (feature / user stories / roles / acceptance criteria / business rules / expected outcome / edge cases / preconditions), then delivers an ambiguity critique with a revised input, and finally produces a BDD-compliant Gherkin script. Use this whenever the user says "write acceptance criteria", "acceptance criteria", "Gherkin", "Given When Then", "BDD", "turn this requirement into a feature", "write use case / edge case", "break down JIRA acceptance conditions", or "structure this requirement for me". Typical requests include "write acceptance criteria for this BA story", "turn this requirement into Gherkin", and "list the edge cases for this use case".
---

# Gherkin BDD Writer

This skill solves one specific pain: **the business side hands over prose, while developers need executable descriptions of behaviour**. That translation is currently manual, and manual translation is exactly where edge cases get lost.

The work has four steps and **none of them is optional** -- step two (the ambiguity critique) is the step most often skipped and the most valuable. Without it, the Gherkin you produce simply carries the original's vagueness straight into Given/When/Then.

## Input handling

- The user pastes text -> use it directly
- The user gives a file path (`.md` / `.docx` / `.txt` / `.feature`) -> read it first
- The user gives a JIRA or requirement ID -> ask for the content, or ask them to paste it
- The input is already complete (Feature and Scenarios exist) -> shorten step one and spend the effort on the critique and the edge cases

## Output structure

Use exactly these four parts, and **keep the XML tags** -- that makes the output reliably parseable by scripts or downstream tools, and lets the user copy the whole block into a requirements document.

### 1. Echo the input

```
<user_input>
{the user's original text}
</user_input>
```

Copy it character for character. **Only a faithful echo gives the later critique any ground to stand on** -- if you quietly polish the original, the user cannot see what is being criticised.

### 2. Structured analysis

```
<analysis>
a) Feature Description: one-sentence description of the feature
b) User Stories or Requirements: the extracted user stories or requirement items
c) User Roles: the roles involved
d) Acceptance Criteria: explicit acceptance criteria
e) Business Rules: stated or implied business rules and constraints
f) Expected Outcome: the expected result once implemented
g) Possible Edge Cases: potential boundary and exception scenarios
h) Preconditions: relevant preconditions
</analysis>
```

**(g) Edge cases** deserves extra effort. Absence from the source does not mean absence in reality -- zero amounts, empty fields, two people editing the same record concurrently, an upstream system timing out, a time-zone date rollover, duplicate submission. Write them out so the business side can confirm "do we care about this one?".

### 3. Ambiguity critique and revision

```
<critique_and_revision>
a) Point out the ambiguity, inconsistency or missing information in the source
b) Provide a revised version of the input that resolves those issues and is clearer
</critique_and_revision>
```

Criticism must **name names**: not "this requirement is somewhat vague", but "'handle promptly' is unquantified -- confirm whether it means T+0 or T+1, and whether trading days are distinguished from calendar days". Follow each criticism with a concrete question, so the business side can answer item by item.

The revision is a **proposal, not a fact**. Where the missing information involves a business decision (say, simple versus compound interest), do not turn a guess into a definite value. Mark it in the revision as `[TO CONFIRM: ...]`.

### 4. Gherkin script

```
<gherkin_syntax>
Feature: ...
</gherkin_syntax>
```

## Gherkin writing rules

These decide whether the script can be consumed directly by automation tooling:

- **One Scenario, one behaviour.** Title it with a third-person statement of the behaviour ("Login succeeds when credentials are correct"), not "Test login 1".
- **Given describes an existing state only**, never an action. `Given the user clicks the login button` is wrong -- that is a When.
- **When should carry a single trigger.** Two Whens usually mean this is two Scenarios.
- **Then states only observable, verifiable results.** Avoid implementation detail such as "the system sets an internal flag to true".
- **And / But continue the same semantic category.** An And inside a Given block is still a state; an And inside a Then block is still a result.
- **Background holds only the Givens shared by every Scenario** -- never a When or a Then.
- **Scenario Outline + Examples** for multiple data sets of one behaviour. Do not clone five Scenarios to achieve it.
- **Data tables beat long enumerations**: `| field | value |` is far clearer than "the user's email is a, phone is b, tier is c".
- **One language throughout**: the keywords (Feature / Scenario / Given / When / Then / And / Background / Examples) stay in English, and the prose stays in a single language -- no mixing.
- **Business language, not technical jargon.** Write "the user submits a login request", not "calls POST /api/login".

### Positive example

```gherkin
Feature: User login
  As a registered user
  I want to log in with my email and password
  So that I can access my account data

  Background:
    Given an activated account "shirley@example.com" exists in the system

  Scenario: Login succeeds when credentials are correct
    When the user enters the correct email and password
    Then the system navigates to the account overview page
    And the user's display name appears in the top right corner

  Scenario: Login is rejected when the password is wrong
    When the user enters the correct email and an incorrect password
    Then the system stays on the login page
    And it displays "Email or password is incorrect"
    And the account's consecutive failure count increases by 1

  # Business rule: 5 consecutive failures lock the account for 30 minutes
  Scenario Outline: Messages at different stages of consecutive failure
    Given the account has already failed to log in <prior_failures> times consecutively
    When the user enters an incorrect password again
    Then the system displays "<message>"

    Examples:
      | prior_failures | message                                    |
      | 2              | Email or password is incorrect             |
      | 4              | Email or password is incorrect             |
      | 5              | Account locked, please retry in 30 minutes |
```

### Common mistakes

- One Scenario cramming login, checkout and refund together
- Five unrelated results stacked into a single Then, so a failure cannot be localised
- An input action appearing inside a Given
- Using "Test the XX feature" as a Scenario title -- that describes a testing activity, not system behaviour
- A long natural-language sentence packed into one step: "When the user completes the form and ticks the agreement and clicks submit" -- split it, or use a data table

## Saving

- The user wants `.md` -> keep all four parts intact
- The user wants `.feature` -> write only the contents of `<gherkin_syntax>`: pure Gherkin starting with `Feature:`, no Markdown decoration
- The user did not ask for a file -> output in the conversation; do not create files unbidden

## Original instruction (verbatim archive)

The original version required: present `<user_input>` first, then `<analysis>` across items a)-h), then `<critique_and_revision>`, then generate `<gherkin_syntax>` following BDD best practice (including Feature, Background where applicable, Scenario(s), Given/When/Then). It asked for natural language, no technical jargon, behaviour described from the user's perspective, and consistent language and structure throughout. The text above implements that requirement in full and adds worked examples plus rule detail.
