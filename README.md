# 🔁 Linux Shell Script Lab – For Loops, File Iteration & Log Processing

In this lab, I learned how to use **for loops** in Bash to automate repetitive tasks such as launching multiple rockets, reading mission names from a file, printing number sequences, processing app log files, and renaming images based on their extensions.

This lab strengthened my understanding of **iteration**, **conditional checks**, **file handling**, and **pattern substitution** — essential Bash skills for DevOps automation.

---

## 📋 Lab Overview

**Goal:**

* Use `for` loops to iterate over lists, files, and dynamic inputs
* Automate repeated actions like launching rockets or renaming files
* Update existing scripts to loop through mission names and logs
* Use conditionals (`if`, `[[ ]]`) within loops to make scripts intelligent

**Learning Outcomes:**

* Loop using `for item in ...; do ...; done`
* Read values from text files inside loops
* Apply conditional logic inside loops
* Work with file extensions and rename files using `sed`
* Build formatted tabular outputs from log files

---

## 🛠 Step-by-Step Journey

---

### **Step 1 — Create `launch-rockets.sh` to Launch Multiple Missions**

Script path: `/home/bob/launch-rockets.sh`

**Goal:** Call `create-and-launch-rocket` five times using a loop.

**Script:**

```bash
#!/bin/bash

for mission in luna-mission mars-mission jupiter-mission saturn-mission mercury-mission
do
    bash /home/bob/create-and-launch-rocket $mission
done
```

Saved the script and tested:

```bash
bash /home/bob/launch-rockets.sh
```

✅ All five rockets launched successfully.

---

### **Step 2 — Update Script to Read Mission Names From a File**

File containing missions:

```
/home/bob/mission-names.txt
```

Replaced the hard-coded list with dynamic file loading:

```bash
for mission in $(cat /home/bob/mission-names.txt)
do
    bash /home/bob/create-and-launch-rocket $mission
done
```

✅ The script now works for *any* number of missions by simply updating the `.txt` file.

---

### **Step 3 — Create `loop.sh` to Print Numbers 31–40**

Script path: `/home/bob/loop.sh`

**Script:**

```bash
#!/bin/bash

for i in {31..40}
do
    echo $i
done
```

Saved and tested:

```bash
bash /home/bob/loop.sh
```

✅ Numbers 31 to 40 printed line-by-line.

---

### **Step 4 — Process App Logs Using a For Loop (`count-requests.sh`)**

App list file:

```
/home/bob/apps.txt
```

Log files stored in:

```
/var/log/apps/<app>_app.log
```

Updated script to use a loop and print results in a formatted table.

**Final Script (`count-requests.sh`):**

```bash
#!/bin/bash

echo -e " Log name \t GET \t POST \t DELETE "
echo -e "------------------------------------------------------------"

for app in $(cat /home/bob/apps.txt)
do
    get_requests=$(cat /var/log/apps/${app}_app.log | grep "GET" | wc -l)
    post_requests=$(cat /var/log/apps/${app}_app.log | grep "POST" | wc -l)
    delete_requests=$(cat /var/log/apps/${app}_app.log | grep "DELETE" | wc -l)

    echo -e " ${app} \t ${get_requests} \t ${post_requests} \t ${delete_requests}"
done
```

Running the script produced:

```
Log name     GET   POST   DELETE
finance      10    20     50
marketing    20    10     30
partners     15    18     22
pay          11    17     19
```

✅ Correct tabular summary of GET/POST/DELETE requests.

---

### **Step 5 — Rename `.jpeg` Images to `.jpg` (`rename-images.sh`)**

Image folder:

```
/home/bob/images
```

Script path:

```
/home/bob/rename-images.sh
```

**Final Script:**

```bash
#!/bin/bash

for file in $(ls images)
do
    if [[ $file = *.jpeg ]]
    then
        new_name=$(echo $file | sed 's/jpeg/jpg/g')
        mv images/$file images/$new_name
    fi
done
```

Executed with:

```bash
bash /home/bob/rename-images.sh
```

✅ All `.jpeg` files renamed to `.jpg` while all other files remained unchanged.

---

## 🧠 Key Concepts Reinforced

| Concept                  | Description                                                |
| ------------------------ | ---------------------------------------------------------- |
| **For loops**            | Automate repetitive tasks by iterating over lists or files |
| **Command substitution** | Use `$(cat file.txt)` to load content dynamically          |
| **Pattern matching**     | `[[ $file = *.jpeg ]]` checks file extensions              |
| **Text substitution**    | `sed 's/jpeg/jpg/g'` replaces patterns inside strings      |
| **Log processing**       | Count request types using `grep` + `wc -l`                 |
| **Script modularity**    | Pass variables into other scripts using loops              |

---

## 🧩 Common Bash Loop Techniques

| Use Case        | Example                                     |
| --------------- | ------------------------------------------- |
| List iteration  | `for x in a b c; do ...; done`              |
| Number ranges   | `for i in {1..10}; do echo $i; done`        |
| Files in folder | `for f in $(ls folder); do ...; done`       |
| Lines from file | `for line in $(cat file.txt); do ...; done` |

---

## 💡 Notes / Tips

* Always quote variables inside scripts if filenames contain spaces
* Prefer `$(...)` over backticks for clarity and nesting
* Use descriptive loop variable names (`mission`, `app`, `file`)
* Use `sed` for renaming, pattern detection, and text replacement
* Keep loops clean and readable with proper indentation

---

## ✅ Summary Commands

| Task              | Command               |        |
| ----------------- | --------------------- | ------ |
| Create script     | `vi script.sh`        |        |
| Save file         | `:wq`                 |        |
| Make executable   | `chmod +x script.sh`  |        |
| Run script        | `bash script.sh`      |        |
| List images       | `ls /home/bob/images` |        |
| Count log entries | `grep "GET" file.log  | wc -l` |

---

### 🏁 End of Lab

Completed multiple challenges involving:
✅ Looping through arrays and files
✅ Replacing hard-coded values with reusable loops
✅ Processing logs programmatically
✅ Renaming files using loops + conditionals
✅ Generating structured tabular output

This lab strengthened my understanding of **Bash loops, file iteration, and automating multi-step operations** — essential for DevOps scripting at scale.
