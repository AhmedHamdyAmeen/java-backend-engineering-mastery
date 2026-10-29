# BEG-034 · Files and I/O — Quiz

Outcomes: O1 Path and Files · O2 reading and writing text · O3 byte vs character streams, encoding · O4 errors and closing.

**Q01 (O1)** Creating a `Path` object: A. Creates the file B. Deletes the file C. Opens the file D. Only describes a location
**Q02 (O1)** Check whether a file exists: A. `Files.exists(path)` B. `path.exists()` C. `Files.has(path)` D. `Path.check()`
**Q03 (O1)** Which path style travels well between computers? A. `C:\Users\me\data.csv` B. `/home/me/data.csv` C. A relative path such as `data/contacts.csv` D. A URL only
**Q04 (O2)** `Files.readAllLines(path)` returns: A. A `String` B. A `List<String>` C. A `byte[]` D. A `Path`
**Q05 (O2)** `Files.writeString(path, text)` by default: A. Appends B. Fails if the file exists C. Writes nothing D. Replaces the file content
**Q06 (O2)** `BufferedReader` is useful because it: A. Reads bytes only B. Encrypts files C. Reads in chunks and has `readLine()` D. Deletes lines
**Q07 (O3)** Raw binary files such as images are best handled with: A. Byte streams B. `Reader` C. `String` D. `Scanner`
**Q08 (O3)** The recommended text encoding is: A. ASCII B. Platform default C. Random D. UTF-8
**Q09 (O4)** The safest way to ensure a file is closed: A. Hope for the best B. `System.gc()` C. try-with-resources D. Call `close()` only on success
**Q10 (O4)** `IOException` is: A. A checked exception B. Unchecked C. An `Error` D. A warning

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 D · Q06 C · Q07 A · Q08 D · Q09 C · Q10 A

## Practical part
Three exercises `BEG-034-EX01` to `EX03` plus the lab. Pass: all three exercises correct and the lab survives a missing file and a corrupt line.
