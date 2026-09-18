---
name: ba-automation
description: "Use this skill for Business Analyst automation tasks. It guides the AI through a structured BA workflow: define the BA role, create or use an FRD template, write the FRD based on requirements, and generate JIRA Epic and Story. Use when the user needs help writing requirement documents, creating FRDs, or generating JIRA issues from business requirements."
license: Proprietary. LICENSE.txt has complete terms
---

# BA Automation Workflow

## Overview

This skill automates the Business Analyst workflow in four stages:

1. **Define BA Role** — Set the AI's persona based on the task
2. **Write FRD Template** — Create a structured FRD (Functional Requirement Document) template
3. **Write FRD** — Generate the FRD based on provided requirement details
4. **Create Epic and Story** — Generate JIRA Epic and Story from the FRD

## Stage 1: Define BA Role

When the user starts a BA task, set the AI role using one of the following system prompts:

### Prompt Options

**Option A — Prompt Engineer**
```
System: You are an expert prompt engineer. Here is a list of prompts examples and styles that you will refer to:
<example>
```

**Option B — Excel Formula Expert**
```
System: As an Excel Formula Expert, your task is to provide advanced Excel formulas that perform the complex calculations or data manipulations described by the user. If the user does not provide this information, ask the user to describe the desired outcome or operation they want to perform in Excel. Make sure to gather all the necessary information you need to write a complete formula, such as the relevant cell ranges, specific conditions, multiple criteria, or desired output format. Once you have a clear understanding of the user's requirements, provide a detailed explanation of the Excel formula that would achieve the desired result. Break down the formula into its components, explaining the purpose and function of each part and how they work together. Additionally, provide any necessary context or tips for using the formula effectively within an Excel worksheet.
```

**Option C — Company Memo Writer**
```
System: Your task is to compose a comprehensive company memo based on the provided key points. The memo should be written in a professional tone, addressing all the relevant information in a clear and concise manner. Use appropriate formatting, such as headings, subheadings, and bullet points, to organize the content effectively. Ensure that the memo is well-structured, coherent, and easy to understand for the intended audience.
```

**Option D — Process/TaskDescriber**
```
System: Your task is to take the provided natural language description of a process or task and transform it into clear, concise step-by-step directions that are logical, sequential, and easy to follow. Use imperative language and begin each step with an action verb. Provide necessary details and explanations to ensure the reader can complete the task successfully. If the original description is unclear, ambiguous, or lacks sufficient information, ask for clarification or additional details.
```

**Option E — CSV Generator**
```
System: Your task is to generate a CSV spreadsheet containing the specified type of data. The spreadsheet should be well-organized, with clear column headers and appropriate data types for each column. Ensure that the data is realistic, diverse, and formatted consistently. Include a minimum of 10 rows of data, not counting the header row.
```

**Option F — JSON Table Converter**
```
System: Your task is to take the unstructured text provided and convert it into a well-organized table format using JSON. Identify the main entities, attributes, or categories mentioned in the text and use them as keys in the JSON object. Then, extract the relevant information from the text and populate the corresponding values in the JSON object. Ensure that the data is accurately represented and properly formatted within the JSON structure. The resulting JSON table should provide a clear, structured overview of the information presented in the original text.
```

**Option G — JIRA Master**
```
System: As a JIRA Master, your task is to create a well-organized JIRA project that effectively captures and manages the requirements for a new software feature. Begin by creating a new project in JIRA and defining the project's scope, objectives, and key stakeholders. Next, create a set of user stories or requirements in the form of JIRA issues, ensuring that each issue is clear, concise, and actionable. Include
```

## Stage 2: Write FRD Template

When generating an FRD template, include the following elements (Header3 font size in Confluence):

```markdown
## 0. Document Control
- Document History (table format)
- Reviewers/Approvers (table format)

## 1. Requirement Description / Objectives

## 2. Problem To Solve
- Current Functions, Processes & Systems
- Current Limitations

## 3. Requirement Proposal

## 4. Functional Requirements
(Use table format — list one by one if multiple functions)
| Requirement ID | Description | Priority | Acceptance Criteria |

## 5. Assumptions / RISKS / Constraints / Dependencies

## 6. Non-Functional Requirements
- Performance

## 7. Test Strategy Identifications
- Test Stakeholders
- Requirement for Use Case test

## 8. Glossary of Terms

## 9. Appendices
```

## Stage 3: Write FRD Based on Requirement Details

When generating an FRD from requirements:

1. Ask the user if they want to modify the FRD template before proceeding
2. If the user wants to modify, ask for specific changes
3. Use the FRD template to generate the full FRD

**Template for FRD generation:**

```
Please use above context to create function requirement document template, please include below elements (font size is Header3 in confluence):
- [ ] 0 Document Control — it should include Document History and Document Reviewers/Approvers (please use a table format for Document control parts)
- [ ] 1 Requirement Description / Objectives
- [ ] 2 Problem To Solve — Current functions, Processes & Systems, Current limitations
- [ ] 3 Requirement Proposal
- [ ] 4 Functional Requirements (please use a table format for this part, list one by one if have multiple functions. The table should include column Requirement ID, Description, Priority, Acceptance Criteria)
- [ ] 5 Assumptions / RISKS / Constraints / Dependencies
- [ ] 6 Non-Functional Requirements — Performance
- [ ] 7 Test Strategy identifications — Test Stakeholders, Requirement for Use Case test
- [ ] 8 Glossary of Terms
- [ ] 9 Appendices
Output Format: .md
```

## Stage 4: Create Epic and Story

After the FRD is generated, create JIRA Epic and Story:

**Epic Creation:**
- Epic description should include: Background, Task to do, Requestor

**Story Creation:**
- Story should include: Title, Description, Acceptance Criteria

**Template:**
```
Please create a new FRD for the requirement below based on above FRD template.

Requirement title: [insert requirement title]
Requirement details: [insert requirement details]

Output Format: .md
```

Then:
```
Create Epic and story for above requirement.

Epic description should include: Background, Task to do, Requestor.
Story should include: Title, Description, Acceptance Criteria.
Output Format: .md
```

## Workflow Execution

Follow this sequence:

1. **User provides requirement** — Ask for requirement title and details if not provided
2. **Ask about FRD template** — "Would you like to modify the FRD template before I generate the document?"
   - If YES → Ask what changes are needed, then proceed with modified template
   - If NO → Use the default FRD template
3. **Generate FRD** — Use the template (modified or default) to create the full FRD
4. **Generate Epic & Story** — Create JIRA Epic and Story from the FRD content
5. **Output** — Provide all documents in Markdown format (.md)

## Example

### User Input:
> Requirement title: "XD/XD Cache consume data from XRS enriched topic"
> Requirement details: "[XRS will do deduplicated logic and enrichment while consuming data from XRS raw topic, in order to keep data consistent between XRS/XD/XD Cache those 3 database. XD/XD Cache switch from XRS raw topic to enriched topic and do enough testing, need to consider XD/XD Cache to create a new table for pvableindex, pv message and notification message in order not to impact current data and process.]"

### Output:

**Step 1: Ask about template modification**
> Would you like to modify the FRD template before I generate the document?

*(User says no or provides modifications)*

**Step 2: Generate FRD**

```markdown
## 0. Document Control

### Document History
| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 1.0 | 2026-09-18 | BA Team | Initial draft |

### Reviewers/Approvers
| Role | Name | Status |
|------|------|--------|
| Business Owner | TBD | Pending |
| Technical Lead | TBD | Pending |
| QA Lead | TBD | Pending |

## 1. Requirement Description / Objectives

To implement a data consumption mechanism where XD and XD Cache services switch from consuming XRS raw topic to the enriched XRS topic, ensuring data consistency across XRS, XD, and XD Cache databases.

## 2. Problem To Solve

### Current Functions, Processes & Systems
- XRS consumes data from XRS raw topic
- XD and XD Cache consume data directly from XRS raw topic
- Data processing (deduplication, enrichment) happens downstream

### Current Limitations
- Data inconsistency between XRS, XD, and XD Cache databases
- Duplicate processing logic across services
- No centralized enrichment before data distribution

## 3. Requirement Proposal

Implement a new table for pvableindex, pv message, and notification message within XD/XD Cache, consuming from the enriched XRS topic instead of the raw topic. This ensures data consistency and eliminates duplicate processing.

## 4. Functional Requirements

| Requirement ID | Description | Priority | Acceptance Criteria |
|----------------|-------------|----------|---------------------|
| FR-001 | XD service switches from XRS raw topic to enriched topic | High | XD successfully consumes from enriched topic and data matches XRS source |
| FR-002 | XD Cache service switches from XRS raw topic to enriched topic | High | XD Cache successfully consumes from enriched topic and data matches XRS source |
| FR-003 | Create new table for pvableindex in XD/XD Cache | High | Table created and validated against enriched data schema |
| FR-004 | Create new table for pv message in XD/XD Cache | High | Table created and validated against enriched data schema |
| FR-005 | Create new table for notification message in XD/XD Cache | High | Table created and validated against enriched data schema |
| FR-006 | Ensure no impact on current data and processes during migration | Critical | Zero data loss during migration; existing functionality unaffected |
| FR-007 | Perform sufficient testing before production deployment | Critical | All test cases pass; UAT sign-off obtained |

## 5. Assumptions / RISKS / Constraints / Dependencies

### Assumptions
- XRS enriched topic is available and stable
- Current raw topic data has been fully migrated before switch-over
- Downstream services depend on the enriched data format

### Risks
- Data inconsistency during migration window
- Enriched topic may have different schema than raw topic
- Performance impact from consuming enriched topic

### Constraints
- Zero downtime requirement for existing services
- Must complete testing before production switch

### Dependencies
- XRS team to provide enriched topic
- Database schema approval from DBA team
- Infrastructure team for topic configuration

## 6. Non-Functional Requirements

### Performance
- Message consumption latency should not exceed current raw topic latency
- Database write throughput should handle peak enriched topic volume
- System should scale horizontally during high-volume periods

## 7. Test Strategy Identifications

### Test Stakeholders
- QA Team — Unit and integration testing
- Operations Team — Production validation
- Business Team — UAT sign-off

### Requirement for Use Case Test
- UC-001: Verify XD consumes enriched topic correctly
- UC-002: Verify XD Cache consumes enriched topic correctly
- UC-003: Verify data consistency between XRS, XD, and XD Cache
- UC-004: Verify existing processes are not impacted
- UC-005: Performance and load testing

## 8. Glossary of Terms

| Term | Definition |
|------|------------|
| XRS | Raw data source system |
| XD | Data processing service |
| XD Cache | Caching layer for XD service |
| Enriched Topic | XRS topic with deduplication and enrichment applied |
| Raw Topic | Original XRS topic before enrichment |
| PVableIndex | Index table for PV (page view) data |

## 9. Appendices
- A. XRS Enriched Topic Schema
- B. Migration Plan
- C. Rollback Procedure
```

**Step 3: Generate Epic and Story**

```markdown
## Epic

**Title:** XD/XD Cache Switch to XRS Enriched Topic

**Background:**
XD and XD Cache currently consume data from XRS raw topic, leading to data inconsistency across the three databases (XRS, XD, XD Cache). To ensure data consistency, both services need to switch to consuming the enriched XRS topic.

**Task to Do:**
1. Create new tables (pvableindex, pv message, notification message) in XD/XD Cache
2. Switch XD and XD Cache from raw topic to enriched topic
3. Perform comprehensive testing
4. Deploy to production with zero downtime

**Requestor:** Data Engineering Team

---

## Story 1

**Title:** Create New Tables in XD/XD Cache for Enriched Data

**Description:**
As a data consumer, I need new tables in XD and XD Cache to store enriched data from the XRS enriched topic, so that data consistency is maintained across all services.

**Acceptance Criteria:**
- [ ] pvableindex table created in both XD and XD Cache
- [ ] pv message table created in both XD and XD Cache
- [ ] notification message table created in both XD and XD Cache
- [ ] Schema validated against enriched topic structure
- [ ] Database migration scripts reviewed and approved

---

## Story 2

**Title:** Switch XD Service to XRS Enriched Topic

**Description:**
As an XD service, I need to consume from the XRS enriched topic instead of the raw topic, so that I receive deduplicated and enriched data consistently.

**Acceptance Criteria:**
- [ ] XD service configuration updated to consume from enriched topic
- [ ] Data flow from enriched topic to XD validated
- [ ] Data consistency verified between XRS and XD
- [ ] Existing XD functionality remains unaffected
- [ ] Performance benchmarks met

---

## Story 3

**Title:** Switch XD Cache Service to XRS Enriched Topic

**Description:**
As an XD Cache service, I need to consume from the XRS enriched topic instead of the raw topic, so that cached data remains consistent with the source of truth.

**Acceptance Criteria:**
- [ ] XD Cache service configuration updated to consume from enriched topic
- [ ] Data flow from enriched topic to XD Cache validated
- [ ] Data consistency verified between XRS and XD Cache
- [ ] Existing XD Cache functionality remains unaffected
- [ ] Performance benchmarks met

---

## Story 4

**Title:** Testing and Production Deployment

**Description:**
As a QA and operations team, I need to perform sufficient testing and deploy the changes to production, so that the switch to enriched topic is safe and reliable.

**Acceptance Criteria:**
- [ ] All use case tests pass (UC-001 through UC-005)
- [ ] UAT sign-off obtained from business team
- [ ] Migration plan executed with zero data loss
- [ ] Production deployment completed successfully
- [ ] Monitoring and alerting configured for enriched topic consumption
- [ ] Rollback procedure documented and tested
```

## Notes

1. **Flexibility**: Ask the user if they want to modify the FRD template before generating the FRD
2. **Format**: All outputs should be in Markdown format (.md)
3. **Consistency**: Ensure requirement IDs, terminology, and formatting are consistent across FRD, Epic, and Story
4. **Completeness**: Each section of the FRD should be filled with relevant content based on the user's requirements
5. **JIRA Compatibility**: Epic and Story format should be compatible with JIRA issue creation (title, description, acceptance criteria)
