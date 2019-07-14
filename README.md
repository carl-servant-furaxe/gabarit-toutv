# Gabarit Tou.tv
Gabarit pour les projets Tou.tv

- [Pre-requis](#pre-requis)
- [Form State](#form-state)
- [Google Analytics](#google-analytics)
- [Meta](#meta)
- [Omniture](#omniture)
- [Pixel](#pixel)
- [Clicktrackers](#clicktrackers)
- [Code :: Stylesheet](#code-stylesheet)
- [Code :: Javascript](#code-javascript)



## Pre-requis
Il n'y a pas de d'element pre-requis pour ce gabarit.

La librairie JQuery est presente a titre d'exemple.


## Form State
Depuis 2019, nous ajoutons l'attribut "data-form-state", aux pages de type concours.
Cette attribut est ensuite recupere dans le css pour changer l'apparence de la page selon la valeur de l'attribut.

En general, c'est surtout le bouton de participation qui change de l'etat "Participer" a "Concours termine".

```
<html class="nojs" lang="fr" dir="ltr" data-form-state="!closed">
```

Il a ete entendu que de facon general, lorsque le concours est dans la periode active, la valeur est "*!closed*".

Ensuite, lorsque le concours est termine, on change la valeur pour "*closed*".

Cela permet a Stefan de faire le changement sans que nous ayons a intervenir, si jamais il voudrait effectuer le travail seul.

Dans le CSS, le changement d'etat se ferait comme suit:

```
html[data-form-state="!closed"] .bouton-de-participation{ background-image: url(../images/bouton-participer.png); }
html[data-form-state="closed"] .bouton-de-participation{ background-image: url(../images/bouton-terminer.png); }
```

## Google Analytics
Toujours mettre un code Google Analytics. Ce n'est pas la mesure officielle, mais le departement des vente s'y refere souvent.
Le code doit absolument avoir les attributs d'anonymisation de l'adresse IP active. Ce n'est pas une valeur par defaut du code Analytics.

```
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-87186208-51&api=1"></script>
<script>
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'UA-87186208-51', { 'anonymize_ip': true });
</script>
```
Le code se trouve dans le URL `&api=1` et dans le code javascript `{'anonymize_ip' : true}`

## Meta
Les meta sont fournis par le charge de projet. Le code est souvent a verifier car il n'est pas toujours bien ecrit.
Voici la facon comment ce devrait etre ecrit.

```
<title> | ICI Radio-Canada.ca</title>
<meta name="Description" content="" />
<meta name="Keywords" content="" />
<meta name="dc.title" content=" | ICI Radio-Canada.ca" />
<meta name="dc.keywords" content="" />
<meta name="dc.description" content="" />
<meta property="og:url" content="" />
<meta property="og:type" content="website" />
<meta property="og:title" content=" | ICI Radio-Canada.ca" />
<meta property="og:description" content="" />
<meta property="og:image" content="" />
```


## Omniture
Contrairement au gabarit Radio-Canada, celui de Tou.tv utilise des valeur javascript.

### Initier Omniture
Le systeme de suivit est d'abord initie par un code javascript general. Il doit etre situe avant la declaration des valeurs de tracking.

```
<script src="https://assets.adobedtm.com/2eda04f28b1fa2bbcd3ec449dfdc174232ed3359/satelliteLib-fafff6f6fa41c8ef8818e2ad8c1bfb4776de2f18.js"></script>
```
### Valeur du projet
Les valeurs de tracking vous seront fourni via courriel par le charge de projet. Le code sera soit inclus dans le message courriel ou dans un document Word. Vous devrez mettre ces valeurs a l'endroit que vous souhaitez, tant que c'est apres le code d'initiation du systeme de suivi et que ce soit dans la partie HEAD du code HTML.

```
<script>
dataLayerQueue.push ({
	page : {
		Section : "",
		GroupeSection : "",
		Segment : "",
		CodePage : ""
	},
	dataPushType : "prePageView"
});
</script>
```

## Pixel
Il arrive que le client souhait ajouter un pixel de "retargeting". Un espace est deja prevu a cet effet (ligne #78).
Le pixel est un code image. Vous pouvez en ajouter autant que vous le voulez, tant que les codes soient dans le div pixel.

```
<div id="pixel">
	<img src="http://lien-vers-le-pixel.jpg" alt="" height="1" width="1" />
</div>
```

## Clicktrackers
Le client pourrait fournir des code "clicktrackers". Ces code remplacent les URL cliquables.

SVP, s'assurer que les codes fournis fonctionnent correctement et que ce sont bien des redirection URL.
Parfois, ce sont des url de pixel qui vous seront fourni a la place.


## Code :: Stylesheet
### Google Font
Toujours utiliser des police Google. De cette facon, on s'assure que le site fonctionnera correctement sur tous les navigateurs sans avoir a les tester.
A l'exception, des polices Radio-Canada, Rubrik (tou.tv) et FontAwesome.

### toutv.css
Le gabarit Tou.tv a ete fait par l'equipe Furaxe. Aucun gabarit n'a ete fourni par Radio-Canada ou ses sous-divisions.
S'il y avait changement a apporter dans les menus, ils devront etre fait manuellement.

La feuille `toutv.css` se compose des elements suivants:
- Appels aux polices
- Declaration de RESET. source Yahoo.
- Declaration des elements de base, pour un affichage uniforme sur tous les navigateurs. source Yahoo.
- Tou.tv, declaration "Entete" et "Pied de page" generaux.

*Une declaration #wrapper{ overflow-x:hidden} a ete ajoute pour s'assurer que tout element sortant du cadre ne nuise pas a la navigation*

### style.css
Les breakpoints poour le responsive est inclus dans le code. Ce sont les formats les plus standard.
Si vous les respectez, vous aurez moins de probleme avec la compatibilite des navigateurs.

En pied de code, il y a aussi un espace nomme "demo". Ce code est en place pour aider au developpeur a placer les elements selon la maquette fournie.

## Code :: Javascript
Si vous deviez utiliser du javascript dans votre projet, mettre les js dans le pied du site.

Pour eviter tout conflit avec d'autres codes, il est preferable d'isoler vos declarations de cette facon:

```
(function($) {
	/// votre code
})(jQuery);
```
