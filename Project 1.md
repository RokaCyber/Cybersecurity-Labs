# Cybersteps PowerShell Challenge - Part 1 🚀

Welcome to the lab report of my first practical PowerShell challenge with **Cybersteps**! In this file, I explain step-by-step how I tackled and solved all 25 tasks plus the initial setup, breaking down the logic behind each command used.

---

### ⚙️ Initial Setup: Unblocking the Script
Before running any commands, Windows restricts downloaded internet files by attaching a security zone identifier (`Zone.Identifier`) to prevent unauthorized script execution. To safely bypass this block without turning off system-wide policies, we use the `Unblock-File` cmdlet on our downloaded file[cite: 1]:
- Command: `Unblock-File .\CyberstepsPSChallenge-Part1.ps1`
- [INSERT SCREENSHOT HERE]

---

### 📋 Full Tasks Breakdown (Step by Step)

#### Phase 1: Output & Basic Math (Tasks 1–3)

* **Task 1 (Hello, terminal):** To print a standard text string to the screen, we know that the `echo` alias in PowerShell works just like `Write-Output`, allowing us to send the message straight to the console[cite: 1]:
  - Command: `echo "Hello, terminal"`

* **Task 2 (The console is a calculator):** If we want to calculate a math expression (like `1 + 3`) instead of hardcoding the result `4`, we wrap the expression in parentheses `()`. This forces PowerShell to evaluate the math calculation first and then return the value[cite: 2]:
  - Command: `Write-Output (1 + 3)`

* **Task 3 (The answer to everything):** Following the same principle as the previous task, to print the number `42` through multiplication, we use the `*` operator inside the evaluation parentheses[cite: 2]:
  - Command: `Write-Output (6 * 7)`

#### Phase 2: Navigation & Directory Inspection (Tasks 4–9)

* **Task 4 (Where am I?):** To find out which absolute directory path we are currently in at any given moment, we simply call the `pwd` command (Print Working Directory)[cite: 2]:
  - Command: `pwd`

* **Task 5 (List folders only):** Using a standard listing command shows both files and folders. To isolate exclusively subdirectories while excluding files, we apply the `-Directory` filter to `Get-ChildItem`[cite: 2]:
  - Command: `Get-ChildItem -Directory`

* **Task 6 (Peek without entering):** If we want to check what's inside a specific folder (like a folder named `storage`) without physically moving from our current position, we can specify the target path directly using the `-Path` parameter[cite: 3]:
  - Command: `Get-ChildItem -Path "storage"`

* **Task 7 (Chaining commands):** PowerShell lets us run multiple sequential commands on the same line by separating them with a semicolon (`;`). For instance, we can enter a directory and immediately list its contents like this[cite: 3]:
  - Command: `cd lab; ls`

* **Task 8 (Two levels down):** To quickly dive deep into nested folders (like `tools\scripts`) and immediately verify we reached the right place, we combine path navigation and location checks with a semicolon[cite: 3]:
  - Command: `cd tools\scripts; pwd`

* **Task 9 (Up we go):** The `..` notation moves us up one level from the current folder. We can use it to ascend and immediately enter an adjacent folder (`bunker`), then verify our path with `pwd`[cite: 4]:
  - Command: `cd ..\bunker; pwd`

#### Phase 3: Variables & String Interpolation (Tasks 10–12)

* **Task 10 (Your first variable):** To store a temporary value, we use the dollar sign `$` followed by the variable name. We can assign the string `"Neo"` to `$name` and print it right after on the same line using a semicolon[cite: 4]:
  - Command: `$name = "Neo"; $name`

* **Task 11 (Math with variables):** We can define two separate numeric variables (for example, `$a = 10` and `$b = 32`) and then sum them up on the fly by referencing them with their dollar signs[cite: 4]:
  - Command: `$a = 10; $b = 32; $a + $b`

* **Task 12 (Build a message):** If we want to insert a variable's value inside a phrase, we just enclose the text in **double quotes** `""`. This way, PowerShell automatically recognizes the `$target` variable inside and replaces it with its actual real value (interpolation)[cite: 5]:
  - Command: `$target = "server01"; "Scanning $target"`

#### Phase 4: File Counting & Filtering (Tasks 13–18)

* **Task 13 (Solo i nomi / Names only):** When listing files, we usually see a table full of details (sizes, dates, permissions). If we want to clean up the output and see *only* the names in text format, we add the `-Name` modifier[cite: 5]:
  - Command: `ls -Name`

* **Task 14 (Count the loot):** To know the exact number of files in a folder, we first filter elements with `-File`, enclose the action in parentheses to treat it as a single block, and finally read the `.Count` property of the resulting array[cite: 5]:
  - Command: `(ls -File).Count`

* **Task 15 (Specific extension):** If we want to extract only text files, we can combine a wildcard filter (`*.txt`) together with the `-Name` parameter for a clean list[cite: 6]:
  - Command: `ls *.txt -Name`

* **Task 16 (Read content):** To open and read the raw text of a file line by line straight in the terminal, we use the `cat` command (which is a convenient alias for `Get-Content`)[cite: 6]:
  - Command: `cat secret.txt`
  - [INSERT SCREENSHOT HERE]

* **Task 17 (Count lines in a log):** Leveraging the fact that `cat` reads each line as an element of a list, we can wrap file reading in parentheses and calculate its size with `.Count` to find out how many lines a log file contains[cite: 6]:
  - Command: `(cat log.txt).Count`
  - [INSERT SCREENSHOT HERE]

* **Task 18 (Find the hidden flag):** When an important file like `flag.txt` is hidden deep inside some subdirectory, standard search isn't enough. We activate recursive and forced searching by combining the `-Filter`, `-Force` (to see hidden items), and `-Recurse` (to scan all subfolders) parameters, piping the result directly into `cat` to read its content[cite: 6]:
  - Command: `ls -Filter "flag.txt" -Force -Recurse | cat`

#### Phase 5: Pipe, Sorting & Absolute Paths (Tasks 19–25)

* **Task 19 (Alphabetical sort):** To sort lines read from a text file alphabetically, we can pipe the data stream through the pipe symbol `|` straight into the `sort` command[cite: 7]:
  - Command: `cat names.txt | sort`
  - [INSERT SCREENSHOT HERE]

* **Task 20 (Tidy file list):** We can combine file name listing (`ls -Name`) with the `sort` command using a pipe, giving us a clean, alphabetically sorted list[cite: 7]:
  - Command: `ls -Name | sort`

* **Task 21 (Backwards, please):** By default, `sort` orders from A to Z or smallest to largest number. If we want to flip the direction and sort in reverse (Z to A), we simply add the `-Descending` option[cite: 7]:
  - Command: `cat ranks.txt | sort -Descending`

* **Task 22 (Variable loot):** We can store a filename inside a variable (e.g., `$file = "vault.txt"`) and then pass that same variable to the `cat` command to dynamically read its content[cite: 8]:
  - Command: `$file = "vault.txt"; cat $file`

* **Task 23 (The absolute path):** When relative paths aren't enough, we can read a file by specifying its full absolute path starting directly from the root drive letter (`C:\...`)[cite: 8]:
  - Command: `cat C:\Users\robi9\AppData\Local\Temp\CyberstepsPSQuest_Part1\sandbox\keys.txt`

* **Task 24 (Filtered logs):** We can combine multiple logics in one go: enter the logs directory, pick only files with the `.log` extension by name, and sort everything alphabetically using the pipe[cite: 8]:
  - Command: `cd logs; ls -Name *.log | sort`

* **Task 25 (Sign off):** To wrap up the challenge and print the final completion message, we use a final text output command[cite: 9]:
  - Command: `echo "I am one with the shell"`

---
*Completed as part of my learning journey with Cybersteps!* 💻🔥
