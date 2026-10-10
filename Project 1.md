# Cybersteps PowerShell Challenge - Part 1 🚀

Welcome to the lab report of my first practical PowerShell challenge with **Cybersteps**! In this file, I explain step-by-step how I tackled and solved all 25 tasks plus the initial setup, breaking down the logic behind each command used.

---

### ⚙️ Initial Setup: Unblocking the Script
Before running any commands, Windows restricts downloaded internet files by attaching a security zone identifier (`Zone.Identifier`) to prevent unauthorized script execution. To safely bypass this block without turning off system-wide policies, we use the `Unblock-File` cmdlet on our downloaded file:
- Command: `Unblock-File .\CyberstepsPSChallenge-Part1.ps1`

---

### 📋 Full Tasks Breakdown (Step by Step)

#### Phase 1: Output & Basic Math (Tasks 1–3)

* **Task 1 (Hello, terminal):** To print a standard text string to the screen, we know that the `echo` alias in PowerShell works just like `Write-Output`, allowing us to send the message straight to the console:
  - Command: `echo "Hello, terminal"`
  - <img width="368" height="56" alt="1-25" src="https://github.com/user-attachments/assets/82e962af-124e-47ea-999a-3bb7d4bbb226" />


* **Task 2 (The console is a calculator):** If we want to calculate a math expression (like `1 + 3`) instead of hardcoding the result `4`, we wrap the expression in parentheses `()`. This forces PowerShell to evaluate the math calculation first and then return the value:
  - Command: `Write-Output (1 + 3)`
  - <img width="368" height="52" alt="2-25" src="https://github.com/user-attachments/assets/201c040f-abd7-40af-9411-e787a895cf67" />


* **Task 3 (The answer to everything):** Following the same principle as the previous task, to print the number `42` through multiplication, we use the `*` operator inside the evaluation parentheses:
  - Command: `Write-Output (6 * 7)`
  - <img width="377" height="55" alt="3-25" src="https://github.com/user-attachments/assets/3568e8eb-1f99-4826-853d-dc2c1d180c9b" />


#### Phase 2: Navigation & Directory Inspection (Tasks 4–9)

* **Task 4 (Where am I?):** To find out which absolute directory path we are currently in at any given moment, we simply call the `pwd` command (Print Working Directory):
  - Command: `pwd`

* **Task 5 (List folders only):** Using a standard listing command shows both files and folders. To isolate exclusively subdirectories while excluding files, we apply the `-Directory` filter to `Get-ChildItem`:
  - Command: `Get-ChildItem -Directory`
  - <img width="173" height="29" alt="5-25" src="https://github.com/user-attachments/assets/c6068d0c-8321-415f-90b0-5f34ff1e4f80" />


* **Task 6 (Peek without entering):** If we want to check what's inside a specific folder (like a folder named `storage`) without physically moving from our current position, we can specify the target path directly using the `-Path` parameter:
  - Command: `Get-ChildItem -Path "storage"`
  - <img width="449" height="54" alt="6-25" src="https://github.com/user-attachments/assets/056e46f9-aa10-4f79-9616-eaac573d2564" />


* **Task 7 (Chaining commands):** PowerShell lets us run multiple sequential commands on the same line by separating them with a semicolon (`;`). For instance, we can enter a directory and immediately list its contents like this:
  - Command: `cd lab; ls`
  - <img width="170" height="26" alt="7-25" src="https://github.com/user-attachments/assets/59870752-689c-4f8f-ac09-343afc799b2d" />


* **Task 8 (Two levels down):** To quickly dive deep into nested folders (like `tools\scripts`) and immediately verify we reached the right place, we combine path navigation and location checks with a semicolon:
  - Command: `cd tools\scripts; pwd`
  - <img width="839" height="98" alt="8-25" src="https://github.com/user-attachments/assets/9ad464cd-9149-4523-b5c3-cf44e16cae02" />


* **Task 9 (Up we go):** The `..` notation moves us up one level from the current folder. We can use it to ascend and immediately enter an adjacent folder (`bunker`), then verify our path with `pwd`:
  - Command: `cd ..\bunker; pwd`
  - <img width="560" height="64" alt="9-25" src="https://github.com/user-attachments/assets/32353f82-556e-4a54-9aab-c6b13956a183" />


#### Phase 3: Variables & String Interpolation (Tasks 10–12)

* **Task 10 (Your first variable):** To store a temporary value, we use the dollar sign `$` followed by the variable name. We can assign the string `"Neo"` to `$name` and print it right after on the same line using a semicolon:
  - Command: `$name = "Neo"; $name`
  - <img width="823" height="83" alt="10-25" src="https://github.com/user-attachments/assets/5669c5b2-51a2-4e58-bf8e-0cae1de75060" />


* **Task 11 (Math with variables):** We can define two separate numeric variables (for example, `$a = 10` and `$b = 32`) and then sum them up on the fly by referencing them with their dollar signs:
  - Command: `$a = 10; $b = 32; $a + $b`

* **Task 12 (Build a message):** If we want to insert a variable's value inside a phrase, we just enclose the text in **double quotes** `""`. This way, PowerShell automatically recognizes the `$target` variable inside and replaces it with its actual real value (interpolation):
  - Command: `$target = "server01"; "Scanning $target"`
  - <img width="857" height="104" alt="12-25" src="https://github.com/user-attachments/assets/87f4de5b-bb42-4997-aab5-bedf3bf5c61c" />


#### Phase 4: File Counting & Filtering (Tasks 13–18)

* **Task 13 (Solo i nomi / Names only):** When listing files, we usually see a table full of details (sizes, dates, permissions). If we want to clean up the output and see *only* the names in text format, we add the `-Name` modifier:
  - Command: `ls -Name`
  - <img width="655" height="92" alt="13-25" src="https://github.com/user-attachments/assets/bf2560fc-e435-4081-8514-1c58b5b18afb" />


* **Task 14 (Count the loot):** To know the exact number of files in a folder, we first filter elements with `-File`, enclose the action in parentheses to treat it as a single block, and finally read the `.Count` property of the resulting array:
  - Command: `(ls -File).Count`
  - <img width="629" height="92" alt="14-25" src="https://github.com/user-attachments/assets/c6d71a6a-c7ce-4647-8163-ffedd9708d1d" />


* **Task 15 (Specific extension):** If we want to extract only text files, we can combine a wildcard filter (`*.txt`) together with the `-Name` parameter for a clean list:
  - Command: `ls *.txt -Name`
  - 

* **Task 16 (Read content):** To open and read the raw text of a file line by line straight in the terminal, we use the `cat` command (which is a convenient alias for `Get-Content`):
  - Command: `cat secret.txt`

* **Task 17 (Count lines in a log):** Leveraging the fact that `cat` reads each line as an element of a list, we can wrap file reading in parentheses and calculate its size with `.Count` to find out how many lines a log file contains:
  - Command: `(cat log.txt).Count`

* **Task 18 (Find the hidden flag):** When an important file like `flag.txt` is hidden deep inside some subdirectory, standard search isn't enough. We activate recursive and forced searching by combining the `-Filter`, `-Force` (to see hidden items), and `-Recurse` (to scan all subfolders) parameters, piping the result directly into `cat` to read its content:
  - Command: `ls -Filter "flag.txt" -Force -Recurse | cat`
  - <img width="848" height="104" alt="18-25" src="https://github.com/user-attachments/assets/4d0fa34a-9294-45b6-bec7-a99154f44ae7" />


#### Phase 5: Pipe, Sorting & Absolute Paths (Tasks 19–25)

* **Task 19 (Alphabetical sort):** To sort lines read from a text file alphabetically, we can pipe the data stream through the pipe symbol `|` straight into the `sort` command:
  - Command: `cat names.txt | sort`

* **Task 20 (Tidy file list):** We can combine file name listing (`ls -Name`) with the `sort` command using a pipe, giving us a clean, alphabetically sorted list:
  - Command: `ls -Name | sort`
  - <img width="611" height="85" alt="20-25" src="https://github.com/user-attachments/assets/a9435452-ee73-4a8c-af50-a874b0d4e77f" />


* **Task 21 (Backwards, please):** By default, `sort` orders from A to Z or smallest to largest number. If we want to flip the direction and sort in reverse (Z to A), we simply add the `-Descending` option:
  - Command: `cat ranks.txt | sort -Descending`
  - <img width="642" height="92" alt="21-25" src="https://github.com/user-attachments/assets/05da704a-91a0-4971-adeb-fd5c273e6fd5" />


* **Task 22 (Variable loot):** We can store a filename inside a variable (e.g., `$file = "vault.txt"`) and then pass that same variable to the `cat` command to dynamically read its content:
  - Command: `$file = "vault.txt"; cat $file`
  - <img width="728" height="89" alt="22-25" src="https://github.com/user-attachments/assets/3dd591c8-a8d1-4815-8a60-161e8beb69a5" />


* **Task 23 (The absolute path):** When relative paths aren't enough, we can read a file by specifying its full absolute path starting directly from the root drive letter (`C:\...`):
  - Command: `cat C:\Users\robi9\AppData\Local\Temp\CyberstepsPSQuest_Part1\sandbox\keys.txt`
  - <img width="856" height="92" alt="23-25" src="https://github.com/user-attachments/assets/624524eb-19d6-4358-9df9-420cccf1b6d3" />


* **Task 24 (Filtered logs):** We can combine multiple logics in one go: enter the logs directory, pick only files with the `.log` extension by name, and sort everything alphabetically using the pipe:
  - Command: `cd logs; ls -Name *.log | sort`
  - <img width="308" height="47" alt="24-25" src="https://github.com/user-attachments/assets/1cb1e424-1321-4433-ad9d-905f1d7ef070" />


* **Task 25 (Sign off):** To wrap up the challenge and print the final completion message, we use a final text output command:
  - Command: `echo "I am one with the shell"`
  - <img width="590" height="98" alt="25-25" src="https://github.com/user-attachments/assets/43e3da33-611a-4637-88cc-b2472ba7a39b" />


---
*Completed as part of my learning journey with Cybersteps!* 💻🔥

