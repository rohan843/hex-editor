# hex-editor

## Requirements

1. There is a need to build a software tool that can display any file in binary, using hexadecimal digits for bytes and also where possible, the relevant ASCII/EBCDIC/Extended ASCII-encoded characters.
2. The tool should allow editing files in binary mode, using atleast the following basic operations:
   1. Changing a byte
   2. Deleting a byte
   3. Inserting a byte
3. The tool must allow specification of a byte either via hex digits, or via the relevant character from the currently used character set (ASCII/EBCDIC/Extended ASCII).
4. The tool must be accessed from the terminal. It should be a CLI tool.
5. The tool must be portable across OSes. Specifically, it should be portable across linux OSes, with a focus on Kali and ParrotOS (for CTFs or forensic applications).
6. The tool must have a feature to apply _structure configs_ to a file while in use. This essentially means that the tool must be able to present a file to the user based on some structure, as described in the active structure config. **There should be a default config for _no_ inherent structure, or for those cases where the structure is unknown.**

Consider an example for structure configs: ELF files have a file header structure, a program header structure, a section header structure, and various other structures. These structures give semantics to the bytes of the file. The members of these structures may be data or offset. In case some data member is an offset, it can be either unsigned, signed in 2's complement or signed in 1's complement. The offset may be from the start of the file, end of the file, starting byte of the structure, ending byte of the structure, or from some other byte.
