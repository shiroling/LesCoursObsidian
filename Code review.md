## Remarques
## Carte c'est le bordel faut refactor


## Filtres
faire une chaine de responsabilité pour ça





## controleur BD
### Equipe :
L 89 :  appel a du sql dans Equipe, ce qui ne respecte pas la model.
A la place il faut appeler BDSelect.getListeEquipe.

### Appels à bd
Source de bug, les appels à la bd ne sont pas obligé de renvoiyer des données, il faut s'assurer de tester le résultat.
```java
if(rs.next()) {
	//traitement 
}
```

### PreJoueur
Dans le constructeur, n'est pas en paramétre id_equipe, il faut l'enlever des attributs étant donné que le joueur à ce moment là n'esst pas dans la BD donc n'as pas d'ID

### ControleurAcceuil 
#### Case
Un case inutile.

#### L304, 444; 474, 592 et L619, 693 
Faire des extract method, beaucoup de code qui se répéte.

### Contrôleur popupTournoi
le case est fucked up, un case inutile (vide), et un case avec une créatoin de fenétre jamais utilisé.

### Controleur connexion
#### case
les case pour MANAGER, GESTIONNAIRE, ARBITRE sont le mémes, ça se refactor

### Contrôleur form créer tournoi
#### Action perfomed 
Réduire le nombre de ligne en créant des méthodes dans la vue
réduire le code qui se répéte.

### Contrôleur form enregistrer équipe
Répétition de code ...


