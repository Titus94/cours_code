# Introduction

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

Avec un tel logiciel, fini le stress et les dossiers remplis de fichiers inutiles ! Bonne nouvelle : ce genre de logiciels existe et on les appelle des "gestionnaires de version" (version control software). J'aime bien ce schéma de GitTower qui explique bien à quoi ils servent : 

![schema](https://www.git-tower.com/learn/git/ebook/en/desktop-gui/basics/what-is-version-control)