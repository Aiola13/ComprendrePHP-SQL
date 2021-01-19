# PDO

PDO (PHP Data Objects) est également une extension qui permet d'interfacer le langage PHP avec du langage SQL.
Mais son gros avantage est le faite qu'il fasse abstraction du moteur SGBD utilisé.

- Ses avantages sont :
  - Abstraction du moteur SGBD (en théorie)
  - Orienté Objet
  - Utilisation d'exception (Système de gestion d'erreur)



## Connexion (sans gestion d'erreur)

PDO étant une classe, nous allons instancié cette classe (créer un objet)

```php
$database = new PDO('mysql:host=localhost;dbname=store;charset=ut8', 'username', 'password'); (mais si mauvais password alors tout est affiché)
```

```php
<?php

define('DB_HOST', 'localhost'); //define('DB_HOST', 'mysql:host=localhost;dbname=store;charset=ut8'); 
define('DB_PORT', '3306');
define('DB_DATABASE', 'bd_client');
define('DB_USERNAME', 'u_db_client');
define('DB_PASSWORD', '123456');

database = new PDO('mysql:host='.DB_HOST.';port'.DB_PORT.';dbname='.DB_DATABASE, DB_USERNAME, DB_PASSWORD);

?>
```

## Connexion (avec gestion d'erreur)

```php
try
{
  database = new PDO('mysql:host='.DB_HOST.';port'.DB_PORT.';dbname='.DB_DATABASE, DB_USERNAME, DB_PASSWORD);
  // $database = new PDO('mysql:host='.DB_HOST.';port'.DB_PORT.';dbname='.DB_DATABASE, DB_USERNAME, DB_PASSWORD, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
  database->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION); // rapport d'erreur : emet des exceptions
  database->exect("SET NAMES 'utf8'"); // Codage utilisé
}
catch(Exception $e) //interception de l'erreur
{
  echo 'Erreur : '.$e->getMessage().'<br />';
  echo 'Numéro : '.$e->getCode();
  exit();
}
```

## Requête

- On distingue deux méthodes de la classe PDO permettant d’exécuter deux types de requête :
  - La méthode query() pour l’interrogation de données, dés que vous utilisez le SELECT
  - La méthode exec() pour la manipulation de données, dés que vous utilisez le UPDATE, INSERT ou DELETE

- Pour faire simple :
une requête qui retourne un résultat doit être exécutée avec la méthode query() dans les autres cas on utilise la méthode exec();

### Exec

```php
include 'config.BD.inc.php'; // Connexion à la BD

try
{
  $iNbLigne = $database->exec('insert into customers(first_name, last_name) Values (loic,durand)');
}
catch(Exception $e)
{
  die('Erreur : '.$e->getMessage().'<br />');
}

echo $iNbLigne.' ligne(s) modifiée(s)';
```

### Query

```php
include 'config.BD.inc.php'; // Connexion à la BD

try
{
  $results = $database->query('SELECT first_name, last_name FROM customers');

}
catch(Exception $e)
{
  die('Erreur : '.$e->getMessage().'<br />');
}


    
while($row = $results->fetch())
{
  echo $row['first_name'].'<br />';
}


$array = $results->fetchAll();
foreach($array as $row)
  foreach($row as $value)
    echo $value.'<br />';

```




## Prepare

La méthode prepare() offre la possibilité de préparer la requête

Il existe deux types de marqueurs :
- Le marqueur Interrogatif
- Le marqueur Nominatif

### Marqueurs Interrogatif

```php
$sql = $database->prepare('insert into customers(firstName, lastName) Values (?,?)');

$firstName = 'Hector';
$lastName = 'Sinapi';

$sql->execute(array($firstName, $lastName));
```


### Marqueurs Nominatifs (Nommés)

```php
$sth appartient à la classe PDOStatement
                $sth = $dbco->prepare("
                    INSERT INTO Clients(Nom,Prenom,Adresse,Ville,Codepostal,Pays,Mail)
                    VALUES (:nom, :prenom, :adresse, :ville, :cp, :pays, :mail)
                ");
                $sth->execute(array(
                                    ':nom' => $nom,
                                    ':prenom' => $prenom,
                                    ':adresse' => $adresse,
                                    ':ville' => $ville,
                                    ':cp' => $cp,
                                    ':pays' => $pays,
                                    ':mail' => $mail));
                echo "Entrée ajoutée dans la table";
```






Associatif : 

fetch(PDO::FETCH_ASSOC);
fetch(PDO::FETCH_NUM);
fetch(PDO::FETCH_OBJ);


Différence entre requête et requête préparé 


Schéma d'une requête normale :
1 : envoi de la requête par le client vers le SGBD
2 : compilation de la requête 
3 : plan d'exécution par le SGBD
4 : exécution de la requête
5 : résultat du SGBD vers le client

Schéma d'une requête préparée :
Phase 1 :
1 : envoi de la requête à préparer
2 : compilation de la requête
3 : plan d'exécution par le SGBD
4 : stockage de la requête compilée en mémoire
5 : retour d'un id de requête au client
Phase 2 :
1 : le client demande l'exécution de la requête avec l'id
2 : exécution
3 : résultat du SGBD au client





Avec la méthode prepare()
 Avantage
   Optimisation des performances pour des requêtes appelées
  plusieurs fois ;
  Exécuter une requête "préparée"
   limiter la bande passante utilisée entre le client et le serveur :
  dû au fait que l'échange d'informations est limité au strict
  minimum, la requête est stockée en mémoire du SGBD.
   Protection des injections SQL;
     L'attaque par SQL injection, consiste à injecter une requête
    SQL dans un paramètre. Si ce paramètre n’est pas contrôlé
    par l'application alors des actions non prévues peuvent être
    pilotées à distance par un pirate.