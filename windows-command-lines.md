# L'invite de commandes Windows (CMD)

Quand on travaille sous Windows, on cherche souvent par réflexe la même commande que sous `bash`, par exemple `rm` au lieu de `del`.

L'invite de commandes de Windows (`cmd.exe`) est un outil puissant, à portée de main de la plupart des utilisateurs. Que vous découvriez la ligne de commande ou que vous ayez l'habitude d'un système UNIX alors que vous devez travailler sous Windows, ce guide devrait vous être utile.

- [Avant de commencer](#avant-de-commencer)
- [Notions de base](#notions-de-base)
- [Navigation dans les dossiers](#navigation-dans-les-dossiers)
- [Gestion des fichiers](#gestion-des-fichiers)
- [Gestion du disque dur](#gestion-du-disque-dur)
- [Informations sur le système et le réseau](#informations-sur-le-système-et-le-réseau)
- [Gestion des processus et du système](#gestion-des-processus-et-du-système)
- [Correspondance entre CMD et Bash](#correspondance-entre-cmd-et-bash)
- [Retour au guide principal](README.md)

## Avant de commencer

- **Ouvrir l'invite de commandes** : appuyez sur les touches **Windows + R**, tapez `cmd` puis appuyez sur **Entrée**. Vous pouvez aussi taper « invite de commandes » dans la barre de recherche du menu Démarrer.
- **En mode administrateur** : certaines commandes (`chkdsk`, `sfc`, `diskpart`, etc.) demandent des droits élevés. Faites un clic droit sur « Invite de commandes » puis choisissez « Exécuter en tant qu'administrateur ».
- **Lire une commande** : une commande se compose d'un *nom* (ce qu'on veut faire), éventuellement suivi d'*options* (qui modifient son comportement, sous Windows elles commencent par `/`) et d'*arguments* (ce sur quoi la commande agit, par exemple un fichier).
  ```bat
  dir /s C:\Users
  ```
  Ici `dir` est la commande, `/s` est une option (« inclure les sous-dossiers ») et `C:\Users` est l'argument (le dossier à lister).
- **Les chemins** : sous Windows, les dossiers sont séparés par une barre oblique inversée `\` (sous Linux c'est `/`). Si un chemin contient des espaces, mettez-le entre guillemets : `cd "C:\Program Files"`.
- **Majuscules / minuscules** : CMD ne fait pas la différence entre `DIR`, `Dir` et `dir`.
- **Obtenir de l'aide sur une commande** : ajoutez `/?` après le nom de la commande, par exemple `copy /?`.

## Notions de base

- `help` affiche la liste des commandes disponibles. `help <commande>` (par exemple `help dir`) explique une commande en détail, comme `<commande> /?`.
- `cls` (*clear screen*) efface l'écran. Équivalent de `clear` sous Linux.
- `echo` affiche un texte à l'écran : `echo Bonjour` affiche `Bonjour`. Très utilisé dans les scripts.
- `color` change les couleurs de l'invite de commandes. Elle prend deux caractères : le premier pour la couleur du fond, le second pour la couleur du texte.
  Par exemple `color 60` affiche un texte noir sur fond jaune, et `color` sans argument rétablit les couleurs par défaut.

    | Couleur     | Code | Couleur     | Code |
    | ----------- | -----| ----------- | -----|
    | Noir        | 0    | Gris        | 8    |
    | Bleu        | 1    | Bleu clair  | 9    |
    | Vert        | 2    | Vert clair  | a    |
    | Aqua        | 3    | Aqua clair  | b    |
    | Rouge       | 4    | Rouge clair | c    |
    | Pourpre     | 5    | Violet      | d    |
    | Jaune       | 6    | Jaune clair | e    |
    | Gris clair  | 7    | Blanc       | f    |

- `cmd` ouvre une nouvelle instance de l'invite de commandes. Utilisée sans paramètre, elle affiche les informations de version et de droits d'auteur du système d'exploitation :
    > Microsoft Windows [version xx.xxxx.xxxx.xxxx]
    > (c) Microsoft Corporation. Tous droits réservés.
- `prompt` modifie le texte affiché au début de chaque ligne (l'*invite*). Par exemple `prompt $P$G` affiche le chemin courant suivi de `>` (c'est la valeur par défaut) et `prompt Ma console$G` affiche `Ma console>`.
- `title <titre>` donne un titre à la fenêtre de l'invite de commandes, par exemple `title Exercice 1`.
- `exit` ferme l'invite de commandes ou arrête le script en cours.
- **Tab** n'est pas une commande mais une touche : elle complète automatiquement le nom d'un fichier ou d'un dossier. Appuyez plusieurs fois pour faire défiler les propositions.
- **F7** affiche la liste des commandes utilisées précédemment et permet d'en choisir une. Les flèches **haut** et **bas** permettent aussi de rappeler les commandes précédentes.
- **Ctrl + C** interrompt la commande en cours (utile si une commande ne s'arrête pas).

## Navigation dans les dossiers

- `c:` ou `d:` change de lecteur de travail (passer du disque `C:\` au disque `D:\` par exemple).
- `cd` (*change directory*) change de dossier ou, sans argument, affiche le dossier courant.
  - `cd Documents` entre dans le sous-dossier `Documents` ;
  - `cd ..` remonte d'un niveau (dans le dossier parent) ;
  - `cd \` retourne à la racine du lecteur (par exemple `C:\`).
- `cd /D` change à la fois de lecteur et de dossier. Par exemple `cd /D D:\Téléchargements` passe du disque `C:` au dossier de téléchargement du disque `D:`.
- `dir` affiche les fichiers et dossiers présents dans le dossier courant. Options utiles : `dir /s` (inclut les sous-dossiers), `dir /a` (affiche aussi les fichiers cachés), `dir /o:n` (trie par nom), `dir *.txt` (seulement les fichiers `.txt`).
- `tree` affiche l'arborescence des dossiers sous forme d'arbre. `tree /f` affiche aussi les fichiers.
- `md` (ou `mkdir`, *make directory*) crée un dossier : `md MonProjet`.
- `rd` (ou `rmdir`, *remove directory*) supprime un dossier **vide**. `rd /s MonProjet` supprime le dossier et tout son contenu (une confirmation est demandée, sauf si on ajoute `/q`). **Attention, il n'y a pas de corbeille !**
- `move` déplace un fichier ou un dossier, ou le renomme : `move rapport.txt Archives\`.
- `attrib` affiche ou modifie les attributs d'un fichier : `+r` / `-r` (lecture seule), `+h` / `-h` (caché), `+s` / `-s` (fichier système). Par exemple `attrib +h secret.txt` cache le fichier.
- `pushd` et `popd` : `pushd D:\Projet` mémorise le dossier courant puis se déplace, `popd` permet ensuite de revenir au dossier mémorisé.

## Gestion des fichiers

- `type` affiche le contenu d'un fichier texte : `type notes.txt` (équivalent de `cat` sous Linux).
- `more` affiche un long texte page par page : `type long.txt | more` (appuyez sur **Espace** pour la page suivante, **Q** pour quitter).
- `copy` copie un ou plusieurs fichiers : `copy notes.txt D:\Sauvegarde\`. On peut aussi concaténer des fichiers : `copy a.txt + b.txt total.txt`.
- `xcopy` copie des fichiers **et des dossiers** avec plus d'options : `xcopy Source Destination /s /e` copie aussi tous les sous-dossiers, même vides. Pour les copies importantes, `robocopy` est plus récent, plus rapide et capable de reprendre une copie interrompue.
- `del` (ou `erase`) supprime un ou plusieurs fichiers : `del brouillon.txt`, `del *.tmp`. Ajoutez `/p` pour demander une confirmation pour chaque fichier. **Les fichiers supprimés ne passent pas par la corbeille !**
- `ren` (ou `rename`) renomme un fichier : `ren ancien.txt nouveau.txt`. Avec les jokers : `ren *.txt *.bak` change l'extension de tous les fichiers `.txt`.
- `comp` compare le contenu de deux fichiers octet par octet. `fc` fait la même chose mais affiche les lignes différentes, ce qui est plus lisible pour des fichiers texte : `fc version1.txt version2.txt`.
- `find` recherche un texte dans un ou plusieurs fichiers : `find "erreur" journal.txt`. Options : `/i` ignore la casse, `/c` compte les lignes trouvées, `/n` affiche les numéros de ligne. `findstr` est plus puissant et accepte des expressions régulières.
- `sort` trie les lignes d'un fichier ou du résultat d'une commande et affiche le résultat à l'écran ou dans un fichier : `sort noms.txt`, `sort /r noms.txt` (ordre inverse), `sort noms.txt /o tries.txt` (enregistre le résultat).
- `print` envoie un fichier texte à l'imprimante : `print /d:LPT1 notes.txt`.
- `notepad` ouvre le Bloc-notes, éventuellement avec un fichier : `notepad notes.txt`.
- `start` ouvre un fichier avec le programme associé, ou un dossier dans l'explorateur : `start rapport.pdf`, `start .` (ouvre le dossier courant).

### Les jokers, les redirections et les tubes

Comme sous Linux, ces caractères spéciaux permettent de combiner les commandes :

| Symbole | Rôle | Exemple |
| ------- | ---- | ------- |
| `*` | remplace n'importe quelle suite de caractères | `del *.tmp` |
| `?` | remplace un seul caractère | `dir photo?.jpg` |
| `>` | envoie le résultat dans un fichier (l'écrase s'il existe) | `dir > liste.txt` |
| `>>` | ajoute le résultat à la fin d'un fichier | `echo Fin >> liste.txt` |
| `<` | lit l'entrée depuis un fichier | `sort < noms.txt` |
| `\|` | (*tube* ou *pipe*) envoie le résultat d'une commande à la suivante | `tasklist \| find "chrome"` |
| `&&` | exécute la 2ᵉ commande seulement si la 1ʳᵉ a réussi | `md Test && cd Test` |

## Gestion du disque dur

La plupart de ces commandes nécessitent une invite de commandes **ouverte en tant qu'administrateur**. Certaines (`format`, `diskpart`, `convert`) peuvent **effacer des données** : à utiliser avec la plus grande prudence.

- `chkdsk` (*check disk*) vérifie l'état d'un disque et affiche un rapport. `chkdsk C: /f` corrige les erreurs trouvées (un redémarrage peut être nécessaire pour le disque système).
- `defrag` défragmente un disque, c'est-à-dire regroupe les morceaux de fichiers dispersés pour accélérer leur lecture : `defrag C: /a` analyse seulement, `defrag C: /o` optimise. Inutile (voire déconseillé) sur un SSD, que Windows optimise automatiquement.
- `label` change le nom (l'étiquette) d'un disque : `label D: Sauvegardes`.
- `vol` affiche le nom et le numéro de série d'un disque : `vol C:`.
- `sfc /scannow` (*System File Checker*) vérifie l'intégrité des fichiers système de Windows et répare ceux qui sont endommagés.
- `format` formate un disque, c'est-à-dire **efface tout son contenu** et prépare un nouveau système de fichiers : `format E: /fs:NTFS`.
- `diskpart` ouvre un outil interactif de gestion des disques et des partitions (`list disk`, `select disk 1`, `list partition`, `exit`...). **Outil puissant : une erreur peut effacer un disque entier.**
- `convert` convertit un disque FAT32 en NTFS sans perdre les données : `convert E: /fs:ntfs`.
- `fsutil` regroupe des outils avancés sur le système de fichiers. Par exemple `fsutil volume diskfree C:` affiche l'espace libre.
- `recover` tente de récupérer les données lisibles d'un fichier situé sur un disque endommagé : `recover D:\document.txt`.
- `powercfg` gère les options d'alimentation. `powercfg /batteryreport` génère un rapport HTML sur l'état de la batterie d'un ordinateur portable, `powercfg /list` liste les modes d'alimentation.

## Informations sur le système et le réseau

### Système

- `date` affiche la date du jour et propose de la modifier. `date /t` affiche seulement la date.
- `time` affiche l'heure et propose de la modifier. `time /t` affiche seulement l'heure.
- `ver` affiche la version de Windows.
- `hostname` affiche le nom de l'ordinateur sur le réseau.
- `whoami` affiche le nom de l'utilisateur connecté.
- `systeminfo` affiche de nombreuses informations sur l'ordinateur : version de Windows, date d'installation, processeur, mémoire, mises à jour installées, etc.
- `driverquery` liste les pilotes (*drivers*) installés. `driverquery /v` donne plus de détails.

### Réseau

- `ipconfig` affiche la configuration réseau : adresse IP, masque de sous-réseau, passerelle par défaut.
  - `ipconfig /all` affiche tous les détails, dont l'adresse MAC et les serveurs DNS.
  - `ipconfig /release` puis `ipconfig /renew` libèrent puis redemandent une adresse IP au serveur DHCP.
  - `ipconfig /flushdns` vide le cache DNS.
- `ping` vérifie si une machine répond sur le réseau et mesure le temps de réponse : `ping 8.8.8.8` ou `ping www.exemple.fr`. `ping -t` continue jusqu'à ce qu'on appuie sur **Ctrl + C**.
- `tracert` affiche le chemin (les routeurs traversés) pour atteindre une machine : `tracert www.exemple.fr`. Équivalent de `traceroute` sous Linux.
- `nslookup` interroge un serveur DNS pour connaître l'adresse IP correspondant à un nom de domaine (et inversement) : `nslookup www.exemple.fr`.
- `netstat` affiche les connexions réseau en cours. `netstat -an` affiche toutes les connexions avec les adresses et ports en chiffres, `netstat -ano` ajoute le numéro du processus (PID) concerné.
- `arp -a` affiche la table ARP, c'est-à-dire la correspondance entre adresses IP et adresses MAC des machines du réseau local.
- `getmac` affiche l'adresse MAC des cartes réseau de l'ordinateur.

## Gestion des processus et du système

Un *processus* est un programme en cours d'exécution. Chaque processus possède un numéro unique, le *PID* (*Process IDentifier*).

- `tasklist` liste les processus en cours avec leur PID et la mémoire utilisée. Équivalent de `ps` sous Linux. On peut filtrer : `tasklist | find "notepad"`.
- `taskkill` arrête un processus, soit par son nom : `taskkill /im notepad.exe`, soit par son PID : `taskkill /pid 1234`. Ajoutez `/f` pour forcer l'arrêt.
- `schtasks` crée, liste ou supprime des tâches planifiées (exécutées automatiquement à une heure donnée) : `schtasks /query` liste les tâches, `schtasks /create /tn "Sauvegarde" /tr "C:\sauvegarde.bat" /sc daily /st 18:00` lance un script tous les jours à 18 h.
- `set` affiche ou définit des *variables d'environnement* (des valeurs mémorisées par le système). `set` seul les affiche toutes, `set PRENOM=Alice` crée une variable, et `echo %PRENOM%` affiche sa valeur.
- `path` affiche ou modifie la variable `PATH`, c'est-à-dire la liste des dossiers dans lesquels Windows cherche les programmes quand on tape une commande.
- `where` indique où se trouve un programme : `where notepad`.
- `shutdown` éteint ou redémarre l'ordinateur : `shutdown /s /t 0` éteint immédiatement, `shutdown /r /t 60` redémarre dans 60 secondes, `shutdown /a` annule un arrêt programmé.
- `regedit` ouvre l'éditeur du Registre (la base de données de configuration de Windows). **Modifier le registre sans savoir ce que l'on fait peut rendre Windows instable.** En ligne de commande, `reg query` permet de consulter le registre sans le modifier.
- `runas` exécute un programme sous l'identité d'un autre utilisateur : `runas /user:Administrateur cmd`.
- `powershell` lance PowerShell, l'interpréteur de commandes plus moderne de Windows, depuis CMD. Voir la page [Windows et PowerShell](PowerShell.md).

## Correspondance entre CMD et Bash

Ce tableau aide à retrouver une commande quand on connaît son équivalent sous Linux (et inversement) :

| Action | CMD (Windows) | Bash (Linux / macOS) |
| ------ | ------------- | -------------------- |
| Afficher le dossier courant | `cd` | `pwd` |
| Lister les fichiers | `dir` | `ls -l` |
| Changer de dossier | `cd` | `cd` |
| Créer un dossier | `md` | `mkdir` |
| Supprimer un dossier | `rd /s` | `rm -r` |
| Copier un fichier | `copy` | `cp` |
| Déplacer / renommer | `move` / `ren` | `mv` |
| Supprimer un fichier | `del` | `rm` |
| Afficher un fichier | `type` | `cat` |
| Chercher du texte | `find` / `findstr` | `grep` |
| Effacer l'écran | `cls` | `clear` |
| Lister les processus | `tasklist` | `ps` |
| Arrêter un processus | `taskkill` | `kill` |
| Configuration réseau | `ipconfig` | `ip addr` (ou `ifconfig`) |
| Suivre la route réseau | `tracert` | `traceroute` |
| Aide sur une commande | `commande /?` | `man commande` ou `commande --help` |
