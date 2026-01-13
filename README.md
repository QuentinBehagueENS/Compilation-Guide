# ***Compilation Guide***

## Method to Compile a C Application Project


### Preventing Console Access

To prevent the appearance of a command prompt when launching the application, you have two options:

- Use the `FreeConsole()` command as the first line of the `main` function (**not recommended**, as a command prompt might still briefly appear and then close).
- Use the `-mwindows` flag during compilation (**preferred**). Note that this requires ensuring no system calls requiring a command prompt, such as `system("cls")`, are present in your code.

---

### Changing the Executable Icon

This step is slightly more complex. You need to place your `.ico` file in the `bin` directory, then create a file named **`resources.rc`** with the following content:

```bash
ID_ICON ICON "path/icon.ico"
```

Next, compile this file into an .o format using the following command:
```bash
windres resources.rc -o resources.o
```

(Once compiled, the ***resources.rc*** file is no longer needed and can be safely deleted.)

Finally, modify the compilation command from the project root to include this object file:

```bash
gcc src\*.c bin\resources.o -o ...
```
---

### Changing the Root Folder Icon

There are two solutions:

- Manually change the folder icon : Right-click on the folder and select Properties > Customize > Change Icon... Unfortunately, this method only supports absolute paths. If the folder is moved, the path must be updated manually.

- Modify the desktop.ini file. Open the hidden desktop.ini file using your code editor and modify it to include a relative path:

```ini
[.ShellClassInfo]
IconResource=.bin\icon.ico,0
[ViewState]
Mode=
Vid=
FolderType=
```



------


