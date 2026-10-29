# BEG-049 · Relational modeling — Quiz

Outcomes: O1 tables and columns · O2 keys · O3 relationships · O4 normalization.

**Q01 (O1)** In a table, one row represents: A. One column B. One instance of the entity C. The schema D. A database
**Q02 (O1)** Which is the best type for a birth date? A. `date` B. `integer` C. `boolean` D. `text` with commas
**Q03 (O2)** A primary key must be: A. Unique and not empty B. The person's name C. Changeable D. Optional
**Q04 (O2)** A foreign key is: A. A password B. A second primary key in the same row C. A column pointing to another table's key D. A table name
**Q05 (O3)** One author, many books: where does the FK go? A. `authors` B. `books` C. A third table always D. Nowhere
**Q06 (O3)** Many-to-many needs: A. A comma-separated column B. Duplicate rows C. Two primary keys in one row D. A junction table
**Q07 (O3)** A column holding "java,sql,web" breaks: A. 1NF B. 3NF only C. Nothing D. Types only
**Q08 (O4)** 3NF means columns depend on: A. Any other column B. The key and nothing else C. Only the first column D. The table name
**Q09 (O4)** Changing one phone number in many rows is an: A. Insert anomaly B. Delete anomaly C. Update anomaly D. Index
**Q10 (O4)** Normalization mainly: A. Removes duplicated facts B. Adds duplicates C. Deletes tables D. Speeds up Java

## Answers
Q01 B · Q02 A · Q03 A · Q04 C · Q05 B · Q06 D · Q07 A · Q08 B · Q09 C · Q10 A

## Practical part
Assessment: normalize a provided spreadsheet to 3NF (EX06) plus the library ER diagram lab. Pass: at least 8 of 10 quiz questions and a correct 3NF result.
