---

# Bash Command Analyzer (ca) – Threat Semantics Reference

This document explains the **risk classifications and primitives** used by the `ca` when scanning SUID/SGID binaries and world-writable directories.

---

## 1️⃣ Risk Classification

| Label                    | Score Range | Meaning                                                             |
| ------------------------ | ----------- | ------------------------------------------------------------------- |
| **None**                 | 0           | No practical risk detected. Binary or directory is considered safe. |
| **Low**                  | 1–4         | Minimal risk. Usually safe under normal usage.                      |
| **Interesting / Medium** | 5–7         | Potentially exploitable under certain conditions. Worth reviewing.  |
| **High / Critical**      | 8+          | Privileged escalation or attack is feasible. Review immediately.    |

> **Note:** Scores are based on *potential* abuse, not confirmed vulnerabilities. Some binaries (e.g., `sudo`, `passwd`) are hardened and may be scored high due to their nature, but are typically safe on patched systems.

---

## 2️⃣ Primitives

| Primitive           | Description                                                           |
| ------------------- | --------------------------------------------------------------------- |
| **shell**           | Binary can spawn an interactive shell.                                |
| **exec**            | Binary can execute arbitrary commands.                                |
| **user-input**      | Binary processes user-supplied data.                                  |
| **file-read**       | Binary can read files, potentially sensitive.                         |
| **file-write**      | Binary can write files, potentially overwriting important data.       |
| **env-inject**      | Binary may use environment variables in an unsafe manner.             |
| **path-hijack**     | Binary may rely on `PATH` in a way that allows command injection.     |
| **auth-impact**     | Binary affects authentication, passwords, or credentials.             |
| **group-sensitive** | SGID binary belonging to sensitive groups (e.g., `shadow`, `docker`). |
| **priv-drop**       | Binary properly drops privileges internally to reduce risk.           |
| **sticky**          | Directory has the sticky bit set, reducing world-write abuse.         |
| **runtime-dir**     | Temporary directories that are recreated on boot (`/tmp`, `/run`).    |
| **persistent**      | Directories that persist across reboots (`/var/tmp`).                 |
| **path-inject**     | Directory may allow executable path hijacking.                        |
| **symlink-attack**  | Binary or directory may be abused via symbolic links.                 |

---

## 3️⃣ Context & Notes

1. **Hardened binaries**

   * `sudo`, `passwd`, `su`, and similar are specifically hardened and not trivially exploitable. High scores reflect *potential attack surface*, not confirmed vulnerabilities.

2. **World-writable directories**

   * Sticky directories (`drwxrwxrwt`) reduce risk.
   * Non-sticky, persistent directories have higher potential for abuse.

3. **SGID binaries**

   * Belonging to sensitive groups (`shadow`, `docker`, `adm`, etc.) increases risk.
   * Privilege escalation is only feasible if the binary can be abused based on its primitives.

---

## 4️⃣ Recommended Actions

* **High/Critical**: Review binary or directory thoroughly before allowing untrusted access.
* **Medium**: Monitor usage; patch if applicable; consider restrictions.
* **Low/None**: Typically safe; no immediate action needed.

---
