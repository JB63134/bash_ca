
# ca – Bash Command Analyzer

**ca** is an advanced Bash command analysis tool that inspects commands, aliases, builtins, keywords, functions, text executables, and external binaries. Instead of relying on multiple tools (type, which, command -V, declare, alias, etc.), ca unifies all resolution logic into a single command analysis engine.



---

[![MIT License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.38-blue)](https://github.com/JB63134/bash_ca/releases) 
   
Package Lookup: supports dpkg, rpm, and pacman 

---

## Features

* **Syntax-highlighting** of scripts and functions
* Inspect **aliases and functions**:

  * show alias definition or function body
  * location (file and line number, or interactive shell)
* Inspect **builtins**:

  * Detect if the builtin is enabled
  * Detect whether it is a core builtin or loadable.
* Inspect **external binaries**:

  * Displays the full resolved path and alerts you of symlinks
  * Detects shadowed binaries
  * File type (script, ELF, etc.)
  * Interpreter for scripts
  * list Dependencies and detect missing dependencies
  * File size
  * Permissions and ownership
  * SUID/SGID bits
  * Timestamps
  * Root privilege requirement
 
* Display **Package info**:

  * package name
  * version
  * maintainer info
  * package description
* Detect **overrides**:

  * Aliases overriding builtins or files
  * Functions overriding aliases, builtins, or binaries
  * Disabled builtins and their replacements
* Scan your system for:

  * **SUID / SGID binaries**
  * **World-writable directories**
  * Writable directories in `$PATH`
  * Recursivly detect **Sourced files** in the enviroment
* Interactive search using `fzf` for commands (optional)
* Pretty-printed, colorized output (uses `tput` or ANSI colors)

---

## Installation

Clone the repository and source the script in your `.bashrc` or `.bash_profile`:

```bash
git clone https://github.com/yourusername/ca.git
source /path/to/ca/.bash_ca
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

## Screenshots / Output Preview

![Source and $Path modes](images/source-path.png)
![Overridden commands](images/override.png)
![Builtins and Keywords](images/builtin-keyword.png)
![binry](images/awk.png)
![Script](images/script.png)
![World-Writable file](images/world-writable.png)
![SGID](images/sgid.png)
![SUID](images/suid.png)
![Scan mode](images/scanmode.png)

---





