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

### 8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS
La commande : `echo "Bonjour à vous deux ! $NOMS"`

### 9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?
Une valeur vide à une variable signifie que la variable existe toujours mais qu'elle ne contient rien, elle peut être utilisé comme tout autre variable existante. Cependant la commande unset SUPPRIME entièrement la variable, elle n'existe plus.

### 10.Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)
Commande : `echo "\$HOME = $HOME"`

## Exercice 2 : Contrôle de mot de passe
### Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par l’utilisateur ne doit pas s’afficher.

```
#!/bin/bash
goodPassword="aze"
read -s -p 'Veuillez saisir votre mot de passe : ' passwd

if [ "$passwd" = "$goodPassword" ]; then
        echo "Le mot de passe saisi concorde"
else
        echo "Le mot de pass saisi ne concorde pas"
fi
```

## Exercice 3 : Expressions rationnelles

```
#!/bin/bash

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
        return 1
else
        return 0
fi
}

is_number $1

if [ $? -eq 0 ]; then
        echo "Le nombre est réel"
else
        echo "Le nombre n'est pas réel"
fi
```
## Exercice 4. Contrôle d’utilisateur
### Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”, où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement)

```
#!/bin/bash
if [ -z "$1" ]; then
        echo "Utilisation : $0 nom_utilisateur"
else
        if [ $(id -u $1) ]; then
                echo "L'utilisateur existe"
        else
                echo "L'utilisateur n'existe pas"
        fi
fi
```


