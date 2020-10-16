# Guide & Cheatsheet Flexbox HTML/CSS

## Table des matières

* [Propriétés du parent (la flexbox en elle-même)](#parent)
* [Propriétés des enfants / items](#children)

[ANCRE_PARENT_PROPS]: g
## <a name="parent"></a>Les propriétés de la balise parent

![image flex parent](./img/01-container.svg)

* [display: flex](#display-flex)
* [flex-direction (row/col)]()
* [flex-wrap: no/wrap](#flex-wrap)
* [flex-flow: column wrap](#flex-flow)
* [justify-content](#justify-content)
* [align-items](#align-items)
* [align-content](#align-content)

### <a name="display-flex"></a>display: flex

Tout container flex (l'élément "parent"), doit être initialisé via la propriété CSS `display: flex`

Cette propriété active un contexte flex pour tous ses enfants direct.

```css
.container {
	display: flex;
}
```

### <a name="flex-direction"></a>flex-direction

![image flex-direction](./img/flex-direction.svg)

Flex-Direction permet de changer l'axe principal.

`flex-direction: row` -> de gauche à droite
`flex-direction: column` -> de haut en bas

```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

### <a name="flex-wrap"></a>flex-wrap

![image flex-wrap](./img/flex-wrap.svg)

Par défaut tous les items essayeront d'être sur une ligne.
Cette propriété permet d'autoriser le parent à disposer les enfants sur plusieurs lignes.

```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

### <a name="flex-flow"></a>flex-flow

Raccourci pour `flex-direction` et `flex-wrap`

La valeur par défaut est `row nowrap`

```css
.container {
	flex-flow: column wrap;
}
```

### <a name="justify-content"></a>justify-content

![image justify-content](./img/justify-content.svg)

**Agit sur l'axe principal**

Ceci définit l'alignement le long de l'axe principal. Il aide à répartir l'espace libre supplémentaire restant lorsque tous les éléments flexibles d'une ligne sont rigides ou flexibles mais ont atteint leur taille maximale. Il exerce également un certain contrôle sur l'alignement des éléments lorsqu'ils dépassent la ligne.

```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe;
}
```

### <a name="align-items"></a>align-items

![image align-items](./img/align-items.svg)

**Agit sur l'axe secondaire (perpendiculaire à l'axe principal)**

Cela définit le comportement par défaut de la disposition des éléments flexibles le long de l'axe transversal sur la ligne courante. Considérez-le comme la version justify-content pour l'axe transversal.

```css
.container {
  align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe;
}
```

### <a name="align-content"></a>align-content

![image align-content](./img/align-content.svg)

Cela aligne les lignes d'un conteneur flexible à l'intérieur lorsqu'il y a un espace supplémentaire dans l'axe transversal, de la même manière que justify-content aligne les éléments individuels dans l'axe principal.

Remarque: cette propriété n'a aucun effet lorsqu'il n'y a qu'une seule ligne d'éléments flexibles.

```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end | baseline | first baseline | last baseline + ... safe | unsafe;
}
```

## <a name="children"></a>Les propriétés des éléments enfants
> éléments enfants direct au parent qui possède la propriété `display: flex`

![image flex children](./img/02-items.svg)

Ces propriétés s'appliquent sur les items d'un container flex.

* [order](#order)
* [flex-grow](#flex-grow)
* [flex-shrink](#flex-shrink)
* [flex-basis](#flex-basis)
* [flex](#flex)
* [align-self](#align-self)


### <a name="order"></a>order

![image order](./img/order.svg)

Par défaut, les éléments flexibles sont disposés dans l'ordre de la source (HTML). Cependant, la propriété `order` contrôle l'ordre dans lequel ils apparaissent dans le conteneur flex.

```css
.item {
  order: 5; /* valeur par défaut: 0 */
}
```

### <a name="flex-grow"></a>flex-grow

![image order](./img/flex-grow.svg)

Cela définit la capacité d'un élément flexible à croître si nécessaire. Il accepte une valeur sans unité qui sert de proportion. Il dicte la quantité d'espace disponible à l'intérieur du conteneur flexible que l'élément doit occuper.

Si flex-grow est défini sur 1 pour tous les éléments, l'espace restant dans le conteneur sera distribué de manière égale à tous les enfants. Si l'un des enfants a une valeur de 2, l'espace restant prendrait deux fois plus d'espace que les autres (ou il essaiera de le faire, au moins).

```css
.item {
  flex-grow: 4; /* défault: 0 */
}
```

> Nombres négatifs invalides

### <a name="flex-shrink"></a>flex-shrink

Cela définit la possibilité pour un élément flexible de se réduire si nécessaire.

```css
.item {
  flex-shrink: 3; /* défault: 1 | 0 = ne peut pas se rétrécir */
}
```

> Inverse de flex-grow

### <a name="flex-basis"></a>flex-basis

![image order](./img/rel-vs-abs-flex.svg)

Ceci définit la taille par défaut d'un élément avant que l'espace restant ne soit distribué. Il peut s'agir d'une longueur (par exemple 20%, 5rem, etc.) ou d'un mot-clé. Le mot-clé auto signifie «regardez ma propriété width ou height» (ce qui a été temporairement fait par le mot-clé main-size jusqu'à ce qu'il soit obsolète). Le mot-clé de contenu signifie "dimensionner le contenu en fonction du contenu de l'élément". Ce mot-clé n'est pas encore bien pris en charge. Il est donc difficile à tester et plus difficile de savoir ce que font ses frères max-content, min-content et fit-content.

```css
.item {
  flex-basis:  | auto; /* default auto */
}
```

S'il est défini sur 0, l'espace supplémentaire autour du contenu n'est pas pris en compte. S'il est défini sur auto, l'espace supplémentaire est distribué en fonction de sa valeur flex-grow. Voir ce graphique.


### <a name="flex"></a>flex

C'est le raccourci pour `flex-grow`, `flex-shrink` et `flex-basis` combinés. Les deuxième et troisième paramètres (`flex-shrink` et `flex-basis`) sont facultatifs. La valeur par défaut est 0 `1 auto`, mais si vous la définissez avec une valeur numérique unique, c'est comme `1 0`.

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

**Il est recommandé d'utiliser cette propriété abrégée plutôt que de définir les propriétés individuelles. La sténographie définit les autres valeurs de manière intelligente.**

### <a name="align-self"></a>align-self

Cela permet de remplacer l'alignement par défaut (ou celui spécifié par align-items) pour les éléments flex individuels.

Veuillez consulter l'explication d'align-items pour comprendre les valeurs disponibles.

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

[Voir doc officiel MDN](https://developer.mozilla.org/fr/docs/Web/CSS/align-self)

> Notez que float, clear et vertical-align n'ont aucun effet sur un élément flexible.
