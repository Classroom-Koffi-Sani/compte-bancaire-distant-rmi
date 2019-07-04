# compte-bancaire-distant-rmi
Compte bancaire distant à base de RMI

# Sujet

On souhaite implémenter un compte bancaire distant. Le client pourra créditer ou débiter son compte en préci-
sant le montant et un code opération via la ligne de commande. Par exemple :
```java
java RmiClient + 50 pour ajouter 50 €
``` 
ou
```java
java RmiClient - 30 pour débiter 30 €
```
Le serveur gèrera le compte, caractérisé par son solde. Dans un premier temps, on ne considère que des mani-
pulations avec des entiers. L’objet de type "compte Bancaire" sera donc doté d’un attribut entier "solde" ainsi que
des méthodes suivantes :
- `void crediter( int montant )`
- `void debiter( int montant )`
- `int getSolde()`.

1. Créer les quatre fichiers nécessaires :
    -  `RmiClient.java`
    -  `RmiServeur.java`
    -  `Compte.java`
    -  `IntfCompte.java`
Les compléter et vérifier le fonctionnement.
2. Modifier le client pour que le montant puisse être donné avec les centimes, mais laisser le transfert et
l’attribut solde sous forme entière : la valeur stockée et transmise est simplement exprimée en centimes.
L’affichage devra du coup simplement procéder à une division par 100 pour afficher des €.
3. Modifier le serveur pour que celui-ci affiche toutes les secondes le solde du compte. On réalisera ceci via
une boucle infinie dans laquelle on placera le code suivant :
```
TimeUnit.SECONDS.sleep(1);
System.out.println( "solde=" + cpte.getSolde() );
```
(Note : Il faudra aussi ajouter en tête du fichier l’import de
java.util.concurrent.TimeUnit)
4. Vérifier le fonctionnement en procédant à quelques transactions via le client.
Dans cette boucle infinie, ajouter le code nécessaire pour qu’un taux d’intérêt de 1% par tranche de 10 s.
soit appliqué sur le compte. Il faudra compter les périodes de 1 s. et au bout de 10 ajouter au compte un
montant calculé sur le solde présent 10 s. auparavant. Il faudra donc mémoriser ce montant via une variable
du serveur, et le réactualiser à chaque calcul d’intérêts.
A l’exécution, on devra avoir sur le serveur un affichage du type :
```java
...
solde=17.8 compt=8
solde=17.8 compt=9
interets:0.178 arrondi: 0.18
solde=17.98 compt=0
solde=17.98 compt=1
...
```
L’arrondi est obtenu via la bibliothèque mathématique avec la fonction round(). Par exemple, pour obtenir
les intérêts sous forme entière à partir d’une valeur de type Double, on écrira :
```
int interets_i = (int) Math.round( interets_d );
```
