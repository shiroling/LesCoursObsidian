#php #révisions 

## Les fonctionnalités du langage PHP  
### Syntaxe :
Paradigme de C a l'intérieur de 
``<?php ... ?>``
### Fonctions utiles
- echo : affichage sur la sortie standard  
- print_r : affichage sur la sortie standard, y  
compris des types complexes  
- var_dump : retourne les informations  
structurées d’une variable, y compris son type  
et sa valeur  
>Utile pour les types complexes (tableau et  
objets)
### Opérateurs :
- and / &&, Et logique
- or / ||, ou logique
- xor, ou inversé
-  !, négation
- == , égalité
- != , diférence
- === , identicité de type (same)
- < / <=, inf
- > / >= , sup
### Structures de contrôle
#### Test (if elseif else, switch...case ) 
``` php
if ($expr1) {  
	echo "$expr1 est vrai";  
}  
elseif ($expr2) {  
	echo "$expr2 est vrai";  
}   
else {  
echo "tout est faux";  
} 
switch ($foo) {  
	case condition1 :  /*Traitement condition1*/ break;  	
	default :  //Traitement par défaut  
}
```
#### Boucles (while, for, do...while, foreatch ) 
```php
for ($i = 0; $i < 3; $i++) { }

$i = 0;  
while ($i < 10) {}  

$i = 0;  
do {
 //
} while ($i < 10);

foreach ($tab as $val){  }
```
#### Fonctions :
```php
function nomFonction([?]int $params): [string] {  
	//Traitement de la fonction  
return ($resultat);
} 
```
#### Tableaux :
```php
//Tableau à index numéroté  
$tab = array ('valeur0', 12, 'valeur2', ...);  
$val0 = $tab[0];

$tab = array ('index1'=>'valeur1', 'index2'=>123, ...);  
$val1 = $tab['index1'];  

```
#### Tansmitions de variables
```html
<form action="destination.php" method="post">  
	<input type=“text” name=“login”>  
</form>  
```
> on peut utiliser comme méthode post ou get
> à noter que get laisse passer les infos en clair dans l'URL
#### transmition en dur dans un lien
```html

<a href="destination.php?var1=contenu1&var2=contenu2&...">  
mon lien avec des paramètres  
</a>
```
#### Récupération des valeurs 
```php
if (!empty($_POST[‘nom_saisi’]) && !empty($_POST[‘prenom_saisi’])){  
$prenom = $_POST[‘prenom_saisi’];  
echo "Bonjour $nom $prenom !”;
```
# Exploitation du SGBD MySQL  
Instantier PDO :
```php
try {  
$linkpdo = new PDO("mysql:host=$server;dbname=$db", $login, $mdp);  
}  
catch (Exception $e) {  
die('Erreur : ' . $e->getMessage());  
}  
$res = $linkpdo->query('SELECT * FROM carnet_adresse');  
while ($data = $res->fetch()) {  
echo $data[1].'<br/>'.$data['prenom'].'<br/>'.$data['ville'];  
}  
$res->closeCursor();
```
#### Prepared statement 
```php
$req = $linkpdo->prepare('SELECT nom FROM carnet_adresse WHERE nom = ?');  
$req->execute(array($_GET['nom'], $_GET['prenom']));  
$req = $linkpdo->prepare('SELECT nom FROM carnet_adresse WHERE nom = :lenom');  
$req->execute(array('lenom' => $_GET['nom']));
```
#### BindParam
```php
$req = $linkpdo->prepare('SELECT nom FROM carnet_adresse WHERE nom = :lenom');  
$req->bindParam(':lenom', $_GET[‘nom’], PDO::PARAM_STR);  
///Exécution de la requête  
$req->execute();
```
#### Ecriture de données
```php
$req = $linkpdo->prepare('INSERT INTO carnet_adresse(nom, pren) VALUES(:nom, :pren');  
///Exécution de la requête  
$req->execute(array('nom' => $nom,  
'prenom' => $pren));
```
# Accès à des fichiers  
#### Ouvrir
```php
$file = fopen ('mon_fichier.txt', 'a');
?>
```
#### modes d'ouvertures :
- ‘r’ : lecture seule  
- ‘r+’ : lecture/écriture
- ‘w’ : écriture seule - création si le fichier n’existe pas  
‘w+’ : lecture/écriture -  création si le fichier n’existe pas  
‘a’ : écriture seule - pointeur en fin de fichier -  création si le fichier n’existe pas  
‘a+’ : lecture/écriture - pointeur en fin de fichier -  création si le fichier n’existe pas
# Variables persistantes : cookies et sessions
#### Superglobales
- $_SERVER : variables de serveur et d’exécution  
- $_FILES : variables de téléchargement de fichiers
- $_GET : variables passées au script courant via  les paramètres d’une URL  
- $_POST : variables passées au script courant  via le protocole HTTP et la méthode POST  
- $_REQUEST : variables de requête HTTP  (contient par défaut le contenu des variables  
- $_GET, $_POST et $_COOKIE)  
- $_ENV : variables d’environnement (celles du  système Unix par exemple).
#### Cookies
```php
$val = 'ceci est la valeur du cookie';  
if (setcookie('myCookie', $val, time() + 3600) == 0) {  
exit ('Impossible de créer le cookie !');  
}  
//Lecture du cookie myCookie  
echo $_COOKIE['myCookie'];  
//Destruction du cookie myCookie  
if (setcookie('myCookie', '', time() - 100) == 0) {  
exit ('Impossible de détruire le cookie !');
```
#### Session
```php
session_start(); 
$_SESSION['prenom'] = 'jean'; // on mets un e val dans la session
$var = $_SESSION['nom_variable'];  //Lecture d'une variable de session  
unset($_SESSION['nom_variable']);  //Destruction d'une variable de la session  
session_destroy();//Destruction de l'environnement de session  
```
# Bonnes pratiques de sécurité  
#### Faites des prepared statement 
#### Neutraliser les entrées utulisateur
```php
$var = htmlentities("letruc a neutraliser");
$var2 = html_entity_decode($var);```
# PHP et la conception orientée objet  
```php
class vehicule {  
	private $date_fabrication;  
	public function __construct($m, $d) {  
		$this->date_fabrication = $d;  
	}  
	public function __destruct() {  
	}  
	public function __toString() {  
		$ch .= "Date de fabrication : $this->date_fabrication <br/>";  
		return $ch;  
	}
	public function setDateFab($d) {  
		$this->date_fabrication = $d;  
	}  
	public function info() {  
		echo "Marque : $this->marque <br/>";  
		echo "Date de fabrication : $this->date_fabrication <br/>";  
	}  
}
```
#### Instantiation
```php
	$objet = new nom_classe([valeur1, valeur2, ...]);
	$objet->methode();
```
