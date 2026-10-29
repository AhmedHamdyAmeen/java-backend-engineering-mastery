# BEG-034 · Files and I/O — Exercises and lab

## Lab
### BEG-034-LAB1 · Contacts persistence
**Outcomes:** 1–4 · **Time:** ~2 h
Save contacts to CSV on exit and load them on start. Survive a missing or corrupt file. Use UTF-8 and relative paths.
**Acceptance:** data survives restarts; bad lines reported, not fatal.

## Exercises (assessment: three exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-034-EX01 | 1, 2 | Create a `data` folder if missing, write three lines to `data/notes.txt`, read them back and print them with line numbers. |
| BEG-034-EX02 | 2, 4 | Write a method that copies a text file line by line with `BufferedReader` and `BufferedWriter` in try-with-resources, printing a clear message on `IOException`. |
| BEG-034-EX03 | 3 | Explain when to use a byte stream vs a character stream, and what goes wrong if the encoding differs between writing and reading. |

## Solutions
- **EX01** `Files.createDirectories(Path.of("data"));` `Files.write(p, List.of("a","b","c"));` then `List<String> ls = Files.readAllLines(p); for (int i=0;i<ls.size();i++) System.out.println((i+1)+": "+ls.get(i));`
- **EX02** `try (var in = Files.newBufferedReader(src); var out = Files.newBufferedWriter(dst)) { String l; while ((l = in.readLine()) != null) { out.write(l); out.newLine(); } } catch (IOException e) { System.out.println("Copy failed: " + e.getMessage()); }`
- **EX03** Byte streams for binary data (images, archives); character streams for text. Different encodings produce garbled characters (for example Arabic letters turn into symbols), so always use UTF-8 explicitly.
- Outcome 4 (always close) is also checked by the lab and quiz Q09.
