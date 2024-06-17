# hex-editor

## Requirements

1. There is a need to build a software tool that can display any file in binary, using hexadecimal digits for bytes and also where possible, the relevant ASCII/EBCDIC/Extended ASCII-encoded characters.
2. The tool should allow editing files in binary mode, using atleast the following basic operations:
   1. Changing a byte
   2. Deleting a byte
   3. Inserting a byte
3. The tool must allow specification of a byte either via hex digits, or via the relevant character from the currently used character set (ASCII/EBCDIC/Extended ASCII).
4. The tool must be accessed from the terminal. It should be a CLI tool.
