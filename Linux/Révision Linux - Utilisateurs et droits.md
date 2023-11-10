---


---

<h1 id="revisions-linux">Revisions Linux</h1>
<h2 id="commandes-bash">Commandes Bash</h2>
<h3 id="ajout--suppression-dun-utilisateur">Ajout / suppression d’un utilisateur</h3>
<p>🙋 Ajouter avec <strong>useradd :</strong></p>
<ul>
<li>Préciser <mark>-m</mark> pour créer un <em>dossier perso</em> au nouveau user</li>
<li>Préciser <mark>-s</mark> pour choisir un <em>shell</em> comme <em>/bin/bash</em></li>
<li>Préciser <mark>-g</mark> pour spécifier un <em>groupe primaire</em></li>
<li>Utiliser <mark>passwd nvUser</mark> pour lui attribuer un mot de passe<br>
▶️ <code>sudo useradd -m -s /bin/bash -g sudo Gaby</code><br>
▶️ <code>sudo passwd Gaby</code></li>
</ul>
<p>🙋 Ajouter avec <strong>adduser :</strong></p>
<ul>
<li>Créer <em>automatiquement</em> un dossier perso</li>
<li>Permet de <em>détailler</em> les infos sur un user (nom, prénom, mdp…)<br>
▶️ <code>sudo adduser Gaby</code></li>
</ul>
<p>💡 Si aucun groupe n’est spécifié, un <strong>nouveau groupe</strong> à son nom est crée</p>
<p>❎ Supprimer avec <strong>userdel</strong> ou <strong>deluser</strong></p>
<ul>
<li>Par défaut, supprimer un user NE SUPPRIME PAS son dossier personnel,</li>
<li>Pour une suppression propre : <code>sudo userdel -r -f Gaby</code><br>
<mark>-r (remove)</mark> : supprime le dossier perso<br>
<mark>-f (force)</mark> : supprime les fichiers dans le dossier perso (même fichiers root)</li>
</ul>
<hr>
<h3 id="commandes-utilisateurs">Commandes utilisateurs</h3>
<ul>
<li>
<p>Afficher <strong>users</strong> : <code>cat /etc/passwd</code> ou <code>cut -d -f1 /etc/passwd</code></p>
</li>
<li>
<p>Afficher <strong>groups</strong> : <code>cat /etc/groups</code> ou <code>cut -d: -f1 /etc/group</code></p>
</li>
<li>
<p>Afficher <strong>groupes d’appartenance</strong> : <code>groups [user]</code></p>
</li>
<li>
<p>Afficher <strong>uid et guid</strong> : <code>id [user]</code><br>
💡 Les identifiants &lt; 1000 sont réservés  au <mark>système</mark></p>
</li>
</ul>
<hr>
<h3 id="modifier-propriétés-utilisateurs">Modifier propriétés utilisateurs</h3>
<ul>
<li>
<p>Modifier <strong>login</strong> : <code>sudo usermod -l [ancienUsername] [nvUsername]</code></p>
</li>
<li>
<p>Modifier <strong>dossier perso</strong> : <code>sudo usermod -m -d [nvHomeDire] [userName]</code></p>
</li>
<li>
<p>Modifier <strong>groupe primaire</strong> : <code>sudo usermod [userName] -g [nvGroupePrim]</code></p>
</li>
<li>
<p>Modifier nom d’un <strong>groupe</strong> : <code>sudo groupmod -n [nvNomGroupe] [ancienNomGrp]</code></p>
</li>
<li>
<p>Modifier <strong>id groupe</strong> : <code>sudo groupmod -g [nvID] [nomGroupe]</code></p>
</li>
<li>
<p>Ajouter user <strong>à un groupe</strong> : <code>usermod -a -G [nomGrp] [nomUser]</code></p>
</li>
<li>
<p>Modifier groupe <strong>primaire</strong> : <code>usermod -g [nomGrp] [nomUser]</code></p>
</li>
</ul>
<hr>
<h3 id="fichiers-etcpasswd-et-etcshadow">Fichiers /etc/passwd et /etc/shadow</h3>
<p>📍 /etc/<strong>passwd</strong></p>
<ul>
<li>Ce fichier contient <mark>7</mark> champs qui sont :<br>
nomUser | mot de passe (<strong>x</strong>) | UserID | GroupID | nom réel | dossier perso | shell</li>
<li>Le mot de passe <mark>x</mark> signifie qu’il est chiffré dans le fichier <code>/etc/shadow</code></li>
<li>Il ne faut <strong>JAMAIS</strong> éditer ce fichier</li>
</ul>
<p>📍 /etc/<strong>shadow</strong></p>
<ul>
<li>Fichier contenant les <strong>mot de passe chiffrés</strong></li>
<li>Les colonnes sont séparés par <mark>:</mark><br>
login | chiffre mdp | date dernier change mdp…</li>
<li>Les <strong>3 premiers caractères</strong> du chiffre mdp indique l’algo de <strong>hachage</strong> du mdp<br>
💡 Exemple : <code>$6$</code> pour du <mark>SHA-512</mark></li>
<li>Un <mark>!</mark> signifie qu’aucun mot de passe n’a pas été défini</li>
</ul>
<hr>
<h3 id="gestion-des-comptes-et-des-mots-de-passe">Gestion des comptes et des mots de passe</h3>
<ul>
<li><code>sudo chage -l [user]</code> : lister les infos de <strong>validité</strong> d’un mdp<br>
▶️ <em>Dernier changem’, fin validité, mdp desactivé…</em></li>
<li><code>passwd -e [user]</code> : forcer un user à <strong>changer son mdp</strong></li>
<li><code>chage --expiredate 0 [user]</code> : date d’expiration <strong>passée</strong></li>
</ul>
<hr>
<h3 id="super-utilisateur-root">Super-utilisateur root</h3>
<p>📍Particularités :</p>
<ul>
<li>Peut accéder à <mark>tout les fichiers/dossiers</mark></li>
<li>Prendre l’identité de nimp user <mark>sans mdp</mark></li>
<li>Répertoire perso dans <mark>/root</mark> et non /home</li>
<li>Son <mark>uid = 0</mark></li>
</ul>
<p>📍 <strong>su</strong> et <strong>sudo</strong></p>
<ul>
<li>
<p><strong>su</strong> (Switch User) : on change d’utilisateur<br>
💡 Si aucun user spécifié, par défaut c’est <mark>root</mark><br>
💡 Pour changer aussi <strong>d’environnement</strong>, on ajoute <mark>-l</mark><br>
▶️  <code>su -l Gaby</code></p>
</li>
<li>
<p><strong>sudo (-u) commande</strong> : execute une commande en tant que <em>user</em><br>
💡 Les commandes sudo sont logués dans <mark>/var/log/auth.log</mark><br>
💡 sudo demande le mdp du user <strong>courant</strong> et non cible (su)<br>
▶️  <code>sudo apt install nano</code><br>
💡 Possible de bypass le mdp de root avec <code>sudo su</code></p>
</li>
</ul>
<p>📍 Fichier <strong>/etc/sudoers</strong></p>
<ul>
<li>Indique qui a les <mark>droits sudo</mark><br>
💡 Pour éditer le fichier, on utilise <code>sudo visudo /etc/sudoers</code></li>
</ul>
<p>📍 Commande <strong>newgrp</strong></p>
<ul>
<li>Permet de changer de groupe <mark>temporairement</mark> (pendant 1 session)<br>
▶️  <code>newgroup groupe2</code></li>
</ul>
<hr>
<h2 id="gestion-des-droits">Gestion des droits</h2>
<h3 id="droits">Droits</h3>
<p>📍 Fichiers</p>
<ul>
<li><strong>Lecture</strong> (<mark>r</mark>) : Afficher le contenu (ex : <code>cat</code>)</li>
<li><strong>Ecriture</strong> (<mark>w</mark>) : Modifier le contenu (ex : <code>nano</code>)</li>
<li><strong>Exécution</strong> (<mark>x</mark>) : Exécuter un binaire / script (ex : <code>ls</code> ou <code>./script</code>)</li>
</ul>
<p>📍 Dossiers</p>
<ul>
<li><strong>Lecture</strong> (<mark>r</mark>) : Afficher le contenu</li>
<li><strong>Ecriture</strong> (<mark>w</mark>) : Créer / Supprimer fichiers (ex : <code>touch / rm</code>)</li>
<li><strong>Exécution</strong> (<mark>x</mark>) : Rentrer dans le dossier</li>
</ul>
<p><img src="https://hrouhanidotorg.files.wordpress.com/2017/11/perms1.png" alt="Droits après un ls -l"></p>
<p>📍 Principaux types de fichiers</p>
<ul>
<li><mark>-</mark> : fichiers <strong>normaux</strong></li>
<li><mark>d</mark> : <strong>dossiers</strong></li>
<li><mark>l</mark> : lien <strong>symbolique</strong></li>
<li><mark>c</mark> : périphérique mode <strong>caractère</strong> (ex : clavier)</li>
<li><mark>b</mark> : périphérique mode <strong>block</strong> (ex : disque durs)</li>
</ul>
<hr>
<h3 id="modifications-des-droits">Modifications des droits</h3>
<p>📍 <strong>chmod</strong> permet de modifier les droits sur les fichiers / dossiers. Il y a <mark>2</mark> manières de l’utiliser :</p>
<ul>
<li>
<p>Avec des <mark>lettres / signes</mark><br>
💡 <strong>chmod [u g o a] [+ - =] [r w x] nom du fichier</strong><br>
▶️ <code>chmod u+x</code> = droit exécution propriétaire<br>
▶️ <code>chmod go-rwx</code> = enlève tous les droits aux autres utilisateurs / groupe.<br>
▶️ <code>chmod a+r</code> = droit de lecture à tt le monde</p>
</li>
<li>
<p>Avec une <mark>valeur numérique</mark><br>
💡 Par défaut, les droits des FICHIERS sont <strong>666</strong><br>
💡 Par défaut, les droits des DOSSIERS sont <strong>777</strong><br>
<img src="https://1.bp.blogspot.com/-pOBNG7Jk-Ts/XMrCYdeb-gI/AAAAAAAABTs/IOie9xu8_7o2t9yPupiARMhYvrv3qAURgCLcBGAs/s640/130.png" alt="Droits numérique"><br>
▶️ <code>chmod 541 fichier</code> (=) <mark>rw- r-- --x</mark><br>
▶️ <code>chmod 644 fichier</code> (=) <mark>rw- r-- r–</mark> (Après <strong>umask 022</strong> par défaut)<br>
▶️ <code>chmod 755 dossier</code> (=) <mark>rwx r-- r–</mark> (Après <strong>umask 022</strong> par défaut)</p>
</li>
</ul>
<p>📍 Fichier <strong>/etc/adduser.conf</strong></p>
<ul>
<li>Contient valeurs par défaut des commandes <em>adduser, addgroups, deluser, delgroup</em></li>
<li>La variable <mark>DIR_MODE</mark> contient les <strong>permissions par défaut</strong> lors de la <strong>création d’un dossier</strong></li>
</ul>
<p>📍 Droits par défaut <strong>umask</strong></p>
<ul>
<li>Définie les droits qui seront <strong>retiré par défaut</strong> d’un fichier / dossier</li>
<li>C’est une valeur <strong>octale</strong><br>
▶️ <code>umask 007</code> -&gt; Défini le umask<br>
▶️ <code>umask -S</code> -&gt; Affiche le umask sous forme <mark>littérale</mark></li>
</ul>
<p>📍 <strong>Sticky bit</strong></p>
<ul>
<li>drwxrwxrw<mark>t</mark></li>
<li>Indique que dans ce dossier, seuls le proprietaire d’un <strong>fichier</strong>, le proprietaire <strong>du dossier</strong> ou <strong>root</strong> ont le droit de <em>renommer ou supprimer</em> ce fichier</li>
<li><code>chmod +t dossier</code> : Active le sticky bit</li>
</ul>
<hr>
<h3 id="changement-de-propriétaire">Changement de propriétaire</h3>
<ul>
<li>
<p><strong>chown</strong> : modifier le <mark>propriétaire</mark> d’un fichier / dossier<br>
▶️ <code>chown [-R] utilisateur cible</code> : -R pour dossier</p>
</li>
<li>
<p><strong>chgrp</strong> : modifier le <mark>groupe</mark> d’un fichier / dossier<br>
▶️ <code>chogrp [-R] groupe cible</code> : -R pour dossier</p>
</li>
<li>
<p>💡 Seul <mark>root</mark> peut utiliser  <strong>chown</strong>, donc avec <em>sudo</em></p>
</li>
</ul>
<hr>
<h3 id="droits-dendossement">Droits d’endossement</h3>
<ul>
<li>
<p>Permettre aux utilisateurs d’exécuter ce programme comme s’ils etaient <strong>root</strong><br>
▶️ Par exemple, la commande <code>passwd</code>, les droits sont -<mark>rw<strong>s</strong> r-x r-x</mark></p>
</li>
<li>
<p>Le <mark>s</mark> indique que ce programme est exécuté avec les <strong>droits de son propriétaire</strong>, ici <em>root</em></p>
</li>
<li>
<p>Pour activer le droits d’endossement :<br>
💡 <code>chmod u+s fichier</code> # pour activer le setuid (<mark>user</mark>)<br>
💡 <code>chmod g+s fichier</code> # pour activer le setgid (<mark>group</mark>)</p>
</li>
</ul>

