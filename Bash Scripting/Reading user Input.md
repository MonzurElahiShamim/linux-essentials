# Reading user input

In Bash scripting, you can read user input using the `read` command. Here are some examples of how to use it:

### 1. **Simple User Input**
   ```bash
   echo "Enter your name:"
   read name
   echo "Hello, $name!"
   ```

   - This will prompt the user to enter their name, store it in the `name` variable, and then display a greeting.

### 2. **Prompting with `-p` Option**
   ```bash
   read -p "Enter your favorite color: " color
   echo "Your favorite color is $color."
   ```

   - The `-p` option allows you to include the prompt message on the same line as the `read` command.

### 3. **Silent Input with `-s` (for Passwords)**
   ```bash
   read -s -p "Enter your password: " password
   echo
   echo "Password received."
   ```

   - The `-s` option hides the input (useful for passwords). Note that `echo` on a new line is often added to ensure the next output appears on a new line.

### 4. **Reading Multiple Variables**
   ```bash
   echo "Enter your first and last name:"
   read first_name last_name
   echo "First Name: $first_name"
   echo "Last Name: $last_name"
   ```

   - This reads two inputs separated by a space and stores them in `first_name` and `last_name` respectively.

### 5. **Using a Default Value with Input**
   ```bash
   read -p "Enter your country (default: USA): " country
   country=${country:-USA}
   echo "Country: $country"
   ```

   - If the user doesn’t input anything, the variable `country` will default to "USA" by using `${variable:-default}` syntax.

### 6. **Timeout Option with `-t`**
   ```bash
   read -t 5 -p "Enter your age (you have 5 seconds): " age
   if [ -z "$age" ]; then
       echo "Timed out. No input received."
   else
       echo "You entered: $age"
   fi
   ```

   - The `-t` option sets a timeout in seconds for input. If no input is received within 5 seconds, the `age` variable remains empty.

These examples should cover common scenarios for reading user input in Bash scripts. Let me know if you want examples for specific use cases!