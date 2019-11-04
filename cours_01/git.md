# 1 Introduction

As-tu déjà travaillé en entreprise ou sur un projet étudiant ? Si oui, tu t'es peut-être déjà retrouvé dans mon cas avec un dossier qui ressemble à ça :

    .
    └── big_project
        ├── big_project_01.xls
        ├── big_project_03.xls
        ├── big_project_final_féfé.xls
        ├── big_project_final.xls
        ├── big_project.xls
        └── [WIP] big_project_fin.xls

En gros, c'est souvent le bordel dans le monde des moldus du code. Ces derniers passent leur temps à créer des milliers de fichiers, juste au cas où ils auraient besoin de revenir à une version précédente.

Maintenant, imagine devoir travailler en équipe sur des dossiers de code contenant des milliers de fichiers. Créer des *index_VERSIONNUMBER.html* à tire-larigot n'est clairement pas la meilleure solution. L'idéal serait d'avoir un logiciel capable de faire des photographies à un instant T d'un dossier, et de préciser pour chacune de ces sauvegardes la réponse aux 4 questions suivantes :

-**Quoi** : quels fichiers ont été modifiés dans cette photographie ?

-**Qui** : qui est responsable de cette modification ?

-**Quand** : de quand cette modification date ?

-**Pourquoi** : pourquoi cette modification existe-t-elle ?

Avec un tel logiciel, fini le stress et les dossiers remplis de fichiers inutiles ! Bonne nouvelle : ce genre de logiciels existe et on les appelle des "gestionnaires de version" (version control software). J'aime bien ce schéma de [GitTower](https://www.git-tower.com/learn/git/ebook/en/desktop-gui/basics/what-is-version-control) qui explique bien à quoi ils servent : 

![schema](https://i.imgur.com/ClgRIOW.png)

Comprends-tu maintenant pourquoi le gestionnaire de version appelé Git est un super logiciel, et pourquoi c'est un indispensable dans l'univers du code ? Dans cette ressource, nous verrons comment l'installer et s'en servir. Ensuite, nous verrons de quelle manière l'utiliser pour mettre ses dossiers en ligne avec GitHub (un équivalent de DropBox) pour te permettre de partager ton code et collaborer facilement avec d'autres devs.

# 2 Contexte et historique

Tout comme il existe plusieurs explorateurs Internet (Firefox, Chrome, Safari, etc), il existe plein de logiciels de gestion de versions ([SVN](https://subversion.apache.org/), [BitKeeper](https://www.bitkeeper.org/), etc). Nous allons travailler avec Git pour ce cours car c'est de très très loin le plus connu et utilisé.

Git a été créé en 2005 par Linus Torvald, qui a (entre autres) créé le système d'exploitation Linux.

[GitHub](https://github.com/) est un service de mise en ligne de projets "versionnés" via Git, créé en 2008. Il a été racheté par Microsoft en 2018 pour la modique somme de 7,5 milliards de dollars.

En gros, voici ce que font Git et GitHub :

-**Git** est un logiciel de gestion de versions. C'est à dire, un logiciel permettant de photographier à l'instant T les fichiers d'un dossier.

-**GitHub** est un service en ligne qui utilise Git, et qui permet entre autres de : 

    Mettre en ligne ses dossiers Git (dans ce qu'on appelle "un repository").

    Collaborer à plusieurs sur un même dossier Git.

# 3 Le cours
## 3.1 Git
Nous allons maintenant voir :

-Comment installer Git sur ton ordinateur.

-Comment créer un dossier Git (repository).

-Comment faire une photographie (appelé "commit").

-Comment revenir à des versions précédentes.

### 3.1.1 Instalation
Pour installer Git, rien de plus simple : va sur le site du même nom dans la rubrique [téléchargements](https://git-scm.com/downloads), choisis ton OS, puis télécharge et installe le logiciel. Redémarre ton terminal, et voilà !


## 🚀 ALERTE BONNE 
Git est un logiciel **CLI** (Command Line Interface). Avec ce type de logiciels, tout passe par le terminal. Il s'oppose à **GUI**, Graphical User Interface.

Exemple : lorsque tu utilises la GUI de ton explorateur de fichiers, tu double-cliques sur un fichier pour l'ouvrir. Avec la CLI, tu tapes la commande *$ open nom_du_fichier* dans ton terminal. Autre exemple : pour créer un dossier en GUI, tu cliques droit -> nouveau dossier en GUI. En CLI, tu tapes *$ mkdir nom_dossier* dans ton terminal.

Bref, toutes les actions de ce cours traiteront de la CLI et passeront par le terminal avec les commandes que nous allons t'enseigner. Il existe [des versions GUI](https://git-scm.com/downloads/guis) pour Git, mais elles ne seront pas enseignées dans ce cours pour plusieurs raisons :

-Un peu comme Photoshop, la version GUI peut faire très peur avec ses milliers de boutons.

-Pas besoin d'avoir moult softwares installés : il suffit d'un terminal et à toi la gloire !

-Le but de cette semaine est de te donner les bases pour comprendre l'univers du développement. La version GUI n'étant pas utilisée par les devs, l'enseigner ne répond pas à notre vision : rendre l'univers du développement plus accessible. 

Lance (ou relance) ton terminal, puis rentre la ligne suivante :

        $ git --version

Le terminal devrait te renvoyer quelque chose comme : git version X.XX.X. S'il te renvoie un truc du genre command not found: git, c'est que tu n'as pas installé Git ou relancé ton terminal !

Pour se servir de Git, c'est simple : il suffit de rentrer dans le terminal les commandes $ git truc ou git machin pour lui faire exécuter truc ou machin. Voyons maintenant la commande permettant d'initialiser un dossier git.

### 3.1.2 Mise en place de ton dossier : git init et git status
## ⚠️ ALERTE ERREUR COMMUNE
Quand on débute dans le code, on a tendance à faire git init à la volée un peu partout. Il ne faut pas. Voici les types de dossiers dans lesquels tu dois initialiser des repository :
-Un dossier contenant le code de ton projet Google.

-Un dossier contenant le projet d'un site internet.

-Un dossier contenant un projet clair et défini.

Voici où **tu ne dois pas** faire git init :

-Le dossier qui contient tout ton ordinateur (exemple : exécuter git init en première ligne de commande de ton terminal).

-Ton dossier Desktop ou My Documents.

-Un dossier the_hacking_project contenant tous tes projets de THP.

-Un dossier qui contiendrait plusieurs dossiers de projets différents.

En général la *rule of thumbs* est : un git init par projet. Si jamais tu as fait git init dans un dossier qui n'est pas bon, tu peux supprimer le dossier caché contenant toutes les informations de git en faisant :
        $ rm -rf .git

Et maintenant, quelle est la commande la plus importante quand on manipule git ? Réponse : git status. Cette commande permet de te donner en un rien de temps l'état de ton projet git. Tu peux tester en entrant git status dans un repository git :

    $ git status
    On branch master

    No commits yet

    nothing to commit (create/copy files and use "git add" to track)

Le logiciel git te dit actuellement qu'il n'y a rien dans ton dossier, et donc rien à photographier ("nothing to commit"). Voyons maintenant comment faire un commit, justement.

### 3.1.3 Faire un commit

Un commit est une photographie à un instant T d'un projet. Pour faire court, tu vas prendre certains fichiers et les ajouter à la liste de ceux que tu veux photographier (cette liste peut aussi être vide). Ensuite, tu vas faire ta photographie en faisant git commit.

#### 3.1.3.1 Ajouter un fichier avec git add

Pour savoir quels fichiers git va prendre en photo, il faut les ajouter avec la commande git add :

        $ git add nom_de_ton_fichier

Tu peux voir avec git status que ton fichier est bien ajouté

#### 3.1.3.2 Faire un commit avec git commit

Maintenant que tu as ajouté tes fichiers à la liste, tu as juste à les prendre en photo avec la commande git commit :

        $ git commit -m "I made a change this is a comment why I did it"
        [master (root-commit) cfec956] change
        n files changed, m insertions(+), x deletions(-)
        create mode 100644 blabla

Et voilà comment marche le commit !

## 🤓 QUESTION RÉCURRENTE

**Mais dis-donc Jamy, pourquoi écrire** git commit -m "mon commentaire" **et pas** git commit **tout simplement** ?

Excellente question. La commande git commit va ouvrir un fichier qui te demandera d'écrire un long message de commit avec Vim. Pas très pratique. Ainsi, comme l'option -l qui affiche les résultats de ls au format long, nous allons utiliser l'option -m qui permet d'écrire le message de commit directement dans la commande.

#### 3.1.3.3 Exemple avec un petit projet

Comme il n'est pas aisé d'expliquer les commits, je te propose un petit pas à pas pour t'aider à comprendre la notion de git ☺ Nous allons prendre l'exemple d'un site de restaurant.

Commence par créer un dossier restaurant_website, puis mets-toi dans le dossier avec ton terminal.

On commence **toujours** par initialiser son repository, donc entre la commande suivante :

         $ git init
        Initialized empty Git repository in /home/felix/ton_chemin/restaurant_website/.git/

Normalement, le dossier est vide et contient uniquement le dossier de configuration .git/ que tu n'as pas besoin de toucher (il s'affichera avec $ ls -a). Tu es fin prêt pour commencer ton projet.

D'abord, créons notre fichier index.html et ajoutons quelques lignes de HTML à l'intérieur :

        <!DOCTYPE html>
        <html>
        <head>
        <title>À la bonne table</title>
        </head>
        <body>
        <h1>Ce est le site de mon restaurant !</h1>
        </body>
        </html>

Si tu fais la commande git status, ton terminal te dira ceci :

        $ git status
        On branch master

        No commits yet

        Untracked files:
        (use "git add ..." to include in what will be committed)

        index.html

        nothing added to commit but untracked files present (use "git add" to track)

Cela veut dire qu'il a vu qu'un fichier index.html existe, et que ce dernier est untracked (c'est à dire que le photographe ne le prend pas en compte). Pour pouvoir le "track", il faut faire git add :

         $ git add index.html

Tu verras que ce dernier est prêt avec git status :

        $ git status
        On branch master

        No commits yet

        Changes to be committed:
        (use "git rm --cached ..." to unstage)

        new file:   index.html

Là, git a bien compris que le fichier index.html doit être photographié. Il sera donc bien pris en compte dans le prochain commit. Faisons ce commit, justement :

        git commit -m "first commit // adding index.html"
        [master (root-commit) 279d87c] first commit // adding index.html
        1 file changed, 9 insertions(+)
        create mode 100644 index.html

Et voilà tu viens de faire ton premier commit ! Poursuivons ce "pas à pas" avec deux autres commits qui vont t'apprendre :

-À faire un commit avec deux fichiers.

-La puissance des commits.

Nous allons maintenant ajouter du CSS à notre site. On va mettre les h1 en rouge. Dans un fichier styles.css, ajoute les lignes suivantes :

        h1 {
        color: red;
        }

Puis, dans le fichier index.html, branche le fichier css :

        <link rel="stylesheet" href="styles.css">

Voilà, tu as mis le titre en rouge, tu peux faire un commit ! Petit rappel : il te faut ajouter les fichiers modifiés, puis faire le commit. Voyons les fichiers avec git commit :

        $ git commit
        On branch master
        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

         modified:   index.html

        Untracked files:
        (use "git add <file>..." to include in what will be committed)

        styles.css

        no changes added to commit (use "git add" and/or "git commit -a")

Git est très malin : il te dit que le fichier index.html a été modifié depuis le dernier commit, et qu'il y a un nouveau fichier pas encore tracked. Pour faire un commit, il nous faut ajouter les deux fichiers avec git add puis faire le commit :

        $ git add index.html
        $ git add styles.css

Si tu fais git status, tu peux voir l'état des fichiers : 

        $ git status
        On branch master
        Changes to be committed:
        (use "git reset HEAD ..." to unstage)

        modified:   index.html
        new file:   styles.css

Parfait, git nous dit que ces fichiers seront pris en compte lors du prochain commit. Nous n'avons plus qu'à faire notre commit :

        $ git commit -m "h1 in red"
        [master d25c926] h1 in red
        2 files changed, 5 insertions(+), 1 deletion(-)
        create mode 100644 styles.css

Super ! Tu viens de faire ton deuxième commit. Nous allons maintenant faire le troisième pour te montrer la puissance des commits, et de git status notamment.
Prenons le cas où tu es en train de travailler sur le menu de ton restaurant. Tu hésites entre des ol et des ul. Pour le moment, ton fichier index.html ressemble à ceci :

        <!DOCTYPE html>
        <html>
        <head>
        <title>À la bonne table</title>
        <link rel="stylesheet" href="styles.css">
        </head>
        <body>
        <h1>Ceci est le site de mon restaurant !</h1>
        <h2>Le menu</h2>
        <ul>
        <li>Harengs pommes à l'huile</li>
        <li>Blanquette de veau</li>
        <li>TODO : trouver un dessert</li>
        </ul>
        </body>
        </html>

En pleine hésitation, un collègue arrive et te demande de mettre les h1 en text-align: center; et de faire un commit. Tu t'exécutes et change le fichier style.css. Si tu fais git status tu as :

        $ git status
        On branch master
        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html
        modified:   styles.css

        no changes added to commit (use "git add" and/or "git commit -a")

Git te dit que tu as modifié deux fichiers, mais tu ne veux en commit qu'un seul, car ce vilain "TODO : trouver un dessert" n'a pas vraiment sa place dans le menu. Pour ceci, il faut que tu add uniquement ton fichier styles.css pour faire un commit ne contenant que ce fichier :

        $ git add styles.css

Si tu fais git status tu auras :

        $ git status
        On branch master
        Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        modified:   styles.css

        Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html












