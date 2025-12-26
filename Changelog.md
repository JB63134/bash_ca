# `bash_ca` Changelog

## V1.1.0
- UI/UX cleanup
- Sourced file detection now shows the order files are sourced
- New variable modes:
  - `-l` / `--listenv` – list all system variables (`printenv` / `env`)
  - `-var` – list all variables loaded by sourced files

## V1.0.85
- UI/UX improvements
- `-p` now marks missing PATH directories instead of ignoring them
- Redundant notifications in overrides stopped

## V1.0.82
- UI/UX improvements
- Wording and display fixes

## V1.0.81
- Added `-d` / `--diff` for shell options to show deviations from defaults

## V1.0.80
- UI/UX improvements
- Trace mode bugs fixed (shadowed functions reliably found)
- Depth count for recursion control fixed

## V1.0.77
- UI/UX improvements
- Trace mode fixes for shadowed builtins

## V1.0.75
- New **Command Resolution Trace**
  - Shows Bash command resolution order
  - Highlights shadowing (e.g., alias overriding a builtin)
- PATH code refinement

## V1.0.72
- Removed heuristic threat assessment (`--t`) – now sticks to defensible facts
- Alias flag `-a` enumerates all aliases
- Function flag `-f` enumerates user functions
- Verbose function flag `-fv` enumerates all functions in the environment

## V1.0.71
- Added clickable file hyperlinks for aliases, functions, and scripts (terminals supporting hyperlinks: iTerm2, Kitty, GNOME Terminal)

## V1.0.70
- New heuristic threat assessment option `-t`
  - Scans SUID, SGID, and world-writable directories

## V1.0.51
- New function to generate hashes of aliases, functions, binaries, and scripts

## V1.0.50
- Improved handling of Bash operators, pipeline symbols, redirections during recursion

## V1.0.48
- Fixed alias expansion problems
- Code cleanup (ShellCheck passed)

## V1.0.45
- Recursive alias expansion improvements (some command operators supported)
- UI fixes

## V1.0.39
- Fixed variable expansion issues (ShellCheck passed)

## V1.0.38
- Major overhaul of sourced file detection:
  - Handles nested sourced files, conditional sourcing
  - Follows Bash internal logic for startup files
  - Detects RHEL/Fedora and adds `profile.d/*sh` for interactive non-login shells

## V1.0.32
- RPM and Pacman support fixed
- Nix support dropped temporarily

## V1.0.30
- Experimental support for RPM, Pacman, and Nix package managers

## V1.0.28
- Fixed dependency check issues

## V1.0.27
- Limited preview of scripts/functions to 50 lines

## V1.0.25
- Code cleanup (ShellCheck passed)

## V1.0.19
- Added `batcat` highlighting with fallback to Perl
- Fixed `$PATH` code for `-p` mode
- UI bug fixes

## V1.0.15
- Code cleanup and UI bug fixes
- Display `$PATH` shadowing for external binaries

## V1.0.12
- Code cleanup and UI bug fixes
- Consolidated PATH manipulation code
- PATH restoration handled with a trap on return

## V1.0.7
- Enhanced `<TAB>` completion and PATH detection
- Code cleanup

## V1.0.5
- Switched to Perl for highlighting instead of sed
- Fixed executable detection code

## V1.0.0
- First independent version (split from `bash_h`)
