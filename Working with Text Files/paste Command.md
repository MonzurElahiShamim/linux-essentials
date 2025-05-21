# `paste` Command in Linux

The `paste` command *merges* lines from multiple files *side-by-side*, joining corresponding lines into single lines separated by a tab or a specified delimiter. It’s useful for combining columns from different files or sections of data.

- **Basic Usage**:
  ```bash
  paste file1 file2
  ```
  This combines each line of `file1` with the corresponding line of `file2`, separated by a tab.

- **Key Options**:
  - **`-d` (delimiter)**: Changes the default tab delimiter to any specified character (e.g., comma, space).
    ```bash
    paste -d, file1 file2
    ```
    This uses a comma to separate fields from each file.
  - **`-s` (serial)**: Combines all lines from each file into one line, rather than merging line-by-line.
    ```bash
    paste -s file1
    ```
    This outputs all lines from `file1` in a single row.

#### Examples

1. **Combine Two Files Side-by-Side**
   ```bash
   # file1 content:
   A
   B
   C
   
   # file2 content:
   1
   2
   3
   
   paste file1 file2
   ```
   Output:
   ```
   A   1
   B   2
   C   3
   ```

2. **Using a Custom Delimiter**
   ```bash
   paste -d":" file1 file2
   ```
   Output with colon as delimiter:
   ```
   A:1
   B:2
   C:3
   ```

3. **Serial Mode**:
   ```bash
   paste -s file1
   ```
   Output if `file1` has multiple lines:
   ```
   A B C
   ```

