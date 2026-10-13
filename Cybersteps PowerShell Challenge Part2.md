Cybersteps PowerShell Challenge - Part 2 
Technical Execution & Portfolio Report 
Author: Roberto Coleine 
Total Time Elapsed: ~4 hour 

Task 1:
This challenge asks to display the message "Hello, World!". We already know this command and we use echo:
Command:
echo "Hello, World!"
<img width="274" height="133" alt="1-26" src="https://github.com/user-attachments/assets/8464a874-5b57-4fa7-94b9-17a0490aeca5" />


Task 2:
This challenge asks to print the number 42, but doesn't ask for anything extra like the challenge in part 1 did. So, to keep life simple, we'll first try with a basic print, and if it throws an error, we'll try with addition:
Command:
echo "42"
<img width="243" height="146" alt="2-26" src="https://github.com/user-attachments/assets/c968c65b-c326-4de8-9fbf-1851b201dc4c" />



Task 3:
The task required printing the text "powershell" and displaying it in all uppercase. Following Python's logic, I thought of an upper command, but not knowing the exact syntax, I searched online. In the end, I tried:
Command:
"powershell".ToUpper()
<img width="322" height="124" alt="3-26" src="https://github.com/user-attachments/assets/40058575-1480-44b2-940a-468f0c7f16cf" />


Task 4:
This task requires displaying the number of characters in the string "powershell". Thinking back to the previous exercise, .Count came to mind, but I remembered reading that .Count was for counting documents/items rather than string length. I searched online and my suspicion was right: I found the appropriate property for this job, which is .Length:
Command:
"powerShell".Length
<img width="299" height="140" alt="4-26" src="https://github.com/user-attachments/assets/ae817a8f-ce85-467e-9e5e-f5e713019458" />



Task 5:
Requires displaying all file names present in the directory. The first idea is to simply use:
Command:
ls -Name
<img width="275" height="184" alt="5-26" src="https://github.com/user-attachments/assets/b5d1149c-850b-43c8-a972-86bf9f187d25" />



Task 6:
Now we need to count the number of files in the directory (only files). As we mentioned earlier, we can use the .Count property.
<img width="282" height="165" alt="6-26" src="https://github.com/user-attachments/assets/27b8f7d5-99ae-4c0b-894b-b266ca894e04" />



Task 7:
Display text files (so .txt) and return them in alphabetical order. I want to take a gamble and try not adding an alphabetical sorting filter because by default they are printed in alphabetical order; if needed, we'll add a sorting filter:
Command:
ls -Filter "*.txt"
It would have worked, but it gave me an error. I tried adding | sort, but still got an error. Reading the error description, I realized I needed to add -Name to the command. The solution is:
PowerShell
ls -Name -Filter "*.txt" | sort
<img width="243" height="100" alt="7-26" src="https://github.com/user-attachments/assets/8089b5fa-0807-4d2a-a8f4-962cd5dd1dc0" />



Task 8:
Requires reading the content of the file readme.txt, so I would simply use:
Command:
cat readme.txt
<img width="278" height="185" alt="8-26" src="https://github.com/user-attachments/assets/f4dce08d-53ba-4baf-a131-aee2b2acabae" />



Task 9:
Display only the first 3 lines of the file story.txt. I remember that in Linux you could use the head command, but I didn't know the PowerShell equivalent. I looked it up online and it turns out it works the same in PowerShell, except that unlike Linux, the parameter goes after instead of before. Let's try:
Command:
cat story.txt -Head 3
<img width="275" height="155" alt="9-26" src="https://github.com/user-attachments/assets/f3392f49-6dd1-4594-b142-a62a05725fb2" />



Task 10:
Now we need to display the number of lines in the text file data.txt. Let's try with the .Count property, maybe it works for this too:
Command:
(cat data.txt).Count

Honestly, I didn't think it would work—I thought there would be a more specific command. And indeed, after searching, I found that there is a dedicated cmdlet for line counts, Measure-Object -Line. Good to know for the future.
<img width="271" height="164" alt="10-26" src="https://github.com/user-attachments/assets/66b72d18-15d0-40a3-ba95-c1bf38b9df9e" />



Task 11:
And here is where the gaps start. The point requires printing all lines from the file app.log that contain the word "ERROR". My first thought was finding a way to search for the word, but -Filter doesn't work inside a file. Apparently PowerShell provides a dedicated command that handles both functions requested by the exercise (easier than I thought):
Command:
cat app.log | sls "ERROR"
<img width="278" height="172" alt="11-26" src="https://github.com/user-attachments/assets/fc4cccab-ed34-4d97-9adf-763707560092" />



Task 12:
Now we need to output all lines from names.txt in alphabetical order. I thought there would be a command to select the lines, but didn't find anything. Let's try with a simple sort and see what happens:
Command:
cat names.txt | sort
<img width="290" height="203" alt="12-26" src="https://github.com/user-attachments/assets/24a84f0f-fb14-4753-b2df-8fcaaa522ad5" />



Task 13:
Required printing the unique values from colors.txt and sorting them alphabetically. I thought there would be some filter for this, but since the task asked for alphabetical order, I searched for additional info on the sort command and found a parameter called -Unique:
Command:
cat colors.txt | sort -Unique
<img width="354" height="188" alt="13-26" src="https://github.com/user-attachments/assets/7b602642-b414-4835-ae15-2e69b9916815" />



Task 14:
Honestly, I didn't understand what it wanted me to print, so for this task I had to rely entirely on AI. I personally would have used ls -Name, but I wasn't convinced because I didn't get the point of the question. In the end, by discussing it with AI, I realized my initial intuition was correct. I ended up using:
Command:
(ls).Name

Though my original choice ls -Name would have worked as well.
<img width="403" height="182" alt="14-26" src="https://github.com/user-attachments/assets/31304e43-1981-4fdb-85ac-865ea8955c80" />



Task 15:
This task requires displaying files with sizes greater than 100 bytes. I had to search for quite a while to discover the right commands. I started with the logic of first reading all files in the directory, and then searching for the command to filter by size: first where Length (to define them by size) and then the -gt operator (to say greater than):
Command:
ls -File | where Length -gt 100
And that command was wrong. I tried adding -Name, but it was still wrong because it needed to display only the file names. Here I had to ask AI for help again, and it suggested putting the .Name property at the end, which worked:
PowerShell
(ls -File | where Length -gt 100).Name
<img width="265" height="91" alt="15-26" src="https://github.com/user-attachments/assets/36bf6a4e-70b5-47d9-bdbc-15557f6e7d5b" />



Task 16:
Now we need to count how many lines in app.log contain the word "ERROR". I thought back to the code we wrote in previous exercises and added the .Count property.
<img width="293" height="165" alt="16-26" src="https://github.com/user-attachments/assets/ab20fd21-000f-4eb7-aeee-26e95d7dd126" />



Task 17:
In this exercise I need to sum all the numbers inside numbers.txt. I looked at the hints provided by Cybersteps and saw the Measure-Object cmdlet. I checked the file: it only contains numbers, 1 number per line, so the described function can be used without too much extra code. Let's try:
Command:
(cat numbers.txt | Measure-Object -Sum).Sum
<img width="257" height="80" alt="17-26" src="https://github.com/user-attachments/assets/b8bfe190-6bb5-471f-a34d-a481c91d0a0f" />




Task 18:
We need to print the name of the largest file in the directory. Let's take the previous function and build on it: Measure-Object offers special properties for length as well. I tried:
Command:
(ls -File | Measure-Object Length -Max).Maximum
But it returned the size of the largest file, so we needed a different approach. Long story short, I had to ask AI for help, which recommended using the sort command. At that point, I thought of sorting in descending order and printing just the first item:
Command:
(ls -File | sort Length -Descending | select -First 1).Name
<img width="331" height="84" alt="18-26" src="https://github.com/user-attachments/assets/f4fdeedc-a1bc-4a5f-925c-90d8e21c1247" />



Task 19:
The exercise requires displaying the name of the last modified file. Let's start by finding the property for modified files: we'll use sort again with the LastWriteTime property, ordering it like in the previous exercise so the first item in the list is that file. The problem is returning just the name: we can try like before by wrapping the entire expression in parentheses:
Command:
(ls -File | sort LastWriteTime -Descending | select -First 1).Name
<img width="453" height="79" alt="19-26" src="https://github.com/user-attachments/assets/f8246f60-55d1-42bf-a533-7ff2be119c1c" />
Managed to get it after 5 attempts!




Task 20:
In this exercise we need to modify the text inside a file, specifically replacing the word "cat" with "dog". Among Cybersteps' tips was the recommendation to use the .Replace() method and look up how it works online:
Command:
"I have a cat and another cat".Replace("cat", "dog")
<img width="439" height="145" alt="20-26" src="https://github.com/user-attachments/assets/14b856f4-a3bd-4d13-96f5-b3c0799129d3" />



Task 21:
In this task we need to replace commas , with newlines. Still considering the .Replace() method, I tried "`n", a known way to insert a newline, but it didn't work—or rather, it worked code-wise, but wasn't what the exercise expected. I checked Cybersteps' notes and saw the .Split() method. After researching how it works online, I tried:
Command:
"one,two,three,four".Split(',')
<img width="254" height="104" alt="21-26" src="https://github.com/user-attachments/assets/0ec3674c-441d-4a99-889d-b83903e5e0c5" />



Task 22:
We need to count the number of words in a string. I tried .Count, but it gave an error. I looked into why, and to the system there was nothing to count. So I opted to use the previous command to split the string into an array and count the elements, which worked:
Command:
("the quick brown fox jumps over the lazy dog".Split(' ')).Count
<img width="337" height="82" alt="22-26" src="https://github.com/user-attachments/assets/cc3e4e58-1b5f-4a7e-b1a4-b0d3a03fa2b8" />



Task 23:
Now we need to print the names of all running processes in alphabetical order. To get the processes, ps is enough, so to display them sorted:
Command:
ps | sort
<img width="354" height="35" alt="23-26" src="https://github.com/user-attachments/assets/7af0723f-90a9-4612-9df3-899c17ee5075" />




Task 24:
We need to display the value of the PATH environment variable. From Cybersteps' tips, it's easy to see the command is:
Command:
$env:PATH
<img width="567" height="92" alt="24-26" src="https://github.com/user-attachments/assets/22b2cb92-b2d5-468a-8bd7-adfa50a55acf" />



Task 25:
The task requires displaying the file format (extension) of a specific file. A quick online search suggested using .Extension, but running it directly on a raw string doesn't work. After much searching without luck, I checked the Cybersteps portal and found a syntax I hadn't used yet. Researching that syntax, I found it could be the solution: [System.IO.Path]::Method().
Command:
[System.IO.Path]::GetExtension("report.final.txt")
<img width="284" height="81" alt="25-26" src="https://github.com/user-attachments/assets/3d16ce87-6867-4d49-86ea-a1b9943446c1" />
I never would have figured it out if it weren't for AI assistance!



Task 26:
Last problem and the most complex: from the file data.csv, we need to find lines containing "active" and count them. Mainly, we need to read the file using cat, use the -match operator from the Cybersteps guide, and the .Count property. After several trial-and-error attempts, the correct form is:
Command:
((cat .\data.csv) -match "active").Count
<img width="278" height="81" alt="26-26" src="https://github.com/user-attachments/assets/ee89ec01-02b7-4db9-a29a-00582ab4e01a" />


