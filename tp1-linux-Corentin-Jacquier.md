# TP1 - Linux Ubuntu

Installation d’Ubuntu Server et prise en main du shell - CPE Lyon - 4ETI, 3IRC & 3ICS - Année 2022/2023 Administration Système

Corentin JACQUIER ICS

## Exercice 2

### Manuel 

On utilise l'interpréteur Bash (programme REPL : Read - Eval - Print) sur Ubuntu pour intéragir avec la machine.

La commande `man which`  permet d'afficher la documentation associée à la commande `which` grace à la commande `man` qui permet d'afficher le manuel de différentes commandes de Linux.

Afin de trouver des termes particuliers dans l'affichage du manuel de la commande `which`, il faut exécuter la commande suivante dans le manuel `/options` qui permet de surligner les mots désirés (ici 'options'). 

Pour quitter un manuel, on presse `q`. 

On sait que le manuel ouvre la première commande qu'il trouve, donc avec l'argument `-K` pour spécifier la section. 

Après avoir entré la commande `man -K 6`, est affiché le manuel du gestionnaire de package d'Ubuntu ('dpkg').  

### Navigation

On va dans le dossier `var/log` avec la commande `cd /var/log`. 

On remonte dans le dossier var avec le chemin relatif suivant `cd ..`.

Pour revenir dans le dossier personnel, on exécute la commande suivante `cd $home`.

Et pour revenir dans le dossier précédent (/var), on fait `cd -`, argument  de la commande `cd` qui permet de revenir en arrière. 

Pour essayer d'accéder au dossier racine : `cd /root`, mais le compte utilisé n'est admin.  

Mais avec `sudo cd /root`, il est impossible d'accéder au dossier `/root`. En effet, `sudo` s'applique uniquement aux programmes.

Voici, les commandes afin de créer l’arborescence suivante : 
```
~
└───dossier1
│   │   fichier1.txt
│
└───dossier2.1
│ 
└───dossier2.2
│       │   fichier2.txt
│       │   fichier3.txt
│   
```

D'abord, on créer le 'dossier1' avec `mkdir dossier1`. Puis, on ajoute dans le fichier 'fichier1.txt' en entrant la commande `touch fichier1`. Ensuite, on fait des commandes similaires pour créer la suite de l’arborescence. 

Pour supprimer le 'fichier1' dans 'dossier1' avec la commande `rm dossier/fichier1`. Or, avec la commande `rm`, on ne peut pas supprimer de dossier.

Grace à la commande `man rm`, on découvre qu'il y a des arguments `-f` pour forcer  l'opération, `rm dir` pour supprimer un dossier vide et `rm -r` pour ajouter la récursivité dans l'opération. 

Il faut utiliser la commande `rmdir dossier1` pour supprimer le 'dossier1'.

Et pour supprimer tout le contenu du 'dossier2' et son contenu récursivement, on exécute `rm -rf dossier2`.

### Commandes importantes 

Pour afficher la date et  l'heure, on utilise `date`. Avec le manuel, on apprend que l'on peut faire la commande suivante pour afficher l'heure et la date du jour :  `date "+%H:%M:%S   %d/%m/%y"`. 

Avec la commande `ls`, on affiche tous les fichiers visibles du dossier actuel tandis que `la` affiche également les fichiers cachés (qui commencent par un point, ex : .bashrc). 

Avec la commande `which`, on peut alors situer le programme `ls`. Donc avec `which ls`, on apprend que `ls` est situé dans '/usr/bin/ls'.

`ll` ou `ls - alF` (d'après `alias  ll`) permet de découvrir le détail des différents fichiers et dossiers avec date de créations, permissions et autres. 

Pour afficher les fichiers et dossiers du dossier '/bin', on fait `ls /usr/bin`.

La commande  `ls ..` , permet d'afficher le contenu du dossier précédent (chemin relatif). 

La commande `pwd` affiche le chemin complet du dossier courant. 

La commande `echo 'bip' > plop`, crée un fichier plop qui contient le text "echo 'bip''". Si on exécute deux fois la commande le fichier sera simple écrit par dessus une nouvelle fois. 

Pour ajouter du texte dans le fichier 'plop', il faut utiliser les doubles chevrons comme ceci : `echo 'bip' >> plop`.

La commande `sleep 10 | echo 'toto'` permet d'afficher dans le terminal `toto` et met en pause le terminal pendant 10 secondes (`CTRL+C` pour stoper la pause). 

D'après le manuel, grace à la commande `file`, on apprend quel est le type du fichier (par exemple pour le fichier "plop" avec `file plop`, qui retourne `plop: ASCII text` ou avec le fichier "swap.img" qui retourne `swap.img: Linux swap file...`).

 Après avoir créer le fichier original avec `touch original` et fait le 'lien_phy' avec `ln original lien_phy`. Si on modifie le fichier 'original' ou 'lien_phy', les fichiers seront tous deux modifiés. 
Mais si on supprime le fichier 'original', le fichier 'lien_phy' sera toujours présent. 

Maintenant avec un lien symbolique entre 'lien_phy' et 'lien_sym', créer à partir de la commande `ln -s lien_phy lien_sym`. Si on modifie le fichier 'lien_phy' ou 'lien_sym', les fichiers seront tous deux modifiés. 
Si on supprime le fichier 'lien_phy', alors le fichier 'lien_sym' sera supprimé (en rouge). 

Avec la commande `cat /var/log/syslog`, on peut ouvrir le fichier 'syslog' qui contient les logs du système. Pour stoper le défilement, on fait le raccourci clavier suivant `CTRL+Q` et `CTRL+S`. 

Pour voir les 5 première lignes du fichier log, il faut écrire la commande `head -n 5 /var/log/syslog`. 

Pour voir les 10 dernière lignes du fichier log, il faut exécuter la commande `tail -n 10 /var/log/syslog`. 

La commande `dmesg | less`  et divisée en deux `dmesg` permet de visualiser les données du kernel ring buffer et `less` d'afficher les données sur qu'une partie de l'écran.

Le fichier 'passwd' (`cat /etc/passwd`), stocke les informations relatives aux comptes d'utilisateurs. Le fichier enregistre du texte brut, qui fournira des informations utiles pour chaque comptes d'utilisateurs. 

Pour afficher chaques utilisateurs, on utilise la commande `who`. 

Pour chercher tous les fichiers 'passwd', on entre : `find / -iname 'passwd'`. 

On modifie la commande précédente pour que la liste des fichiers trouvés soit enregistrée dans le fichier `~/list_passwd_files.txt` et que les erreurs soient redirigées vers le fichier spécial `/dev/null`. Alors, on a la commande suivante : `find / -iname 'passwd' > ~/list_passwd_files.txt 2>/dev/null`.

On peut chercher l'alias 'lien_sym' avec la commande `grep lien_sym`. 

Après avoir installé plocate avec la commande `sudo apt install plocate`. On peut faire : `locate history.log` pour voir l'emplacement du fichier 'history.log'. 

Locate ne peut pas localiser des dossier dans le dossier personnel. 





