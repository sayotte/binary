# binary
Package binary is a drop-in replacement for the Go-standard encoding/binary, replacing the function binary.Read(). The replacement function returns the number of bytes read in addition to an error. The rest of its behavior is identical to that of the original, by virtue of being a slightly modified cut/paste of the original code from Go-1.7.4 .
