# BEG-034 · Files and I/O — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a filing cabinet: paths are the drawer and folder labels, readers and writers are the clerk who fetches and files pages.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-034-L01 · Paths and the Files API (10 min)
**Goal:** point at files and check they exist.

**Key points**
- `Path` describes a location; it does not mean the file exists.
- Create: `Path p = Path.of("data", "contacts.csv");`.
- Resolve: `dir.resolve("file.txt")` joins paths with the right separator.
- Use relative paths (like `data/contacts.csv`); hard-coded absolute paths break on other machines.
- `Files.exists(p)`, `Files.createDirectories(dir)`, `Files.delete(p)`, `Files.size(p)`.

**Show**
```java
Path dir = Path.of("data");
Files.createDirectories(dir);
Path file = dir.resolve("contacts.csv");
System.out.println(Files.exists(file));
```

**Check:** Does creating a `Path` create a file? *(No.)*

---

## BEG-034-L02 · Reading and writing text (12 min)
**Goal:** read and write small text files in one line.

**Key points**
- `Files.readAllLines(path)` returns a `List<String>`.
- `Files.readString(path)` returns the whole text.
- `Files.writeString(path, text)` and `Files.write(path, lines)` write.
- By default writing replaces the file; pass `StandardOpenOption.APPEND` to add.
- These methods throw `IOException`, a checked exception. Handle it.
- Fine for small files; for large ones read line by line.

**Show**
```java
try {
    List<String> lines = Files.readAllLines(file);
    Files.writeString(file, "hello\n");
} catch (IOException e) {
    System.out.println("File problem: " + e.getMessage());
}
```

**Check:** What does writing do to an existing file by default? *(Replaces its content.)*

---

## BEG-034-L03 · Streams, readers, and buffering (12 min)
**Goal:** read big files line by line and know the I/O types.

**Key points**
- A byte stream (`InputStream`, `OutputStream`) moves raw bytes: images, PDFs.
- A character stream (`Reader`, `Writer`) moves text.
- Buffering reads or writes in big chunks, which is much faster.
- `BufferedReader` gives `readLine()`; `BufferedWriter` gives `write` and `newLine()`.
- Always use try-with-resources so the file closes.

**Show**
```java
try (BufferedReader r = Files.newBufferedReader(file)) {
    String line;
    while ((line = r.readLine()) != null) {
        System.out.println(line);
    }
}
```

**Check:** Which type reads raw bytes? *(`InputStream`.)*

---

## BEG-034-L04 · Character encoding (UTF-8) (6 min)
**Goal:** avoid garbled text.

**Key points**
- Encoding is the rule that turns characters into bytes.
- UTF-8 handles every language, including Arabic and emoji.
- Reading with a different encoding than writing gives strange symbols.
- The `Files` text methods use UTF-8 by default; still, state it when using classes like `FileReader`, to avoid platform-default surprises.
- Rule: always UTF-8, and say so.

**Show:** `Files.readAllLines(p, StandardCharsets.UTF_8)` and the same text decoded as another charset looking garbled.

**Check:** Which encoding should be your default? *(UTF-8.)*

---

## BEG-034-L05 · A simple CSV format (5 min)
**Goal:** store records as text lines.

**Key points**
- CSV: one record per line, fields separated by commas.
- Write: `String.join(",", name, phone, email)`.
- Read: `line.split(",", -1)` keeps empty trailing fields.
- A field containing a comma breaks this simple format. Real CSV quotes such fields; later you will use a library.
- Validate each line: wrong field count means a bad line.

**Show**
```
Ana,0501112222,ana@example.com
Omar,0503334444,
```

**Check:** What goes wrong if a name contains a comma? *(The line splits into too many fields.)*

---

## BEG-034-L06 · Demo: saving and loading contacts as CSV (8 min)
**Goal:** persist contacts. Prepares `BEG-034-LAB1`.

**Steps**
1. Write `save(List<Contact>, Path)` that builds lines and calls `Files.write`.
2. Write `load(Path)` that returns an empty list if the file does not exist.
3. Parse each line; count and report bad lines instead of crashing.
4. **Planned mistake:** use an absolute path such as `C:\data\contacts.csv`; switch to a relative path built with `Path.of`.
5. Run twice to show data survives a restart.
