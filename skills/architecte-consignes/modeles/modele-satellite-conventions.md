<!--
MODÈLE : fichier satellite « conventions » (kit Architecte consignes, v1.1.2).
Pour Claude, au remplissage :
- Remplir avec les réponses validées du bloc D (classement, nommage, formats, ton et mentions des documents pour tiers), la langue retenue au bloc B et les motifs de nommage relevés à l'étape 1. Remplacer chaque [crochet] ; une valeur inconnue devient « à confirmer ». Supprimer toute section restée vide.
- Emplacement par défaut : `consignes/conventions.md`, dans le dossier de consignes validé à l'étape 3, lu à la demande. Pointeur dans le maître : « Avant de créer, nommer ou classer un fichier, ou de rédiger un document pour un tiers, lire `consignes/conventions.md` ». Le maître garde seulement la règle de classement la plus courante.
- Une convention valable pour un seul dossier ou un seul type de fichier va plutôt dans une règle par chemin (`modele-regle-chemin.md`), chargée seulement quand Claude touche ces fichiers.
- Exemples tirés du dossier ou des réponses, jamais inventés. Ne pas proposer un motif de nommage que l'utilisateur n'a pas choisi.
- La règle de nommage (ordre des éléments, format de date, séparateur, casse) et la date qui fait foi ont pour seul lieu « Classement et nommage » du maître (D2, D2b) ; l'accord avant de renommer (F1) vit dans « Demander mon accord avant de » du maître. Ici, seulement les caractères à éviter, les versions (D3), d'autres exemples et les exceptions. Les noms des fichiers et dossiers de consignes ne contiennent pas d'espace (mecanismes.md §3).
- Ton et mentions des documents pour tiers : quand ce fichier existe, il en est le seul lieu, sauf en refonte une règle sans `paths` existante qui les porte déjà (routage.md section 2 ; supprimer alors « Langue et ton » ici). La section « Documents destinés à des tiers » du maître se réduit à un renvoi, et les skills y renvoient aussi, sans recopier.
- Avec plusieurs agents, les renvois au CLAUDE.md maître visent `AGENTS.md`, sous les mêmes titres de section.
- La ligne sur l'archivage d'un CLAUDE.md vaut pour Claude Code (mecanismes.md §1) ; la supprimer pour un autre outil.
- « Mon accord » désigne l'utilisateur de la session ; dans un espace partagé, nommer le rôle qui donne l'accord.
- Retirer ce commentaire et les autres commentaires de consigne ; garder seulement le dernier.
-->

# Conventions : [nom de l'espace de travail]

Rôle et moment de lecture : lu à la demande, avant de créer, nommer, classer ou convertir un fichier, et avant de rédiger un document destiné à un tiers.

## Classement

| Type de document | Emplacement | Remarque |
|---|---|---|
| [Document reçu, à traiter] | `[zone d'entrée]` | [quand il en sort] |
| [Document produit] | `[dossier]` | [précision] |
| [Document terminé ou inactif] | `[archives]` | Non lu par défaut. |

- Place incertaine : déposer le fichier dans `[zone d'entrée]` et le signaler, plutôt que de créer un dossier.
- Avant d'archiver un dossier, et avec mon accord, renommer tout `CLAUDE.md` qu'il contient (par exemple en `CLAUDE.ancien-AAAA-MM-JJ.md`) ou l'exclure par le réglage `claudeMdExcludes` : sinon il redevient une consigne active dès qu'un fichier voisin est lu.

## Nommage

- Règle générale et date qui fait foi : section « Classement et nommage » du CLAUDE.md maître.
- Caractères à éviter : [liste].
- Versions : [règle, par exemple « une seule version courante ; l'ancienne va aux archives »].
- Exemples conformes : `[exemple tiré du dossier]`, `[autre exemple]`.
- Exceptions, liste fermée (tout autre fichier suit la règle) :
  - `[dossier ou type de fichier]` : [règle propre], parce que [raison].

## Formats de fichiers

| Usage | Format | Remarque |
|---|---|---|
| [Document de travail] | [format] | [précision] |
| [Document remis à un tiers] | [format] | [par exemple version non modifiable] |
| [Données, tableaux] | [format] | [précision] |

## Langue et ton des documents pour tiers

- Langue : [langue retenue au bloc B ; autre langue pour tel destinataire].
- Registre : [vouvoiement ou tutoiement ; niveau de formalité].
- Ouverture et clôture : [formules].
- À éviter : [formules, promesses ou contenus interdits].
- Signature : modèle `[chemin]` ; les coordonnées (téléphone, adresse, e-mail) restent dans ce modèle, jamais ici.
- Exception pour [rôle] : [différence].

## Mentions obligatoires

| Document | Mention | Texte exact |
|---|---|---|
| [type de document] | [nature de la mention] | « [texte] » ou `[fichier qui le porte]` |

- Reprendre le texte exact, sans le reformuler.
- Une mention qui contient un identifiant, une adresse ou des coordonnées se cite par `[fichier qui la porte]`, sans recopier sa valeur.

<!-- Propriétaire : [nom ou rôle] · Créé avec le kit Architecte consignes v1.1.2 -->
