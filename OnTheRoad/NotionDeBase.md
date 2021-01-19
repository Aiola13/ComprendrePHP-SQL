# Notions de bases

Pour pouvoir aller chercher nos informations dans botre base de donnée avec notre code, nous allons devoir passer par PHP.

Mais comment faire ? 

Il existe plusieurs groupes de fonctions (des extensions) qui vont permettre de se connecter à notre BDD.

| fonction  |                                        description                                         |
| :-------: | :----------------------------------------------------------------------------------------: |
| `mysql_`  |  Ancien groupe de fonction disponible jusqu'à PHP 7  mais compatible seulement avec MySql  |
| `mysqli_` | Groupe de fonction aillant pris la suite de  `mysql_` mais compatible seulement avec MySQL |
|   `PDO`   |              Groupe de fonction compatible avec une multitude de moteur SGBD               |


|                                                | MySQLi |    PDO     | PHP's MySQL Extension |
| :--------------------------------------------: | :----: | :--------: | :-------------------: |
|                 Version de PHP                 | > 5.0  |   > 5.0    |         < 5.0         |
|              Inclut avec PHP 5.x               |  Oui   |    Oui     |          Oui          |
|                     Statut                     | Actif  |   Actif    | Maintenance seulement |
|         API avec codage des caractères         |  Oui   |    Oui     |          Non          |
|       API avec instruction côté serveur        |  Oui   |    Oui     |          Non          |
|        API avec instruction côté client        |  Non   |    Oui     |          Non          |
|           API avec procédure stockée           |  Oui   |    Oui     |          Non          |
|        API avec instructions multiples         |  Oui   | La plupart |          Non          |
| Supporte toutes les fonctionnalités MySQL 4.1+ |  Oui   | La plupart |          Non          |



---

# Prêt pour la prochaine partie ? 😉 [C'est par ici](./mysqli_.md)
