![Banner](./assets/banner.jpg)

## SecureCodeWarrior (SCW) AI Security Rules

Current version: **1.0.0**

### Overview
This repository contains security rule files designed to be used with AI-assisted developer tools such as GitHub Copilot, Cursor, Windsurf, and other context-aware coding assistants.

Each rule file defines security best practices that guide how AI tools interact with your codebase.

#### Platform-Specific Rules
- **Backend** (`backend.md`) - Server-side security practices
- **Frontend** (`frontend.md`) - Client-side security practices
- **Mobile** (`mobile.md`) - Mobile application security

#### Language-Specific Rules
- **Python** (`language-specific/python.md`) - Python-specific security practices including deserialization, cryptography, and safe coding patterns

### Purpose
AI coding assistants are powerful, but they can generate insecure or non-compliant code without proper guidance. These tools work best when contextual rules steer them toward safe, standardized output.

By embedding security-focused rule files:
- You reduce the risk of introducing insecure patterns.
- You enforce organizational coding standards at scale.
- You gain greater control over how AI tools support your team.

While these rules are not a replacement for secure development training or human code review and formal research on how best to leverage rules with AI tools are still developing, many teams report that rule files improve code consistency, reduce review burden, and provide improved "virtual guardrails" for developers.

### Usage
1. **Choose your tool(s):**  
   - [GitHub Copilot](https://github.com/features/copilot)  
   - [Cursor](https://www.cursor.sh)  
   - [Windsurf](https://windsurf.com)  
   - [Cline](https://github.com/cline/cline)
   - [Roo](https://github.com/RooCodeInc/Roo-Code)
   - [Aider](https://aider.chat/)
1. **Copy the corresponding rule file into your local project:**
   - **For Copilot:** [Add `.github/copilot-instructions.md`](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
   - **For Cursor:** [Add `.cursor/rules`](https://docs.cursor.com/context/rules)
   - **For Windsurf:** [Add `.windsurfrules`](https://windsurf.com/editor/directory)
   - **For Cline:** [Add `.clinerules`](https://github.com/cline/cline/tree/main/.clinerules)
   - **For Roo:**[Add in `.roorules`](https://docs.roocode.com/features/custom-instructions)
   - **For Aider:** [Add in `CONVENTIONS.md` and add to the `.aider.conf.yml` config file](https://aider.chat/docs/usage/conventions.html)
1. **Configure metadata if needed** to trigger the rules, either always or conditionally, depending on the tool. For example, in [Cursor](https://docs.cursor.com/context/rules#rule-structure).
2. **Update or extend rule files** to reflect your own security and development policies.
3. **Once set up**, your AI tool will automatically apply these instructions during use.

### About SecureCodeWarrior
Secure Code Warrior is a leader in developer risk management helping organizations strengthen their developer teams' security and risk management competencies. We do this by providing the world's leading agile learning platform that delivers the most effective secure coding solution for developers to learn, apply, and retain software security principles. More than 600 enterprises trust Secure Code Warrior to implement agile learning security programs and ensure the applications they release are free of vulnerabilities.For more information about Secure Code Warrior, visit [www.securecodewarrior.com](http://www.securecodewarrior.com/).

### Legal Disclaimer
Secure Code Warrior Limited (the "Company") provides its services, products, and information on an "as is" and "as available" basis. The SCW Security Rules in this GitHub repository are provided on this basis, in addition to the terms below.

To the fullest extent permitted by law, the Company expressly excludes all representations, warranties, or conditions of any kind, whether express or implied, including, but not limited to, any implied warranties of merchantability, fitness for a particular purpose, title, non-infringement, and accuracy.

The Company makes no warranty or representation that the SCW Security Rules in this repo will:
- Meet your requirements or expectations.
- Be uninterrupted, timely, secure, or error-free.
- Provide accurate or reliable results.
- Be free of viruses or other harmful components
- Be compatible with any systems and tools you have in place.

Your use of the SCW Security Rules is solely at your own risk and expense. You assume all responsibility and risk for your use of the SCW Security Rules and the results and performance thereof.

You may use or feature this work in any website, publication, presentation etc, this includes altering, enhancing the SCW Security Rules including the creation of derivative works.

You may not use the SCW Security Rules for commercial purposes without the Company's explicit permission. 

This disclaimer applies to all damages or injury caused by any failure of performance, error, omission, interruption, deletion, defect, delay in operation or transmission, computer virus, communication line failure, theft or destruction, or unauthorized access to, alteration of, or use of records, whether for breach of contract, tortious behavior, negligence, or under any other cause of action.
