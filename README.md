# Solveur-DPLL
  Mini-projet 1 : solveur DPLL récursif
                        

**Un mini-projet sans fichier RENDU rempli ne recevra pas de note.**

Date limite: 29 octobre 2021, 23h59

Identité
--------
Nombre de binôme: 11
Nom, prénom 1: NASR Amira
Nom, prénom 2: MIKIA Benidy


Questions sur votre code
------------------------
0. Avez-vous testé que `make dpll` s'exécute sans erreurs ou warnings,
   et que ensuite `./dpll sudoku-4x4.cnf` donne la réponse attendue (voir
   fichier README) ?

 La commande 'make dpll' s'exécute correctement et './dpll sudoku-4x4.cnf' donne bien la 
 réponse attendue


---

1. Avez-vous utilisé la fonction `filter_map` (donné dans dpll.ml)
   dans votre implémentation de `simplifie` ? 
   - Si oui, expliquez en quelques phrases en français comment vous
     l'avez utilisée.
   - Si non, expliquez en quelques phrases en français comment
     fonctionne votre implémentation de `simplifie`.

   Nous avons utilisé la fonction filter_map dans simplifie, elle prend en paramètre une fonction
   auxiliaire 'filter_simplifie' qui est utilisé comme filtre et 'clauses'.
   'filter_simplifie' prend en paramètre un littéral et un tableau 'acc' (vide au départ)
   Chaque sous tableau de clauses (ou clause) va être filtré selon la fonction auxiliaire:
       -on renvoie la clause simplifié si elle contient l'opposé du littéral recherché 
       -on renvoie rien si la clause contient le littéral recherché
   filter_map retourne le tableau de toutes les clauses retournées par filter_simplifie. 
   


---

2. Pour l'implémentation de `unitaire`, quelles sont les fonctions
   auxiliaires que vous avez utilisées et/ou écrites ? (Par une
   fonction auxiliaire, on entend ici soit une fonction d'une
   bibliothèque, par exemple des fonctions comme `List.length`,
   `List.rev_append`, ou une fonction `aux_unitaire` que vous avez
   écrite vous-mêmes.) Expliquez en quelques phrases en français
   comment ces fonctions auxiliaires sont utilisées dans votre
   implémentation de la fonction `unitaire`.

Pour unitaire nous avons écrit une fonction auxiliaire 'unitaireAux' qui est le corps
de la fonction unitaire. Cette fonction vérifie récursivement si la clause courante 
n'est composé que d'un littéral, si c'est le cas on retourne le littéral sinon on rappelle unitaireAux 
sur les autres clauses de la cnf. 
---

3. Pour l'implémentation de `pur`, quelles sont les fonctions
   auxiliaires que vous avez utilisées et/ou écrites ?  Expliquez en
   quelques phrases en français comment ces fonctions auxiliaires sont
   utilisées dans votre implémentation de la fonction `pur`.

Pour pur nous avons utilisé trois fonctions auxilliaires, deux fonctions de la bibliothèque et une que nous avons implémenté.
 'List.flatten' qui permet de passer d'une liste de listes à une liste simple de littéraux.
 La fonction 'purx' qui prend en paramètre la liste de littéraux, extrait la tête de la liste et qui grâce à List.mem vérifie 
si  l'opposé de ce littéral est présent dans la liste. Si c'est le cas on rappelle la fonction sur une liste où toutes 
les occurences de ce littéral et son opposé ont été supprimés. Sinon on renvoie ce littéral. 

---

4. Donnez un exemple d'une formule pour laquelle les deux fonctions
   `solveur_split` et `solveur_dpll_rec` ont un comportement
   différent, et expliquez les différences entre ces deux fonctions.

   Pour l'exemple `exemple_7_2 = [[1;-1;-3];[-2;3];[-2]]` les deux fonctions ont un 
   comportement différent: 
   **print_modele (solveur_dpll_rec exemple_7_2 [])**  donne : 
   SAT 
   -2 -3 0 
   **print_modele (solveur_split exemple_7_2  [])**  donne : 
   SAT 
   1 -2 3 0 
   Cette différence vient du fait que `solveur_dpll_rec`  va tout d'abord chercher un littéral unitaire (qui est le `-2`) l'ajouter à notre liste interprétation (le retour de la fonction) et simplifier notre clauses par ce littéral ce qui nous donne  exemple_7_2=[[1;-1;-3]] et interprétaion =[-2] .
   Ensuite la fonction recherche de nouveau un littéral unitaire -> il n y en a pas, donc passe à chercher un littéral pur => c'est le `-3` alors après simplification on obtient: exemple_7_2=[]  (**ensemble vide**)et interprétaion =[-2;-3] 

   **ALORS QUE :** `solveur_split` va à chaque fois prendre le tout premier littéral de notre exemple de liste de clauses (qui est le `1`)et simplifier.Ce qui nous donne exemple_7_2=[[-2;3];[-2]] et interpretaion =[1]  ensuite le litéral sera `-2` donc on aura  exemple_7_2=[] (**ensemble vide**) et  interprétation = [1;-2]. Mais on obtient  un résultat inattendu et inexplicable  : solveur_split rajoute le `3` dans interprétation qui devient égale à [1;-2;3] ce qui montre bien le dysfonctionnement de cet algorithme à la fin .

   La différence se résume donc dans le choix du littéral par lequel on voudra simplifier notre clause et notre fonction solveur_dpll_rec rend le choix et le temps d'exécution optimaux  .
---


---

--fin du fichier RENDU--

    © 2022 GitHub, Inc.

    Terms
    Privacy
    Security
    Status
    Docs
    Contact GitHub
    Pricing
    API
    Training
    Blog
    About


