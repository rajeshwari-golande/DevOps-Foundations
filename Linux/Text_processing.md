# Linux Day 2 — Text Processing & Log Analysis Commands

> Goal: Build strong Linux fundamentals for Cloud, DevOps, MLOps, SRE, and FAANG/product-company interviews.

## Commands Covered

11. `grep`
12. `head`
13. `tail`
14. `less`
15. `wc`
16. `sort`
17. `uniq`
18. `cut`
19. `awk`
20. `sed`

---

# 0. Linux Pipes — Foundation

The pipe `|` sends the output of one command to another command.

```bash
command1 | command2
```

Example:

```bash
ls | grep ".txt"
```

Multiple commands can be chained:

```bash
grep "ERROR" server.log | sort | uniq
```

Think of Linux commands as small tools that can be connected together.

---

# 11. `grep`

## What is `grep`?

`grep` searches for text patterns inside files or command output.

It is extremely important for:

- log analysis
- debugging
- configuration files
- finding errors
- filtering command output

## Syntax

```bash
grep [options] pattern file
```

Example:

```bash
grep "ERROR" server.log
```

## Important Options

### `-i` — Ignore case

```bash
grep -i "error" server.log
```

Matches `ERROR`, `Error`, `error`, etc.

### `-n` — Show line numbers

```bash
grep -n "ERROR" server.log
```

### `-v` — Invert match

Shows lines that do not contain the pattern.

```bash
grep -v "INFO" server.log
```

### `-r` — Recursive search

```bash
grep -r "ERROR" /var/log
```

### `-w` — Match whole word

```bash
grep -w "error" file.txt
```

### `-c` — Count matching lines

```bash
grep -c "ERROR" server.log
```

### `-l` — Show matching filenames

```bash
grep -l "ERROR" *.log
```

### `-E` — Extended regular expressions

```bash
grep -E "ERROR|WARNING" server.log
```

## Search Command Output

```bash
ps aux | grep python
```

```bash
ls -lah | grep ".log"
```

## DevOps Example

```bash
grep -in "error" application.log
```

This searches for errors, ignores case, and shows line numbers.

## Interview Questions

**What is `grep`?**

A command used to search for patterns in files or command output.

**How do you search recursively?**

```bash
grep -r "pattern" directory/
```

---

# 12. `head`

## What is `head`?

`head` displays the beginning of a file.

By default it shows the first 10 lines.

```bash
head file.txt
```

## Show Specific Number of Lines

```bash
head -n 5 file.txt
```

or:

```bash
head -5 file.txt
```

## Show First N Bytes

```bash
head -c 100 file.txt
```

## Why Use `head`?

For a huge file, instead of:

```bash
cat huge.csv
```

use:

```bash
head huge.csv
```

This quickly shows the file structure.

---

# 13. `tail`

## What is `tail`?

`tail` displays the end of a file.

```bash
tail file.txt
```

## Last N Lines

```bash
tail -n 20 server.log
```

## `-f` — Follow a File

This is one of the most important DevOps options.

```bash
tail -f server.log
```

It continuously displays new lines added to the file.

Stop with:

```text
Ctrl + C
```

## Common Production Command

```bash
tail -n 50 -f application.log
```

This shows the last 50 lines and continues monitoring new entries.

## DevOps Use

```bash
tail -f /var/log/syslog
```

## Interview Question

**How do you continuously monitor a log file?**

```bash
tail -f application.log
```

---

# 14. `less`

## What is `less`?

`less` lets you inspect large files interactively.

```bash
less large.log
```

It is generally better than printing an entire huge file using `cat`.

## Navigation

| Key | Action |
|---|---|
| `Space` | Next page |
| `b` | Previous page |
| `↑` | Move up |
| `↓` | Move down |
| `/pattern` | Search |
| `n` | Next search result |
| `N` | Previous search result |
| `g` | Beginning |
| `G` | End |
| `q` | Quit |

## Search

```bash
less server.log
```

Inside `less`, type:

```text
/ERROR
```

Then press Enter.

Use `n` for the next match.

## DevOps Use

```bash
less /var/log/syslog
```

---

# 15. `wc` Word Count

## What is `wc`?

`wc` counts:

- lines
- words
- bytes
- characters

```bash
wc file.txt
```

## Important Options

### Lines

```bash
wc -l file.txt
```

### Words

```bash
wc -w file.txt
```

### Bytes

```bash
wc -c file.txt
```

### Characters

```bash
wc -m file.txt
```

## With Pipes

Count files:

```bash
ls | wc -l
```

Count errors:

```bash
grep "ERROR" server.log | wc -l
```

---

# 16. `sort`

## What is `sort`?

`sort` sorts lines of text.

```bash
sort names.txt
```

## Reverse Sort

```bash
sort -r names.txt
```

## Numeric Sort

```bash
sort -n numbers.txt
```

Example:

```text
2
4
10
30
```

Without `-n`, sorting can be lexical/string-based.

## Human-Readable Sort

```bash
sort -h file.txt
```

Useful for values such as:

```text
10K
2M
500M
1G
```

## Sort by Field

```bash
sort -k2 file.txt
```

`-k2` means sort using field 2.

---

# 17. `uniq`

## What is `uniq`?

`uniq` removes or identifies consecutive duplicate lines.

Example:

```text
apple
apple
banana
banana
orange
```

```bash
uniq fruits.txt
```

Output:

```text
apple
banana
orange
```

## Important Concept

`uniq` only detects **adjacent** duplicates.

Therefore:

```bash
sort fruits.txt | uniq
```

is commonly used to remove duplicates from an unsorted file.

## Count Duplicates

```bash
sort fruits.txt | uniq -c
```

Example:

```text
2 apple
2 banana
1 orange
```

## Most Common Values

```bash
sort access.log | uniq -c | sort -nr
```

---

# 18. `cut`

## What is `cut`?

`cut` extracts characters or fields from each line.

## Character Extraction

```bash
cut -c 1-5 file.txt
```

## Field Extraction

Suppose:

```text
Rajeshwari:Python:8.45
Amit:Java:8.20
Neha:C++:9.10
```

Extract field 1:

```bash
cut -d ":" -f 1 file.txt
```

Output:

```text
Rajeshwari
Amit
Neha
```

Extract field 2:

```bash
cut -d ":" -f 2 file.txt
```

Extract fields 1 and 3:

```bash
cut -d ":" -f 1,3 file.txt
```

### Meaning

```text
-d ":"
```

sets the delimiter.

```text
-f 1
```

selects field 1.

## Linux Example

`/etc/passwd` is colon-separated.

Get usernames:

```bash
cut -d ":" -f 1 /etc/passwd
```

---

# 19. `awk`

## What is `awk`?

`awk` is a powerful text-processing language, especially useful for:

- columns
- structured text
- logs
- filtering
- calculations
- reports

It is a very important DevOps/Linux interview command.

## Basic Syntax

```bash
awk 'pattern { action }' file
```

Suppose:

```text
Rajeshwari Python 8.45
Amit Java 8.20
Neha C++ 9.10
```

Fields are:

```text
$1 = first field
$2 = second field
$3 = third field
```

## Print First Column

```bash
awk '{print $1}' students.txt
```

## Print Second Column

```bash
awk '{print $2}' students.txt
```

## Print Multiple Columns

```bash
awk '{print $1, $3}' students.txt
```

## `$0`

`$0` represents the entire line.

```bash
awk '{print $0}' students.txt
```

## Filtering

Find students with marks greater than 8.5:

```bash
awk '$3 > 8.5 {print $1, $3}' students.txt
```

## Custom Delimiter

```bash
awk -F ":" '{print $1}' /etc/passwd
```

## Calculations

Given:

```text
Python 80
Java 90
C++ 85
```

Calculate total:

```bash
awk '{sum += $2} END {print sum}' marks.txt
```

## Interview Questions

**What is `$1`?**

First field.

**What is `$0`?**

Entire input line.

**How do you specify a delimiter?**

```bash
awk -F ":" '{print $1}' file
```

## `cut` vs `awk`

`cut` is simpler and mainly extracts fields/characters.

`awk` supports:

- conditions
- calculations
- variables
- field processing
- more advanced logic

---

# 20. `sed`

## What is `sed`?

`sed` stands for **Stream Editor**.

It is commonly used for:

- search and replace
- deleting lines
- printing selected lines
- modifying text
- configuration automation

## Basic Syntax

```bash
sed 'command' file
```

## Search and Replace

```bash
sed 's/old/new/' file.txt
```

Example:

```text
I use Python
Python is powerful
Python is popular
```

Run:

```bash
sed 's/Python/Java/' file.txt
```

## Replace All Occurrences

Use `g`:

```bash
sed 's/Python/Java/g' file.txt
```

## Modify File Directly

```bash
sed -i 's/Python/Java/g' file.txt
```

Be careful with `-i` because it changes the original file.

## Delete a Line

Delete line 2:

```bash
sed '2d' file.txt
```

Delete lines 2 through 5:

```bash
sed '2,5d' file.txt
```

## Delete Lines Matching a Pattern

```bash
sed '/ERROR/d' server.log
```

## Print Specific Lines

Print line 5:

```bash
sed -n '5p' file.txt
```

Print lines 5 to 10:

```bash
sed -n '5,10p' file.txt
```

## DevOps Example

Change:

```text
ENV=development
```

to:

```text
ENV=production
```

using:

```bash
sed -i 's/ENV=development/ENV=production/' config.txt
```

---

# 21. Combining Commands

## Count Errors

```bash
grep "ERROR" server.log | wc -l
```

## Find Unique Errors

```bash
grep "ERROR" server.log | sort | uniq
```

## Count Each Error

```bash
grep "ERROR" server.log | sort | uniq -c
```

## Find Most Common Errors

```bash
grep "ERROR" server.log | sort | uniq -c | sort -nr
```

## Monitor Errors in Real Time

```bash
tail -f application.log | grep "ERROR"
```

## Extract Usernames

```bash
cut -d ":" -f 1 /etc/passwd
```

## Find Python Processes

```bash
ps aux | grep python
```

---

# 22. Command Comparison

| Command | Main Purpose |
|---|---|
| `grep` | Search/filter text |
| `head` | Show beginning |
| `tail` | Show end/follow logs |
| `less` | View large files |
| `wc` | Count lines/words/bytes |
| `sort` | Sort lines |
| `uniq` | Remove/count adjacent duplicates |
| `cut` | Extract fields/characters |
| `awk` | Advanced text/field processing |
| `sed` | Stream editing/search-replace |

---

# 23. Important Options Cheat Sheet

| Command | Important Options |
|---|---|
| `grep` | `-i`, `-n`, `-v`, `-r`, `-w`, `-c`, `-l`, `-E` |
| `head` | `-n`, `-c` |
| `tail` | `-n`, `-f`, `-F` |
| `less` | `/`, `n`, `N`, `g`, `G`, `q` |
| `wc` | `-l`, `-w`, `-c`, `-m` |
| `sort` | `-r`, `-n`, `-h`, `-k` |
| `uniq` | `-c`, `-d`, `-u` |
| `cut` | `-c`, `-d`, `-f` |
| `awk` | `-F` |
| `sed` | `-n`, `-i`, `s`, `d`, `p` |

---

# 24. Interview Mental Model

### Search

```bash
grep
```

### View

```bash
head
tail
less
```

### Count

```bash
wc
```

### Sort / Deduplicate

```bash
sort
uniq
```

### Extract

```bash
cut
```

### Advanced Processing

```bash
awk
sed
```

---

# 25. Practical Exercise

Create:

```bash
nano students.txt
```

Add:

```text
Rajeshwari Python 8.45
Amit Java 8.20
Neha Python 9.10
Rahul C++ 7.80
Priya Python 9.10
Amit Java 8.20
```

### Task 1 — First 3 lines

```bash
head -n 3 students.txt
```

### Task 2 — Last 2 lines

```bash
tail -n 2 students.txt
```

### Task 3 — Find Python students

```bash
grep "Python" students.txt
```

### Task 4 — Count Python students

```bash
grep "Python" students.txt | wc -l
```

### Task 5 — Extract names

```bash
awk '{print $1}' students.txt
```

### Task 6 — Extract languages

```bash
awk '{print $2}' students.txt
```

### Task 7 — Marks above 8.5

```bash
awk '$3 > 8.5 {print $1, $3}' students.txt
```

### Task 8 — Sort by marks

```bash
sort -k3 -n students.txt
```

### Task 9 — Find duplicate records

```bash
sort students.txt | uniq -d
```

### Task 10 — Count records

```bash
sort students.txt | uniq -c
```

---

# 26. Real-World DevOps Exercise

Create:

```bash
nano app.log
```

Add:

```text
INFO Server started
INFO Database connected
ERROR Database timeout
INFO Request received
ERROR Connection refused
WARNING High memory usage
ERROR Database timeout
INFO Request completed
ERROR Connection refused
INFO Server running
```

### Find all errors

```bash
grep "ERROR" app.log
```

### Count errors

```bash
grep "ERROR" app.log | wc -l
```

### Find unique errors

```bash
grep "ERROR" app.log | sort | uniq
```

### Count each error

```bash
grep "ERROR" app.log | sort | uniq -c
```

### Find the most frequent error

```bash
grep "ERROR" app.log | sort | uniq -c | sort -nr
```

### Monitor new errors

```bash
tail -f app.log | grep "ERROR"
```

---

# 27. Final Cheat Sheet

```bash
# Search
grep "ERROR" app.log

# Case-insensitive search
grep -i "error" app.log

# Search with line numbers
grep -n "ERROR" app.log

# Recursive search
grep -r "ERROR" /var/log

# First 10 lines
head app.log

# First 20 lines
head -n 20 app.log

# Last 10 lines
tail app.log

# Follow log
tail -f app.log

# View large file
less app.log

# Count lines
wc -l app.log

# Sort
sort names.txt

# Numeric sort
sort -n numbers.txt

# Remove duplicates
sort names.txt | uniq

# Count duplicates
sort names.txt | uniq -c

# Extract field
cut -d ":" -f 1 file.txt

# Print first column
awk '{print $1}' file.txt

# Filter using awk
awk '$3 > 80 {print $1}' marks.txt

# Replace text
sed 's/old/new/g' file.txt

# Replace directly in file
sed -i 's/old/new/g' file.txt

# Delete matching lines
sed '/ERROR/d' app.log

# Count errors
grep "ERROR" app.log | wc -l

# Most common errors
grep "ERROR" app.log | sort | uniq -c | sort -nr
```

---

# 28. Day 2 Success Criteria

Before moving forward, you should be comfortable with:

- [ ] Searching files using `grep`
- [ ] Using `grep` with pipes
- [ ] Reading files with `head`
- [ ] Monitoring logs with `tail -f`
- [ ] Navigating large files with `less`
- [ ] Counting data with `wc`
- [ ] Sorting data with `sort`
- [ ] Removing/counting duplicates with `uniq`
- [ ] Extracting fields with `cut`
- [ ] Processing columns with `awk`
- [ ] Replacing/editing text with `sed`
- [ ] Understanding Linux pipes
- [ ] Combining multiple commands into pipelines
- [ ] Performing basic log analysis

---

# Linux Learning Progress

## Day 1 — File & Directory Management

```text
1.  pwd
2.  ls
3.  cd
4.  mkdir
5.  touch
6.  cp
7.  mv
8.  rm
9.  cat
10. find
```

## Day 2 — Text Processing & Log Analysis

```text
11. grep
12. head
13. tail
14. less
15. wc
16. sort
17. uniq
18. cut
19. awk
20. sed
```

## Next Topic — Linux Permissions

The next commands/concepts to learn:

```text
chmod
chown
chgrp
umask
sudo
su
id
groups
passwd
```

These are important for Linux administration, Cloud, Docker, Kubernetes, DevOps, and security interviews.
