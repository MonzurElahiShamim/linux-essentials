---
updated_at: 2024-09-10T19:34:07.584+06:00
edited_seconds: 40
---
### `export` Command in Linux

- **Purpose**: Sets and exports environment variables, making them available to child processes and scripts.
- **Usage**: 
  ```bash
  export VARIABLE_NAME=value
  ```
  Sets `VARIABLE_NAME` and makes it accessible to other programs.

- **Key Features**:
  - **Environment Management**: Controls variables that configure processes.
  - **Session Scope**: Changes affect the current session and child processes.
  - **Persistence**: Add `export` commands to `.bashrc` or `.bash_profile` to keep variables set across sessions.

- **Examples**:
  - **Set and Export**: 
    ```bash
    export PATH=/usr/local/bin:$PATH
    ```
    Updates the `PATH` to include `/usr/local/bin`.
  - **View Variables**: Use `export`, `env`, or `printenv` to list exported variables.

`export` is essential for managing environment settings, ensuring variables are available to scripts and commands throughout the session.

