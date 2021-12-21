# Comment coder proprement
**Les conseils proposés dans ce guide sont tirés, en majeur partie, de l'ouvrage _Clean Code: A Handbook of Agile Software
Craftsmanship_ de Robert C. Martin. Il s'agit d'un ouvrage de référence sur la question
des bonnes pratiques de programmation. Seul le contenu des quatre premiers chapitres de l'ouvrage sont résumés dans ce guide. 
Nous vous invitons à consulter le livre si vous voulez aller plus loin.**

## 1. Nommer les variables

Coder proprement nécessite d'abord et avant tout de bien nommer ses variables. Du code
dont les variables sont mal nommées peut rapidement dewvenir incompréhensible, même pour
son auteur.

Le grand principe à respecter lorsqu'on nomme ses variables : **révéler l'intention**.
Pour le dire succintement il faut dire :
>* **d'une variable -> ce que c'est.**
>* **d'une fonction -> ce qu'elle fait.**

### Quelques conseils pour bien nommer ses variables
>1. **Éviter les noms de variables courts.**
>2. **Éviter les abréviations.**
>3. **Éviter des noms de variables qui varient peu entres eux.**
>4. **Éviter d’utiliser deux mots différents pour dénoter la même chose/action** (un mot par concept).
>5. **Utiliser un _verbe_ qui décrit ce que fait une fonction lorsque vous la nommer.**

| Conseil | Mauvais | Bon |
|---------|---------|-----|
| 1       | Mauvais |`a = pd.read_csv("articles.csv")` |
| 1       | Bon     |`articles = pd.read_csv("articles.csv")`|
| 2       | Mauvais |`tot_obs = 10` |
| 2       | Bon     |`total_observations = 10`|
| 3       | Mauvais | `count_of_trees_in_the_city = 50` <br> `count_of_plants_in_the_city = 40 `<br> |
| 3       | Bon     | `trees_count = 50` <br>`plants_count = 40 ` |
| 4       | Mauvais | `get_observations()` <br>`fetch_annotations()`<br> |
| 4       | Bon     | `get_observations()` <br>`get_annotations()` |
| 5       | Mauvais | `def articles(file_path):`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`[code]`<br> |
| 5       | Bon     | `def get_articles(file_path)`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`[code]`<br> |



## 2. Les commentaires

Il y a une croyance assez répendue dans le monde de la programmation selon laquelle plus
on commente notre code, mieux c'est. Selon l'auteur de _Clean Code_, cette croyance est fausse. Le grand
danger réside dans le fait que l'on peut oublier de mettre à jour des commentaires. Lorsque
cela se produit, les commentaires peuvent nous induire en erreur. Pour paraphraser Robert C. Martin :
**«les commentaires peuvent mentir, mais le code dit la vérité»**. Sachant cela, il vaut mieux,
la plupart du temps, utiliser son énergie pour essayer d'écrire du code propre au lieu d'écrire
des commentaires. Voici donc quelques conseils en lien avec les commentaires
Privilégier le code propre. 
>**Les choses à éviter**
>1. Plutôt que d’écrire de longs commentaires afin d’expliquer comment fonctionne un bout de code malpropre, prenez ce temps pour essayer de **rendre votre code plus propre**. 
>2. **Éviter les commentaires qui expliquent ce que fait du code simple**. Vous pouvez tenir pour acquis que la personne qui lira votre code connaît les fonctionnalités de base du langage que vous utilisez. Il n’a pas besoin de plus d’explications. 
>3. **Ne pas laisser de code commenté**. On peut avoir tendance à commenter du code qui ne sert plus, mais dont on pense avoir besoin plus tard. Il vaut mieux l’effacer et se reposer sur notre outil de contrôle des versions (git). 

| Conseil |      |                                                                                                                                                                                                                                                |
|---------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 et 2  | **Mauvais** | `# itération sur la liste d'articles pour aller chercher les titres`<br>`# 'a' représente la liste des articles (qui est une liste de liste)` <br>`list = []`<br>`for i in range(52):`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`list.append(a[i][3])` |
| 1 et 2  | **Bon**     | `title_index = 3`<br>`number_of_articles = len(articles)`<br>`article_titles = []`<br>`for article_index in range(number_of_articles):`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`article_titles.append(articles[article_index][title_index])`<br>     |
| 3       | **Mauvais** | `articles = get_articles(path)`<br>`# articles = articles[:-1]`<br>`# articles = do_something_funky(articles)`<br>`save(articles)`<br>                                                                                                         |
| 3       | **Bon**     | `articles = get_articles(path)`<br>`save(articles)`<br>                                                                                                                                                                                        |



>**Les commentaires sont **utiles** pour** : <br>
>1. **Justifier un choix**, par exemple si vous faites un choix d’algorithme, un choix de libraire, ou un choix de conception qui mérite d’être justifié. <br>
>2. **Indiquer la durée que prend l’exécution d’un bout de code** (si c’est long). <br>
>3. **Documenter une fonction** (préciser le type des paramètres et les données retournées). Voir, par exemple, l'outil [Docstrings](https://realpython.com/documenting-python-code/#documenting-your-python-code-base-using-docstrings) en _python_
>4. **Expliquer un bout de code complexe** (dont la logique serait difficile à comprendre même pour un programmeur ou une programmeuse d’expérience). 

## 3. Les fonctions

>**L’utilité des fonctions** : 
>* **Éviter la redondance**. Avoir plusieurs versions d’un même bout de code peut générer des erreurs. En effet, si l’on veut modifier ce bout de code, on devra mettre à jour chaque version. Or, il se peut qu’on oublie de le faire pour une version. On prend alors le risque d’avoir deux bouts de code qu’on croit identiques, mais qui font des choses différentes. 
>* **Dévoiler ce que son code fait**. En imbriquant notre code dans des fonctions, et en faisant bien notre travail de nommage de ces fonctions, on dévoile au lecteur ce que notre code fait. 
>* **Masquer la complexité**. La personne qui lit notre code n’a pas toujours besoin de savoir comment fonctionne notre code dans le détail. En imbriquant notre code dans des fonctions, on offre au lecteur une sorte de résumé de ce que notre code fait. S’il veut avoir plus de détails, il pourra aller voir l’implémentation de nos fonctions. 

>**Conseils pour écrire de bonnes fonctions** <br>
>1. **Courtes**. Viser un maximum de 20 lignes. Si elle est plus longue, on doit la décomposer en de multiples fonctions plus courtes. 
>2. **Aucun _side effect_** : Une fonction ne change pas la valeur de variables déclarées à l’extérieur d’elle. 
>3. **Un niveau d’abstraction**. Le code au plus bas niveau d'abstraction est le code qui fait les opérations les plus simples, par exemple, lire un fichier, faire des opérations simples sur des chaînes de caractères ou sur des listes, faire des opérations mathématiques, etc. Une fonction qui regroupe du code du plus bas niveau serait au deuxième niveau d’abstraction, et une fonction qui regroupe une multitude de fonctions de deuxième niveau serait au troisième niveau, et ainsi de suite. Dans une fonction, il faut éviter d’avoir des lignes de codes qui sont à différents niveaux d'abstractions. 
>4. **Fait une chose** (à un niveau d’abstraction). Votre fonction doit uniquement faire ce que son nom suggère. Par exemple, si votre fonction s’occupe de télécharger des données, elle doit uniquement faire cela. Elle ne doit pas s’occuper d’une partie de travail de nettoyage des données. «Faire une chose» doit être compris en relation avec le concept de niveau d'abstraction. La «chose», ou l’action, que fait une fonction peut très bien être décomposable en de multiples 
actions plus simples. Pour faire une analogie avec une tâche de la vie quotidienne, «acheter du lait» peut être considéré comme faire une action, même si l’on peut décomposer cette action en une multitude d’actions plus simples. Si j'arrête prendre un café en allant acheter du lait, j'ai alors fait deux choses.

| Conseil |             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 2       | **Mauvais** | `VALEUR_CONSTANTE = 5` <br> <br> `def function_avec_side_effect(arg):` <br> &nbsp;&nbsp;&nbsp;&nbsp;`VALEUR_CONSTANTE = arg`   <br><br/>                                                                                                                                                                                                                                                                                                                                                       |
| 2       | **Bon**     | `VALEUR_CONSTANTE = 5` <br> <br>`def function_sans_side_effect(arg):` <br> &nbsp;&nbsp;&nbsp;&nbsp;`arg = arg + VALEUR_CONSTANTE` <br> &nbsp;&nbsp;&nbsp; `return arg` <br><br/>                                                                                                                                                                                                                                                                                                               |
| 3       | **Mauvais** | `def function_multi_niveau(argument_1, argument_2):` <br> &nbsp;&nbsp;&nbsp;&nbsp; `argument_1 = fait_quelque_chose_de_tres_complexe(argument1, argument2)` <br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`argument_1 = argument_1 + argument_2`<br>  &nbsp;&nbsp;&nbsp;&nbsp; `return argument_1`<br><br/>                                                                                                                                                                                        |
| 3       | **Bon**     | `def function_un_niveau_simple(argument_1, argument_2):`<br> &nbsp;&nbsp;&nbsp;&nbsp; `argument_1 = argument_1 ** 2` <br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`argument_1 = argument_1 + argument_2`<br>  &nbsp;&nbsp;&nbsp;&nbsp; `return argument_1`<br><br/>                                                                                                                                                                                                                                                                                       |
| 3       | **Bon**     | `def function_un_niveau_complexe(argument_1, argument_2):`<br> &nbsp;&nbsp;&nbsp;&nbsp; `argument_1 = fait_quelque_chose_de_tres_complexe(argument_1)` <br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`argument_1 = fait_une_autre_chose_complexe(argument_1, argument_2)` <br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `return argument_1` <br><br/>                                                                                                                                                             |
| 4       | **Mauvais** | `def nettoyer_les_dates(data):`<br> &nbsp;&nbsp;&nbsp;&nbsp; `data = enlever_les_mauvaises_date(data)`<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`data = mettre_les_dates_dans_le_bon_format(data)`<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`data = calcule_moyenne_par_jour(data)`<br> &nbsp;&nbsp;&nbsp;&nbsp; `data = calcule_moyenne_par_mois(data)`<br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `return data`<br><br/>                                                                                          |
| 4       | **Bon**     | `def nettoyer_les_dates(data):`<br> &nbsp;&nbsp;&nbsp;&nbsp; `data = enlever_les_mauvaises_date(data)`<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`data = mettre_les_dates_dans_le_bon_format(data)`<br>  &nbsp;&nbsp;&nbsp;&nbsp; `return data`<br><br/>`def calculer_statistiques_par_jour`<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`data = calcule_moyenne_par_jour(data)`<br> &nbsp;&nbsp;&nbsp;&nbsp; `data = calcule_moyenne_par_mois(data)`<br>  &nbsp;&nbsp;&nbsp;&nbsp; `return data`<br><br/> |
<br>

> **Structure de l’article de journal**. 
> Dans un fichier de fonctions (ou le fichier d’une classe), mettre les fonctions du plus haut niveau en haut du fichier, 
> et les fonctions de plus bas niveau en bas du fichier. De cette manière, le lecteur pourra avoir accès à une vue d’ensemble 
> en lisant le début du fichier, et pourra avoir accès à la complexité seulement s’il le désire. Le premier exemple de code
> ci-bas présente un bout de code qui obéit à ce principe, et le second un bout de code qui y désobéit.
> 
>Dans le premier exemple, la première fonction que l'on rencontre, `nettoyer_les_donnees(data)`, est celle du plus haut niveau. On
> rencontre ensuite les fonctions de plus bas niveau selon leur ordre d'apparition dans `nettoyer_les_donnees(data)`. Dans le second exemple, les fonctions sont dans un ordre aléatoire. On voit
> tout de suite qu'il est plus difficile de naviguer dans ce «fichier» de fonctions.

<br>

**Exemple de code qui respecte la structure de l'article de journal**
```python
def nettoyer_les_donnees(data):
    data = remplacer_les_NA_par_moyenne(data)
    data = nettoyer_les_dates(data)
    data = gerer_les_donnees_aberrantes(data)
    return data

def remplacer_les_NA_par_moyenne(data):
    [code]
    
def nettoyer_les_dates(data):
    [code]
    
def gerer_les_donnees_aberrantes(data):
    for colonne in data:
        if colonne_contient_valeurs_aberrantes(colonne):
            effacer_valeurs_abberantes(colonne)

def colonne_contient_valeurs_aberrantes(colonne):
    [code]

def effacer_valeurs_abberantes(colonne):
    [code]
```

<br>

**Exemple de code qui _NE respecte PAS_ la structure de l'article de journal**
```python
def colonne_contient_valeurs_aberrantes(colonne):
    [code]

def effacer_valeurs_abberantes(colonne):
    [code]
    
def remplacer_les_NA_par_moyenne(data):
    [code]
    
def nettoyer_les_dates(data):
    [code]

def nettoyer_les_donnees(data):
    data = remplacer_les_NA_par_moyenne(data)
    data = nettoyer_les_dates(data)
    data = gerer_les_donnees_aberrantes(data)
    return data
    
def gerer_les_donnees_aberrantes(data):
    for colonne in data:
        if colonne_contient_valeurs_aberrantes(colonne):
            effacer_valeurs_abberantes(colonne)

```

