# Watcher Eyeshow — état des lieux avant la V5

> Reconstitution du 20 août 2026. Le code de la V4.4 est perdu (jamais poussé sur GitHub).
> Ce document rassemble ce qui est **prouvable**, ce qui est **sourcé**, et ce qui est **déclaré**.

## Comment lire ce document

Chaque fait porte son niveau de preuve. C'est la règle de travail du projet : on ne
présente pas comme acquis ce qu'on n'a pas vérifié.

| Marque | Sens |
|---|---|
| **MESURÉ** | Vérifié par recalcul dans l'export `EYESHOW_V4_EVIDENCE_eyeshowfirst_poste01_20260819.json` |
| **SOURCÉ** | Cité dans l'annexe de `dossier.html` (document primaire, en notre possession) |
| **DÉCLARÉ** | Inventaire de mémoire. Le fichier source n'existe plus — invérifiable en l'état |

---

## 1. Ce que la V4.4 proposait

### 1.1 Architecture de données — SOURCÉ

Extrait de l'annexe du dossier direction, ligne 16 :

> Rétention 7–45 jours, défaut 30, reçu de purge ; chiffrement AES-256-GCM, clés protégées
> Windows ; **deux plans de données étanches** ; quarantaines ; **réseau sortant coupé au manifeste**.
>
> — `contracts/v44/FROZEN_ACCEPTANCE_V4_4.md` §3 ; handoff §5 et §8

Les deux plans étanches sont la pièce maîtresse : un plan pour les données d'observation,
un plan pour la configuration/identité, sans passerelle entre les deux. C'est ce qui permet
de dire « rien de sensible n'est lu » sans que ce soit une promesse.

### 1.2 Garanties de non-collecte — SOURCÉ

Annexe ligne 17 :

> Pas d'enregistreur de frappe ; mots de passe / codes / cartes / cookies jamais lus.
>
> — `EYESHOW_V44_DISCOVERY_TO_REVENUE_ARCHITECTURE_BUILD_PLAN_2026-08-04.md` §7

**Vérifié indépendamment (MESURÉ)** : l'export du 19/08 ne contient aucun mot de passe,
aucun jeton, aucune adresse e-mail, aucun numéro de sécurité sociale, aucun IBAN, aucun
numéro de carte. Les seules chaînes ressemblant à des identifiants sont des empreintes
SHA-256 et des UUID. Les champs métier sont des **catégories** (`customer_name`, `amount`,
`phone`) et jamais des valeurs.

La garantie tient. C'est l'actif le plus précieux du projet.

### 1.3 Sortie attendue — SOURCÉ

Annexe ligne 18 :

> Feuille de route type : diagnostic à J+14, portefeuille à J+30 (10–20 opportunités,
> trois options par dossier dont « configurer l'existant »).
>
> — `contracts/v44/SPEC_SOURCE_V44_2026-08-04.md` §11

Annexe ligne 12, résultat obtenu sur le terrain :

> 55 routines candidates ; 17 opportunités classées ; corpus noté 78/100.
>
> — `v44/opportunities/output/diagnostic-j14.json` ; `portfolio-j30.json`

Le « trois options par dossier dont configurer l'existant » est une décision de conception
forte : l'outil doit pouvoir conclure « votre logiciel actuel sait déjà le faire, il suffit
de l'activer ». C'est ce qui le rend crédible plutôt que vendeur.

### 1.4 Discipline sur le bruit — SOURCÉ

Annexe lignes 13 et 14 :

> Bruit exclu des calculs : 67 880 démarrages de téléchargement / 118 fins (canal contaminé) ;
> 13 événements (~0,023 %) isolés en quarantaine.
> 20 236 signaux exploitables (chiffre canonique, contradiction 20 380 tranchée par recalcul
> le 07/08/2026).

Deux choses à retenir : le canal téléchargement était **déjà** identifié comme pollué en
juillet, et une contradiction de comptage a été tranchée par recalcul plutôt que par choix.
Cette rigueur doit être conservée.

### 1.5 Inventaire au 7 août — DÉCLARÉ

Invérifiable : les fichiers n'existent plus.

- 13 contrats/schémas JSON (1 exemplaire + 11 fabriqués + `common.defs.json`)
- `InstallationProfileV2` : la V1 stockait `store_route_secret` **en clair**. La V4.4
  l'interdit, seul `store_key_id` dérivé est conservé. **Règle non négociable.**
- Pare-feu V4.3 : interdit le segment `dom` dans les noms de champs
- Gel : 12 fichiers + empreinte d'ensemble
- 64 fixtures, 12/12 contrats couverts, banc `run-fixtures.mjs`
- Politique : 14 règles, 14 utilisées, 0 morte ; 29 codes émis, tous couverts
- Extension V4.3 : 24 fichiers, ZIP gelé, arbre identique octet pour octet
- Banc E2E sur Chromium épinglé en 147.0.7727.15
- 23/23 assertions chiffrées vérifiées

### 1.6 Les trois défauts ouverts — DÉCLARÉ

1. Le candidat V4.3 gelé ne repasse plus sa propre preuve Chrome E2E. Échec reproductible,
   non causé par la V4.4. Piste « dérive de version Chrome » écartée. **Cause racine jamais
   trouvée.** Piège connu : un `tail` renvoyant son propre code de sortie avait masqué l'échec.
2. Le banc renvoie « succès » sur **zéro fixture** — un vert qui ne prouve rien.
3. 15 codes de politique jamais exercés par aucune fixture.

---

## 2. Ce qui tourne réellement aujourd'hui

Version en production sur le poste 01 : `4.0.0.1`, build `eyeshow-v4alpha-20260724`.
**Antérieure à la V4.4.** C'est elle qui a produit l'export du 19 août.

### 2.1 Ce qu'elle sait faire — MESURÉ

- **46 origines déclarées** au manifeste : Cosium, 18 portails fournisseurs et verriers,
  16 portails mutuelles, Google (mail/docs), Alma, ZeroSix
- Contrôle d'intégrité : `events_sha256` **reproduit exactement** par recalcul
- 13 types d'événements, dont `semantic_click`, `field_interaction`, `form_submitted`,
  `foreground_span`, `idle_entered`/`idle_left`, `coverage_lost`
- Un analyseur produisant 10 familles de motifs et 200 candidats classés

### 2.2 Ce qu'elle produit vraiment — MESURÉ

Sur 18 851 événements couvrant le 5 → 19 août :

| Poste | Volume | Part |
|---|---|---|
| `heartbeat` (onglet ouvert, ping/minute) | 15 595 | **82,7 %** |
| `download_started` (canal connu pollué) | 359 | 1,9 % |
| **Activité réelle** | **2 897** | **15,4 %** |

Six jours consécutifs (12 → 17 août) à **exactement 1440 événements/jour**, tous des
heartbeats sur Cosium, week-end compris. Un onglet resté ouvert, rien d'autre.

L'activité réelle se concentre sur **deux journées** : le 18 août (2 561) et le 19 août (315).

**Bon point** : l'analyseur exclut correctement les heartbeats — le mot n'apparaît pas une
seule fois dans les 250 n-grammes ni dans les 200 candidats.

**Mauvais point** : `download_started` n'est **pas** exclu. Le n-gramme le mieux classé
(support 289) et les candidats n°2 et n°3 sont des répétitions pures de téléchargements
Cosium. 14 des 200 candidats sont contaminés. Le canal est toujours cassé : 359 démarrages
pour 27 fins, **13 pour 1** — la même pathologie qu'en juillet.

---

## 3. Les trois trous prouvés

### 3.1 Gmail est un angle mort — MESURÉ

Sur les 1 222 événements Gmail de l'export :

| Champ | Résultat |
|---|---|
| `page_kind` | **1 023 sur 1 222 classés `error`** — soit 84 % |
| `message_intent` | `unknown` sur **100 %** des 18 851 événements du corpus |
| `action_concept` | `unknown` sur 1 165 sur 1 222 |
| motifs `message_journeys` produits | **0** |
| motifs `reentries` produits | **0** |

Le champ `message_intent` et la famille `message_journeys` **existent dans le schéma** et ne
sont jamais alimentés. Le classifieur d'écrans échoue sur Gmail et retombe sur `error`.

Conséquence directe : cette mauvaise classification remonte jusque dans les résultats — les
transitions inter-domaines les mieux classées partent de `mail.google.com / page_kind: error`.

**C'est le trou le plus grave.** Le chantier n°1 du dossier — 3 h 30 par jour dans la boîte
mail, un quart de tout le temps écran — est le seul que le watcher ne sait pas instrumenter.
Il compte les allers-retours vers Gmail ; il ne sait rien de ce qui s'y joue.

### 3.2 La mesure s'arrête sans le dire — MESURÉ

`coverage.status = UNKNOWN`. Une perte de couverture ouverte depuis le **18 août 09 h 16**,
`recovered: false`, `end_at: null`. Elle ne s'est jamais refermée, et rien ne le signale.

Sur un pilote de 30 jours, un trou silencieux invalide le rapport J+14.

### 3.3 Aucun euro possible — MESURÉ, et c'est voulu

Le watcher enregistre `field_concept: "amount"` — le fait qu'un champ montant existe — mais
**jamais le montant**. Aucune valeur monétaire nulle part.

Ce n'est pas un défaut : c'est ce qui rend l'outil acceptable. Mais il faut en tirer la
conséquence d'architecture : **les euros ne viendront jamais du watcher.** Ils viendront des
exports Cosium, par un autre outil, avec d'autres règles.

Deux outils, deux rôles :

- le watcher mesure **où ça frotte** — sans rien lire
- les exports mesurent **combien ça coûte** — sous contrôle du magasin

Ne jamais les fusionner. Le jour où ils le sont, l'argument de sécurité tombe, et le dossier
avec.

---

## 4. Ce que la V5 doit faire

Cadré par les six chantiers de la synthèse direction, pas par l'envie technique.

### 4.1 Priorité 1 — Voir les mails sans les lire

Le défi central. L'intention doit se déduire **du parcours, jamais du texte** :

- `Cosium(dossier) → Gmail(rédaction) → pièce jointe → envoi` = envoi de document
- `Portail mutuelle → Gmail` = problème de remboursement
- `Gmail → Cosium(dossier) → Gmail` = réponse sur une disponibilité

Le champ `message_intent` est déjà prévu au schéma. Il suffit de l'alimenter à partir du
contexte de navigation. Aucun contenu n'est lu, la garantie tient.

Prérequis : **réparer le classifieur d'écrans sur Gmail** avant tout le reste. Tant que
84 % des écrans sont `error`, tout ce qui est bâti dessus est faux.

### 4.2 Priorité 2 — Le dossier comme unité, pas la transition

Aujourd'hui l'outil voit des paires A→B. Le chantier « caisse & conformité » exige de relier
**trois** domaines dans une même séquence de travail : encaissement, facture, départ en
télétransmission.

Il faut une notion d'**épisode de travail** corrélant plusieurs onglets sur une même
séquence — sans jamais identifier le client.

### 4.3 Priorité 3 — Mesurer l'attente du samedi

`foreground_span`, `idle_entered` et `idle_left` existent déjà. Il manque la métrique qui
en découle : **occupation des postes par créneau**. C'est le chiffre qui prouve le
chantier n°4, samedi contre samedi.

### 4.4 Priorité 4 — Ne plus jamais rendre un vert vide

Trois règles, tirées des défauts 2 et 3 de la V4.4 :

1. Un banc qui passe sur zéro fixture doit **échouer**, pas réussir
2. Tout code de politique jamais exercé par une fixture est un **échec de couverture**
3. Toute perte de couverture non refermée doit **apparaître en tête du rapport**, pas dans
   un champ que personne ne lit

### 4.5 Assainissement immédiat

- Exclure `download_started` des motifs tant que le canal reste cassé — ou réparer le canal
- Réduire la fréquence des heartbeats, ou les sortir du corpus exporté : 82,7 % du volume
  pour zéro information

---

## 5. Ce qu'il reste à récupérer

Le PC est hors d'atteinte. Reste la transcription de la session d'origine, côté serveur :

- `session_01Jwbc3Vbs7qcXy96EsFbBcP` — Eyeshow V4.4 architecture et handoff (4 → 7 août)
- `session_01P7yNmBftpQZ411iFQBNDEo` — Design architecture plan for kimi-bridge
- `session_01PhXMquUqR4wZCRYy3wLfQB` — Optimiser extension Chrome Kimi WebBridge

Impossible à relancer, à lire seulement. Le contenu de chaque fichier écrit se trouve dans
les blocs d'appels d'outils.

**À récupérer en premier, dans cet ordre :** `common.defs.json`, puis `InstallationProfileV2`
(règle `store_route_secret`), puis `FROZEN_ACCEPTANCE_V4_4.md` §3. Tout le reste en dépend.

---

## 6. Note d'environnement

Le banc E2E de la V4.4 était épinglé sur Chromium **147.0.7727.15**. L'environnement de
travail actuel dispose de **141.0.7390.37**. Avant toute conclusion sur le défaut n°1, il
faudra épingler la bonne version — sans quoi on rouvrira une piste déjà écartée.
