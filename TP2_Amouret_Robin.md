# tp-2-Rob-amrt
tp-2-Rob-amrt created by GitHub Classroom

# TP2 CPE Lyon - 4ETI & 3IRC - Année 2018/19 Administration Système 

## Exercice 1

### 1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
Pour voir les dossiers dans lesquels Bash cherchent, il faut utiliser la commande : `printenv PATH`
Ce qui retourne : `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin`

### 2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?
La commande : `cd $HOME`

### 3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.
`LANG` est une variable d'environnement contenant la langue utilisé par les logiciels pour communiquer avec l'utilisateur.
`PWD` est une variable d'environnement permettant d'afficher le chemin absolu dans lequel nous nous trouvons.
`OLDPWD` est une variable d'environnement contenant l'ancien chemin absolu dans lequel nous nous trouvions.
`SHELL` est une variable contenant le chemin du BASH.
`_` est une variable contenant la dernière commande executé

### 4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe
Pour vérifier que la variable existe, il faut faire : `echo $MY_VAR` et voir si le résultat est celui escompté ou alors utiliser la commande `set` puis voir si la variable créer est presente parmis celles listées.

### 5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale
La commande BASH ouvre une nouvelle session que ne prend pas en compte les variables locales instanciées dans la précédente session, ainsi la variable `MY_VAR` n'existe point.

### 6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.
Avec la commande `export MY_VAR="jsuismongole` cela transforme la variable locale en variable d'environnement. Les commande d'environnement sont retenu peut importe la session dans laquelle nous nous trouvons.

### 7. Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace. Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.

Nous créons la variable environnemental `NOMS` : `declare -x NOMS="Robin Eloi`
Puis nous affichons la valeur de NOMS : `printenv NOMS` ce qui retourne `Robin Eloi`


