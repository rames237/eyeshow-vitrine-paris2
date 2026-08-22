# EYESHOW — Passation de session

> Rédigé le 20 août 2026. À lire en entier avant toute action.
> Ce document remplace la mémoire de la session précédente.

---

# PARTIE 1 — PROMPT DE CONFIGURATION

> Copie tout ce bloc dans la nouvelle session, en attachant le dépôt
> `rames237/eyeshow-vitrine-paris2` comme source.

```
Je suis James, opticien chez Eyeshow Paris 2 (rue Montmartre).
Lis le fichier PASSATION.md à la racine du dépôt AVANT toute action.
Il contient tout le contexte.

RÈGLES DE RÉPONSE — les plus importantes :

1. Réponds TOUJOURS en français, très simplement.
   Phrases courtes. Pas de jargon technique. Pas de longs pavés.
   Si tu dois utiliser un mot technique, explique-le en trois mots.

2. Va droit au but. Ce que j'ai à faire d'abord, en haut.

3. Ne me dis jamais qu'une chose marche sans l'avoir vérifiée.
   Si tu n'as pas pu vérifier (réseau bloqué, fichier absent),
   dis-le franchement. Je préfère « je n'ai pas pu » à un faux oui.

4. Un test qui passe sur zéro cas n'est pas un test qui passe.

5. Développe sur la branche claude/eyeshow-watcher-dossier-yvtw9y,
   commit et push à chaque avancée.

6. Tout ce qu'on produit part sur GitHub immédiatement.
   Plus jamais de fichier qui n'existe que sur un PC : c'est comme ça
   que j'ai perdu tout le travail de la V4.4.

7. Je fais beaucoup de fautes de frappe et j'écris vite.
   Comprends l'intention, ne me corrige pas.

8. À la fin de chaque session de travail, mets à jour PASSATION.md
   et pousse-le. C'est ma sauvegarde.

NE TRAVAILLE QUE SUR EYESHOW.
Pas de QWIFON, pas de Charlotte, pas de WhatsApp-Bot.
```

---

# PARTIE 2 — LE CONTEXTE

## Qui est qui

| Personne | Rôle | À savoir |
|---|---|---|
| **James** | Opticien à Paris 2 | C'est moi. Je porte ce projet sur mon temps personnel. |
| **Léa** | Dirigeante du magasin | On se tutoie. C'est son accord qui suffit pour lancer le pilote. |
| **David** | Franchiseur | Vouvoiement. A répondu très positivement le 20/08. |
| **Manel** | Équipe | Volontaire n°1 pour filmer les contenus vidéo. |
| **Nataniel** | Équipe | Volontaire aussi. |

## Les logiciels du magasin

- **Cosium** — les dossiers clients. Le cœur, 53 % du temps écran.
- **Gmail** — 25 % du temps écran. Le 2ᵉ poste, et le plus gros chantier.
- **Alma** — paiement fractionné.
- **ZeroSix** — relances clients. Envoie déjà des messages tous les jours.
- **Un Google Doc** — registre parallèle tenu à la main (restes à charge, attente ordo).
- **7 portails mutuelles** — viamedis, almerys, mercernet, tp-isante, santeclair, solpay, ameli.
- **18 portails fournisseurs** — Kering, Luxottica, Shamir, Marcolin, Thelios, Ophtalmic…

---

# PARTIE 3 — CE QUI EST FAIT

## Le dépôt

`github.com/rames237/eyeshow-vitrine-paris2` — **PUBLIC**, attention.
Branche de travail : `claude/eyeshow-watcher-dossier-yvtw9y`.

| Fichier | Rôle |
|---|---|
| `synthese.html` | **La page d'entrée.** C'est ce qu'on envoie. Lecture 2 min. |
| `dossier.html` | Le dossier complet, 18 pages. **NE PAS MODIFIER.** |
| `index.html` | Maquette du site du magasin |
| `instagram.html` | Simulation du compte Instagram |
| `watcher/00_ETAT_DES_LIEUX_V44.md` | Tout ce qu'on sait du watcher |
| `assets/` | 32 fichiers : photos, polices, aperçus |

**Règle absolue sur `dossier.html` :** il est gelé. Son empreinte doit
toujours valoir `6391083c6c3d6ea00d678f08734279cbb549bc229fbd1e356c5f5e5a10e0996f`.
Vérifier avec `sha256sum dossier.html` après toute manipulation.

## Les pages en ligne

- Synthèse : `https://rames237.github.io/eyeshow-vitrine-paris2/synthese.html`
- Dossier : `.../dossier.html`
- Site : `.../index.html`
- Instagram : `.../instagram.html`

Les quatre pages sont reliées par une barre fixe en bas.
GitHub Pages est activé et publie automatiquement depuis `main`.

**Limite connue :** depuis l'environnement de travail Claude, les adresses
`github.io` sont bloquées par le proxy. Impossible de vérifier une page en
ligne. Toujours demander à James de cliquer.

## La synthèse — ce qu'elle contient

Six chantiers, chacun en trois colonnes (aujourd'hui / ce qui coince /
ce qu'on met en place) plus un bandeau « ce que ça change pour vous ».

1. **Caisse & conformité** — MESURÉ
2. **Vitrine du magasin** — DÉCLARÉ (avec les deux maquettes cliquables)
3. **Relation client** — MESURÉ
4. **Le samedi** — DÉCLARÉ
5. **Carnet noir & mutuelles** — DÉCLARÉ
6. **Les mails** — MESURÉ (ajouté le 20/08, absent du dossier)

Puis un **socle commun** : tous les chantiers tiennent dans un seul outil
relié à Cosium, dont le **carnet noir numérique est le cœur**, avec le
chiffre du jour, les notes de vente, les fiches de paie et le planning.

Enfin la demande : 30 jours, 0 €, point à J+14, arbitrage à J+30.

## Les chiffres, et d'où ils viennent

Tous mesurés du 28 juillet au 1ᵉʳ août 2026, sur 2 postes, 4 jours.

| Chiffre | Sens |
|---|---|
| 296 | allers-retours Cosium ↔ Alma |
| 1 000 | passages registre Google Doc ↔ Cosium (1/3 entre 17 h et 19 h) |
| 1 299 | allers-retours Cosium ↔ ZeroSix (dont 66 relances envoyées) |
| 1 546 | passages sur les portails mutuelles |
| 103 453 | gestes analysés au total |
| **3 h 30/jour** | temps passé dans Gmail, à deux postes (25 % du temps écran) |

**Ne jamais écrire « 3 h sur 7 »** — ce serait 43 %, le mesuré est 25 %.
La formulation défendable est « 3 h 30 par jour à deux postes ».

Toutes les sources sont dans l'annexe de `dossier.html`.

## Les envois

Message envoyé à **Léa** (tutoiement, ton amical) et à **David**
(vouvoiement, en précisant que Léa avait demandé le dossier).

**Réponse de David le 20/08** : très positive. « Travail exceptionnel »,
« à mettre en pratique dès que possible ». Il rentre de congés fin de
semaine prochaine, rendez-vous la semaine suivante.

Il signale que **les succursales ne fonctionnent pas comme Paris 2** sur
le carnet noir et sur les interactions Alma, et que plusieurs procédures
lui restent incomprises. À clarifier au rendez-vous — et c'est une piste :
une partie des réponses existe peut-être déjà dans le réseau.

**Action prévue :** préparer une note d'une page pour David expliquant
simplement le carnet noir et le flux Alma, avant le rendez-vous.

---

# PARTIE 4 — LE WATCHER

## Ce que c'est

Une extension Chrome installée sur les postes du magasin. Elle mesure les
frictions entre les logiciels. Elle ne lit **aucun contenu**.

## L'état exact

| Version | Statut |
|---|---|
| **V4 alpha** `4.0.0.1`, build `eyeshow-v4alpha-20260724` | **Tourne sur le poste 01.** C'est elle qui produit les exports. |
| **V4.4** | **PERDUE.** Jamais poussée sur GitHub. Le PC est hors d'atteinte. |
| **V4.3** (extension) | Perdue aussi. |

## Ce qui a été vérifié sur l'export du 19 août

Fichier reçu : `EYESHOW_V4_EVIDENCE_eyeshowfirst_poste01_20260819.json`, 20 Mo,
18 851 événements. **Empreinte `events_sha256` reproduite exactement** — le
fichier est authentique.

**Sécurité : la garantie tient.** Zéro mot de passe, zéro e-mail, zéro nom
de client, zéro numéro de sécu, zéro carte bancaire. Les champs métier sont
des catégories (`customer_name`, `amount`), jamais des valeurs.

**Mais 82,7 % du volume ne sert à rien** : 15 595 heartbeats (un ping par
minute d'un onglet Cosium resté ouvert). Six jours de suite à exactement
1440/jour, week-end compris. L'activité réelle : **2 897 événements**,
concentrés sur deux journées.

## Les trois trous prouvés

**1. Gmail est un angle mort — le plus grave.**
Sur 1 222 événements Gmail : 1 023 écrans (84 %) classés `error` par le
classifieur. `message_intent` à `unknown` sur **100 %** du corpus entier.
Zéro motif `message_journeys` produit alors que la famille existe.
→ Le chantier n°1 du dossier est le seul que l'outil ne sait pas mesurer.

**2. La mesure s'arrête sans le dire.**
`coverage.status = UNKNOWN`. Une perte ouverte depuis le 18 août 09 h 16,
jamais refermée, jamais signalée.

**3. Le canal téléchargement est toujours cassé.**
359 démarrages pour 27 fins. Même défaut qu'en juillet. 14 des 200
candidats sont pollués, dont les mieux classés.

## Décision d'architecture — à ne jamais transgresser

Le watcher n'enregistre **jamais** de montant. Il note qu'un champ montant
existe, pas sa valeur. C'est ce qui le rend acceptable.

Donc **deux outils séparés, pour toujours** :

- le **watcher** mesure *où ça frotte* — sans rien lire
- les **exports Cosium** mesurent *combien ça coûte* — sous contrôle du magasin

Le jour où on les fusionne, l'argument de sécurité tombe, et le dossier avec.

## Ce que la V5 doit faire, dans l'ordre

1. **Réparer le classifieur d'écrans sur Gmail.** Tant que 84 % sont
   `error`, tout ce qui est bâti dessus est faux.
2. **Remplir `message_intent` à partir du parcours, jamais du texte.**
   Exemple : `Cosium(dossier) → Gmail(rédaction) → pièce jointe → envoi`
   = envoi de document. Aucun contenu lu, la garantie tient.
3. **Créer la notion d'épisode de travail** reliant trois domaines
   (encaissement, facture, télétransmission) — aujourd'hui l'outil ne voit
   que des paires.
4. **Mesurer l'occupation des postes par créneau** — c'est le chiffre qui
   prouve le chantier « samedi ».
5. **Assainir** : exclure `download_started` tant que le canal est cassé,
   réduire les heartbeats.

Détail complet dans `watcher/00_ETAT_DES_LIEUX_V44.md`.

## Le blocage en cours

James a essayé trois fois d'envoyer le code de l'extension. Les trois fois,
c'est une **page d'erreur Gmail de 344 octets** qui est arrivée :

> « Pour des raisons de sécurité, Gmail ne vous autorise pas à utiliser ce
> type de fichier, car cela enfreint la politique de Google en matière de
> fichiers exécutables ou d'archives. »

Gmail refuse de servir l'archive. Renommer en `.txt` ne change rien : le
blocage est à la source.

**Solutions, dans l'ordre :**

1. Coller le contenu de `manifest.json` en texte dans la conversation
2. Dans Gmail, cliquer « Ajouter à Drive » sur la pièce jointe, puis
   télécharger depuis Drive
3. Sur le poste 01 : `chrome://extensions` → Mode développeur → lire le
   chemin « Chargée depuis : » → téléverser ce dossier dans un dépôt
   **privé** `eyeshow-watcher` via le navigateur

**Avertissement :** cette version date du 24 juillet, donc **avant** le
correctif V4.4 sur `store_route_secret`. Un secret peut y être en clair.
Ne jamais la mettre dans un dépôt public sans avoir vérifié.

---

# PARTIE 5 — CE QUI RESTE À FAIRE

## Tout de suite

1. Récupérer le code de l'extension (voir le blocage ci-dessus)
2. Réparer le classifieur Gmail
3. Créer le dépôt **privé** `eyeshow-watcher`

## Avant le rendez-vous avec David

4. La note d'une page : le carnet noir et le flux Alma, expliqués simplement
5. Prévenir Léa de la remarque de David sur les succursales

## Si Léa dit oui

6. La note à l'équipe (le dossier promet « équipe informée par écrit »,
   elle n'existe pas encore)
7. Les trois lignes « pour démarrer, il me faut… » : combien de postes,
   qui installe, quel navigateur, qui est le contact
8. Le watcher prêt — c'est la vraie échéance

## Idées gardées de côté

- **Réception des livraisons automatisée** : lire le bon de livraison →
  créer les références dans Cosium → trier dans l'ordre des plateaux →
  imprimer les étiquettes dans cet ordre. Deux questions bloquantes : le
  bon de livraison arrive-t-il en PDF ? Cosium sait-il importer un fichier ?
- **Annulation des devis mutuelles** : bon module, mais Paris 2 fait trop
  peu de devis. À garder pour d'autres magasins.
- **Veille fournisseurs** (nouveautés → suggestion de commande) : viendra
  après, il faut un stock propre d'abord.
- **Nettoyage et sortie des données** : les PC rament. Le vrai enjeu n'est
  pas le ménage, c'est que le magasin possède une copie propre de ses
  données, hors de Cosium.

## Abandonné, et pourquoi

- **Paires jamais récupérées** : impossible à mesurer sans ajouter un geste
  au comptoir. On ne crée pas une friction pour en mesurer une autre.
- **Les avoirs comme trésorerie** : faux. Un avoir non réclamé expire au
  profit du magasin. C'est un levier de retour client, pas de l'argent à
  récupérer.
- **Les télétransmissions comme argent perdu** : faux. Le magasin est payé
  dans tous les cas. C'est le client qui n'est pas remboursé — donc un
  risque de réputation, pas une perte financière.

---

# PARTIE 6 — SAUVEGARDE

Le PC précédent est tombé et tout le travail V4.4 a disparu avec lui.
Cela ne doit pas se reproduire.

## La règle

Rien ne vit uniquement sur un PC. Tout va sur GitHub le jour même.

## La routine, à faire à chaque fin de session

1. Mettre à jour ce fichier `PASSATION.md`
2. Le pousser sur GitHub
3. Le télécharger et **se l'envoyer par mail** — un `.md` passe sans
   problème, contrairement aux archives
4. Le déposer dans Drive

**Limite à connaître :** Claude ne peut ni écrire dans Drive ni envoyer de
mail depuis cet environnement. Les étapes 3 et 4 sont manuelles. Claude
fournit le fichier, James le range.

## Les trois copies à avoir en permanence

| Où | Quoi |
|---|---|
| GitHub | le dépôt complet — la source de vérité |
| Drive | `PASSATION.md` et les exports du watcher |
| Boîte mail | `PASSATION.md` envoyé à soi-même après chaque session |
