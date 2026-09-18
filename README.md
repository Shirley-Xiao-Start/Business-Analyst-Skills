This skill suite empowers Business Analysts to author FRDs/PRDs/user stories and generate diagrams efficiently. 
Below is a step-by-step guide for usage within VS Code.

### How to Use

1. Install the ClaudeCode extension in VS Code.
2. Download all BA skill files and place them into your ClaudeCode skills folder, for example: `C:***\Claudecode.claude\skills`
3. In the ClaudeCode chat box, navigate to `/mermaid-diagrammer` or any other available skill.
4. Enter your prompt, for example:
> please draw a diagram for a login process
5. Create a new file with the `.mmd` extension, paste all the generated code and save the file.
6. Install the **Markdown Preview Mermaid Support** plugin in VS Code. Press `Ctrl+Shift+P`, search and select `Mermaid: Preview Diagram` to view your diagram.

### Quick Tips

- For Mermaid diagrams:
Plugin: *Markdown Preview Mermaid Support* | File suffix: `.mmd`
Shortcut: `Ctrl+Shift+P` → `Mermaid: Preview Diagram`
- For PlantUML sequence diagrams:
Plugin: *PlantUML* | File suffix: `.puml`
Shortcut: `Ctrl+Shift+P` → `Preview Current Diagram`
