# Windows Registry (.reg) Syntax Highlighting

A VSCode extension providing accurate syntax highlighting for Windows Registry `.reg` files.

## Features

- **Registry hives** — `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, etc. colored distinctly from the path
- **Key paths** — subkey path segments styled separately from the hive root
- **Key deletion** — `[-HKEY_...]` styled as a delete operation
- **Value names** — `"MyValue"=` colored distinctly from the data that follows
  - Numeric names (`"3"=`, `"15"=`) recognized separately
  - GUID names (`"{7A53B94A-...}"=`) recognized separately
  - Default value (`@=`) styled as a language keyword
- **Data types**
  - `REG_SZ` — string data with escape sequence and `%ENV_VAR%` highlighting
  - `REG_DWORD` — `dword:` keyword + hex value
  - `REG_QWORD` — `hex(b):` keyword + hex bytes
  - `REG_BINARY` / `REG_MULTI_SZ` / `REG_EXPAND_SZ` — `hex`, `hex(2)`, `hex(7)`, etc. with byte-level highlighting
  - Multi-line hex continuation lines highlighted correctly
- **Comments** — `;` line comments, including inline comments after values
- **Value deletion** — `"Name"=-` styled as a delete operation

## Installation

### From VSIX (releases)
1. Download the `.vsix` from the [Releases](../../releases) page
2. In VSCode: `Extensions` → `...` → `Install from VSIX...`


## Example

```reg
Windows Registry Editor Version 5.00

; Set shell icons
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons]
"3"="%SystemRoot%\\system32\\imageres.dll,-178"
"4"="%SystemRoot%\\system32\\imageres.dll,-178"

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Shell Extensions\Blocked]
"{7A53B94A-4E6E-4826-B48E-535020B264E5}"=""

[HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Accent]
"AccentPalette"=hex:64,64,64,00,6b,6b,6b,00,\
  00,00,00,00,00,00,00,00
"StartColorMenu"=dword:00000000

; Remove a value
"OldValue"=-

; Delete a key
[-HKEY_LOCAL_MACHINE\Software\OldApp]
```
