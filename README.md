# `ca` — A Bash Command Analyzer

[![MIT License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.25-blue)](https://github.com/JB63134/bash_ca/releases) 

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


**Advantages to using ca**
 
1. Shell introspection
`type` – identify if a command is a builtin, alias, function, or external command
`command` – get command resolution info
`alias `– show alias definitions
`declare` – show function definitions
`builtin` – check if a command is a shell builtin
`hash` – detect overridden commands
ca advantage: Shows aliases, functions, builtins, and external commands together, including nested aliases/functions and depth-limited recursion.

2. Binary / script inspection
`which` – locate binaries in $PATH
`file` – detect file type (script, ELF binary, etc.)
`readlink` / realpath – canonical path resolution and symlink chains
`stat` – permissions, ownership, timestamps
`getcap` – POSIX capabilities on binaries
`ldd` – list dynamic library dependencies
ca advantage: Combines path resolution, ELF info, permissions, symlinks, capabilities, and dependencies in one view, which usually requires 5+ commands.

3. Package / system info
`dpkg` (Debian based distributions) – find which package a file belongs to and its info
ca advantage: Displays package info alongside binary metadata without switching tools.

4. Script / function source
`head` – quickly see shebang
`cat` / `less` – inspect script contents
`declare` – function bodies
ca advantage: Shows full source with line numbers, including alias and function definitions, plus optional syntax highlighting.

5. Security / audit checks
`find` `ls` – search for SUID/SGID or world-writable files
`echo $PATH` + manual inspection – check writable dirs in $PATH
`hash` / `type` – detect overridden commands
ca advantage: Automates SUID/SGID world-writable search, writable $PATH directories, and overridden command detection, which normally requires multiple commands and scripting.

✅ Summary
In short: ca is a single, unified replacement for 15–20 commands, giving developers and sysadmins a much faster, one-command inspection tool.
