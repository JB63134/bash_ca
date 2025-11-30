# ca — A Buggy (But Ambitious) Bash Command Analyzer

[![MIT License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.12-blue)](https://github.com/JB63134/bash_ca/releases) 

ca is very BASH specific, and Debian specific. Should work on Debian based distributions like Ubuntu, and Linux Mint. 
  
The command resolution engine from my h function became the basis for ca.  
ca is a shell-command introspection tool that tells you what a command really is.   Instead of relying on multiple tools (type, which, command -V, declare, alias, etc.), ca unifies all resolution logic into a single command analysis engine.

🚀 Overview: Modern shells resolve commands through a layered chain: Alias → Function → Builtin → keyword → File in $PATH (Script / Binary).  ca tries to walk this chain recursively, determining the true implementation of any command while providing relevent information.

🧪 Use Cases Understand what actually runs when you type a command.   Audit scripts and wrappers in toolchains.   Debug $PATH problems.   Identify missing dependencies.   Identify SUID / capability-based escalation paths.   Identify aliases and functions that override other commands.   Identify disabled builtins that have been overridden by executables.

✨ Key Features 

🔍Command Resolution: For any given command, ca identifies: aliases, functions, builtins, keywords, external binaries, wrapper scripts, interpreted scripts and follows symlinks to find the exact thing that Bash will execute.

🧭 PATH Inspection: Displays the full resolved path and alerts you of symlinks. Can help you identify $PATH ordering issues, and overridden commands.

🔁 Recursive Analysis: (work in progress) Depth-limited to avoid infinite loops.

📜 Alias Introspection: If a command resolves to an alias, ca shows: alias definition, source file & line number (when available), recursive expansion and can alert you of aliases that shadow other files, etc.

📜 Function Introspection: ca extracts full function definition with a syntax-highlighted preview, and source file & line number (when available). Can alert you of Functions that shadow other files, builtins, etc.

📜 Script Introspection: ca identifies shebang interpreter, real file location (follows symlinks), shows syntax-highlighted preview.  Supports: bash, sh, python, perl, ruby, node, awk, sed, and any #! file.

📜 Builtin Introspection Shows: whether the builtin is enabled, whether it is a core builtin or loadable.

⚙️ ELF Binary Analysis Displays: architecture, dynamic vs static linking, ELF interpreter, (ld-linux) capabilities, SUID/SGID bits, owner & permissions, resolved real path  (follows symlinks), List all dependencies and identify missing dependencies. 

📦 Package Lookup On Debian/Ubuntu/linux-Mint systems: uses dpkg to display the package name, version,  maintainer info, and package description.

🛠️ Installation: Source .bash_ca
 
🛠️ Usage Basic: 

     ca without an argument uses history to lookup the last command ran.
     ca <command> gives you info about a specific command.
     Examples: 
     ca grep  
     ca which
     ca awk
     ca then
     ca 'sudo cp'  # output can get long, i might change this
     Analyze history references:
     ca !42 

💡 Tips Use ca when a command behaves unexpectedly. Use it to debug PATH issues or command conflicts. Use it when aliases or functions override global tools. Use it to audit your environment for security problems Or simply use it to explore Bash internals



| Feature / Scope                | `h` (Bash help)                          | `ca` (Command Analyzer)                                                                |
| ------------------------------ | ---------------------------------------- | -------------------------------------------------------------------------------------- |
| **Type detection**             | ✅ Keywords, builtins, aliases, functions | ✅ Keywords, builtins, aliases, functions                                               |
| **External commands**          | Path + --help, man, info alert            | ✅ Path, symbolic links, binary type, ELF headers, dependencies, permissions             |
| **Scripts / Functions**        | ✅ Shows content with syntax highlighting | ✅ Shows content with syntax highlighting                                               |
| **Permissions / Ownership**    | ❌                                        | ✅ Includes SUID/SGID, owner/group, octal permissions                                   |
| **Shadow / Overrides**         | ❌                                        | ✅ Detects overridden commands, shadowing                                               |
| **Dependencies / Environment** | ❌                                        | ✅ Checks missing deps, sourced files hierarchy                                         |
| **Package info**               | ❌                                        | ✅ Version, maintainer, description                                                     |
| **Interactive search**         | ✅ fzf                                    | ✅ fzf                                                                                  |
| **Ease of use**                | ✅ Tab Completion                         | ✅ Tab Completion                                                                       |
| **Focus / Use case**           | Shell-level explanation                  | Deep system/binary inspection                                                          |
