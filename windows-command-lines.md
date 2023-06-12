# L'invite de lignes de commandes Windows (CMD)

Quand on travaille sous windows, il est facile de se perdre et de rechercher la même commande que l'on utilise sous `bash`, comme utiliser `rm`au lieu de `del`.

L'invite de commandes de windows est un outil puissant à portée de main de la plupart des utilisateurs, si vous travaillez sous système UNIX mais que votre client utilise WINDOWS, j'espère que ce guide vous sera utile.

- [Notions de base](#notions-de-base)
- [Navigation dans les dossier](#navigation-dans-les-dossier)
- [Gestion des fichiers](#gestion-des-fichiers)
- [Informations sur le système et le réseau](#informations-sur-le-système-et-le-réseau)
- [Gestion des processus](#gestion-des-processus)

## Notions de base

- `help` La commande `help`vous aidera à en savoir plus sur chaque commandes que vous serez ammené à utiliser.
- `cls` Cette commande sert à effacer l'écran.
- `color`à l'aide des arguments de couleur, cette commande vous permet de changer les couleurs de votre invite de commande.
`color 60`pour un texte noir sur fond jaune.
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
- `cmd` Cette commande ouvre une nouvelle instance de l'invite de commande, quand elle est utilisée sans paramètres, elle affiche les informations de version et de droits d’auteur du système d’exploitation.
    > Microsoft Windows [version xx.xxxx.xxxx.xxxx]
(c) Microsoft Corporation. Tous droits réservés.
- `prompt` Modifie l'invite de commandes, avec notemment la possibilité d'afficher le texte souhaité.
- `title <titre que vous souhaitez donner à la fenêtre` cette commande vous permet de donner un titre à votre fenêtre d'invite de commandes.
- `exit` Permet de quitter l'invite de commande ou le script actuel.
- `Tab` Cette commande vous permet de compléter automatiquement votre commande
- `F7` Cette commande vous permet de lister les commandes que vous avez utilisées précédement et de choisir l'une d'entre elle.

## Navigation dans les dossier

- `c: ou d:`Changer le disque de travail actuel vers le disque spécifié (aller du dique C:\ vers le disque D:\ par exemple).
- `cd` Changer de répertoire ou afficher le répertoire actuel
- `cd /D` Permet de changer de disque pour afficher le répertoire souhaité. Passer du disque `C:`au disque `D:` pour afficher le dossier de téléchargement avec `cd /D d:\téléchargements\`par exemple.
- `dir`Affiche les fichiers et dossiers présent dans le répertoire actuel.
- `sort`Lit l’entrée, trie les données et écrit les résultats à l’écran, dans un fichier.
- `move`.
- `md`.
- `rd`.
- `tree`.
- `attrib`.

## Gestion des fichiers

- `copy`
- `xcopy`
- `del`
- `ren`
- `comp`
- `find`
- `print`
- `notepad`

## Gestion du disque dur

- `chkdsk`
- `defrag`
- `label d:x`
- `sfc /scannow`
- `format`
- `diskpart`
- `convert`
- `fsutil`
- `recover`
- `powercfg`

## Informations sur le système et le réseau

- `date`
- `time`
- `ver`
- `hostname`
- `syteminfo`
- `driverquery`
- `ipconfig`
- `ping`
- `tracert`
- `nslookup`
- `arp`
- `getmac`

## Gestion des processus

- `schtasks`
- `tasklist`
- `taskkill`
- `set`
- `path`
- `shutdown`
- `regregedit`
- `runas`
- `powershell`
