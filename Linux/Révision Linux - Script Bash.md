---


---

<h1 id="revisions-linux">Revisions Linux</h1>
<h2 id="scripts-bash">Scripts Bash</h2>
<h3 id="variables-denvironnement">Variables d’environnement</h3>
<ul>
<li><strong>printenv LANG</strong> : afficher variable d’environnement</li>
<li><strong>echo $LANG</strong> : afficher contenu d’une V.E</li>
<li><strong>export VAR=“test”</strong> : créer une V.E<br>
💡 Pour que la création/modifcation d’une V.E soit <strong>permanente</strong> pour <strong>l’utilisateur courant</strong>, il faut ajouter la <em>commande</em> au fichier <code>.bashrc</code> puis le recharger avec <code>source ~/.bashrc</code></li>
<li>Variable <strong>PATH</strong> : où trouver les commandes taper par l’utilisateur</li>
<li><strong>unset VAR</strong> : supprimer une variable</li>
</ul>
<hr>
<h3 id="intro-au-scripts">Intro au scripts</h3>
<ul>
<li>
<p><strong>#!/bin/bash</strong> : shebang</p>
</li>
<li>
<p><strong>chmod u+x</strong> : rendre script exécutable</p>
</li>
<li>
<p><strong>myVar</strong> : initialiser une variable globale</p>
</li>
<li>
<p><strong>local myVar</strong>: initialiser une variable local</p>
</li>
<li>
<p><strong>$(…)</strong> : récupérer résultat d’une commande<br>
💡 Exemple : rep=<em>dollar</em>(pwd)</p>
</li>
<li>
<p><strong>read</strong> : demander au user de saisir une valeur<br>
💡 Exemple : <code>read -p 'Saisir deux valeurs a et b : ' a b</code><br>
▶️ <strong>-p</strong> : affiche un message<br>
▶️ <strong>-s</strong> : n’affiche pas le texte saisi<br>
▶️ <strong>-n</strong> : limite nbr caractères</p>
</li>
<li>
<p><strong>echo -e “\n Echo”</strong> : utiliser le retour chariot <em>\n</em></p>
</li>
<li>
<p><strong>Paramètres et $ :</strong></p>
</li>
</ul>
<p>▶️ <strong>$#</strong> = nombre de paramètres</p>
<p>▶️ <strong>$0</strong> = nom du script</p>
<p>▶️ <strong>$1…</strong> = premier paramètre…</p>
<p>▶️ <strong>$</strong>* = récupère l’ensemble des paramètres à la ligne</p>
<p>▶️ <strong>“$*”</strong> = idem mais inclu paramètres avec espaces</p>
<p>▶️ <strong>$?</strong> = récupérer valeur return</p>
<p>▶️ <strong>shift</strong> = nettoie à chaque fois $1 et remplace par $2</p>
<p>💡 Boucle for qui affiche les paramètres :<br>
for i in $(seq 1 3); do<br>
echo ${!i}<br>
done</p>
<hr>
<h3 id="tableau">Tableau</h3>
<ul>
<li><strong>tab=()</strong> : créer un tableau</li>
<li><strong>${tab[0]}</strong> : accéder à une valeur à l’index 0</li>
<li><strong>${tab[*]}</strong> : afficher contenu du tableau avec *</li>
<li><strong>${#tab[*]}</strong> : affiche taille du tableau</li>
</ul>
<hr>
<h3 id="conditions">Conditions</h3>
<ul>
<li>
<p>Structure de base :<br>
<strong>if</strong> [ condition1 ]<strong>; then</strong><br>
echo “…”<br>
elif [ condition2 ]; then<br>
echo “…”<br>
else<br>
echo “autre”<br>
<strong>fi</strong></p>
</li>
<li>
<p>Tests possible sur les <strong>chaînes de caractères</strong> entre <em>guillemets</em> :<br>
▶️ $chaine1 <strong>==</strong> $chaine2 : les deux sont <strong>identiques</strong><br>
▶️ $chaine1 <strong>!=</strong> $chaine2 : les deux sont <strong>différentes</strong><br>
▶️ <strong>-z</strong> $chaine2 : test si chaine est <strong>vide</strong></p>
</li>
<li>
<p>Tests possible sur les nombres :<br>
▶️ $num1 <strong>-eq</strong> $num2 : nombres <strong>égaux</strong><br>
▶️ $num1 <strong>-ne</strong> $num2 : nombres <strong>différents</strong><br>
▶️ $num1 <strong>-lt</strong> $num2 : <strong>num1 &lt; num2</strong><br>
▶️ $num1 <strong>-le</strong> $num2 : <strong>num1 &lt;= num2</strong><br>
▶️ $num1 <strong>-gt</strong> $num2 : <strong>num1 &gt; num2</strong><br>
▶️ $num1 <strong>-ge</strong> $num2 : <strong>num1 &gt;= num2</strong></p>
</li>
<li>
<p><strong>[[…]]</strong> et <strong>((…))</strong> : permettent d’utiliser <em>operateurs mathématiques</em> / <em>operateurs logiques || et &amp;&amp;</em></p>
</li>
</ul>
<hr>
<h3 id="boucles">Boucles</h3>
<p>📍  While<br>
while [ test ]<br>
<strong>do</strong><br>
echo ‘Action en boucle’<br>
<strong>done</strong></p>
<p>📍  For liste caractères<br>
for fichier in $(ls)<br>
<strong>do</strong><br>
cp $fichier $fichier.bak<br>
<strong>done</strong></p>
<p>📍  For suite de nombres<br>
for i in $(seq 1 10)<br>
<strong>do</strong><br>
echo $i<br>
<strong>done</strong></p>
<hr>
<h3 id="fonctions">Fonctions</h3>
<ul>
<li>
<p>Syntaxe 1 pour déclarer une fonction :<br>
<strong>ma_fonction () {</strong><br>
<em>instructions</em><br>
<strong>}</strong></p>
</li>
<li>
<p>Syntaxe 2 pour déclarer une fonction :<br>
<strong>function ma_fonction  {</strong><br>
<em>instructions</em><br>
<strong>}</strong></p>
</li>
<li>
<p><strong>return</strong> : s’utilise seulemnt pour renvoyer le statut de la derni_re instruction<br>
▶️ <strong>0</strong> : succès (par défaut)<br>
▶️ <strong>1-255</strong> : si autre<br>
💡 <strong>$?</strong> : Récupéré la valeur du return</p>
</li>
</ul>

