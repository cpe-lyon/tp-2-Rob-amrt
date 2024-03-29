
## Robin Amouret

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

### Exercice 5. Factorielle
Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que
l’utilisateur saisit toujours un entier naturel).

```
#!/bin/bash

nb=$1
CALCUL=1

while [ $nb -ge 1  ]
do
        CALCUL=$((nb*$CALCUL))
        nb=$((nb-1))
done

echo "Le Factoriel de $1 est $CALCUL"
```

### Exercice 6. Le juste prix
Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner.
Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).

```
#!/bin/bash

nb=$[ ( $RANDOM % 1000 ) +1 ]

read -p "Le nombre à été généré ! Devinez le nombre : " input

while [ $input -ne $nb ]
do
        if [ $input -lt $nb ]; then
                read -p "C'est plus ! Retentez : " input
        else
                read -p "C'est moins ! Retentez : " input
        fi
done

echo "Gagné ! Le nombre était bien $input !"
```

### Exercice 7. Statistiques
1. Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max
et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres
sont bien des entiers.
2. Généralisez le programme à un nombre quelconque de paramètres (pensez à SHIFT)
3. Modifiez votre programme pour que les notes ne soient plus données en paramètres, mais saisies et
stockées au fur et à mesure dans un tableau.

```
#!/bin/sh

function reelounon()
{
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $nb =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}

keep=1
nb=0
i=0
marks=()

while [ $keep != 0 ]
do
        echo "entrez une note"
        read nb

        reelounon $nb
        if [ "$?" != "0" ]; then
                echo "merci d'entrer que des réels"
        else
                marks[$i]=$nb
        fi

        echo "continuer ? o / n"
        read answer
        if [ "$answer" = "n" ]; then
                keep=0;
        fi

        ((i++))
done

mini=${marks[0]}
maxi=${marks[0]}
moy=0
longueurtableau=${#marks[@]}
for mark in "${marks[@]}"
do
        if [[ $mark < $mini ]]; then
                mini=$mark
        fi
        if [[ $mark > $maxi ]]; then
                maxi=$mark
        fi
        ((moy=moy+mark))
done
moy=$((moy / longueurtableau))
echo "le max est $maxi, le min est $mini et la moyenne est de $moy"
```
