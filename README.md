# Méthode pour compiler un projet d'application en C :

## Empécher l'accés à la console

Pour empécher l'apparition d'un command prompt lors de l'ouverture de l'application, nous avons deux choix :
- Utiliser la commande ``FreeConsole()`` en première ligne du main (Que je déconseille ar on peut toujours voir un command prompt se fermer et s'ouvrir).
- Utiliser le flag ``-mwindows`` lors de la compilation (attention, il faut être certain de ne pas laisser de commande système qui nécessite une connection à un command prompt comme ``system("cls")``).

## Modifier l'icon de l'executable

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

## Modifier l'icon du dossier racine

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
