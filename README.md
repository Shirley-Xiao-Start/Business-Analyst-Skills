# Business-Analyst-Skills
The skills for BAs to write FRD/PRD/Use story/Draw Diagrams and etc， below is how to use it in VSCode.
1) Install ClaudeCode in VSCode
2) Dowload all BA skills to ClaudeCode skill folder, e.g C:\***\Claudecode\.claude\skills
3) direct to /mermaid-diagrammer or other skills in ClaudeCode chatbox
4) input: please draw a diagram for a login process
5) it will list the code for the diagram as below:
   flowchart TD
    A([Start]) --> B["Enter username & password"]
    B --> C{"Validate credentials"}
    C -- Valid --> D["Issue session token"]
    C -- Invalid --> E["Show: incorrect username or password"]
    E --> F{"Consecutive failures >= 5?"}
    F -- No --> B
    F -- Yes --> G["Lock account for 30 minutes"]
    D --> H["Redirect to home page"]
    G --> I([End])
    H --> I

    classDef ok fill:#d1fae5,stroke:#059669,color:#064e3b
    classDef err fill:#fee2e2,stroke:#dc2626,color:#7f1d1d
    classDef neutral fill:#f3f4f6,stroke:#6b7280,color:#1f2937
    class D,H ok
    class E,F,G err
    class A,B,I neutral
   
6) please create a new file ending with .mmd including all above code details, make sure you saved this file
7) Install Plugin : Markdown Preview in VSCode and press hot key " Ctrl+Shift+P" and input " Mermaid: Preview Diagram", then you can preview the diagram.
