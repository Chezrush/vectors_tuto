# Tutoriel de la bibliothèque Vectors

Ce tutoriel vous guidera à travers plusieurs exercices pour vous familiariser avec la bibliothèque de vecteurs. Chaque exercice comporte un code de départ, les résultats attendus et une solution.

## Table des matières

- [Exercice 1: Création et affichage d'un vecteur](#exercice-1-création-et-affichage-dun-vecteur)
- [Exercice 2: Manipulation des éléments d'un vecteur](#exercice-2-manipulation-des-éléments-dun-vecteur)
- [Exercice 3: Recherche dans un vecteur](#exercice-3-recherche-dans-un-vecteur)
- [Exercice 4: Insertion et suppression](#exercice-4-insertion-et-suppression)
- [Exercice 5: Traitement avancé avec les vecteurs](#exercice-5-traitement-avancé-avec-les-vecteurs)
- [Exercice 6: Utilisation de `split_word_array`](#exercice-6-utilisation-de-split_word_array)
- [Exercice 7: Vecteur automatiquement libéré](#exercice-7-vecteur-automatiquement-libéré)

## Exercice 1: Création et affichage d'un vecteur

Dans cet exercice, vous allez créer un vecteur d'entiers et afficher son contenu.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>

int main(void)
{
    // TODO: Créer un vecteur d'entiers avec une capacité initiale de 5

    // TODO: Ajouter les valeurs 10, 20, 30, 40, 50 au vecteur

    // TODO: Afficher la longueur du vecteur

    // TODO: Afficher chaque élément du vecteur

    // TODO: Libérer la mémoire

    return 0;
}
```

### Résultat attendu

```
Longueur du vecteur: 5
- [0] = 10
- [1] = 20
- [2] = 30
- [3] = 40
- [4] = 50
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>

int main(void)
{
    // Créer un vecteur d'entiers avec une capacité initiale de 5
    vector_t *my_vector = vector_create(5, sizeof(int));
    
    // Ajouter les valeurs 10, 20, 30, 40, 50 au vecteur
    int values[] = {10, 20, 30, 40, 50};
    for (int i = 0; i < 5; i++) {
        vector_pushback(&my_vector, &values[i]);
    }
    
    // Afficher la longueur du vecteur
    printf("Longueur du vecteur: %zu\n", vector_getlength(my_vector));
    
    // Afficher chaque élément du vecteur
    for (size_t i = 0; i < vector_getlength(my_vector); i++) {
        printf("- [%zu] = %d\n", i, *(int *)vector_get_at(my_vector, i));
    }
    
    // Libérer la mémoire
    vector_destroy(my_vector);
    
    return 0;
}
```
</details>

## Exercice 2: Manipulation des éléments d'un vecteur

Dans cet exercice, vous allez manipuler les éléments d'un vecteur de chaînes de caractères.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>
#include <string.h>

int main(void)
{
    // TODO: Créer un vecteur de chaînes de caractères avec une capacité initiale de 3

    // TODO: Ajouter les chaînes "Bonjour", "Monde", "!" au vecteur

    // TODO: Afficher les chaînes

    // TODO: Supprimer la dernière chaîne (pop_back)

    // TODO: Ajouter une nouvelle chaîne "Vector" au vecteur

    // TODO: Afficher le vecteur mis à jour

    // TODO: Libérer la mémoire

    return 0;
}
```

### Résultat attendu

```
Vecteur initial:
- [0] = Bonjour
- [1] = Monde
- [2] = !

Vecteur mis à jour:
- [0] = Bonjour
- [1] = Monde
- [2] = Vector
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>
#include <string.h>

int main(void)
{
    // Créer un vecteur de chaînes de caractères avec une capacité initiale de 3
    vector_t *my_vector = vector_create(3, sizeof(char *));
    
    // Ajouter les chaînes "Bonjour", "Monde", "!" au vecteur
    char *str1 = strdup("Bonjour");
    char *str2 = strdup("Monde");
    char *str3 = strdup("!");
    
    vector_pushback(&my_vector, &str1);
    vector_pushback(&my_vector, &str2);
    vector_pushback(&my_vector, &str3);
    
    // Afficher les chaînes
    printf("Vecteur initial:\n");
    for (size_t i = 0; i < vector_getlength(my_vector); i++) {
        char *str = *(char **)vector_get_at(my_vector, i);
        printf("- [%zu] = %s\n", i, str);
    }
    
    // Supprimer la dernière chaîne (pop_back)
    // Note: Il faudrait libérer la mémoire pour str3 dans un cas réel
    vector_popback(my_vector);
    
    // Ajouter une nouvelle chaîne "Vector" au vecteur
    char *str4 = strdup("Vector");
    vector_pushback(&my_vector, &str4);
    
    // Afficher le vecteur mis à jour
    printf("\nVecteur mis à jour:\n");
    for (size_t i = 0; i < vector_getlength(my_vector); i++) {
        char *str = *(char **)vector_get_at(my_vector, i);
        printf("- [%zu] = %s\n", i, str);
    }
    
    // Libérer la mémoire (dans un cas réel, il faudrait libérer chaque chaîne aussi)
    for (size_t i = 0; i < vector_getlength(my_vector); i++) {
        char *str = *(char **)vector_get_at(my_vector, i);
        free(str);
    }
    vector_destroy(my_vector);
    
    return 0;
}
```
</details>

## Exercice 3: Recherche dans un vecteur

Dans cet exercice, vous allez utiliser la fonction `vector_find` pour rechercher un élément dans un vecteur.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>

// TODO: Créer une fonction de comparaison pour les entiers
// int compare_int(const void *a, const void *b);

int main(void)
{
    // TODO: Créer un vecteur d'entiers avec une capacité initiale de 10

    // TODO: Ajouter les valeurs 5, 12, 8, 23, 9, 14 au vecteur

    // TODO: Rechercher la valeur 8 dans le vecteur et afficher son index
    
    // TODO: Rechercher la valeur 50 (qui n'existe pas) et afficher un message approprié

    // TODO: Libérer la mémoire

    return 0;
}
```

### Résultat attendu

```
La valeur 8 a été trouvée à l'index 2
La valeur 50 n'existe pas dans le vecteur
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>

// Fonction de comparaison pour les entiers
int compare_int(const void *a, const void *b)
{
    const int *pa = (const int *)a;
    const int *pb = (const int *)b;
    
    return *pa - *pb;
}

int main(void)
{
    // Créer un vecteur d'entiers avec une capacité initiale de 10
    vector_t *my_vector = vector_create(10, sizeof(int));
    
    // Ajouter les valeurs 5, 12, 8, 23, 9, 14 au vecteur
    int values[] = {5, 12, 8, 23, 9, 14};
    for (int i = 0; i < 6; i++) {
        vector_pushback(&my_vector, &values[i]);
    }
    
    // Rechercher la valeur 8 dans le vecteur et afficher son index
    int search_value = 8;
    size_t index = vector_find(my_vector, &search_value, compare_int);
    
    if (index != (size_t)-1) {
        printf("La valeur %d a été trouvée à l'index %zu\n", search_value, index);
    } else {
        printf("La valeur %d n'existe pas dans le vecteur\n", search_value);
    }
    
    // Rechercher la valeur 50 (qui n'existe pas) et afficher un message approprié
    search_value = 50;
    index = vector_find(my_vector, &search_value, compare_int);
    
    if (index != (size_t)-1) {
        printf("La valeur %d a été trouvée à l'index %zu\n", search_value, index);
    } else {
        printf("La valeur %d n'existe pas dans le vecteur\n", search_value);
    }
    
    // Libérer la mémoire
    vector_destroy(my_vector);
    
    return 0;
}
```
</details>

## Exercice 4: Insertion et suppression

Dans cet exercice, vous allez utiliser les fonctions `vector_insert_at` et `vector_pop_at` pour insérer et supprimer des éléments à des positions spécifiques.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>

void print_vector(vector_t *vector);

int main(void)
{
    // TODO: Créer un vecteur d'entiers avec une capacité initiale de 5

    // TODO: Ajouter les valeurs 10, 20, 30, 40 au vecteur

    printf("Vecteur initial:\n");
    print_vector(/* TODO: votre vecteur */);

    // TODO: Insérer la valeur 25 à l'index 2 (entre 20 et 30)

    printf("\nAprès insertion de 25 à l'index 2:\n");
    print_vector(/* TODO: votre vecteur */);

    // TODO: Supprimer l'élément à l'index 1 (valeur 20)

    printf("\nAprès suppression de l'élément à l'index 1:\n");
    print_vector(/* TODO: votre vecteur */);

    // TODO: Libérer la mémoire

    return 0;
}

void print_vector(vector_t *vector)
{
    // TODO: Implémenter la fonction d'affichage
}
```

### Résultat attendu

```
Vecteur initial:
- [0] = 10
- [1] = 20
- [2] = 30
- [3] = 40

Après insertion de 25 à l'index 2:
- [0] = 10
- [1] = 20
- [2] = 25
- [3] = 30
- [4] = 40

Après suppression de l'élément à l'index 1:
- [0] = 10
- [1] = 25
- [2] = 30
- [3] = 40
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>

void print_vector(vector_t *vector);

int main(void)
{
    // Créer un vecteur d'entiers avec une capacité initiale de 5
    vector_t *my_vector = vector_create(5, sizeof(int));
    
    // Ajouter les valeurs 10, 20, 30, 40 au vecteur
    int values[] = {10, 20, 30, 40};
    for (int i = 0; i < 4; i++) {
        vector_pushback(&my_vector, &values[i]);
    }
    
    printf("Vecteur initial:\n");
    print_vector(my_vector);
    
    // Insérer la valeur 25 à l'index 2 (entre 20 et 30)
    int value = 25;
    vector_insert_at(&my_vector, &value, 2);
    
    printf("\nAprès insertion de 25 à l'index 2:\n");
    print_vector(my_vector);
    
    // Supprimer l'élément à l'index 1 (valeur 20)
    vector_pop_at(my_vector, 1);
    
    printf("\nAprès suppression de l'élément à l'index 1:\n");
    print_vector(my_vector);
    
    // Libérer la mémoire
    vector_destroy(my_vector);
    
    return 0;
}

void print_vector(vector_t *vector)
{
    for (size_t i = 0; i < vector_getlength(vector); i++) {
        printf("- [%zu] = %d\n", i, *(int *)vector_get_at(vector, i));
    }
}
```
</details>

## Exercice 5: Traitement avancé avec les vecteurs

Dans cet exercice, vous allez créer une fonction pour filtrer un vecteur en fonction d'un critère.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>

// TODO: Créer une fonction qui filtre les nombres pairs d'un vecteur
// vector_t *filter_even_numbers(vector_t *source);

// TODO: Créer une fonction qui vérifie si un nombre est pair
// int is_even(int num);

void print_vector(vector_t *vector);

int main(void)
{
    // TODO: Créer un vecteur d'entiers avec une capacité initiale de 10

    // TODO: Ajouter les valeurs de 1 à 10 au vecteur

    printf("Vecteur original:\n");
    print_vector(/* TODO: votre vecteur */);

    // TODO: Filtrer les nombres pairs et créer un nouveau vecteur

    printf("\nVecteur filtré (nombres pairs):\n");
    print_vector(/* TODO: votre vecteur filtré */);

    // TODO: Libérer la mémoire des deux vecteurs

    return 0;
}

void print_vector(vector_t *vector)
{
    for (size_t i = 0; i < vector_getlength(vector); i++) {
        printf("- [%zu] = %d\n", i, *(int *)vector_get_at(vector, i));
    }
}
```

### Résultat attendu

```
Vecteur original:
- [0] = 1
- [1] = 2
- [2] = 3
- [3] = 4
- [4] = 5
- [5] = 6
- [6] = 7
- [7] = 8
- [8] = 9
- [9] = 10

Vecteur filtré (nombres pairs):
- [0] = 2
- [1] = 4
- [2] = 6
- [3] = 8
- [4] = 10
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>

// Fonction qui vérifie si un nombre est pair
int is_even(int num)
{
    return num % 2 == 0;
}

// Fonction qui filtre les nombres pairs d'un vecteur
vector_t *filter_even_numbers(vector_t *source)
{
    vector_t *result = vector_create(vector_getlength(source), sizeof(int));
    
    for (size_t i = 0; i < vector_getlength(source); i++) {
        int value = *(int *)vector_get_at(source, i);
        if (is_even(value)) {
            vector_pushback(&result, &value);
        }
    }
    
    return result;
}

void print_vector(vector_t *vector);

int main(void)
{
    // Créer un vecteur d'entiers avec une capacité initiale de 10
    vector_t *my_vector = vector_create(10, sizeof(int));
    
    // Ajouter les valeurs de 1 à 10 au vecteur
    for (int i = 1; i <= 10; i++) {
        vector_pushback(&my_vector, &i);
    }
    
    printf("Vecteur original:\n");
    print_vector(my_vector);
    
    // Filtrer les nombres pairs et créer un nouveau vecteur
    vector_t *filtered_vector = filter_even_numbers(my_vector);
    
    printf("\nVecteur filtré (nombres pairs):\n");
    print_vector(filtered_vector);
    
    // Libérer la mémoire des deux vecteurs
    vector_destroy(my_vector);
    vector_destroy(filtered_vector);
    
    return 0;
}

void print_vector(vector_t *vector)
{
    for (size_t i = 0; i < vector_getlength(vector); i++) {
        printf("- [%zu] = %d\n", i, *(int *)vector_get_at(vector, i));
    }
}
```
</details>

## Exercice 6: Utilisation de `split_word_array`

Dans cet exercice, vous allez utiliser la fonction `split_word_array` pour diviser une chaîne en mots et les stocker dans un vecteur.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>

int main(void)
{
    const char *phrase = "Ceci est un test de la fonction split_word_array";
    
    // TODO: Utiliser split_word_array pour diviser la phrase en mots (séparateur: espace)
    
    // TODO: Afficher tous les mots stockés dans le vecteur
    
    // TODO: Afficher le nombre total de mots
    
    // TODO: Libérer la mémoire

    return 0;
}
```

### Résultat attendu

```
Mots de la phrase:
- [0] = Ceci
- [1] = est
- [2] = un
- [3] = test
- [4] = de
- [5] = la
- [6] = fonction
- [7] = split_word_array

Nombre total de mots: 8
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>

int main(void)
{
    const char *phrase = "Ceci est un test de la fonction split_word_array";
    
    // Utiliser split_word_array pour diviser la phrase en mots (séparateur: espace)
    vector_t *words = split_word_array(phrase, ' ');
    
    // Afficher tous les mots stockés dans le vecteur
    printf("Mots de la phrase:\n");
    for (size_t i = 0; i < vector_getlength(words); i++) {
        char *word = *(char **)vector_get_at(words, i);
        printf("- [%zu] = %s\n", i, word);
    }
    
    // Afficher le nombre total de mots
    printf("\nNombre total de mots: %zu\n", vector_getlength(words));
    
    // Libérer la mémoire
    // Note: Il faut libérer chaque chaîne contenue dans le vecteur
    for (size_t i = 0; i < vector_getlength(words); i++) {
        char *word = *(char **)vector_get_at(words, i);
        free(word);
    }
    vector_destroy(words);
    
    return 0;
}
```
</details>

## Exercice 7: Vecteur automatiquement libéré

Dans cet exercice, vous allez utiliser la fonctionnalité `AUTOFREE` pour automatiquement libérer un vecteur lorsqu'il sort de la portée.

### Code de départ

```c
#include "vectors.h"
#include <stdio.h>

void function_with_autofree(void)
{
    // TODO: Créer un vecteur avec l'attribut AUTOFREE
    
    // TODO: Ajouter quelques éléments au vecteur
    
    // TODO: Afficher les éléments du vecteur
    
    printf("Fin de la fonction - le vecteur va être automatiquement libéré\n");
    // Pas besoin d'appeler vector_destroy!
}

int main(void)
{
    function_with_autofree();
    
    printf("De retour dans main() - le vecteur a été libéré automatiquement\n");
    
    return 0;
}
```

### Résultat attendu

```
Vecteur avec AUTOFREE:
- [0] = 100
- [1] = 200
- [2] = 300
Fin de la fonction - le vecteur va être automatiquement libéré
De retour dans main() - le vecteur a été libéré automatiquement
```

<details>
<summary>Solution</summary>

```c
#include "vectors.h"
#include <stdio.h>

void function_with_autofree(void)
{
    // Créer un vecteur avec l'attribut AUTOFREE
    vector_t *my_vector AUTOFREE = vector_create(5, sizeof(int));
    
    // Ajouter quelques éléments au vecteur
    int values[] = {100, 200, 300};
    for (int i = 0; i < 3; i++) {
        vector_pushback(&my_vector, &values[i]);
    }
    
    // Afficher les éléments du vecteur
    printf("Vecteur avec AUTOFREE:\n");
    for (size_t i = 0; i < vector_getlength(my_vector); i++) {
        printf("- [%zu] = %d\n", i, *(int *)vector_get_at(my_vector, i));
    }
    
    printf("Fin de la fonction - le vecteur va être automatiquement libéré\n");
    // Pas besoin d'appeler vector_destroy!
}

int main(void)
{
    function_with_autofree();
    
    printf("De retour dans main() - le vecteur a été libéré automatiquement\n");
    
    return 0;
}
```
</details>

## Conclusion

Félicitations! Vous avez maintenant une bonne compréhension de la bibliothèque de vecteurs. Ces exercices vous ont permis de mettre en pratique les différentes fonctionnalités offertes par la bibliothèque.

N'hésitez pas à explorer davantage en combinant ces fonctions pour créer des structures de données plus complexes et des algorithmes plus avancés!

## Références

Pour plus d'informations sur les fonctions disponibles, consultez le fichier header `vectors.h` ou la documentation de la bibliothèque.
