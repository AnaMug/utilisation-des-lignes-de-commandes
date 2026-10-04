## Contribuer à L'art de la ligne de commande

Ce guide est un [travail collaboratif](AUTHORS.md), fondé sur le travail généreux de nombreux contributeurs. Cette version française s'appuie sur « [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line) » de Joshua Levy et l'enrichit d'explications destinées aux élèves, ainsi que de pages consacrées à Windows ([CMD](windows-command-lines.md) et [PowerShell](PowerShell.md)).

## Questions

[![Poser une question](https://img.shields.io/badge/%3f-Poser%20une%20question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

La façon la plus simple d'aider est de [**soumettre les questions que vous vous posez**](https://airtable.com/shrzMhx00YiIVAWJg).
Plus il y en a, mieux c'est : les questions permettent de repérer les endroits où le guide doit être amélioré.


## Contributions

Les contributions de toutes sortes, y compris les corrections, ajouts, améliorations et traductions, sont les bienvenues !

Nous espérons que vous participerez, que ce soit un peu ou beaucoup.
Voici quelques conseils avant de vous lancer.

### Style

- Restez aussi proche que possible du style existant du document.
- Visez la **concision**, la **précision** et l'**utilité**.
- Les noms des commandes, options et exemples de code restent tels quels (en anglais) : seuls les textes explicatifs et les commentaires sont traduits.
- Pour les pages destinées aux élèves, privilégiez des explications courtes accompagnées d'un exemple concret ; pour le reste, préférez les liens vers des ressources aux longues explications.
- Signalez clairement les commandes dangereuses (suppression, formatage, droits administrateur).

### Utiliser les tickets (*issues*) et les demandes de fusion (*pull requests*)

- N'hésitez pas à **créer et commenter des tickets** pour discuter. Une grande partie de la difficulté à accepter des demandes de fusion tient au style, à la forme et à l'opportunité même des changements : expliquer les raisons d'une modification est donc utile.
- Merci de **consulter les tickets et demandes de fusion ouverts** avant d'en soumettre un nouveau, afin d'éviter les doublons.
- Dans la mesure du possible, **découpez vos changements en plusieurs demandes de fusion** afin qu'elles puissent être validées séparément. Les grosses contributions sont aussi les bienvenues, mais elles sont plus difficiles et plus longues à valider, car elles demandent souvent des discussions ou une réécriture.


## Traductions

Le guide original est disponible dans de nombreuses langues. Voici le fonctionnement des traductions dans le projet d'origine :

- La version originale du guide est maintenue en anglais (voir [README-en.md](README-en.md)).
- *Les traductions suivent le contenu de l'original.* Les contributeurs d'une traduction doivent donc pouvoir lire un peu l'anglais, afin que les traductions ne s'en éloignent pas (sauf pour la correction d'une coquille).
- Chaque traduction a un responsable qui la met à jour au fur et à mesure que l'original évolue et qui relit les modifications des autres. Cela ne demande pas beaucoup de temps, mais cette relecture est importante pour la qualité.
- Consultez le fichier [AUTHORS.md](AUTHORS.md) pour connaître les responsables actuels (ce fichier est généré à partir du fichier [authors-info.yml](admin/authors-info.yml)).

### Modifier une traduction

- Les modifications de contenu doivent d'abord être faites dans la version anglaise, puis traduites dans chacune des autres langues.
- Les améliorations d'une traduction se font directement dans le fichier de la langue concernée. Une demande de fusion ne doit modifier qu'une seule langue à la fois.
- Soumettez une demande de fusion contenant les modifications du fichier de cette langue. Chaque langue a un responsable qui relit les changements, puis le responsable principal, @jlevy, les fusionne.
- Préfixez les demandes de fusion et les tickets par le code de la langue s'ils ne concernent que cette traduction, par exemple « fr: Amélioration de la grammaire », pour que les responsables les retrouvent facilement.

### Ajouter une traduction dans une nouvelle langue

Les traductions dans de nouvelles langues sont toujours les bienvenues ! Gardez à l'esprit qu'une traduction doit être maintenue : chaque traduction a besoin d'une personne responsable.

- Consultez les tickets existants pour vérifier si une traduction est en cours ou à l'arrêt. Si c'est le cas, proposez votre aide.
- Avez-vous le temps d'être responsable de la nouvelle langue ? Dites-le, pour que l'on sache pouvoir compter sur vous à l'avenir.
- Si aucune traduction n'est en cours, ouvrez un ticket pour votre langue afin que tout le monde sache que vous y travaillez et que l'on puisse s'organiser. Confirmez que vous maîtrisez cette langue comme un locuteur natif et que vous acceptez de maintenir la traduction, pour qu'elle ne soit pas abandonnée.
- Pour commencer, faites un *fork* du dépôt, puis soumettez une demande de fusion contenant uniquement le fichier README-xx.md, où xx est le code de la langue. Utilisez les [étiquettes de langue IETF](https://www.w3.org/International/articles/language-tags/) standard, c'est-à-dire les mêmes que Wikipédia, et *non* le code d'un pays. Ce sont généralement des codes de deux lettres en minuscules, par exemple `fr` pour le français et `uk` pour l'ukrainien (et non `ua`, qui désigne le pays). Pour les langues qui ont des variantes, utilisez l'étiquette la plus courte, comme `zh-Hant`.
- *Invitez des amis à relire* si possible. Les traductions sont difficiles et contiennent souvent des erreurs que d'autres doivent repérer. Si vous le souhaitez, invitez-les à améliorer votre traduction en faisant un *fork* de votre dépôt, puis fusionnez leurs demandes.
- Ajoutez des liens vers votre traduction en haut de chaque fichier README*.md (par cohérence, ajoutez le lien dans l'ordre alphabétique des codes ISO, avec un texte de lien écrit dans la langue concernée).
- Une fois terminé, indiquez dans la demande de fusion qu'elle est prête à être intégrée au dépôt principal.

### Autres questions

Vous avez un doute sur la procédure ?
Ou vous avez les compétences et l'envie d'aider de façon plus importante ?
Ouvrez un ticket ou écrivez à l'auteur original [@jlevy](https://github.com/jlevy).
