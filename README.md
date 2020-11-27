# SITE WEB D'ANALYSE


## FONCTIONNEMENT
Ce site utilise le framework [Bootstrap 4](https://getbootstrap.com/). Cela permet d'avoir très facilement un site qui s'adapte à tout type d'écran et de nombreuses fonctionnalités sont directement incluses.

Il y a une seule page avec laquelle l'utilisateur va interagir (`index.html`) et les autres pages sont affichées dans celle-ci gâce à un `iframe`. Ainsi, lorsque l'utilisateur choisi une section dans le menu, cela va mettre à jour la source de l'`iframe` et la page correspondante va être affichée.
Cela a plusieurs avantages :
* un temps de chargement beaucoup moins long (chaque page est chargée "à la demande") ;
* un code plus lisible puisque séparé en plusieurs fichiers ;
* le fonctionnement pour l'utilisateur est exactement le même que celui du site initial.

Mais un désavantage aussi :
* redondance de certaines parties du code (notamment le `header` qui est le même pour toutes les pages "sections").

### Numérotations des pages "sections"

Chaque page HTML "section" (c-à-d celles affichées dans l'`iframe` et stockées dans `resources/sections/`) est numéroté selon le numéro de sa section et le numéro de sa sous-section : `[numéro de section]-[numéro de sous-section].html`.


## CHANGELOG

Je tiens compte ici de tous les changements que j'ai effectué sur les environnements qui ne permettent plus d'utiliser le JavaScript et le CSS du site initial.
J'y ajoute le code actualisé.

### Preuves

J'ai décidé d'utiliser les fonctionnalités de Bootstrap pour afficher les preuves. Ainsi, la classe `entete-preuve` ainsi que la fonction `shwo_proof` ne sont plus utilisables.
Pour ajouter une preuve, il suffit d'ajouter le code suivant :

```HTML
<div class="preuve">
  <a class="btn btn-outline-secondary" data-toggle="collapse" href="#preuveExemple" role="button" aria-expanded="false" aria-controls="preuveExemple">Preuve:</a>
  <div class="collapse" id="preuveExemple">
    <div class="card card-body">
      <p>Ceci est une preuve.</p>
    </div>
  </div>
</div>
```

Il faut remplacer les 3 `preuveExemple` avec un id unique.

### Vidéos

De même, pour ajouter les vidéos j'ai décidé d'utiliser les fonctionnalités de Bootstrap. Il suffit d'ajouter le code suivant :

```HTML
<div class="video">
  <a class="btn btn-outline-secondary" data-toggle="collapse" href="#IDvideodiv-v_DL_intro" role="button" aria-expanded="false" aria-controls="IDvideodiv-v_DL_intro">Ceci est une vidéo</a>
  <div class="collapse" id="IDvideodiv-v_DL_intro">
    <div class="card card-body">
      <video class="HTMLvideo" src="../videos/v_DL_intro.mp4" poster="../videos/v_DL_muet_thumbnail.png" controls=true></video>
    </div>
  </div>
</div>
```

Il faut aussi remplacer les 3 `IDvideodiv-v_DL_intro` avec un ID unique ainsi qu'indiquer l'url de la vidéo et de la vignette. La fonction `insert_video` n'est plus utilisable sinon la vidéo ne rentre pas dans le cadre et n'est pas cachée.

### Quiz

J'ai un peu modifié la fonction `montrer_cacher` pour qu'elle affiche les réponses seulement sur le quiz où l'on a cliqué. Pour cela, j'ai du rajouter un ID pour chaque quiz qu'il faut ensuite passer à la fonction. J'ai également modifié le bouton. Il suffit d'ajouter le code suivant :

```HTML
<div class="quiz" id="quiz0_4_1">
  (Ordre total sur \(\mathbb{R}\).)
  <ol>
      <li><span class="itemEMPTY">[ ]</span> Si \(x\leqslant y\) et \(a\leqslant b\), alors \(\frac{x}{a}\leqslant \frac{y}{b}\).
      <li><span class="itemFULL">[ ]</span> Si \(0\lt a\lt b\), alors \(\frac{1}{b}\lt \frac{1}{a}\).
      <li><span class="itemEMPTY">[ ]</span> Si \(x\leqslant y\) et \(a\leqslant b\), alors \(ax\leqslant by\).
      <li><span class="itemEMPTY">[ ]</span> Si \(x\lt y+\varepsilon\) pour tout \(\varepsilon\gt 0\), alors \(x\lt y\).
      <li><span class="itemFULL">[ ]</span> Si \(x\geqslant a\) et \(|y|\leqslant a/2\), alors \(x+y\geqslant a/2\).
      <li><span class="itemFULL">[ ]</span> Si \(x_k\leqslant a\) pour tout \(k=1,2,\dots,n\), alors \(\max\{x_1,,\dots,x_n\}\leqslant a\).
  </ol>
  <span class="quiz-btn"><button type="button" class="btn btn-primary" onclick="montrer_cacher('quiz0_4_1')">Solutions</button></span>
</div>
```

### Images

Pour avoir des images qui s'adapte à la taille d'écran, il suffit d'ajouter la class `img-fluid` et Bootstrap se charge de tout :

```HTML
<img src="../images/i_reels_la_droite_simple.jpg" class="img-fluid" width="350">
```

### Remarques sur KaTeX

* KaTeX est très peu adapté pour l'affichage mobile, les expressions mathématiques forment des blocs donc cela produit fréquement des "overflow" lorsque l'on réduit la taille de l'écran. J'ai réussi à trouver un bout de code CSS sur Github qui permet de rendre chaque expression "scrollable" horizontalement et individuellement lorsqu'il y a overflow, ce qui évite de devoir scroller toute la page horizontalement.
* Parfois KaTeX revient à la ligne après chaque expression mathématique lorsqu'elles sont incluses dans une `div`. Pour corriger cela, il suffit simplement de tout inclure dans une balise paragraphe `<p></p>`.
