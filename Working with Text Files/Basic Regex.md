# Basic Regular Expressions (BRE)

#### Overview
- **Regular Expressions (regex)**: A collection of characters used to define search patterns.
- **Types of Characters**:
  - **Normal Characters**: Alphanumeric characters that match themselves (e.g., `a` matches `a`).
  - **Special Characters**: Characters with special meanings used to match more complex patterns (e.g., `.`, `*`, `^`, `$`).

#### Basic Regular Expressions

| Character | Matches                                                                                       |
|-----------|-----------------------------------------------------------------------------------------------|
| `.`       | Any single character                                                                          |
| `[ ]`     | A list or range of characters to match one character.                                         |
|           | - If the first character is `^` within brackets, it matches any character not in the list.    |
| `*`       | The previous character repeated zero or more times                                            |
| `^`       | - At the beginning of the pattern: matches the start of the line.                             |
|           | - Elsewhere: matches the literal `^` character.                                               |
| `$`       | - At the end of the pattern: matches the end of the line.                                      |
|           | - Elsewhere: matches the literal `$` character.                                               |

#### Usage in Commands
- **`grep`**: A common command for searching text using regex patterns.
- **Other Commands**: `more`, `less`, and other text processing tools support regex.

#### Best Practices
- **Single Quotes**: Use single quotes around regex patterns to prevent the shell from interpreting special characters (e.g., `'pattern'`).

Regular expressions in Basic form are widely supported and provide essential functionality for text search and manipulation. For more complex needs, **[[#Extended Regular Expressions|Extended Regular Expressions (ERE)]]** are used, which include additional features beyond the basics described here.

### The Period `.` Character
- **Purpose**: Define a list or range of characters to match a single character.
- **Syntax**: `[char1char2...]`
  - Matches any one character listed within the brackets.
#### Usage

1. **List of Characters**:
   - Matches any one of the characters inside the brackets.
   ```bash
   grep '[aeiou]' file.txt
   ```
   Matches any vowel (`a`, `e`, `i`, `o`, or `u`).

2. **Range of Characters**:
   - Matches any character within the specified range.
   ```bash
   grep '[a-z]' file.txt
   ```
   Matches any lowercase letter from `a` to `z`.

3. **Negation**:
   - If the first character inside the brackets is `^`, it matches any character not listed.
   ```bash
   grep '[^aeiou]' file.txt
   ```
   Matches any character that is not a vowel.
#### Key Points

- `[0-9]` matches any digit.
- `[A-F]` matches any uppercase letter from `A` to `F`.
- `[a-zA-Z]` matches any letter (upper or lower case).

Use square brackets to create flexible matching patterns for single characters within a specified set or range.

### The Asterisk `*` Character in Regular Expressions
- **Function**: Ensure matches occur at specific positions in a line.
#### Usage

1. **Caret `^`: Beginning of Line**
   ```bash
   grep '^root' /etc/passwd
   ```
   - **Matches**: Lines starting with `root`
   - **Example**:
     ```
     root:x:0:0:root:/root:/bin/bash
     ```

2. **Dollar Sign `$`: End of Line**
   ```bash
   grep 'r$' alpha-first.txt
   ```
   - **Matches**: Lines ending with `r`
   - **Example**:
     ```
     B is for Bear
     F is for Flower
     ```

#### Key Points
- **`^` (Caret)**: Use at the start of the pattern to match the beginning of lines.
- **`$` (Dollar Sign)**: Use at the end of the pattern to match the end of lines.

Anchors refine searches to specific line positions, increasing search precision.

### The Backslash `\` Character
