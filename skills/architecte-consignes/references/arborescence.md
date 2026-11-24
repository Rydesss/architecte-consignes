# Arborescence : diagnostic, principes, modèles et migration

Référence des étapes 3 et 4. Lire ce fichier quand l'utilisateur choisit au cadrage d'analyser l'arborescence existante ou d'en proposer une nouvelle (les deux valent demande d'arborescence), et à l'étape 1 sans accès aux fichiers (section 7). Le diagnostic (section 2) et la proposition (sections 3 à 5) se font à l'étape 3, sans rien déplacer, et se valident avec le plan de fichiers ; l'étape 4 ne garde que la migration (section 6), menée seulement si l'utilisateur l'accepte. Un renvoi « (§n) » vise la section n de `mecanismes.md`.

## 1. Pourquoi l'arborescence compte pour Claude

- Claude ne connaît un dossier que par ce qu'il liste et ce qu'il ouvre. Les noms de dossiers et de fichiers sont ses premiers indices : `contrats/2025/` le guide, `nouveau dossier (3)/` l'oblige à ouvrir pour savoir, et chaque fichier ouvert consomme du contexte.
- Les consignes citent des chemins (suivi, sources, dossier de consignes) : un dossier déplacé ou renommé rend ces pointeurs faux. Une règle par chemin vise des fichiers par motif (`paths:`, relatif au dossier qui contient `.claude`, §4) : si le motif cite un dossier qui change de nom, il ne correspond plus et la règle ne se charge plus.
- Un sous-dossier peut porter son propre `CLAUDE.md`, chargé à la demande : quand Claude lit, écrit ou modifie un fichier de ce sous-dossier (§1). L'arborescence dessine donc des zones de consignes. À l'inverse, un vrai `CLAUDE.md` laissé dans des archives ou des modèles redevient une consigne active dès que Claude lit un fichier voisin (§1).
- Tout s'additionne : le `CLAUDE.md` d'un sous-dossier n'annule pas une règle du parent (§2). Découper l'arborescence ne dispense pas de formuler chaque règle une seule fois, avec sa portée.

## 2. Diagnostiquer une arborescence existante

Rester en lecture seule. Mesurer depuis la racine de l'espace. Ne pas ouvrir les dossiers que l'utilisateur signale comme sensibles ni ceux qui semblent contenir des données personnelles ou des secrets ; si un tel dossier contient une source de vérité ou un fichier qui ressemble à des consignes (mesure 8), n'ouvrir que ce fichier, désigné par son nom. Les outils de lecture de l'agent peuvent suffire ; les commandes ci-dessous servent quand un shell est disponible ou quand l'utilisateur mesure lui-même (section 7). Elles écartent `.git/`, `node_modules/`, les environnements virtuels (`.venv/`, `venv/`) et les dossiers de build (`dist/`, `build/`, `target/`) par le filtre `$x`, à définir en premier. Dans un dépôt git, partir plutôt de `git ls-files`. Sur un très gros dossier, réduire la profondeur. Inventaire à produire :

| N° | Mesure | Signal à relever |
|---|---|---|
| 1 | Dossiers sur trois niveaux, nombre de fichiers de chacun | dossier vide ; dossier de plusieurs centaines de fichiers sans motif de nommage |
| 2 | Profondeur maximale | plus de quatre niveaux |
| 3 | Fichiers à la racine | autre chose que le maître, le suivi, le brouillon d'entretien et quelques fichiers d'usage |
| 4 | Motifs de nommage et formats dominants | plusieurs formats de date ; noms sans indice (`scan001.pdf`) ; versions « final », « final2 » |
| 5 | Préfixes numériques en double | deux dossiers frères qui portent le même numéro |
| 6 | Dossiers fourre-tout | `divers`, `vrac`, `autres`, `temp`, `à trier`, `nouveau dossier` |
| 7 | Résidus de verrouillage, de test ou de copie | `~$…`, `.~lock…`, `*.tmp`, `* (1).*`, « copie », « test » |
| 8 | Consignes à tous les niveaux, avec leur taille ; fichiers texte qui ressemblent à des consignes, par leur nom | `CLAUDE.md` ou `AGENTS.md` sous des archives ou des modèles ; maître de plus de 200 lignes ; fichier chargé à la demande de plus de 40 000 caractères (§5) ; fichier `.md` ou `.txt` dont le nom contient consigne, instruction, prompt, claude ou agent, hors copies `.ancien-*` déjà neutralisées et brouillon d'entretien : le lire comme une consigne existante (SKILL.md, règle 9) |
| 9 | Fichiers très gros | exports, sauvegardes, médias mêlés aux documents de travail |
| 10 | Fichiers de secrets, repérés par leur nom sans les ouvrir | `.env`, `*.key`, coffre (`*.kdbx`), nom qui évoque identifiants, mots de passe, codes d'accès ou banque : constat bloquant (`controle-qualite.md` C21, cas du dossier de code compris) ; proposer à l'utilisateur de le sortir lui-même de l'espace |

### Commandes PowerShell (Windows), lecture seule

```powershell
# 0 Dossiers écartés de toutes les mesures, à définir en premier
$x = '\\(\.git|node_modules|\.venv|venv|dist|build|target)(\\|$)'
# 1 Dossiers sur trois niveaux et nombre de fichiers
Get-ChildItem -Directory -Recurse -Depth 2 -Force | Where-Object FullName -notmatch $x | ForEach-Object { '{0,5}  {1}' -f @(Get-ChildItem -LiteralPath $_.FullName -File -Force).Count, (Resolve-Path -LiteralPath $_.FullName -Relative) }
# 2 Profondeur maximale (0 = fichier à la racine), puis 3 fichiers à la racine
$r = (Get-Location).Path.TrimEnd('\'); Get-ChildItem -Recurse -File -Force | Where-Object FullName -notmatch $x | ForEach-Object { ($_.FullName.Substring($r.Length) -split '\\').Count - 2 } | Measure-Object -Maximum
Get-ChildItem -File -Force | Select-Object Name, Length
# 4 Motifs de nommage, puis formats
Get-ChildItem -Recurse -File | Where-Object FullName -notmatch $x | Group-Object { switch -Regex ($_.Name) { '^\d{4}-\d{2}-\d{2}' {'AAAA-MM-JJ'; break} '^\d{8}' {'AAAAMMJJ'; break} '^\d' {'numero'; break} default {'autre'} } } | Select-Object Count, Name
Get-ChildItem -Recurse -File | Where-Object FullName -notmatch $x | Group-Object Extension | Sort-Object Count -Descending | Select-Object -First 10 Count, Name
# 5 Préfixes numériques en double entre dossiers frères
Get-ChildItem -Directory -Recurse -Depth 2 | Where-Object { $_.FullName -notmatch $x -and $_.Name -match '^\d+' } | Group-Object { $_.Parent.FullName + ' > ' + ($_.Name -replace '^(\d+).*','$1') } | Where-Object Count -gt 1 | Select-Object Name
# 6 Dossiers fourre-tout, puis 7 résidus de verrouillage, de test ou de copie
Get-ChildItem -Directory -Recurse -Force | Where-Object { $_.FullName -notmatch $x -and $_.Name -match '^(divers|autres?|vrac|temp|tmp|misc|old|nouveau dossier|new folder)( \(\d+\))?$|trier' } | ForEach-Object FullName
Get-ChildItem -Recurse -File -Force | Where-Object { $_.FullName -notmatch $x -and $_.Name -match '^~\$|^\.~lock|\.(tmp|bak)$| \(\d+\)\.|copie|(^|[ _-])test([ _.-]|$)' } | ForEach-Object FullName
# 8 Consignes à tous les niveaux (lignes, octets, chemin), dossiers .claude, puis fichiers texte qui ressemblent à des consignes
Get-ChildItem -Recurse -File -Force -Include CLAUDE.md,CLAUDE.local.md,AGENTS.md,.cursorrules,copilot-instructions.md | Where-Object FullName -notmatch $x | ForEach-Object { '{0,5} l. {1,7} o.  {2}' -f @(Get-Content -LiteralPath $_.FullName).Count, $_.Length, $_.FullName }
Get-ChildItem -Recurse -Directory -Force -Filter .claude | Where-Object FullName -notmatch $x | ForEach-Object FullName
Get-ChildItem -Recurse -File -Force -Include *.md,*.txt | Where-Object { $_.FullName -notmatch $x -and $_.Name -match 'consigne|instruction|prompt|claude|agent' -and $_.Name -notmatch '\.ancien-|^(CLAUDE(\.local)?|AGENTS|copilot-instructions|_entretien-claude-md)\.md$' } | ForEach-Object FullName
# 9 Les vingt plus gros fichiers, en Mo
Get-ChildItem -Recurse -File -Force | Where-Object FullName -notmatch $x | Sort-Object Length -Descending | Select-Object -First 20 @{n='Mo';e={[math]::Round($_.Length/1MB,1)}}, FullName
# 10 Fichiers de secrets, par leur nom seulement : ne pas les ouvrir
Get-ChildItem -Recurse -File -Force | Where-Object { $_.FullName -notmatch $x -and $_.Name -match '^\.env|\.(key|pem|pfx|p12|kdbx)$|identifiant|login|mots?.?de.?passe|(^|[^a-z])(mdp|codes|acc(e|è)s)([^a-z]|$)|codes?.?(d.?)?acc(e|è)s|pass(word|wd)|secret|credential|banque|bancaire' } | ForEach-Object FullName
```

### Commandes bash (macOS, Linux), lecture seule

```bash
# 0 Dossiers écartés de toutes les mesures, à définir en premier
x='/(\.git|node_modules|\.venv|venv|dist|build|target)(/|$)'
# 1 Dossiers sur trois niveaux et nombre de fichiers
find . -mindepth 1 -maxdepth 3 -type d | grep -vE "$x" | while IFS= read -r d; do printf '%5s  %s\n' "$(find "$d" -maxdepth 1 -type f | wc -l | tr -d ' ')" "$d"; done
# 2 Profondeur maximale (0 = fichier à la racine), puis 3 fichiers à la racine
find . -type f | grep -vE "$x" | awk -F/ 'NF-2 > m { m = NF-2 } END { print m+0 }'
find . -maxdepth 1 -type f
# 4 Motifs de nommage, puis formats
find . -type f | grep -vE "$x" | sed 's#.*/##' | sed -E -e 's/^[0-9]{4}-[0-9]{2}-[0-9]{2}.*/AAAA-MM-JJ/' -e t -e 's/^[0-9]{8}.*/AAAAMMJJ/' -e t -e 's/^[0-9].*/numero/' -e t -e 's/.*/autre/' | sort | uniq -c
find . -type f -name '*.*' | grep -vE "$x" | sed 's/.*\.//' | sort | uniq -c | sort -rn | head
# 5 Préfixes numériques en double entre dossiers frères
find . -mindepth 1 -maxdepth 3 -type d | grep -vE "$x" | sed -nE 's#^(.*)/([0-9]+)[^/]*$#\1 > \2#p' | sort | uniq -d
# 6 Dossiers fourre-tout, puis 7 résidus de verrouillage, de test ou de copie
find . -type d | grep -vE "$x" | grep -iE '/(divers|autres?|vrac|temp|tmp|misc|old|nouveau dossier|new folder)( \([0-9]+\))?$|trier'
find . -type f | grep -vE "$x" | grep -iE '/~\$|/\.~lock|\.(tmp|bak)$| \([0-9]+\)\.|copie|(/|[ _-])test([ _.-]|$)'
# 8 Consignes à tous les niveaux (lignes, octets, chemin), dossiers .claude, puis fichiers texte qui ressemblent à des consignes
find . -type f \( -name CLAUDE.md -o -name CLAUDE.local.md -o -name AGENTS.md -o -name .cursorrules -o -name copilot-instructions.md \) | grep -vE "$x" | while IFS= read -r f; do wc -lc "$f"; done
find . -type d -name .claude | grep -vE "$x"
find . -type f \( -iname '*.md' -o -iname '*.txt' \) | grep -vE "$x" | grep -iE '/[^/]*(consigne|instruction|prompt|claude|agent)[^/]*$' | grep -vE '/(CLAUDE|CLAUDE\.local|AGENTS|copilot-instructions|_entretien-claude-md)\.md$|\.ancien-[^/]*$'
# 9 Les vingt plus gros fichiers, en Ko
find . -type f -exec du -k {} + | grep -vE "$x" | sort -rn | head -20
# 10 Fichiers de secrets, par leur nom seulement : ne pas les ouvrir
find . -type f | grep -vE "$x" | grep -iE '/\.env|\.(key|pem|pfx|p12|kdbx)$|identifiant|login|mots?.?de.?passe|(^|[^a-z])(mdp|codes|acc(e|è)s)([^a-z]|$)|codes?.?(d.?)?acc(e|è)s|pass(word|wd)|secret|credential|banque|bancaire'
```

Les mesures 5 à 7 et 10 donnent des faux positifs (dossiers datés `2025-01`, « photocopie », dossier de tests d'un projet de code, `.envrc`, `secretariat/`, `acces-client.docx`) : relire la liste avant d'en faire un constat. La recherche par nom de la mesure 8 en donne aussi (`notice-instructions-four.txt`, `agents-commerciaux.md`, modèles de ce skill s'il est installé dans `.claude/skills/`, à citer sans les lire) : relire la liste avant d'ouvrir un fichier. La mesure 10 peut aussi manquer un nom : la compléter par une lecture des noms de la racine et du premier niveau (C21). La mesure 8 compte des octets, un peu plus que les caractères quand le texte est accentué. Si un dossier de travail porte un nom écarté (`build/`, par exemple), le retirer de `$x`.

Restituer le diagnostic en trois parties : ce qui fonctionne ; ce qui gêne, chaque constat avec sa preuve (chemin, compte) et le principe de la section 3 qu'il contredit ; les propositions classées par gain. Le présenter à l'étape 3, avec l'arborescence proposée et le plan de fichiers, bâti sur ses chemins. Ordre habituel des propositions :

1. faire sortir de l'espace les fichiers de secrets, par l'utilisateur lui-même (constat bloquant ; s'il en garde un, deny de lecture nommé et statut « risque accepté », cas du dossier de code compris : `controle-qualite.md` C21) ;
2. neutraliser les consignes égarées (gain fort, effort faible) ;
3. créer la zone d'entrée et la zone d'archives ;
4. renommer les fourre-tout et lever les doublons de numéros ;
5. réduire la profondeur ;
6. harmoniser le nommage des nouveaux documents, et celui de l'existant seulement si l'utilisateur le demande.

## 3. Principes

- Peu de niveaux : deux à trois sous la racine. Un niveau de plus doit servir à trier, pas seulement à ranger. Racine dégagée : le maître (et `AGENTS.md` avec plusieurs agents), `.claude/`, le suivi, le brouillon d'entretien le temps de l'entretien, et les dossiers de premier niveau.
- Noms explicites et stables : le nom dit le contenu et ne change plus une fois cité par une consigne. Préférer des noms sans espace ni accent pour les dossiers que les consignes citent, plus sûrs à recopier dans un chemin ou une commande. Le dossier de consignes et ses fichiers n'ont jamais d'espace (§3).
- Une zone d'entrée (`entree/`, `a-classer/`) : tout ce qui arrive sans place connue. Le classement depuis l'entrée suit la règle du maître.
- Une zone d'archives (`archives/`, par année ou par projet) : l'inactif y va au lieu d'être supprimé, et ses consignes y sont neutralisées (section 6).
- Un dossier de modèles (`modeles/`), séparé des documents produits. Un modèle de consigne n'y porte jamais le nom `CLAUDE.md`.
- Un dossier de consignes (`consignes/` par défaut) : les fichiers satellites et, s'il existe, le registre des numéros de dossiers.
- Un lieu par type de document : la règle « un X va dans Y » tient en une ligne du maître. Ailleurs, un renvoi, jamais une copie.
- Données sensibles à part : un dossier distinct, qu'un deny de lecture peut fermer dans Claude Code (`modele-settings.json`). Ce deny ne couvre ni `grep -r` ni un script (§6) : un secret (clé, mot de passe) reste hors de l'espace de travail.
- Ne pas créer de dossiers en prévision : un dossier naît avec son premier document. Un dossier vide laisse croire qu'un type de document existe. Seule exception : la zone d'entrée, créée d'emblée, même vide, puisque la règle de classement du maître la cite.
- Nommage daté quand l'ordre compte. Proposer plusieurs formats sans en imposer un, et fixer la date qui fait foi (création, envoi ou réception du document) :

```text
2025-03-14-objet.pdf      date complète en tête : tri chronologique
20250314_objet.pdf        même tri, plus court
2025-03_objet.xlsx        document mensuel
objet_2025-03-14.docx     regroupement par objet, puis par date
objet-v02.docx            versions numérotées, sans « final »
```

- Numérotation, seulement si l'utilisateur la veut : préfixes à deux chiffres pour l'ordre d'affichage, numéros uniques entre dossiers frères, et un registre des numéros (numéro, nom, rôle, date d'attribution) dans le dossier de consignes. Un numéro retiré n'est jamais réattribué.

## 4. Modèles d'arborescence

Partir du modèle le plus proche des réponses aux blocs A, D et E, puis retirer tout dossier sans contenu prévu. Les noms sont des exemples à adapter, sauf `CLAUDE.md`, `CLAUDE.local.md` et `.claude/`, imposés par l'outil (§1, §6, §11). Dans chaque modèle, `.claude/` contient les réglages (`settings.json`), les règles par chemin (`rules/`) et les skills (`skills/`) ; `suivi.md` suit `modele-suivi.md`.

### Par actionnabilité (inspiré de PARA)

Convient si le travail se découpe en projets qui ont une fin, à côté d'activités permanentes.

```text
espace/
├── CLAUDE.md               CLAUDE.md maître
├── .claude/                réglages, règles par chemin, skills
├── suivi.md                suivi
├── consignes/              dossier de consignes
├── entree/                 à classer
├── projets/                un sous-dossier par projet ; à sa fin, il passe aux archives
├── responsabilites/        activités sans fin : clients, finances, équipe
├── ressources/             documentation de référence
│   └── modeles/            modèles de documents
└── archives/               inactif, par année
```

### Par domaines numérotés (Johnny.Decimal simplifié)

Convient si les documents sont nombreux et stables, si l'on se renvoie souvent à un numéro, ou si plusieurs personnes doivent trouver la même chose au même endroit. Les dizaines numérotent les domaines, les unités les catégories ; le registre fait foi.

```text
espace/
├── CLAUDE.md               CLAUDE.md maître
├── .claude/
├── 00-gestion/
│   ├── consignes/          dossier de consignes, avec registre-numeros.md
│   ├── modeles/
│   └── suivi.md
├── 01-entree/
├── 10-premier-domaine/
│   └── 11-categorie/
├── 20-deuxieme-domaine/
└── 90-archives/
```

### Projet de code

Convient si l'espace est un dépôt git, avec des conventions déjà portées par l'outillage (tests, formatage). Suivi et entrée : l'outil de tickets, ou `docs/suivi.md` à défaut. `/init` donne un point de départ pour les commandes.

```text
projet/
├── CLAUDE.md               CLAUDE.md maître : commandes et pièges, conventions
├── CLAUDE.local.md         préférences personnelles, exclu de git
├── .claude/
│   ├── settings.json       réglages partagés (deny des secrets)
│   ├── rules/              règles par chemin (tests, migrations)
│   └── skills/
├── docs/
│   ├── consignes/          dossier de consignes
│   ├── modeles/
│   └── archives/           notes et décisions remplacées
└── src/
    └── module-a/CLAUDE.md  ce qui diffère pour ce module
```

### Espace d'équipe partagé

Convient si plusieurs personnes ouvrent le même dossier (dépôt, dossier synchronisé, lecteur réseau) pour des activités distinctes. Les préférences de chacun vont dans son `~/.claude/CLAUDE.md`. `CLAUDE.local.md` et `.claude/settings.local.json` ne restent personnels que si le partage les exclut (§1, §6) : sur un dossier synchronisé sans exclusion, ils seraient chargés pour tout le monde (déduction).

```text
equipe/
├── CLAUDE.md               CLAUDE.md maître : règles communes
├── .claude/settings.json   réglages partagés
├── consignes/              dossier de consignes
├── suivi.md                qui fait quoi, échéances
├── entree/
├── modeles/
├── activite-a/
│   └── CLAUDE.md           ce qui diffère pour cette activité
└── archives/
```

### Dossier administratif personnel

Convient pour des papiers personnels ou familiaux : peu de projets, beaucoup de pièces à retrouver par thème puis par année.

```text
administratif/
├── CLAUDE.md               CLAUDE.md maître
├── .claude/settings.json   deny sur identite/
├── consignes/              dossier de consignes
├── suivi.md                démarches en cours, échéances
├── a-classer/              courriers scannés, téléchargements
├── modeles/                lettres types
├── logement/
├── impots/                 un sous-dossier par année si les pièces sont nombreuses
├── identite/               pièces sensibles, lecture fermée par défaut
└── archives/
```

### Recherche ou rédaction

Convient pour un mémoire, une thèse, un livre, une veille ou une série d'articles : des sources à citer exactement, des textes qui évoluent par versions, des remises à des relecteurs.

```text
redaction/
├── CLAUDE.md               CLAUDE.md maître
├── .claude/                réglages, règle par chemin sur chapitres/, skills
├── consignes/              dossier de consignes : style, norme de citation
├── suivi.md                chapitres en cours, échéances de remise
├── sources/                articles, notes de lecture, bibliographie
├── chapitres/              un fichier par chapitre ou par article
├── remis/                  versions envoyées, non modifiées
└── archives/
```

## 5. Projets et sous-espaces

Donner un `CLAUDE.md` à un sous-dossier quand ses règles diffèrent du parent et ne concernent que ses fichiers, quand il forme une unité de travail (projet, client, activité) avec ses propres sources, ou quand une session y est ouverte directement. Ne pas en créer si la différence tient en une ligne du maître, si elle vise un type de fichier plutôt qu'un dossier (règle par chemin, `modele-regle-chemin.md`), ou s'il s'agit d'état (suivi).

Il contient, d'après `modele-CLAUDE-sous-dossier.md` : une à deux phrases sur ce qu'est le sous-espace ; ses sources qui font foi, et son suivi s'il en a un propre ; ses règles en plus ou différentes ; rien de ce que le parent dit déjà. Une exception à une règle du parent s'écrit dans la règle du parent, avec sa portée, car rien ne s'annule (§2).

- Depuis une session ouverte plus haut, il n'est chargé que lorsque Claude lit, écrit ou modifie un fichier du sous-dossier (§1) et, après une compaction, ne revient que quand Claude retouche un de ces fichiers (§7). Une règle qui doit valoir dès le début d'une tâche reste dans le maître. Au-delà de 40 000 caractères (fenêtre de 200 000 tokens), seul son début est lu (§5).
- Session ouverte dans le sous-dossier : avec Claude Code, les `CLAUDE.md` des dossiers parents se chargent aussi, dépôt git ou non (§1). Le `.claude/settings.json` partagé du parent, lui, ne s'applique pas : il est lu depuis le dossier de travail de la session (§6). Lancer Claude à la racine, ou répéter les deny nécessaires dans le `.claude/settings.json` du sous-dossier, en réécrivant les motifs `./` depuis ce sous-dossier (`Read(./clients/rh/**)` devient `Read(./rh/**)` dans `clients/`) ou en chemin absolu (`//c/…`). Tester ensuite chaque deny sur un fichier factice, dans une session ouverte au sous-dossier : en terminal, `/status` ou `/permissions` montrent les réglages chargés, pas le chemin visé, et dans l'onglet Code `/permissions` est indisponible (§6). Hors git, ce sous-dossier a sa propre mémoire automatique (§8). Les autres agents ont leurs propres règles de découverte (§9) : ne pas supposer qu'ils lisent le parent.
- Cowork : la lecture d'un `CLAUDE.md` de projet n'y est pas documentée (§12) ; mettre les règles dans les instructions du projet. Les interdits et les accords préalables du sous-dossier y ont leur ligne, dans une section par dossier (`routage.md` section 7). Un sous-espace récurrent peut devenir un projet Cowork, avec ses propres instructions.

## 6. Migrer une arborescence

Préalables :

- Plan de fichiers et arborescence cible validés ensemble à l'étape 3 (« Plan validé : oui » dans le brouillon d'entretien).
- Sauvegarde recommandée avant le premier lot : copie du dossier sur un autre support, ou commit si l'espace est sous git. Demander si elle est faite, et quel est son périmètre ; ne pas la faire à la place de l'utilisateur sans son accord. Sans sauvegarde confirmée, proposer une copie dans un dossier frère `<espace>-copie-AAAA-MM-JJ`, hors du dossier de travail de la session (le dire). La copie est faite par l'utilisateur, ou par Claude avec son accord. Noter la sauvegarde retenue au brouillon, sous « Lots de migration faits » (SKILL.md, règle 7).
- Périmètre de la copie : jamais les fichiers de secrets signalés à l'étape 1 ou par la mesure 10 (section 2) ; les compter à part, sans jamais les ouvrir. Avant la copie, nommer les dossiers et fichiers qui peuvent contenir des données personnelles de tiers, archives comprises. Appliquer les réponses du bloc C : si l'utilisateur interdit leur copie hors de leur dossier, les exclure de la copie, ou faire la copie sur un support qu'il choisit. Ne jamais affirmer le contenu d'un fichier non ouvert : écrire « contenu non vérifié ».
- Espace synchronisé par un service en ligne : un dossier frère se trouve en général dans la même zone synchronisée (déduction). La copie y double alors la place occupée et peut dépasser le quota. Proposer un emplacement hors de la synchronisation, ou un autre support. L'historique du service ne vaut sauvegarde que si l'utilisateur le confirme ; le kit ne le vérifie pas.
- Au récapitulatif de l'étape 7, citer la copie et le brouillon qu'elle contient (état d'avant la migration). Dire si elle contient des données personnelles, ou peut en contenir (fichiers non ouverts). Proposer de la ranger, ou à l'utilisateur de la supprimer lui-même, une fois le rangement vérifié.
- À défaut de copie, le dire et s'en tenir à des déplacements sans écrasement, réversibles.

1. Dresser le tableau de migration, découpé en petits lots (un dossier ou un type de document par lot). Exemple fictif :

| Lot | Ancien chemin | Nouveau chemin | Raison | Renvois à corriger |
|---|---|---|---|---|
| 1 | `ancien-projet/CLAUDE.md` | `ancien-projet/CLAUDE.ancien-AAAA-MM-JJ.md` | consigne neutralisée sur place, avant le déplacement | aucun |
| 1 | `ancien-projet/` | `archives/2024/ancien-projet/` (créer seulement `archives/2024/`) | projet terminé | maître, section « Procédures » |

2. Pour chaque lot : présenter ses lignes et le nombre de fichiers concernés, puis obtenir un accord explicite pour ce lot. Un accord ne vaut pas pour le lot suivant. Plusieurs lots peuvent partager un message, chacun avec sa question d'accord, quatre au plus (SKILL.md, règle 4) ; n'exécuter que les lots acceptés, dans l'ordre. Noter au brouillon un lot refusé ou reporté, sous « Lots de migration faits », avec cette mention (sans accès aux fichiers, dans le résumé à recoller).
3. Déplacer sans jamais écraser. Pour un dossier entier, créer seulement le dossier parent de la cible (`archives/2024/`), jamais la cible elle-même : sinon le dossier déplacé s'y imbrique. Pour des fichiers isolés, créer le dossier cible. Pas de `-Force` avec `Move-Item`, et `mv -n` sous bash. Ne pas déplacer le maître, `.claude/` ni le dossier de consignes sans corriger tous leurs renvois dans le même lot.
4. Recompter après le lot. Le nombre de fichiers à la destination égale celui de la source avant le lot, l'ancien emplacement est vide, et `<cible>/<nom du dossier déplacé>` n'existe pas. PowerShell : `(Get-ChildItem -LiteralPath 'chemin' -Recurse -File -Force).Count`, puis `Test-Path -LiteralPath 'archives/2024/ancien-projet/ancien-projet'` (attendu : `False`) ; bash : `find 'chemin' -type f | wc -l`, puis `test ! -e 'archives/2024/ancien-projet/ancien-projet' && echo ok`. En cas d'écart, s'arrêter et le dire.
5. Corriger les renvois. Chercher l'ancien chemin, écrit avec `/` et avec `\`, dans le maître, les satellites et les imports `@` ; dans les `paths:` des règles, les skills et les deny de `.claude/settings.json` ; dans les prompts des tâches programmées (souvent rangés hors de l'espace) et les scripts. PowerShell : `Get-ChildItem -Recurse -File -Include *.md,*.json | Select-String -SimpleMatch 'ancien/chemin','ancien\chemin'` ; bash : `grep -rnF --include='*.md' --include='*.json' 'ancien/chemin' .`. Les liens internes des documents bureautiques échappent à cette recherche : les signaler à l'utilisateur.
6. Noter le lot terminé et ses comptes dans le brouillon d'entretien (« Lots de migration faits »), pour reprendre après une interruption ; sans accès aux fichiers, dans le résumé à recoller (section 7).

Règles de migration :

- Ne rien supprimer. Un fichier inutile, un doublon ou un résidu va dans `archives/` ; la suppression reste une décision que l'utilisateur prend lui-même. Seule exception : la valeur d'un secret ou d'une donnée personnelle trouvée dans une consigne archivée ou une copie de sauvegarde `.ancien-*` d'un fichier de consignes (la copie d'avant migration garde ses documents tels quels : préalables ci-dessus). La remplacer par « [retiré] » avec l'accord de l'utilisateur, et le prévenir que le secret est à changer (dans un dépôt git, il reste dans l'historique).
- Neutraliser toute consigne archivée : un `CLAUDE.md` déplacé aux archives redevient actif dès que Claude lit un fichier voisin (§1). Le renommer (`CLAUDE.ancien-AAAA-MM-JJ.md`, nom que Claude Code ne charge pas ; la date est celle de la neutralisation, avec le suffixe `-2` pour une deuxième copie du même jour dans le même dossier), ou l'exclure avec le réglage `claudeMdExcludes` : liste de motifs comparés aux chemins absolus, par exemple `"claudeMdExcludes": ["**/archives/**"]`, dans les réglages utilisateur, projet, local ou gérés (§1). Vérifier ensuite l'effet : un CLAUDE.md d'archives rangé en sous-dossier n'apparaît jamais dans `/context all`, exclu ou non ; faire lire à Claude un fichier voisin et vérifier qu'aucune ligne « Loaded » suivie de son chemin n'apparaît dans le terminal, ou tracer les chargements avec un hook `InstructionsLoaded` (§1, §10).
- Renommer aussi un `AGENTS.md` archivé : sans `CLAUDE.md`, `.claude/CLAUDE.md` ni `CLAUDE.local.md` dans le dossier de travail, au-dessus ni dans son dossier, ou avec le réglage `claude-md-and-agents-md`, il se lit à la demande (§9), et d'autres agents ont leurs propres règles. Renommer de même un `CLAUDE.local.md` archivé : celui d'un sous-dossier se charge à la demande, comme un CLAUDE.md (§1). Un dossier `.claude/` archivé : les règles de son `rules/` se chargent à la demande (§1) ; proposer de le renommer (`.claude.ancien-AAAA-MM-JJ/`, par exemple) ; l'effet de ses autres fichiers (réglages, skills) n'est pas documenté : le signaler à l'utilisateur.
- Dossier synchronisé par un service en ligne : laisser la synchronisation finir entre deux lots.
- En fin de migration, relancer les mesures 1, 2, 8 et 10 de la section 2 et comparer au diagnostic initial. Avec Claude Code, proposer ensuite une nouvelle session à la racine : `/context all` pour les consignes chargées au lancement (onglet Code : non documenté, à vérifier dans l'application, §10), un deny testé sur un fichier factice pour les réglages (§6).
- Si un lot a été refusé ou reporté, le plan validé peut citer des chemins que la migration n'a pas créés, ou un dossier qui ne contient pas tous les documents visés. Avant l'étape 5, l'ajuster à l'arborescence réelle. Chaque chemin du plan désigne un dossier qui existe, que l'étape 5 crée ou que le maître dit « créé au premier document » (zone d'archives, D4), et le dossier où se trouvent réellement les documents visés ; une partie des documents restée ailleurs se cite aussi (`controle-qualite.md` C04). Présenter les lignes changées, obtenir un nouvel accord, reporter les lignes changées dans le tableau du plan du brouillon, puis noter « Plan validé : oui (ajusté après migration, [date]) » (SKILL.md, étape 4).

## 7. Sans accès aux fichiers

Cas de claude.ai, d'une session sans dossier ouvert, ou d'un utilisateur qui préfère ne pas ouvrir son dossier. À l'étape 1, demander en un seul message :

1. la structure du dossier, au choix : une description (dossiers des deux premiers niveaux et leur contenu, lieu d'arrivée des nouveaux documents, sort des anciens, habitudes de nommage) ; la sortie de `tree /a` (Windows, dossiers seuls) ou de `find . -maxdepth 3 -type d` (macOS, Linux) ; ou celle des mesures de la section 2, qui écartent `.git/`, `node_modules/` et les dossiers de build ;
2. le nom des dossiers sensibles, sans rien de leur contenu ;
3. le texte des consignes existantes, à coller sans aucun secret : `CLAUDE.md`, `CLAUDE.local.md`, `AGENTS.md`, contenu de `.claude/`, fichiers d'autres agents, tout fichier texte qui sert de consignes (mesure 8) et, si le cadrage cite Cowork ou un projet claude.ai, le texte actuel des instructions du projet.

Ensuite :

- Marquer « à confirmer » tout ce que la réponse ne dit pas. Ne pas déduire le contenu d'un dossier de son seul nom sans le dire.
- Rendre l'arborescence proposée dans un bloc de code, et le tableau de migration en Markdown. L'utilisateur exécute lui-même chaque lot, recompte avec les commandes de la section 6 et confirme avant le lot suivant. Sans terminal, il recompte dans l'explorateur de fichiers (propriétés du dossier) et décrit le dossier obtenu en fin de migration.
- Après chaque lot confirmé, remettre le résumé à recoller, cumulé et autonome, avec les titres du brouillon (SKILL.md, règle 7).
- Pour Cowork ou un projet claude.ai, la règle de classement va dans les instructions du projet (`modele-instructions-projet.md`).
