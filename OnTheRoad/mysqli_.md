# mysql_i

Comme indiqué précédemment, mysqli est une extension qui permet d'interfacer du langage PHP avec du langage SQL.

Comment celui-ci fonctionne ? 

## Connexion

```php
<?php
$connexion=mysqli_connect("sql.monserveur.org", "utilisateur", "motdepasse", "basededonnee");

  //... votre script PHP contenant les commandes mysqli_xxx();
mysqli_query($connexion, "CREATE DATABASE 'MaDB'");

mysqli_close($connexion);
?>
```

## Requête

```php
  mysqli_query("CREATE TABLE Gens (nb INT AUTO_INCREMENT, nom VARCHAR(25) NOT NULL) ENGINE=INNODB");
```

## Stocker et afficher le résultat de la requête

```php
  $resultats = mysqli_query($connexion, "SELECT nom, prenom FROM Gens");
  while($rangee=mysqli_fetch_array($resultats))
  {
    $var1=$rangee['champ1'];
    $var2=$rangee['champ2'];
    $var3=$rangee['champ3'];
    echo "$var1 - $var2 - $var3<br>";
  }
```


```php

$resultat=mysqli_query("SELECT categorie, SUM(montant), COUNT(DISTINCT prestataire)
FROM factures_payees GROUP BY categorie");

  // La sortie des résultats se fait de cette manière 
  // (ce sont les paramètres 'SUM(montant)' et 'COUNT(DISTINCT prestataire)' qui servent d'indices au tableau $rangee) :

while($rangee=mysqli_fetch_array($resultat))
 {
 $sommation=$rangee['SUM(montant)'];
 $nbr_prest=$rangee['COUNT(DISTINCT prestataire)'];
 $categorie=$rangee['categorie'];
 echo "Cat. $categorie: $sommation pour $nbr_prest<br>";
 }
 ```