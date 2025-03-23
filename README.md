# Algorithme_2

// ********************************\*********************************
// **********\*\*\*********** PROBLEM 1 **************\*\*\***************
// ********************************\*********************************

ALGORITHM sum_of_distinct_elements

    // Déclaration des variables

VAR
set1, set2 : ARRAY OF INTEGER
sum, i, j : INTEGER
BEGIN
// Initialisation des ensembles avec les valeurs données
set1 := [3, 1, 7, 9]
set2 := [2, 4, 1, 9, 3]
sum := 0 // Initialisation de la somme à zéro

    //  Vérifier les éléments uniques de set1 qui ne sont pas dans set2
    FOR i FROM 0 TO LENGTH(set1) - 1 DO
        // Vérifier si set1[i] est présent dans set2
        IF NOT (set1[i] IN set2) THEN
            sum := sum + set1[i] // Ajouter à la somme s'il est unique
        END_IF
    END_FOR

    //  Vérifier les éléments uniques de set2 qui ne sont pas dans set1
    FOR j FROM 0 TO LENGTH(set2) - 1 DO
        // Vérifier si set2[j] est présent dans set1
        IF NOT (set2[j] IN set1) THEN
            sum := sum + set2[j] // Ajouter à la somme s'il est unique
        END_IF
    END_FOR

    //  Afficher la somme totale des éléments distincts
    Write(sum) // Résultat attendu : 13 (car les éléments distincts sont {4, 7, 2})

END

// Solution alternative en fusionant les deux tableaux (si la taille du tableau nous le permet)

ALGORITHM sum_of_distinct_elements
VAR
set1, set2, mergedSet : ARRAY OF INTEGER
freq : DICTIONARY OF INTEGER // Dictionnaire pour stocker la fréquence de chaque élément
i, sum : INTEGER
BEGIN
// Initialisation des ensembles
set1 := [3, 1, 7, 9]
set2 := [2, 4, 1, 9, 3]

    // Fusionner les deux ensembles en un seul tableau
    mergedSet := set1 + set2 // Concaténer les deux tableaux
    sum := 0 // Initialisation de la somme à zéro
    freq := {} // Initialisation du dictionnaire de fréquence

    //  Calculer la fréquence de chaque élément dans mergedSet
    FOR i FROM 0 TO LENGTH(mergedSet) - 1 DO
        IF mergedSet[i] IN freq THEN
            freq[mergedSet[i]] := freq[mergedSet[i]] + 1 // Incrémenter la fréquence
        ELSE
            freq[mergedSet[i]] := 1 // Initialiser à 1 si l'élément n'existe pas encore
        END_IF
    END_FOR

    //  Ajouter à la somme uniquement les éléments qui apparaissent une seule fois
    FOR i FROM 0 TO LENGTH(mergedSet) - 1 DO
        IF freq[mergedSet[i]] = 1 THEN
            sum := sum + mergedSet[i]
        END_IF
    END_FOR

    //  Affichage du résultat
    Write(sum) // Résultat attendu : 13

END

//**********************************\***********************************
//**********\*\*\*\*********** PROBLEM 2 ****************\*\*****************
//**********************************\***********************************

// ************\*\*\*\************* Procédure ************\*\*\*\*************

ALGORITHM DotProductProc
VAR
v1, v2: ARRAY[50] OF INTEGER // Vecteurs
n, ps: INTEGER // Taille des vecteurs et produit scalaire
i: INTEGER

    //  PROCÉDURE qui calcule le produit scalaire et met à jour `ps`

PROCEDURE dot_product_proc(v1, v2, n, VAR ps)
ps := 0
FOR i FROM 0 TO n-1 DO
ps := ps + (v1[i] \* v2[i])
END_FOR
END_PROCEDURE

BEGIN
// Lecture de la taille du vecteur
Write("Entrez la taille des vecteurs : ")
Read(n)

    //  Lecture des éléments du premier vecteur
    Write("Entrez les éléments du premier vecteur : ")
    FOR i FROM 0 TO n-1 DO
        Read(v1[i])
    END_FOR

    //  Lecture des éléments du second vecteur
    Write("Entrez les éléments du second vecteur : ")
    FOR i FROM 0 TO n-1 DO
        Read(v2[i])
    END_FOR

    // 🔥 Utilisation de la procédure
    dot_product_proc(v1, v2, n, ps)

    //  Affichage du produit scalaire
    Write("Produit scalaire (procédure) :", ps)

    //  Vérification de l'orthogonalité
    IF ps = 0 THEN
        Write("Les vecteurs sont orthogonaux")
    ELSE
        Write("Les vecteurs ne sont pas orthogonaux")
    END_IF

END

// ************\*\*\*\************* Fonction ************\*\*\*\*************

ALGORITHM DotProductFunc
VAR
v1, v2: ARRAY[50] OF INTEGER // Vecteurs
n, result: INTEGER // Taille des vecteurs et produit scalaire
i: INTEGER

    // FONCTION qui retourne directement le produit scalaire

FUNCTION dot_product_func(v1, v2, n): INTEGER
DECLARE ps: INTEGER := 0
FOR i FROM 0 TO n-1 DO
ps := ps + (v1[i] \* v2[i])
END_FOR
RETURN ps
END_FUNCTION

BEGIN
// Lecture de la taille du vecteur
Write("Entrez la taille des vecteurs : ")
Read(n)

    // Lecture des éléments du premier vecteur
    Write("Entrez les éléments du premier vecteur : ")
    FOR i FROM 0 TO n-1 DO
        Read(v1[i])
    END_FOR

    // Lecture des éléments du second vecteur
    Write("Entrez les éléments du second vecteur : ")
    FOR i FROM 0 TO n-1 DO
        Read(v2[i])
    END_FOR

    //  Utilisation de la fonction
    result := dot_product_func(v1, v2, n)

    //  Affichage du produit scalaire
    Write("Produit scalaire (fonction) :", result)

    //  Vérification de l'orthogonalité
    IF result = 0 THEN
        Write("Les vecteurs sont orthogonaux")
    ELSE
        Write("Les vecteurs ne sont pas orthogonaux")
    END_IF

END
