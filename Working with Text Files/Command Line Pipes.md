---
updated_at: 2024-07-06T12:30:48.763+06:00
edited_seconds: 110
---
# [[Command Line Pipes]]

Command Line Pipes allow chaining commands together by using the `|` character to redirect the output of one command as input to another. This enables powerful operations, especially for refining data or processing large outputs without displaying them directly.

- **Basic Functionality**:
  - Output from one command serves as input for the next.
  - Useful for handling large outputs or refining command results.

- **Example Usage**:
  - **Listing Files and Using `head`**:
    ```bash
    ls /etc | head
    ```
    - Displays the first ten files in the `/etc` directory without scrolling through entire output.

- **Multiple Pipes**:
  - Commands can be linked consecutively:
    ```bash
    ls /etc/ssh | nl | tail -5
    ```
    - Lists files in `/etc/ssh`, numbers lines, and shows the last five lines using `tail`.
```Output
6 ssh_host_ed25519_key.pub 
7 ssh_host_rsa_key 
8 ssh_host_rsa_key.pub 
9 ssh_import_id 
10 sshd_config
```

- **Order of Commands**:
  - Each command in a pipe sequence operates on the output of the preceding command.
  - Careful order selection ensures desired results:
    ```bash
    ls /etc/ssh | tail -5 | nl
    ```
    - Numbers only the last five files listed by `ls /etc/ssh`.
```Output
1 ssh_host_ed25519_key.pub 
2 ssh_host_rsa_key 
3 ssh_host_rsa_key.pub 
4 ssh_import_id 
5 sshd_config
```

- **Considerations**:
  - Understand how commands interact in sequence to achieve intended output.
  - Effective for managing and analyzing command outputs efficiently in Unix/Linux environments.