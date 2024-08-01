---
updated_at: 2024-07-18T21:47:36.768+06:00
edited_seconds: 330
---
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
---
- **Function**: Matches any single character except newline (`\n`).
#### Usage: 

1. **Match Specific Patterns**:
   ```bash
   grep 'r..f' red.txt
   ```
   - **Matches**: Lines with `r` followed by any two characters, then `f`.
   - **Example Output**:
     ```
     reef
     roof
     ```

2. **Search Substrings**:
   ```bash
   grep 'r..t' /etc/passwd
   ```
   - **Matches**: Lines containing `r`, any two characters, then `t`.
   - **Example Output**:
     ```
     root:x:0:0:root:/root:/bin/bash
     operator:x:1000:37::/root:
     ```

3. **Match Minimum Length**:
   ```bash
   grep '....' red.txt
   ```
   - **Matches**: Lines with at least four characters.
   - **Example Output**:
     ```
     reef
     roof
     reed
     root
     ```

Use `.` for versatile matching of any single character except the newline.

### Square Brackets `[ ]` 
---
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
---
- **Function**: Matches zero or more occurrences of the character or pattern before it.
#### Usage

1. **Match Zero or More of a Character**:
   ```bash
   grep 're*d' red.txt
   ```
   - **Matches**: `red`, `reeed`, `rd`, `reed`
   - **Explanation**: Finds `r` followed by any number of `e` (including none), ending in `d`.

2. **Combine with Character Sets**:
   ```bash
   grep 'r[oe]*d' red.txt
   ```
   - **Matches**: `red`, `reeed`, `rd`, `rod`, `reed`
   - **Explanation**: Matches `r`, followed by zero or more `o` or `e`, ending in `d`.

3. **Refine Pattern**:
   ```bash
   grep 'ee*' red.txt
   ```
   - **Matches**: `reef`, `reeed`, `reed`, `reel`, `read`
   - **Explanation**: Finds `e` followed by zero or more `e`.

#### Key Points
- **Zero or More**: `*` allows for zero occurrences, so `re*d` matches `rd` as well as `reeed`.
- **Flexible Matching**: Use `*` with patterns or bracket expressions for versatile matching.

### Anchor Characters
---
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
---
- **Function**: Escapes special characters in regular expressions, treating them as literals.
#### Example
- **Literal Match of `*` Character**:
  ```bash
  grep 're\*' newhome.txt
  ```
  - **Matches**: Lines containing `re*`
  - **Example**:
    ```
    **Beware** of the ghost in the bedroom.
    ```

**Explanation**
- Use `\` before special characters like `*`, `^`, `$`, etc., to match them literally.
- Without `\`, `re*` matches `r` followed by zero or more `e`.
- With `\`, `re\*` specifically matches `re*` as a sequence.

The backslash `\` ensures special characters are interpreted literally in regular expressions.

## Extended Regular Expressions

Extended regular expressions offer additional functionality beyond basic regular expressions and require the `-E` option with `grep` for recognition.
#### Examples

1. **`?` Character: Optional Match**
   ```bash
   grep -E 'colou?r' spelling.txt
   ```
   - **Matches**: `color` (American English) and `colour` (British English)
   - **Explanation**: Matches `colou` followed by zero or one `u`, followed by `r`.

2. **`+` Character: One or More Matches**
   ```bash
   grep -E 'e+' red.txt
   ```
   - **Matches**: `red`, `reef`, `reeed`, `reed`, `reel`, `read`
   - **Explanation**: Matches one or more `e` characters.

3. **`|` Character: Alternation**
   ```bash
   grep -E 'gray|grey' spelling.txt
   ```
   - **Matches**: `gray` (American English) and `grey` (British English)
   - **Explanation**: Matches either `gray` or `grey`.

#### Key Points

- **`-E` Option**: Use with `grep` to enable extended regular expressions.
- **Enhanced Features**: Includes `?` for optional matches, `+` for one or more matches, and `|` for alternation.

Extended regular expressions provide powerful pattern matching capabilities useful for complex search requirements.
