---


---

<h1 id="disques-partionnement-et-fs">Disques, partionnement et FS</h1>
<h2 id="disques-et-partitions">Disques et partitions</h2>
<p>💡 <strong>Partition :</strong> Diviser un support <em>physique</em> en espaces <em>logiques</em></p>
<ul>
<li>possible de découper un même disque physique en plusieurs disques virtuels, <strong>indépendants</strong>, et ayant chacun son <strong>propre système de fichiers.</strong></li>
</ul>
<p>💡 Types de partionnements :</p>
<ul>
<li>
<p><strong>MBR</strong> (Master Boot Record) : équipé sur les PC avec un <em>BIOS</em> et possède plusieurs limitation<br>
– ❌ Ne gère pas disque &gt; 4To<br>
– ❌ Limité à 4 partitions (dites <em>primaires</em>) mais possible de créer une partition étendue<br>
– ❌ repose sur l’adressage CHS</p>
</li>
<li>
<p><strong>GPT</strong> (GUID Partition Table) : associé à <em>UEFI</em>, principales caractéristiques :<br>
– Chaque partition possède un <strong>id unique</strong> (Globally Unique ID)<br>
– Jusqu’à <em>128 partitions</em><br>
– Table des partitions <strong>répliquée à divers endroits</strong> du disque (récupération du système <em>+ simple</em>)<br>
– Utilise adressage LBA</p>
</li>
</ul>
<hr>
<h3 id="lister-les-disques-et-les-partitions">Lister les disques et les partitions</h3>
<p>🔴 Un périphérique est un fichier dans le dossier <strong>/dev</strong></p>
<p>💡 <strong>Disque durs</strong> : fichiers spéciaux <code>/dev/sda ou /dev/sdb...</code><br>
💡 <strong>Partitions</strong> : nom du périf + index <code>sda1, sda2, ...</code></p>
<p>❓ Le <strong>b</strong> qui précède les permissions d’un périphérique indique qu’il est en mode <em>bloc</em></p>
<p>💡 Quelques <strong>commandes</strong> :</p>
<ul>
<li><code>lsblk</code> : lister les disques / partitions</li>
<li><code>fdisk -l</code> : début et fin de chaque partition</li>
<li><code>parted</code>, <code>gdisk</code>, <code>sfdisk</code>…</li>
<li><code>blkid</code> : obtenir le UUID d’un disque / une partition</li>
<li><code>fdisk</code> : éditer la table de partition (créer, modifier, supprimer…)</li>
</ul>
<p>💡 Le <strong>swap :</strong></p>
<ul>
<li>Stocker <em>temporairement</em> une partie de la <strong>RAM</strong> dans le <strong>disque dur</strong> quand elle est <em>saturée</em></li>
<li>Pendant une veille prolongée (<em>hibernation</em>), <strong>l’intégralité</strong> de la RAM est stockée dans les DD</li>
</ul>
<hr>
<h2 id="montage--demontage-dune-partition">Montage / Demontage d’une partition</h2>
<p>💡 Monter une partition / un périphérique signifie <strong>relier son SeF à celui de la machine</strong>, en un <em>point de montage</em></p>
<ul>
<li><strong>mount :</strong> monter un SF<br>
– <code>sudo mount /dev/cdrom /media/cdrom</code></li>
<li><strong>umount :</strong> démonter un SF<br>
– <code>sudo umount /media/cdrom</code></li>
<li>❓ Si le montage ne fonctionne pas, utiliser <code>fuser</code> pour savoir quel processus utilise la partition</li>
</ul>
<p>💡 Fichier de conf <strong>/etc/fstab</strong></p>
<ul>
<li>
<p>Contient les infos nécessaires pour <em>automatiser le montage des partitions au démarrage ou branchement d’un périf</em></p>
</li>
<li>
<p>On retrouve colonnes dans le fichier :<br>
– <strong>UUID</strong> :<br>
▶️ si un disque <code>sda</code> change de nom après insertition d’un nv disque, permet de le <em>retrouver</em><br>
▶️ Après formatage, l’UID <strong>change</strong><br>
▶️ Après clonage, l’UUID <strong>reste le même</strong><br>
▶️ Générer un nouvelle UUID avec <code>udevadm trigger</code><br>
– <strong>Point de montage</strong> (chemin absolu)<br>
– <strong>SF</strong><br>
– Options de montage<br>
– Active / désactive la sauvegarde<br>
– Vérification de la partition au démarrage (0 = non, 1 = oui)</p>
</li>
<li>
<p><code>mount -a</code> : forcer la prise en compte des modifications fstab</p>
</li>
<li>
<p><code>/etc/mtab</code> : liste des montages effectués</p>
</li>
</ul>
<hr>
<h2 id="système-de-fichiers">Système de fichiers</h2>
<p>💡 Def :<br>
Décrit la manière dont les données sont <strong>organisées à l’intérieur</strong> d’une <em>partition</em>. Il fait <strong>l’interface</strong> entre <em>l’utilisateur</em> (applications) et le <em>pilote d’E/S</em> du matériel.</p>
<p>💡 Fonctionnement :<br>
Les données sont découpées en <strong>fichiers</strong>, organisés hiérarchiquement, et c’est <strong>l’OS</strong> qui se charge de retrouver les <em>données associées.</em><br>
On peut voir un SF comme <strong>l’index</strong> de la <em>partition</em> : il d<strong>onne l’adresse</strong> de chaque <em>fichier F</em></p>
<p>💡 Fonctionnalités / Caractéristiques :</p>
<ul>
<li>Gestion de <strong>l’espace libre</strong> et de la <strong>fragmentation</strong></li>
<li><strong>Journalisation</strong></li>
<li>Gestion des <strong>droits</strong></li>
<li>Maintien de <strong>l’intégrité</strong> (grâce à journalisation)</li>
</ul>
<p>❓ <code>df -T</code> : affiche <strong>SF</strong> chaque partition</p>
<hr>
<h2 id="inode">Inode</h2>
<p>💡 Def</p>
<ul>
<li>Structure de données qui contient les <strong>métadonnées</strong> associées à un fichier / dossier (permissions, propriétaire, groupe, date de dernier accès…), ainsi que des <strong>pointeurs</strong> sur les données :</li>
<li>Le système de fichiers maintient une <strong>table des inodes</strong> qui lie <em>n° d’inodes et inodes de tous les fichiers</em> présents sur le disque</li>
</ul>
<p>💡 Lien physique / hard link :</p>
<ul>
<li>Associer <strong>plusieurs noms</strong> à un <em>même inode</em></li>
<li>Créer un hard link : <code>ln fichier nvNomFichier</code></li>
<li>La création d’un hard link incrémente un <strong>compteur de nom</strong> qu’on peut voir avec <code>ln -l ou ll</code></li>
<li>Les liens physiques partagent le <strong>même contenu.</strong> Par conséquent, même si on supprime le « fichier » (en réalité, le nom) original, les <em>données</em> sont <strong>toujours accessibles à travers le lien</strong></li>
</ul>
<p><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQZDsf1Jt9prW1ysyC5fpjkHMN3W0EmHKI6UT9AKZti_AMan7My" alt="Hard link"></p>
<p>🔴 Un <em>dossier</em> (= répertoire) est un fichier contenant une <strong>table de correspondance noms ↔ n° d’inodes</strong></p>
<p>💡 Lien symbolique / hard link :</p>
<ul>
<li>Comme un raccourci sous Windows : si on <em>supprime le fichier original</em>, le lien <strong>ne permet plus d’accéder aux données</strong></li>
<li>il pointe sur un nom de fichier (il possède son propre inode, dont les données contiennent le nom du fichier pointé)</li>
</ul>
<p>⭐️ Résumé Inode</p>
<ul>
<li>Le nombre d’inodes est <strong>limité</strong> et déterminé lors de la <strong>création du SF</strong> sur la partition.</li>
<li>Lorsque les inodes sont épuisés, il est <strong>impossible de créer</strong> un <em>nouveau fichier</em> même s’il reste de l’espace sur le disque 2 .</li>
<li>On peut connaître le nombre d’inodes restants avec <code>df -i</code></li>
</ul>

