---
title: Programming Languages
weight: 10
---

## Supported Programming Languages

Around 90 Programming Languages are supported by Notepad++:

|                       |                        |                        |                        |                       |
|-----------------------|------------------------|------------------------|------------------------|-----------------------|
|ActionScript           | Ada                    | ASN.1                  | ASP                    | Assembly              |
|AutoIt                 | AviSynth               | BaanC                  | Batch                  | BlitzBasic            |
|C                      | C#                     | C++                    | CAML                   | CMake                 |
|COBOL                  | CoffeeScript           | Csound                 | CSS                    | D                     |
|Diff                   | Erlang                 | ESCRIPT                | Forth                  | Fortran fixed form    |
|Fortran free form      | FreeBasic              | GDScript               | Gui4Cli                | Haskell               |
|Hollywood              | HTML                   | ini                    | Inno Setup             | Intel HEX             |
|Internal Search        | Java                   | JavaScript             | JavaScript             | json                  |
|json5                  | JSP                    | KiXtart                | LaTeX                  | Lisp                  |
|Lua                    | Makefile               | MATLAB                 | MMIXAL                 | mssql                 |
|NFO                    | Nim                    | Nncrontab              | NSIS                   | Objective-C           |
|OScript                | Pascal                 | Perl                   | PHP                    | PostScript            |
|PowerShell             | Properties file        | PureBasic              | Python                 | R                     |
|RC                     | REBOL                  | registry               | Ruby                   | Rust                  |
|S-Record               | Scheme                 | Shell                  | Smalltalk              | Spice                 |
|SQL                    | Swift                  | TCL                    | Tektronix extended HEX | TeX                   |
|txt2tags               | TypeScript             | Verilog                | VHDL                   | Visual Basic          |
|Visual Prolog          | XML                    | YAML                   |                        |                       |

For these languages, Notepad++ supports [syntax highlighting](../preferences/#style-configurator) (customizable),
syntax folding, [auto-completion](../auto-completion/) (customizable),
[function list](../function-list/) (customizable via PCRE in xml file).

If your beloved language is not in the list above, you can define it yourself easily, by using the
[User Defined Languages System](../user-defined-language-system/).  If that doesn't meet your needs,
you could write (or have someone else write) a [lexer plugin](../plugins/#building-a-lexer-plugin).

Please note that in Notepad++ v8.3 and newer, Notepad++ has a feature will no longer perform syntax highlighting
on files that are over 200MB -- this prevents extreme performance slowdown caused by trying to
syntax highlight extremely large files.  This threshold is configurable in
[Settings > Preferences > Performance](../preferences/#performance) (starting in v8.4.7).

## Language Detection Priority

When opening an existing file, Notepad++ has an algorithm for trying to decide which language a given file is, with the following priorities:

1. A language defined at the [command line using `-l`](./command-prompt) is applied.
2. If the file is in the active [session file](session/) (the automatic `session.xml` or a manually-controlled session), it will use the language stored in that session.
3. If the file extension is a "known extension" (whether it's from the [Style Configurator](../preferences/#style-configurator)'s default extension list [in `langs.xml` or `langs.model.xml`] or user-defined extension list [from `stylers.xml` or `themes\<ThemeName>.xml`] for a built-in language, or the [User Defined Language](../user-defined-language-system/)'s extension settings [from `userDefineLang.xml` or `userDefineLangs\<UDLName>.xml`]), Notepad++ will use that language.
4. If the filename matches one of a few specific names, Notepad++ knows what language they should be:

    filename | language
    ---|---
    `makefile` | Makefile
    `GNUMakefile` | Makefile
    `CMakeLists.txt` | CMake
    `SConstruct` | Python
    `SConscript` | Python
    `wscript` | Python
    `Rakefile` | Ruby
    `Vagrantfile` | Ruby
    `crontab` | Shell Script
5. If the first line in the file gives a known hint as to the file type, it will use that.  This includes "prolog lines" starting with `<?xml` or `<?php` or `<html` or `<!DOCTPE html` or `<?`, or linux-style "shebang" lines like `#!/usr/bin/bash` which are looking for `sh` or `python` or `perl` or `php` or `ruby` or `node` to define the correct language.
6. It will use the default language only if none of the other rules have matched[.](# "There was a bug through v8.4.6 that made the default language apply on files without extensions, even if the first-line rule had already matched")

As Notepad++ goes through that list in order, it will stop as soon as it finds a matching language for the file.  And after Notepad++ has made its detection, you can override what it chose by using the **Language** menu (and when a session gets saved, the language will remember whatever language is currently active for that file for next time, as described in priority 2).

If you do a **Save As** on a file, it will use that same sequence for deciding the language, based on the new name and file contents.

Newly-created documents will assume the default language until they are saved.
