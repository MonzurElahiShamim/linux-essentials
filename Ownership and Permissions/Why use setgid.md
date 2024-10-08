---
updated_at: 2024-08-29T22:22:06.896+06:00
edited_seconds: 60
---
Why would an *administrator* want to set up a `setgid` directory? First, consider the following user accounts:

- The user `bob` is a member of the `payroll` group.
- The user `sue` is a member of the `staff` group.
- The user `tim` is a member of the `acct` group.

In this scenario, these three users need to work on a joint project. They approach the administrator to ask for a shared directory in which they can work together, but that no one else can access their files. The administrator does the following:

1. Creates a new group called `team`.
2. Adds `bob`, `sue`, and `tim` to the `team` group.
3. Makes a new directory called `/home/team`.
4. Makes the group owner of the `/home/team` directory be the `team` group.
5. Gives the `/home/team` directory the following permissions: `rwxrwx---`

As a result, `bob`, `sue`, and `tim` can access the `/home/team` directory and add files. However, there is a potential problem: when `bob` creates a file in the `/home/team` directory, the new file is owned by his primary group:

`-rw-r-----. 1 bob payroll 100 Oct 30 23:21 /home/team/file.txt`

Unfortunately, while `sue` and `tim` can access the `/home/team` directory, they can't do anything with bob's file. Their permissions for that file are the others permissions (`---`).

If the administrator sets the setgid permission to the `/home/team` directory, then when `bob` creates a file, it is owned the `team` group:

`-rw-r-----. 1 bob team 100 Oct 30 23:21 /home/team/file.txt`

As a result, `sue` and `tim` would have access to the file through the group owner permissions (`r--`).

Certainly, `bob` could change the group ownership or the others permissions after creating the file, but that would become tedious if there were many new files being created. The setgid permission makes it easier for this situation.

