# RF2 Server Manager

[English](README.md) · [Italiano](README.it.md) · [Español](README.es.md) · **Français** · [Deutsch](README.de.md) · [Português](README.pt.md)

**Téléchargement :** [dernière version](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

**Soutenir le projet :** [faire un don avec PayPal](https://www.paypal.com/donate/?business=3T7ZTAXBQY3EN&no_recurring=0&item_name=Sostieni+Karma+TV%3A+progetti+e+canali+YouTube%2C+Instagram%2C+TikTok.+Support+my+projects+and+channels.+Grazie%21+Thanks%21&currency_code=EUR) – l'appli est gratuite, chaque don aide à la maintenir à jour.

---

Outil pour Windows qui configure et lance un serveur dédié de RF2.
Ce n'est pas un produit officiel et il n'est pas lié à Studio 397 ni à Motorsport Games.

Au premier démarrage, l'appli reconnaît la langue de Windows : italien, anglais, espagnol, français, allemand ou portugais. Les autres langues passent en anglais. Le bouton avec le drapeau en haut à droite la change, et l'appli retient ton choix.

## Configuration requise

- Windows 10 ou 11 en 64 bits. .NET est déjà inclus dans l'exe.
- De l'espace disque pour le serveur et les contenus.
- Microsoft Edge WebView2 Runtime, seulement pour le navigateur de l'onglet Workshop. Sans lui, tu peux coller l'ID du Workshop à la main.

Le serveur dédié et SteamCMD ne sont pas inclus : l'appli peut les télécharger depuis Valve et Steam avec la configuration guidée.

## Premier démarrage

1. Lance `RF2ServerManager.exe`. Pas besoin de l'installer.
2. Si Windows affiche « Windows a protégé votre ordinateur », choisis **Informations complémentaires** puis **Exécuter quand même**. Ce message apparaît parce que l'exe n'a pas de signature numérique.
3. Dans la configuration guidée, choisis les dossiers de SteamCMD et du serveur, ou laisse l'appli les télécharger.
4. Démarre le serveur une fois : il crée ses fichiers de configuration. Si Windows demande l'autorisation pour le pare-feu, choisis **Autoriser**.

## Mises à jour

Au démarrage, l'appli regarde sur GitHub s'il y a une nouvelle version. Si oui, l'encadré **Mettre à jour** apparaît en bas du menu de gauche. L'appli la télécharge, vérifie son empreinte SHA-256 et se rouvre toute seule ; le serveur, s'il est allumé, reste allumé. Sous le numéro de version, **Rechercher des mises à jour** refait la vérification à la main. Si le dossier de l'appli n'est pas accessible en écriture (par exemple dans Program Files), télécharge la nouvelle version depuis la [page des versions](https://github.com/KarmaTV80/rf2-server-manager/releases).

## Les contenus que tu as déjà dans le jeu

Pas besoin de les retélécharger ni de les copier à la main. L'appli trouve toute seule le dossier du jeu, que tu peux aussi choisir à l'étape 1. Préparer. À l'étape 3. Contenus, appuie sur **Ajouter depuis le jeu**, sélectionne voitures et circuits puis appuie sur **Copier sur le serveur**. Le jeu est seulement lu.

Dans **Bibliothèque**, chaque contenu affiche son état : *Prêt*, *À installer* ou *Paquet manquant*, quand les amis ne peuvent pas le télécharger. Le bouton de la ligne fait ce qu'il faut : il installe, copie le paquet depuis le jeu ou ouvre le Workshop sur la recherche de ce contenu. Les voitures et circuits de l'événement se choisissent à l'étape 4. Événement, avec **Créer un nouvel événement**.

Les contenus installés dans le jeu sans paquet `.rfcmp` (par exemple achetés sur un site) apparaissent en bas des listes : c'est leur installation qui est copiée sur le serveur, et seuls les pilotes qui les ont déjà, dans la même version, pourront rejoindre.

Les DLC officiels achetés fonctionnent sur le serveur : l'appli copie toute seule le fichier de déverrouillage que le jeu prépare (`ServerUnlock.bin`). Les mises à jour des contenus s'appliquent elles aussi toutes seules.

## Jouer avec d'autres personnes

Sur le routeur, redirige vers l'IP du PC :

| Port | Protocole | Usage |
|---|---|---|
| 54297 | TCP et UDP | Simulation |
| 64297 | TCP | Téléchargement des fichiers par les clients |
| 64299 | UDP | Steam : sans lui le serveur n'apparaît pas dans la liste du jeu |

L'UDP 64298 n'est pas nécessaire : le serveur ne l'ouvre jamais (mesuré sur le vrai serveur).

**N'ouvre jamais les ports 5397 et 5398** : ils contrôlent le serveur et le jeu. Mets toujours un mot de passe d'accès et un mot de passe admin différents l'un de l'autre. Le bouton **Vérifier le réseau et les ports** à l'étape 10. Serveur t'aide à vérifier : il part de ton PC, donc seul un test depuis une autre connexion confirme que les ports sont ouverts.

### CGNAT, double routeur et VPN

Si ton fournisseur utilise le CGNAT (une IP publique partagée entre plusieurs clients), ouvrir les ports sur le routeur ne sert à rien : les amis n'atteignent pas le serveur. À partir de la version 1.0.7, **Vérifier le réseau et les ports** te prévient quand il trouve une adresse CGNAT sur le chemin vers Internet. Tu peux aussi comparer l'IP WAN affichée sur la page du routeur avec l'IP publique affichée par l'app : si elles sont différentes, tu es derrière un CGNAT ou un second routeur. Dans ce cas, demande une IP publique à ton fournisseur, ou ouvre les ports sur les deux routeurs. Les VPN (Hamachi, ZeroTier et similaires) ne sont pas gérés par l'app.

## Serveur sur le même PC que le jeu

Un PC séparé est l'idéal, mais beaucoup n'en ont qu'un, et l'app est aussi faite pour ce cas :

- Le serveur dédié est un programme séparé : l'app l'installe avec SteamCMD dans son propre dossier. Le jeu contient aussi un serveur dédié, mais à partir de la version 1.0.11 l'app refuse le dossier du jeu, pour ne pas pouvoir le modifier.
- Le jeu et le serveur utilisent tous les deux le port 5397 pour leur interface web : avant chaque démarrage, si le serveur est encore sur le 5397, l'app le déplace sur le 5398, pour qu'ils n'utilisent pas le même port.
- Démarrer le serveur pendant que le jeu charge ralentit les deux : avec **Démarrer d'abord le jeu**, l'app attend que le jeu soit au menu, puis démarre le serveur toute seule.
- Pour les grands événements, un PC séparé reste préférable : le serveur ne prend pas de ressources au jeu.

## Paquets et DLC payants

- Les amis téléchargent voitures, circuits et événements uniquement depuis le dossier `Packages` du serveur : chaque `.rfcmp` et `.rfmod` doit s'y trouver, sinon ils reçoivent une erreur en rejoignant. La Bibliothèque signale ce qui manque (*Paquet manquant*) et peut le copier depuis le jeu, et les événements créés avec l'app y placent leur `.rfmod` tout seuls.
- Les DLC officiels payants ne s'ouvrent sur le serveur qu'avec `ServerUnlock.bin`, que le jeu crée dans son dossier `UserData` pour le contenu que tu possèdes. L'app le copie dans le dossier `UserData` du serveur avant d'installer du contenu et avant chaque démarrage. Si le serveur est sur un autre PC, copie ce fichier toi-même, et de nouveau après avoir acheté de nouveaux DLC.

## Anti-triche

À l'étape 9. Chat et ping, l'appli peut signaler les pilotes aux tours ou vitesses impossibles et les sauts d'un point à l'autre de la piste, en comparant chacun aux autres de la même classe. Elle ne déconnecte personne : elle prévient et écrit tout dans le journal des suspects (`sospetti.log`), puis c'est celui qui gère le serveur qui décide. Le serveur ne voit pas à l'intérieur du PC des pilotes, il trouve donc les effets des triches, pas les programmes.

## Où sont les données

- Réglages et journal : `%AppData%\RF2ServerManager`
- Mots de passe : seulement dans les fichiers de configuration du serveur, qui les garde en clair. Ils ne vont pas dans les profils.

## Signaler un problème

Utilise **Signaler** en haut à droite de l'app, ou **Info → Signaler un problème** (à partir de la version 1.0.6). L'app affiche le journal après avoir masqué les données qu'elle reconnaît (nom d'utilisateur Windows, noms des pilotes, Steam ID, adresses IP publiques et messages du chat). Relis-le avant de le partager, car quelque chose a pu lui échapper. L'app l'enregistre dans un fichier texte et ouvre sur GitHub le [formulaire de signalement](https://github.com/KarmaTV80/rf2-server-manager/issues/new?template=segnalazione.yml) : décris ce qui s'est passé et joins le fichier. Les signalements sont publics et demandent un compte GitHub gratuit. Le bouton **Ouvrir le dossier des journaux** est à l'étape 1. Préparer.

## Limites connues

- La création des mods et l'installation des paquets pilotent MAS2 et ModMgr en arrière-plan, avec leurs fenêtres cachées : l'avancement se lit dans le journal de l'appli. Avec « Démarrer la session aussitôt », la fenêtre du serveur démarre aussi réduite : elle se rouvre depuis la barre des tâches de Windows. Une mise à jour de ces outils peut demander d'adapter l'appli.
- Les contenus payants et les paquets recopiés du Workshop peuvent ne pas s'installer : l'appli affiche l'erreur et nettoie les fichiers.
- Essais 2 n'a pas d'horaire ni de durée propres dans la configuration du serveur.

## Conditions d'utilisation

Gratuit, y compris pour les championnats et les ligues. Il est interdit de le modifier, de le décompiler, de le revendre ou de le distribuer depuis d'autres sites : partage seulement le lien officiel. Texte complet dans `LICENSE.txt` et dans la fenêtre **À propos** de l'appli.

Composants tiers : FlaUI et Newtonsoft.Json (licence MIT), Microsoft WebView2 SDK (licence Microsoft), .NET (licence MIT), polices Saira Extra Condensed et Barlow (SIL Open Font License, textes dans `Licenze\`).
