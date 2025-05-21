### **1. `for` Loop**
The `for` loop is used to iterate over a list of items, such as filenames, numbers, or strings.

#### **Basic Syntax**
```bash
for item in list; do
    # commands
done
```

#### **Example: Iterating Over a List of Files**
```bash
for file in /path/to/directory/*; do
    echo "Processing $file"
done
```

#### **Example: Looping Over a Range of Numbers**
```bash
for i in {1..5}; do
    echo "Number $i"
done
```

#### **Example: Using C-style Syntax**
Bash also supports a C-style `for` loop with initialization, condition, and increment.

```bash
for (( i=0; i<5; i++ )); do
    echo "Counter: $i"
done
```

---

### **2. `while` Loop**
The `while` loop continues executing as long as a specified condition is true.

#### **Basic Syntax**
```bash
while [ condition ]; do
    # commands
done
```

#### **Example: Basic Counter with `while`**
```bash
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

#### **Example: Reading from a File Line by Line**
```bash
while read line; do
    echo "Read line: $line"
done < "/path/to/file.txt"
```

- **Explanation**: `read line` reads each line from the file, and `< "/path/to/file.txt"` redirects the file content as input to the loop.

---

### **3. `until` Loop**
The `until` loop is the opposite of `while`; it runs until a specified condition becomes true.

#### **Basic Syntax**
```bash
until [ condition ]; do
    # commands
done
```

#### **Example: Basic Counter with `until`**
```bash
count=1
until [ $count -gt 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

**Explanation**: This will run until `count` becomes greater than 5.

---

### **4. `break` and `continue` Statements**
- **`break`**: Exits the loop entirely.
- **`continue`**: Skips the rest of the loop iteration and proceeds to the next iteration.

#### **Example: Using `break`**
```bash
for i in {1..5}; do
    if [ $i -eq 3 ]; then
        break  # Exit the loop when i equals 3
    fi
    echo "i is $i"
done
```

#### **Example: Using `continue`**
```bash
for i in {1..5}; do
    if [ $i -eq 3 ]; then
        continue  # Skip this iteration when i equals 3
    fi
    echo "i is $i"
done
```

---

### **5. Infinite Loops**
An infinite loop runs indefinitely until you manually interrupt it (e.g., with `Ctrl+C`).

#### **Example: Infinite `while` Loop**
```bash
while true; do
    echo "Press Ctrl+C to stop"
    sleep 1
done
```

- **Explanation**: `true` always evaluates to true, making this loop run forever.

---

### **6. Nested Loops**
Loops can be nested within each other, which is useful for iterating over multi-dimensional structures.

#### **Example: Nested `for` Loop**
```bash
for i in {1..3}; do
    for j in {1..3}; do
        echo "i=$i, j=$j"
    done
done
```

---

### **7. Looping Through Command Output**
You can use loops to iterate over the output of a command.

#### **Example: Loop Through Files Listed by `ls`**
```bash
for file in $(ls /path/to/directory); do
    echo "Found file: $file"
done
```

#### **Example: `while` Loop with Command Output**
```bash
ps aux | while read line; do
    echo "$line"
done
```

- **Explanation**: This example uses `ps aux` to list running processes and iterates over each line.

---

### **8. Looping Through Arrays**
In Bash, arrays can be used in loops, making it easy to process lists of values.

#### **Example: `for` Loop Over an Array**
```bash
fruits=("apple" "banana" "cherry")
for fruit in "${fruits[@]}"; do
    echo "Fruit: $fruit"
done
```

---

### **9. Summary of Loop Types and Use Cases**

| Loop Type   | Purpose                                             | Example Use Case                        |
|-------------|-----------------------------------------------------|-----------------------------------------|
| `for`       | Iterate over a fixed list or range of items         | Processing files in a directory         |
| `while`     | Repeat as long as a condition is true               | Monitoring a resource until it’s free   |
| `until`     | Repeat until a condition is true                    | Wait for a condition to be met          |
| Infinite    | Run indefinitely until interrupted                  | Service that should run continuously    |
| Nested      | Combine multiple loops                              | Working with multi-dimensional data     |
| Command output | Iterate over lines of command output             | Processing command output line-by-line  |

---

These examples should give you a solid foundation in Bash loops. Let me know if you need more details or examples on any specific loop type!