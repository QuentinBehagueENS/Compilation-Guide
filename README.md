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


## Méthode pour compiler un projet d'application en C :

### Empécher l'accés à la console

Pour empécher l'apparition d'un command prompt lors de l'ouverture de l'application, nous avons deux choix :
- Utiliser la commande ``FreeConsole()`` en première ligne du main (Que je déconseille ar on peut toujours voir un command prompt se fermer et s'ouvrir).
- Utiliser le flag ``-mwindows`` lors de la compilation (attention, il faut être certain de ne pas laisser de commande système qui nécessite une connection à un command prompt comme ``system("cls")``).

### Modifier l'icon de l'executable

Un peut plus compliqué, il faut ici placer votre fichier .ico dans e bin puis ouvrir un fichier ***resources.rs*** dont le contenu est le suivant :
```c
    ID_ICON ICON "path/icon.ico"
```

Ensuite, compiler ce fichier au format .o à l'aide de la commande suivante 
```
    windres resources.rc -o resources.o
```

(Le fichier ***resources.rs*** n'est alors plus nécessaire, vous pouvez le supprimer.)
Enfin, il ne reste plus qu'à modifier la commande de compilation, effectuée depuis la racine du projet, pour prendre en compte ce fichier :
```gcc src\*.c bin\resources.o -o ...```

### Modifier l'icon du dossier racine

Il existe deux solutions :
- Modifier manuellement l'icone du dossier : après un clic droit, sélectionner **Propriétés>Personaliser>Changer d'icône...** Malheuresement cette méthode ne prend en compte que des chemins absolus. En particulier, à chaque fois que le dossier est déplacé, il faudra changé le PATH manuellement
- Une solution consiste à ouvrir le fichier caché ***desktop.ini*** à l'aide de votre éditeur de code et changer le PATH pour un chemin realtif :

```ini
[.ShellClassInfo]
IconResource=.bin\icon.ico,0
[ViewState]
Mode=
Vid=
FolderType=
```
