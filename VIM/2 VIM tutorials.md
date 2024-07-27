---
updated_at: 2024-07-09T21:00:13.709+06:00
edited_seconds: 680
---
# VI tutorials
### Step-by-Step VI Tutorial

#### Moving the Cursor and Basic Editing

1. **Move the cursor to the beginning of the word "very":**
   - 
   - Press `3G` (hold down the number "3" key and press `g`) to jump to the third line.
   - Press `k` to move the cursor up one line.
   - Press `8l` (press the number eight and then `l`) to move the cursor eight characters to the right.
   - Now, the cursor should be on the letter `v` of the word "very".

2. **Delete the word “very”:**
   - Issue the command `dw` (delete word).
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     It is a powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

3. **Undo the last operation:**
   - Press `u` to undo the last delete operation.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

4. **Delete two words:**
   - Issue the command `2dw` (delete two words).
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     It is a text editor.
     Especially for those who master it.
     ~
     ```

5. **Undo the last operation:**
   - Press `u` to undo the last delete operation.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

#### Deleting Characters

6. **Delete four characters, one at a time:**
   - Type `xxxx` to delete four characters individually.
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     It is a   powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

7. **Undo the last 4 operations and recover the deleted characters:**
   - Press `4u` to undo the last four delete operations.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

8. **Delete 14 characters:**
   - Type `14x` to delete 14 characters.
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     It is a text editor.
     Especially for those who master it.
     ~
     ~
     ```

9. **Undo the last operation:**
   - Press `u` to undo the last delete operation.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

10. **Delete the five characters to the left of the cursor (type `5` then `Shift+x`):**
    - Type `5X` to delete the five characters to the left of the cursor.
    - Your screen should now look like this:
      ```vim
      Welcome to the vi editor.
      It very powerful text editor.
      Especially for those who master it.
      ~
      ~
      ```

11. **Undo the last operation:**
    - Press `u` to undo the last delete operation.
    - Your screen should revert to:
      ```vim
      Welcome to the vi editor.
      It is a very powerful text editor.
      Especially for those who master it.
      ~
      ~
      ```

#### Deleting Lines

12. **Delete the current line:**
    - Type `dd` to delete the current line.
    - Your screen should now look like this:
      ```vim
      Welcome to the vi editor.
      Especially for those who master it.
      ~
      ~
      ```


#### Pasting and Undoing Operations

13. **Paste the deleted lines below the current line:**
   - Type `p` to paste the deleted line(s) below the current line.
   - Your screen should look similar to the following:
     ```vim
     Welcome to the vi editor.
     Especially for those who master it.
     It is a very powerful text editor.
     ~
     ~
     ```

14. **Undo the last two operations:**
   - Press `2u` to undo the last two operations.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

#### Advanced Editing

15. **Delete two lines, the current and the next:**
   - Type `2dd` to delete two lines.
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     ~
     ~
     ```

16. **Undo the last operation:**
   - Press `u` to undo the last delete operation.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

17. **Move to the fourth word then delete from the current position to the end of the line:**
   - Type `4w` to move to the fourth word.
   - Press `D` (Shift+d) to delete from the current cursor position to the end of the line.
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     It is a very
     Especially for those who master it.
     ~
     ~
     ```

18. **Undo the last operation:**
   - Press `u` to undo the last delete operation.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

19. **Join two lines, the current and the next by typing a capital J (Shift+j):**
   - Type `J` (Shift+j) to join the current line with the next line.
   - Your screen should now look like this:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor. Especially for those who master it.
     ~
     ~
     ```

20. **Undo the last operation:**
   - Press `u` to undo the last join operation.
   - Your screen should revert to:
     ```vim
     Welcome to the vi editor.
     It is a very powerful text editor.
     Especially for those who master it.
     ~
     ~
     ```

#### Copying and Pasting

21. **Copy (or “yank”) the current word:**
   - Type `yw` to yank the current word (copy).
   - No change will appear on the screen.

22. **Paste (or “put”) the copied word before the current cursor:**
    - Type `P` to paste the copied word before the current cursor.
    - Your screen should look like this:
      ```vim
      Welcome to the vi editor.
      It is a very powerful powerful text editor.
      Especially for those who master it.
      ~
      ~
      ```

23. **Undo the last operation:**
    - Press `u` to undo the last paste operation.
    - Your screen should revert to:
      ```vim
      Welcome to the vi editor.
      It is a very powerful text editor.
      Especially for those who master it.
      ~
      ~
      ```

#### Moving and Joining Lines

24. **Move to the first line, then join three lines:**
    - Type `1G` to move to the first line.
    - Type `3J` to join the current line with the next three lines.
    - Your screen should now look like this:
      ```vim
      Welcome to the vi editor. It is a very powerful text editor. Especially for those who master it.
      ~
      ~
      ```

25. **Undo the last operation:**
    - Press `u` to undo the last join operation.
    - Your screen should revert to:
      ```vim
      Welcome to the vi editor.
      It is a very powerful text editor.
      Especially for those who master it.
      ~
      ~
      ```

#### Search, Replace, and Insert Operations

26. **Search for and delete the word "text" (add a space after the word "text"):** 
    - 
    - Use the command `:%s/text //g` to replace "text " with an empty space throughout the document.
    - Your screen should look like this:
      ```vi
      Welcome to the vi editor.
      It is a very powerful editor.
      Especially for those who master it.
      ~
      ~
      ```
      
27. **Navigate to beginning of file, then enter insert mode to add text:**
    - Use `1G` to go to the beginning of the file.
    - Press `i` to enter insert mode.
    - Add text to the document:
      ```vi
      Hello and Welcome to the vi editor.
      It is a very powerful editor.
      Especially for those who master it.
      ~
      ~
      ```
    - Exit insert mode by pressing the `Esc` key.

28. **Move forward one space and toggle the letter to lower case:**
    - Use `l` to move forward one space.
    - Press `~` (Shift+`)` to toggle the letter to lower case.
    - Your screen should look like this:
      ```vi
      Hello and welcome to the vi editor.
      It is a very powerful editor.
      Especially for those who master it.
      ~
      ~
      ```

29. **Save the file:**
    - Ensure you are in command mode (press `Esc` if needed).
    - Type `:w` and press `Enter` to save the changes.
    - Your file has been saved.

30. **Navigate to the space between the words "powerful" and "editor" in the second line:**
    - Use `j` to move down to the second line.
    - Use `10l` or arrow keys to move to the space between "powerful" and "editor".
    - Your cursor should be positioned correctly.

31. **Append text to the right of the cursor:**
    - Press `a` to enter insert mode after the cursor.
    - Type `text ` (including a space) to add text.
    - Your screen should look like this:
      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      Especially for those who master it.
      ~
      ```
    - Exit insert mode by pressing the `Esc` key.

32. **Open a blank line below the current line:**
    - Type `o` to open a blank line below the current line.
    - Your screen should look like this:
      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      
      Especially for those who master it.
      ~
      ```

33. **Enter text on the newly opened line:**
    - Type the following text:
      ```
      This line was added by pressing lowercase o.
      ```
    - Your screen should look like this:
      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ```
    - Exit insert mode by pressing the `Esc` key.

34. **Open a blank line above the current line:**
    - Type `O` (uppercase o) to open a blank line above the current line.
    - Your screen should look like this:
      ```
      Hello and welcome to the vi editor.
      
      It is a very powerful text editor.
      
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ```

35. **Enter text on the newly opened line:**
    - Type the following text:
      ```
      You just pressed O to open a line above.
      ```
    - Your screen should look like this:
      ```
      Hello and welcome to the vi editor.
      
      It is a very powerful text editor.
      You just pressed O to open a line above.
      
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ```
    - Exit insert mode by pressing the `Esc` key.

36. **Save the file and close the vi editor:**
    - Ensure you are in command mode.
    - Use any of the following commands to save and close:
      - `:x` (write and quit)
      - `:wq` (write and quit)
      - `:wq!` (force write and quit)
      - `ZZ` (save and quit without colon)
      - `:q!` (quit without saving changes)
      - `:e!` (discard changes and reload file)
      - `:w!` (write to read-only file, if possible)

#### Further Editing and Navigation Commands


37. **Navigate to the third line, and delete the third and fourth lines:**

    - Open myfile using the vi editor
    - Use `3G` to navigate to the third line.
    - Use `2dd` to delete the current and the next line.
    - Your screen should look similar to the following:

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      Especially for those who master it.
      ~
      ~
      ```

38. **Press the Esc key to confirm you are in command mode. Quit the vi editor without saving your changes:**

    - Press `Esc`.
    - Type `:q!` and press `Enter` to quit without saving.
    - Open myfile with the vi editor again
    - Notice that lines 3 and 4 are still present.

39. **Search forward for the word "line":**

    - Type `/line` and press `Enter`.
    - Your screen should look similar to the following:

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      You just pressed O to open a line above.
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ~
      ```

40. **Search for the next instance of the word "line" by pressing `n`:**

    - Your screen should update as follows:

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      You just pressed O to open a line above.
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ~
      ```

41. **Search backward for the word "line":**

    - Type `?line` and press `Enter`.
    - Your screen should look similar to the following:

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      You just pressed O to open a line above.
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ~
      ```

42. **Search for the previous instance of the word "line" by pressing `n`:**

    - Your screen should update and indicate "search hit TOP, continuing at BOTTOM":

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      You just pressed O to open a line above.
      This line was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ~
      ```

43. **Replace the word "line" with "entry":**

    - Use `cw` to change the word "line".
    - Type `entry` to replace it.
    - Your screen should look similar to the following:

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor.
      You just pressed O to open a line above.
      This entry was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ~
      ```

44. **Press the Esc key to exit insert mode. Add text at the beginning of a line:**

    - Use `I` to enter insert mode at the beginning of the line.
    - Add the desired text.

45. **Add text at the end of a line:**

    - Move to the second line with `2G`.
    - Press `A` to append text at the end of the line.
    - Type `[Space]Indeed!` to add the phrase.
    - Press `Esc` to return to command mode.
    - Your screen should look like this:

      ```
      Hello and welcome to the vi editor.
      It is a very powerful text editor. Indeed!
      You just pressed O to open a line above.
      This entry was added by pressing lowercase o.
      Especially for those who master it.
      ~
      ~
      ```

46. **Save your changes and exit vi:**

    - Ensure you are in command mode.
    - Type `:x` and press `Enter` to save and exit.

Congratulations! You have completed additional advanced tasks in the vi editor, including searching, replacing, and modifying text in various ways. These commands will help you efficiently edit and navigate through your documents.