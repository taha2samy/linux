
<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=linux,bash" width="400" height="200" />
  </a>
</p>

## Question 1 ❓

**Question:**  
How can I change the mode of a file to give the owner read and write permissions, the group write and execute permissions, and execute only for others (using `chmod`)?

---

### 📝 Answer:

To change the file permissions as specified, you can use the `chmod` command in two ways:

> [!NOTE]
> Assume file is called test


1. **Numeric Method**:
   The desired permissions are:
   - **Owner (User)**: Read and write
   - **Group**: Write and execute
   - **Others**: Execute only

   The command is:
   ```bash
   chmod 761 test
   ```

2. **Symbolic Method**:
   The command using symbolic notation is:
   ```bash
   chmod u=rw,g=wx,o=x test
   ```

In this command:
- `u=rw`: Sets the owner's permissions to read and write.
- `g=wx`: Sets the group's permissions to write and execute.
- `o=x`: Sets others' permissions to execute only.

---


## Question 2 ❓

**Question:**  
How can I change my default permissions to give the owner read and write permissions, the group write and execute permissions, and execute only for others?



### 📝 Answer:

To change your default permissions in a Unix-like system, you can modify your `umask` value. The `umask` determines the default permissions assigned to newly created files and directories.

To set your default permissions to the desired values, you can use the following command in your terminal:

```bash
umask 017
```

### Explanation of the umask:

1. **Numeric Method**:

The `umask 017` will result in the following default permissions:

- **Owner**: Read and write (remains unchanged)
- **Group**: Write and execute
- **Others**: Execute only

2. **Symbolic Method**:
   To set the default permissions using symbolic notation, you can use:
   ```bash
   umask u=rw,g=wx,o= 
   ```

- The symbolic method also achieves the same result by explicitly stating the desired permissions for the user, group, and others.
> ![IMPORTANT]
> Put the `umask 017` command in one of the following files:
> - `$HOME/.bash_profile`  
> - `$HOME/.bash_login`  
> - `$HOME/.profile`  
> - `$HOME/.bashrc`  
> 
> Note: The first three files are read in order during login. If any of these files exist, they will be executed one by one. The `$HOME/.bashrc` file is usually executed from one of these files (typically from `.bash_profile`).
> 
> Additionally:
> - `/etc/profile` is the system-wide configuration file for login shells, applied to all users.
> - Files in `/etc/profile.d/` can also be used to set environment variables and run scripts at login for specific applications or services.

---

## Question 3 ❓

**Question:**  
What is the maximum permission a file can have, by default when it is just created? And what is that of a directory?



### 📝 Answer:

By default, the maximum permissions for files and directories depend on the `umask` setting of the user. Here's how it works:

1. **Default File Permissions:**
   - The default maximum permission for a newly created file is **666** (read and write for owner, group, and others).
   - However, due to the `umask`, which typically removes certain permissions, the actual permissions may be less than this.

   For example, if the default `umask` is **022**, the actual permissions for a new file would be:
   ```bash
   666 - 022 = 644
   ```
   Resulting in: 
   - Owner: Read and write (rw-)
   - Group: Read only (r--)
   - Others: Read only (r--)

2. **Default Directory Permissions:**
   - The default maximum permission for a newly created directory is **777** (read, write, and execute for owner, group, and others).
   - Similar to files, the `umask` will adjust these permissions.

   For example, with a `umask` of **022**, the actual permissions for a new directory would be:
   ```bash
   777 - 022 = 755
   ```
   Resulting in:
   - Owner: Read, write, and execute (rwx)
   - Group: Read and execute (r-x)
   - Others: Read and execute (r-x)

---

## Question 4 ❓

**Question:**  
Change your default permission to read and execute for you (owner), full permission for your group member, and no permission for all the others. Create a file and a directory. Note the permissions.

---

### 📝 Answer:

To change your default permissions and create a file and directory with the specified permissions, follow these steps:

1. **Change Default Permissions:**
   To set the `umask` for your desired permissions, use the following command:
   ```bash
   umask 007
   ```

   ### Explanation of the umask:
   - **Owner (User):** Read and execute (r-x) 
   - **Group:** Full permission (rwx) 
   - **Others:** No permission (---) 

2. **Create a File:**
   To create a new file, you can use the `touch` command:
   ```bash
   touch myfile
   ```

3. **Create a Directory:**
   To create a new directory, use the `mkdir` command:
   ```bash
   mkdir mydirectory
   ```

4. **Check Permissions:**
   After creating the file and directory, you can check their permissions using:
   ```bash
   ls -l myfile mydirectory
   ```

### Expected Permissions:

After executing the above commands, the expected permissions should be:

- **For the File (myfile):**
   - Owner: Read and execute (r-x)
   - Group: Full permission (rwx)
   - Others: No permission (---)
   - Displayed as: `-r-xrwx---`

- **For the Directory (mydirectory):**
   - Owner: Read and execute (r-x)
   - Group: Full permission (rwx)
   - Others: No permission (---)
   - Displayed as: `dr-xrwx---`

---

## Question 5 ❓

**Question:**  
Copy `/etc/passwd` to your home directory. Note the permissions allowed to you before and after. Specify why?

---

### 📝 Answer:

1. **Check Initial Permissions:**
   Before copying the file, check your current permissions using:
   ```bash
   ls -l /etc/passwd
   ```

   ### Expected Permissions for `/etc/passwd`:
   - The typical permissions for `/etc/passwd` are:
     - Owner: Read (r--)
     - Group: Read (r--)
     - Others: Read (r--)
   - Displayed as: `-rw-r--r--`

2. **Copy the File:**
   To copy the `/etc/passwd` file to your home directory, use the following command:
   ```bash
   cp /etc/passwd ~/
   ```

3. **Check Permissions After Copying:**
   After copying, check the permissions of the copied file in your home directory:
   ```bash
   ls -l ~/passwd
   ```

   ### Expected Permissions for the Copied File:
   - The permissions for the copied file (e.g., `passwd` in your home directory) should typically be:
     - Owner: Read and write (rw-)
     - Group: Read (r--)
     - Others: Read (r--)
   - Displayed as: `-rw-r--r--`

4. **Note on Permissions:**
   - **Before Copying:** You had permissions to read the original file.
   - **After Copying:** The copied file allows you to read and write since the default behavior of `cp` (when copying files) preserves the original permissions for the owner but applies your user’s default umask for the group and others.


>[!TIP]
>**Why This Happens:**
> - The `cp` command copies the content of the original file and retains the ownership. As a result, the copied file inherits the user’s permissions based on the current `umask` setting.
> - Since you are the owner of the copied file, you can modify its permissions through your umask settings, which is usually set to allow read and write access for the owner.

---

## Question 6 ❓

**Question:**  
What are the minimum permissions needed for:
a. Copy a directory (source and target)  
b. Copy a file (source and target)  
c. Delete a file  
d. Change to a directory  
e. List a directory content  
f. View a file content  
g. Modify a file content  

---

### 📝 Answer:

Here are the minimum permissions required for each of the specified actions:

### a. **Copy a Directory (Source and Target)**

- **Source Directory:** 
  - **Required Permissions:** Read (r) and Execute (x)
  - **Explanation:** You need read access to list the contents and execute access to traverse into the directory.
  
- **Target Directory:**
  - **Required Permissions:** Write (w) and Execute (x)
  - **Explanation:** You need write access to create the copied directory and execute access to access the directory.

### b. **Copy a File (Source and Target)**

- **Source File:**
  - **Required Permissions:** Read (r)
  - **Explanation:** You need read access to copy the contents of the file.

- **Target Directory:**
  - **Required Permissions:** Write (w) and Execute (x)
  - **Explanation:** You need write access to create the copied file and execute access to access the directory.

### c. **Delete a File**

- **Required Permissions:** Write (w) and Execute (x) on the containing directory
- **Explanation:** You need write access to remove the file and execute access to access the directory that contains the file.

### d. **Change to a Directory**

- **Required Permissions:** Execute (x)
- **Explanation:** You need execute access to change into the directory.

### e. **List a Directory Content**

- **Required Permissions:** Read (r) and Execute (x)
- **Explanation:** You need read access to see the contents and execute access to access the directory.

### f. **View a File Content**

- **Required Permissions:** Read (r)
- **Explanation:** You need read access to view the content of the file.

### g. **Modify a File Content**

- **Required Permissions:** Write (w)
- **Explanation:** You need write access to modify the content of the file.

> [!NOTE]
> | Action                              | Required Permissions                     |
> |-------------------------------------|-----------------------------------------|
> | a. Copy a Directory                 | Source: r, x | Target: w, x           |
> | b. Copy a File                      | Source: r | Target: w, x             |
> | c. Delete a File                   | w, x (on the containing directory)      |
> | d. Change to a Directory            | x                                       |
> | e. List a Directory Content         | r, x                                    |
> | f. View a File Content              | r                                       |
> | g. Modify a File Content            | w                                       |