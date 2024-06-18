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

7. The basic aim of this structure business is to allow insertion/removal of bytes from a file without causing damage to its meaning. Say we remove a byte from an ELF file. This means all offsets after that byte are now pointing one byte further than where they should, which will lead to execution errors. The tool must automatically update the offsets to allow proper execution, or preserve file semantics in general.
8. The tool must provide a model of any file as a graph of various chunks (structures) pointing to various other chunks (structures). This way, the graph can be used to re-construct the file (theoretically speaking) with proper offsets.

> While structures will require further analysis, so far nested sub-structures are not allowed. Languages such as C allow a structure data member to be of another structure type, but when recursively expanded, all primitive data members are either data bytes or pointers. The aim here is to auto-update the pointers, not to provide semantics of the data bytes.

9. The tool must be able to work with arbitrarily large files that are under 20GB in size (this number is just to provide a near-infinite ceiling; bottom line is, work normally with large files).
10. The tool must provide common hex editor features such as search for sub string, jump to offset, _change the active structure config_, jump to next search result, search for a specified sequence of bytes, replace a specified sequence of bytes (with possibly more or less or equal number of bytes), copying and pasting, internal clipboard (separate from the device clipboard). See [this](https://linux.die.net/man/1/hexedit) list for the usual commands expected.
11. The tool should allow opening a file in view-only mode. In this mode, only the non-editing features should be available.
12. Installing the tool must be simple, easy even for complete beginners. Running the tool must also be straightforward, including the command line args.
13. Manual docs must be made available for the tool. Also, hints should be provided for keyboard commands.
14. The tool must have focus on endianness. Its possible that in a little endian file, a user wants to search for a number that they specified in big endain format. I.e., the user may want to find `2A3DAA` but this may be stored as `AA 3D 2A 00 00 00 00 00`.
15. A byte can only be in one structure. Structures cannot overlap. All bytes need to be in exactly one structure.
16. Structures can have varying sizes based on values of data members. I.e., the same structure can have different byte sizes based on one of its data members.
