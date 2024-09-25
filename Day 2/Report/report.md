
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
> file is called test


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




```bash
source ~/.bashrc
```
