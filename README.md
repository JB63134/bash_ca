# `ca` — A Bash Command Analyzer

[![MIT License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.38-blue)](https://github.com/JB63134/bash_ca/releases) 
   
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

📦 Package Lookup: supports dpkg, rpm, and pacman to display the package name, version, maintainer info, and package description. 

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




---

# ca – Bash Command Analyzer

**ca** is an advanced Bash command analysis tool that inspects commands, aliases, builtins, functions, and external binaries. It provides detailed insights about where commands are defined, how aliases expand, command help, file metadata, permissions, and even SUID/SGID or world-writable binaries on your system.

---

## Features

* Analyze **Bash commands, builtins, functions, and aliases**
* Show where a command is **defined** (file, line number, or interactive shell)
* Inspect **external binaries**:

  * File type (script, ELF, etc.)
  * Interpreter for scripts
  * Dependencies and missing libraries
  * File size
  * Permissions and ownership
  * Timestamps
  * Root privilege requirement
* Detect **overrides**:

  * Aliases overriding builtins or files
  * Functions overriding aliases, builtins, or binaries
  * Disabled builtins and their replacements
* **Recursive analysis** for aliases and functions, even in pipelines
* Scan your system for:

  * **SUID / SGID binaries**
  * **World-writable directories**
  * Writable directories in `$PATH`
* Interactive search using `fzf` for commands (optional)
* Pretty-printed, colorized output (uses `tput` or ANSI colors)

---

## Installation

Clone the repository and source the script in your `.bashrc` or `.bash_profile`:

```bash
git clone https://github.com/yourusername/ca.git
source /path/to/ca/.bash_ca
```

Optionally, add to your PATH:

```bash
export PATH="$PATH:/path/to/ca"
```

---

## Usage

```bash
ca [command]
```

If no command is provided, `ca` will analyze your **most recent command**.

### Options

| Option               | Description                                                        |
| -------------------- | ------------------------------------------------------------------ |
| `-h`, `--help`       | Show help text                                                     |
| `-v`, `--version`    | Show version information                                           |
| `-f`, `--fzf`        | Interactively search for commands (requires `fzf`)                 |
| `-s`, `--sourced`    | List all sourced files in your environment                         |
| `-o`, `--overridden` | List commands that override others                                 |
| `-p`, `--path`       | List all directories in `$PATH` and highlight writable directories |
| `-S`, `--scan`       | Scan for SUID/SGID binaries and world-writable directories         |

---
## Examples

```bash
# Analyze the last command you executed
ca

# Analyze a specific command
ca ls

# Analyze history
ca !42

# Inspect files directly
ca /usr/bin/egrep
```
---

## Screenshots / Output Preview

![Source and $Path modes](images/source-path.png)
![Overridden commands](images/overridden.png)
![Builtins and Keywords](images/builtin-keyword.png)
![binry](images/awk.png)
![Script](images/script.png)
![World-Writable file](images/world-writable.png)
![SGID](images/sgid.png)
![SUID](images/suid.png)
![Scan mode](images/scanmode.png)

---





