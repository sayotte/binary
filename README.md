[![Build Status](https://travis-ci.org/sayotte/binary.svg?branch=master)](https://travis-ci.org/sayotte/binary)

# binary
Package binary is a replacement for the Go-standard encoding/binary, replacing only the function binary.Read(). The replacement function returns the number of bytes read in addition to an error. The rest of its behavior is identical to that of the original, by virtue of being a slightly modified cut/paste of the original code from Go-1.7.4 .

**Don't use this package.** Do this instead:
```
type readCounter struct {
    reader io.Reader
    offset int
}

func (rc *readCounter) Read(buf []byte) (int, error) {
    off, err := rc.reader.Read(buf)
    rc.offset += off
    return off, err
}

func readAndCount(innerReader io.Reader, obj *MyObjType) (int, error) {
    rCtr := readCounter{reader: innerReader}
    err := binary.Read(rCtr, binary.BigEndian, obj)
    return rCtr.offset, err
}
```
