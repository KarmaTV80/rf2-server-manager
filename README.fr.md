# RF2 Server Manager

[English](README.md) · [Italiano](README.it.md) · [Español](README.es.md) · **Français** · [Deutsch](README.de.md) · [Português](README.pt.md)

**Téléchargement :** [dernière version](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

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
| 64298 et 64299 | UDP | Steam : sans eux le serveur n'apparaît pas dans la liste du jeu |

**N'ouvre jamais les ports 5397 et 5398** : ils contrôlent le serveur et le jeu. Mets toujours un mot de passe d'accès et un mot de passe admin différents l'un de l'autre. Le bouton **Vérifier le réseau et les ports** à l'étape 10. Serveur t'aide à vérifier.

## Anti-triche

À l'étape 9. Chat et ping, l'appli peut signaler les pilotes aux tours ou vitesses impossibles et les sauts d'un point à l'autre de la piste, en comparant chacun aux autres de la même classe. Elle ne déconnecte personne : elle prévient et écrit tout dans le journal des suspects (`sospetti.log`), puis c'est celui qui gère le serveur qui décide. Le serveur ne voit pas à l'intérieur du PC des pilotes, il trouve donc les effets des triches, pas les programmes.

## Où sont les données

- Réglages et journal : `%AppData%\RF2ServerManager`
- Mots de passe : seulement dans les fichiers de configuration du serveur, qui les garde en clair. Ils ne vont pas dans les profils.

En cas de problème, envoie le journal du dossier `logs`. Le bouton **Ouvrir le dossier des journaux** est à l'étape 1. Préparer.

## Limites connues

- La création des mods et l'installation des paquets pilotent MAS2 et ModMgr en arrière-plan, avec leurs fenêtres cachées : l'avancement se lit dans le journal de l'appli. Avec « Démarrer la session aussitôt », la fenêtre du serveur démarre aussi réduite : elle se rouvre depuis la barre des tâches de Windows. Une mise à jour de ces outils peut demander d'adapter l'appli.
- Les contenus payants et les paquets recopiés du Workshop peuvent ne pas s'installer : l'appli affiche l'erreur et nettoie les fichiers.
- Essais 2 n'a pas d'horaire ni de durée propres dans la configuration du serveur.

## Conditions d'utilisation

Gratuit, y compris pour les championnats et les ligues. Il est interdit de le modifier, de le décompiler, de le revendre ou de le distribuer depuis d'autres sites : partage seulement le lien officiel. Texte complet dans `LICENSE.txt` et dans la fenêtre **À propos** de l'appli.

Composants tiers : FlaUI et Newtonsoft.Json (licence MIT), Microsoft WebView2 SDK (licence Microsoft), .NET (licence MIT), polices Saira Extra Condensed et Barlow (SIL Open Font License, textes dans `Licenze\`).
