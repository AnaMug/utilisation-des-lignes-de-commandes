# Commandes spécifiques à Windows et PowerShell

Cette section couvre l'utilisation de la ligne de commande sous Windows avec **PowerShell**. Pour l'invite de commandes classique (`cmd.exe`), consultez la page [L'invite de commandes Windows (CMD)](windows-command-lines.md).

- [CMD ou PowerShell ?](#cmd-ou-powershell-)
- [Ouvrir PowerShell](#ouvrir-powershell)
- [Comprendre une commande PowerShell](#comprendre-une-commande-powershell)
- [Trouver de l'aide](#trouver-de-laide)
- [Navigation et gestion des fichiers](#navigation-et-gestion-des-fichiers)
- [Le pipeline : enchaîner les commandes](#le-pipeline--enchaîner-les-commandes)
- [Système, processus et réseau](#système-processus-et-réseau)
- [Variables et scripts](#variables-et-scripts)
- [Retour au guide principal](README.md)

## CMD ou PowerShell ?

- **CMD** est l'ancien interpréteur de commandes de Windows, hérité de MS-DOS. Il reste utile pour les commandes simples et les vieux scripts `.bat`.
- **PowerShell** est l'interpréteur moderne de Windows (il existe aussi sur Linux et macOS). Il est bien plus puissant : ses commandes ne renvoient pas du simple texte mais des **objets**, dont on peut sélectionner, trier ou filtrer les propriétés.
- Bonne nouvelle : PowerShell connaît des **alias** (des surnoms) qui reprennent les noms des commandes de CMD et de Linux. Par exemple `dir`, `ls`, `cd`, `cp`, `mv`, `rm`, `cat` ou `cls` fonctionnent directement.

## Ouvrir PowerShell

- Appuyez sur **Windows + X** puis choisissez « Terminal » ou « Windows PowerShell ».
- Ou bien tapez `powershell` dans la barre de recherche du menu Démarrer (ou dans une invite CMD).
- Pour les tâches d'administration, faites un clic droit et choisissez « Exécuter en tant qu'administrateur ».

## Comprendre une commande PowerShell

Les commandes PowerShell s'appellent des **cmdlets** (prononcer « command-lets »). Leur nom suit toujours la forme **Verbe-Nom**, en anglais :

| Verbe | Signification | Exemple |
| ----- | ------------- | ------- |
| `Get` | obtenir, afficher | `Get-Process` (liste les processus) |
| `Set` | modifier | `Set-Location` (change de dossier) |
| `New` | créer | `New-Item` (crée un fichier ou un dossier) |
| `Remove` | supprimer | `Remove-Item` (supprime) |
| `Copy` / `Move` | copier / déplacer | `Copy-Item`, `Move-Item` |
| `Start` / `Stop` | démarrer / arrêter | `Start-Process`, `Stop-Process` |

Les **paramètres** commencent par un tiret `-` :

```powershell
Get-ChildItem -Path C:\Users -Recurse
```

Ici `Get-ChildItem` est la cmdlet (« obtenir les éléments enfants », c'est-à-dire le contenu d'un dossier), `-Path` indique le dossier à lister et `-Recurse` demande d'inclure les sous-dossiers.

Astuce : la touche **Tab** complète les noms de cmdlets et de paramètres. Tapez `Get-Chi` puis **Tab**, ou `-Rec` puis **Tab**.

## Trouver de l'aide

- `Get-Help <cmdlet>` affiche l'aide d'une cmdlet, par exemple `Get-Help Get-ChildItem`. Ajoutez `-Examples` pour voir uniquement des exemples. La première fois, `Update-Help` (en administrateur) télécharge l'aide complète.
- `Get-Command` liste les commandes disponibles. `Get-Command *process*` cherche toutes celles qui contiennent « process ».
- `Get-Alias` liste les alias. `Get-Alias ls` montre que `ls` correspond à `Get-ChildItem`.
- `Get-Member` affiche les propriétés et méthodes des objets renvoyés par une commande : `Get-Process | Get-Member`.

## Navigation et gestion des fichiers

| Action | Cmdlet PowerShell | Alias | Exemple |
| ------ | ----------------- | ----- | ------- |
| Afficher le dossier courant | `Get-Location` | `pwd` | `Get-Location` |
| Changer de dossier | `Set-Location` | `cd` | `Set-Location C:\Users` |
| Lister le contenu | `Get-ChildItem` | `ls`, `dir` | `Get-ChildItem *.txt` |
| Créer un dossier | `New-Item -ItemType Directory` | `mkdir` | `New-Item -ItemType Directory Projet` |
| Créer un fichier vide | `New-Item -ItemType File` | | `New-Item -ItemType File notes.txt` |
| Afficher un fichier | `Get-Content` | `cat`, `type` | `Get-Content notes.txt` |
| Écrire dans un fichier | `Set-Content` / `Add-Content` | | `Add-Content notes.txt "Nouvelle ligne"` |
| Copier | `Copy-Item` | `cp`, `copy` | `Copy-Item notes.txt D:\Sauvegarde` |
| Déplacer | `Move-Item` | `mv`, `move` | `Move-Item notes.txt Archives` |
| Renommer | `Rename-Item` | `ren` | `Rename-Item notes.txt notes-old.txt` |
| Supprimer | `Remove-Item` | `rm`, `del` | `Remove-Item brouillon.txt` |
| Tester l'existence | `Test-Path` | | `Test-Path C:\Windows` (renvoie `True` ou `False`) |
| Chercher du texte | `Select-String` | `sls` | `Select-String "erreur" journal.txt` |

Quelques remarques :

- `Remove-Item -Recurse Projet` supprime un dossier et tout son contenu. **Il n'y a pas de corbeille !** Ajoutez `-WhatIf` pour voir ce qui *serait* supprimé sans rien supprimer : c'est une excellente habitude à prendre avant toute commande dangereuse.
- `Get-Content journal.txt -Tail 10` affiche les 10 dernières lignes d'un fichier, et `-Wait` permet de suivre les ajouts en direct (comme `tail -f` sous Linux).
- `Invoke-Item rapport.pdf` (alias `ii`) ouvre un fichier avec le programme associé ; `ii .` ouvre le dossier courant dans l'explorateur.

## Le pipeline : enchaîner les commandes

Comme sous Linux, le symbole `|` (*tube* ou *pipe*) envoie le résultat d'une commande à la suivante. La différence est qu'en PowerShell ce sont des **objets** qui circulent, et non du texte : on peut donc filtrer ou trier directement selon une propriété.

| Cmdlet | Rôle | Exemple |
| ------ | ---- | ------- |
| `Where-Object` (alias `where`, `?`) | filtrer | `Get-Process \| Where-Object CPU -gt 100` |
| `Sort-Object` (alias `sort`) | trier | `Get-ChildItem \| Sort-Object Length -Descending` |
| `Select-Object` (alias `select`) | choisir des propriétés ou les N premiers | `Get-Process \| Select-Object -First 5 Name, Id` |
| `Measure-Object` (alias `measure`) | compter, additionner | `Get-ChildItem \| Measure-Object Length -Sum` |
| `Format-Table` / `Format-List` | mettre en forme l'affichage | `Get-Process \| Format-Table Name, Id` |
| `Out-File` | enregistrer dans un fichier | `Get-Process \| Out-File processus.txt` |
| `Export-Csv` | exporter en CSV (ouvrable avec un tableur) | `Get-Process \| Export-Csv processus.csv` |

Exemple complet, à lire de gauche à droite :

```powershell
Get-ChildItem -Recurse -File | Sort-Object Length -Descending | Select-Object -First 5 Name, Length
```

1. `Get-ChildItem -Recurse -File` liste tous les fichiers du dossier courant et de ses sous-dossiers ;
2. `Sort-Object Length -Descending` les trie du plus gros au plus petit (`Length` est la taille en octets) ;
3. `Select-Object -First 5 Name, Length` garde les 5 premiers et n'affiche que leur nom et leur taille.

Les opérateurs de comparaison s'écrivent avec des lettres : `-eq` (égal), `-ne` (différent), `-gt` (plus grand que), `-lt` (plus petit que), `-ge` / `-le` (supérieur / inférieur ou égal), `-like` (correspond à un motif avec `*`).

## Système, processus et réseau

- `Get-Process` (alias `ps`) liste les processus en cours. `Get-Process notepad` affiche seulement le Bloc-notes.
- `Stop-Process -Name notepad` ou `Stop-Process -Id 1234` arrête un processus (alias `kill`).
- `Start-Process notepad` lance un programme. `Start-Process powershell -Verb RunAs` ouvre PowerShell en administrateur.
- `Get-Service` liste les services Windows ; `Start-Service`, `Stop-Service` et `Restart-Service` les gèrent (en administrateur).
- `Get-ComputerInfo` affiche des informations détaillées sur l'ordinateur et le système.
- `$PSVersionTable` affiche la version de PowerShell.
- `Get-NetIPAddress` affiche les adresses IP de l'ordinateur (équivalent moderne de `ipconfig`).
- `Test-Connection www.exemple.fr` teste si une machine répond (équivalent de `ping`).
- `Test-NetConnection www.exemple.fr -Port 443` vérifie si un port précis est joignable.
- `Resolve-DnsName www.exemple.fr` interroge le DNS (équivalent de `nslookup`).
- `Restart-Computer` et `Stop-Computer` redémarrent ou éteignent l'ordinateur.

## Variables et scripts

- Les variables commencent par `$` :
  ```powershell
  $prenom = "Alice"
  Write-Output "Bonjour $prenom"
  ```
- Une variable peut contenir le résultat d'une commande : `$fichiers = Get-ChildItem *.txt`, puis `$fichiers.Count` donne le nombre de fichiers.
- Les variables d'environnement s'utilisent avec `$env:` : `$env:USERNAME`, `$env:Path`.
- Une boucle pour traiter plusieurs éléments :
  ```powershell
  foreach ($f in Get-ChildItem *.txt) {
      Write-Output "Fichier : $($f.Name) - $($f.Length) octets"
  }
  ```
- Un script PowerShell est un fichier texte d'extension `.ps1` que l'on lance avec `.\mon-script.ps1`.
  Par sécurité, Windows bloque souvent l'exécution des scripts. `Get-ExecutionPolicy` affiche la règle en vigueur et `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` autorise les scripts créés sur votre ordinateur.
- Les commentaires commencent par `#`.
