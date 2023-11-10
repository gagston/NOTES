---


---

<h1 id="revisions-linux">Revisions Linux</h1>
<h2 id="commandes-bash">Commandes Bash</h2>
<ul>
<li>Shell principaux : <strong>sh, bash, ksh, zsh</strong></li>
<li>Changer de console virtuelle : <strong>Alt+F1</strong> (6 consoles max)</li>
<li>Info sur une section <strong>man :</strong> <code>$ man 3 cat</code></li>
<li>Rechercher un terme dans un man : <code>/.....</code></li>
<li>Info sur les différentes pages d’un manuel : <code>$ man -f cat</code></li>
<li>Infos commande format GNU : <code>info cat</code></li>
<li>Infos brève d’une commande : <code>head --help</code></li>
<li>Infos très brève d’une commande : <code>whatis head</code></li>
<li>Rappeler la dernière commande : <code>!!</code></li>
<li>Rechercher le chemin d’une commande : <code>which commande</code></li>
<li><strong>FHS</strong> = <em>Filesystem Hierarchy Standard</em></li>
</ul>
<hr>
<h3 id="repertoires">Repertoires</h3>
<ul>
<li><strong>/bin</strong> : commandes de base (binaires)</li>
<li>/boot : chargeur d’amorçage</li>
<li><strong>/dev</strong> : device, périphériques</li>
<li>/etc : Editable Text Configuration, fichiers de conf</li>
<li>/home : répertoires perso des users</li>
<li><strong>/lib</strong> : library, biblitohèques logicielles</li>
<li><strong>/media</strong> : point de montage médias amovibles</li>
<li><strong>/lost+found</strong> : fichiers récupérés après un crash</li>
<li><strong>/mnt</strong> : point de montage <em>temporaire</em></li>
<li><strong>/run</strong> : infos sur la session en cours</li>
<li><strong>/sbin</strong> : binaires système et tâches d’administration</li>
<li><strong>/sys</strong> : infos sur les périphériques, drivers, noyau</li>
<li><strong>/temp</strong> : fichiers temporaires</li>
<li><strong>/usr</strong> : racine <em>hierarachie secondaire</em>, applications utilisateurs</li>
<li><strong>/var</strong> : <em>variable files</em>, fichiers divers dont le contenu change en permanence (logs, mails, site web)</li>
</ul>
<hr>
<h3 id="operations-sur-fichiers">Operations sur fichiers</h3>
<ul>
<li>
<p><strong>cat -n</strong> : affiche un fichier avec les numéros de lignes</p>
</li>
<li>
<p><strong>tac :</strong> affiche un fichier dans le sens inverse</p>
</li>
<li>
<p><strong>nl :</strong> affiche un fichier avec les lignes</p>
</li>
<li>
<p><strong>join :</strong> fusionner un fichier <em>ligne par ligne</em></p>
</li>
<li>
<p><strong>sort :</strong> permet de trier un fichier</p>
</li>
<li>
<p><strong>tree :</strong> permet de lister l’arborescence</p>
</li>
<li>
<p><strong>head -n</strong> : affiche les n <em>premières lignes</em></p>
</li>
<li>
<p><strong>tail -n</strong> : affiche les n <em>dernières lignes</em></p>
</li>
<li>
<p><strong>tar</strong> : créer une archive de plusieurs fichiers</p>
</li>
<li>
<p><strong>ln fichier -s nomRaccourci</strong> : créer un raccourci d’un fichier</p>
</li>
<li>
<p><strong>wc</strong> : affiche nbr <em>lignes, mots et caractères</em> d’un flux de données</p>
</li>
<li>
<p><strong>sort</strong> : trie la sortie par ordre <em>alphabétique</em> par défaut (inverse, aléatoire, fusion…)</p>
</li>
<li>
<p><strong>cut</strong> : coupe chaque ligne de la sortie (selon nombre, séparateur…)<br>
💡 Afficher les 5 premières colonne d’un fichier : <code>cut -d' ' -f1-5 nom_du_fichier</code><br>
💡 Afficher une colonne d’un fichier : <code>cut -d: -f1 nom_du_fichier</code></p>
</li>
<li>
<p><strong>grep</strong> : recherche d’une expression dans un fichier<br>
💡 On peut utiliser grep de manière plus poussé avec des <em>expressions rationnelles</em><br>
▶️<em>"^debut"</em> : toutes les lignes commençant par debut<br>
▶️ <em>“fin$”</em> : toutes les lignes se terminant par fin</p>
</li>
<li>
<p><strong>locate</strong> : localiser un fichier dans la BDD des fichiers indexés<br>
💡 Exemple : <code>locate passwd | less</code> (meilleure lecture)</p>
</li>
<li>
<p><strong>find</strong> : comme locate mais avec plus de possibilités<br>
💡 Exemple : <code>find / -name "passwd" -size +5k</code></p>
</li>
<li>
<p><strong>sed</strong> : permet de réaliser des substitutions dans un fichier<br>
💡 Remplacer toutes les occurences de gab par gaby :<code>sed 's/gab/gaby/g fichier</code></p>
</li>
</ul>
<hr>
<h3 id="redirection-des-flux">Redirection des flux</h3>
<ul>
<li><strong>&gt;</strong> : Redirige la sortie dans un fichier (<em>écraser si existe déjà</em>)</li>
<li><strong>&gt;&gt;</strong> : Redirige la sortie à la <em>fin d’un fichier</em></li>
<li><strong>2&gt; ou 2&gt;&gt;</strong> : Redirige les erreurs dans un fichier<br>
💡 Exemple : <code>cat ppaer 2&gt; erreur.txt</code> // no such file or directory</li>
<li><strong>- 2&gt;&amp;1</strong> : Redirige erreurs / sortie standard dans un meme fichier<br>
💡 Exemple : <code>commande &gt; /dev/null 2&gt;&amp;1</code></li>
<li><strong>&lt;</strong> : prend un fichier en entrée<br>
💡 Exemple : <code>tr a-z A-Z &lt; fichier</code> -&gt; converti en majuscule</li>
<li>Rediriger la sortie <strong>standard</strong> vers un fichier et la sortie <strong>d’erreur</strong> vers un autre fichier<br>
💡 Exemple : <code>find / -name 'passwd' &gt; passwd-files.txt 2&gt; erreurs.txt</code></li>
</ul>
<hr>
<h3 id="multitaches-et-autres">Multitaches et autres</h3>
<ul>
<li><strong>commande &amp;</strong> : passe la commande en arrière plan</li>
<li><strong>ps (aux)</strong> : affiche (tout) les processus en cours</li>
<li><strong>CTRL + Z</strong> : met en pause le processus courant</li>
<li><strong>htop</strong> : utilitaire interactifs de visualisation des processus</li>
<li><strong>kill -9 k</strong> : tue le processus n°k</li>
<li><strong>xargs</strong> : convertit l’entrée standard en arguments pour une commande<br>
💡 J’ai plusieurs fichiers (test1, test2) et j’ai un autre fichier (<em>fichier.txt</em>) dont le contenu est ligne par ligne : test1, test2. La commande xargs va <strong>prendre en arguments chaque ligne de fichier.txt</strong> et l’utiliser avec une autre commande.</li>
</ul>
<p>▶️ Exemple pour supprimer fichiers : <code>cat fichier.txt | xargs rm</code><br>
▶️ Exemple pour créer fichiers : <code>cat fichier.txt | xargs touch</code></p>
<hr>
<h3 id="pipelines">Pipelines</h3>
<ul>
<li>Un pipeline relie la sortie <em>standard</em> d’une commande à l’entrée d’une autre commande</li>
<li><strong>commande1 | commande1</strong> : syntaxe d’un pipeline</li>
<li><strong>commande1 |&amp; commande2</strong> : si on souhaite relier une sortie <em>d’erreur</em></li>
<li><strong>tee</strong> : lit une entrée standard d’un pipe et écrit simultanément sur un fichier<br>
💡 Exemple : <code>ll | tee resume.txt | cat</code> -&gt; Affiche contenu de <em>resume.txt</em></li>
</ul>
<hr>
<h3 id="bashrc">Bashrc</h3>
<p>Pour <strong>activer la couleur</strong> du shell bash, étape à suivre :</p>
<ol>
<li>Faire une copie du fichier bashrc : <code>cp .bashrc .bashrc_bak</code></li>
<li>Modifer et décommenter la ligne suivante : <code>force_color_prompt=yes</code></li>
<li>Recharger le fichier avec la commande : <code>source .bashrc</code></li>
</ol>

