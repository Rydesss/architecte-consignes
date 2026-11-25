<!--
MODÈLE : CLAUDE.md qui importe AGENTS.md (kit Architecte consignes, v1.1.2).
Destination : `CLAUDE.md` dans le même dossier qu'`AGENTS.md` (`modele-AGENTS.md`), jamais `CLAUDE.local.md`, personnel. À utiliser quand plusieurs agents partagent l'espace.
Pour Claude, au remplissage :
- La ligne `@AGENTS.md` est indispensable : Claude Code ne lit AGENTS.md de lui-même que s'il ne trouve ni CLAUDE.md, ni .claude/CLAUDE.md, ni CLAUDE.local.md dans le dossier de travail ou au-dessus ; `~/.claude/CLAUDE.md`, le CLAUDE.md géré par l'organisation et `.claude/rules/` ne comptent pas (mecanismes.md §9 ; réglable par « Project instructions » : `/config` dans un terminal, ou `pluginConfigs` de `~/.claude/settings.json`, d'un fichier passé avec `--settings` ou des réglages gérés). Dès que ce fichier existe, l'import seul fait lire AGENTS.md, jamais deux fois, et un CLAUDE.local.md n'en coupe plus la lecture. Exception : sur `managed-only`, aucun CLAUDE.md de projet n'est chargé, import compris : changer le réglage, ou le signaler à l'administrateur s'il vient des réglages gérés.
- Le chemin d'un import part du fichier qui le contient (§3) : si ce fichier est placé en `.claude/CLAUDE.md`, écrire `@../AGENTS.md`. Pour un `.claude/AGENTS.md`, écrire `@.claude/AGENTS.md` dans le CLAUDE.md du dossier, ou `@AGENTS.md` dans `.claude/CLAUDE.md` s'il est le seul CLAUDE.md du dossier, sans jamais créer le second (controle-qualite.md E06).
- Ne pas remplacer l'import par un lien symbolique, déconseillé sous Windows (§9), ni par une phrase « lire AGENTS.md », qui n'est pas un import (§3).
- Après l'import, n'écrire que ce qui est propre à Claude ou touche aux fonctions de Claude Code : imports de satellites, skills, règles par chemin, réglages, commandes `/…`, mémoire automatique, outils et connecteurs. Une règle valable pour tous les agents va dans AGENTS.md, sans copie ici. Une préférence de réponse (bloc B) va par défaut dans « Façon de travailler avec moi » d'AGENTS.md ; réservée à Claude par l'utilisateur, elle s'écrit ici sous un titre « Façon de répondre », avant « Procédures (skills) ».
- Un skill qui couvre une procédure citée dans AGENTS.md renvoie à son fichier sans le recopier.
- Les réglages de `.claude/settings.json` ne valent que pour Claude Code, et seulement pour une session lancée dans ce dossier (§6). Pour un autre agent, l'interdit écrit dans AGENTS.md reste une consigne tant que cet agent n'est pas réglé de son côté.
- Les règles de `modele-settings.json` sont des propositions : garder celles qui répondent aux blocs C, F et G, et nommer en mots ce qu'elles bloquent. La section « Réglages appliqués par l'outil » ne contient que ce que l'outil applique ; une consigne qui l'accompagne va dans AGENTS.md si elle vaut pour tous les agents (l'interdit lui-même), sinon sous « Commandes et pièges propres à Claude Code ». Un outil de connecteur se vise par son nom canonique `mcp__<serveur>__<outil>`, sans parenthèses, demandé à Claude (ce n'est pas le libellé de la demande d'autorisation) ; aucun avertissement ne signale un nom faux : vérifier dans une nouvelle session que Claude ne voit plus l'outil (§6) ; pour un serveur de `.mcp.json` pas encore approuvé, ou un serveur de plugin pas encore connecté (blocage d'avance `mcp__plugin_<plugin>_<serveur>__*`, §6), cette absence ne prouve pas le deny, noté alors « à vérifier », et le service n'est pas nommé parmi les services bloqués (controle-qualite.md section 3). Ce que la section « Réglages appliqués par l'outil » dit bloqué ou soumis à autorisation suit SKILL.md, étape 5, « Mentions au maître » : mêmes restrictions, mêmes mots, jamais dans AGENTS.md. Pour un interdit d'envoi, tant que restent permis les outils qui transmettent aux sessions ou aux appareils de l'utilisateur, écrire « les outils d'envoi vers l'extérieur », jamais « tous les outils d'envoi » ni « rien ne sort » (SKILL.md, étape 1). Pour un push sur `main` (routage.md section 5) : option Oui, mention d'une commande en ask, jamais « bloqué » ; option Non, mention d'une commande en deny ; dans les deux cas, `git -C . push`, `git -c … push`, `bash -c` et un script échappent à ces règles (§6).
- Remplacer chaque [crochet] par une réponse validée ; supprimer toute section restée vide ; aucun crochet dans le fichier final (« à confirmer », ajouté à la liste remise à l'utilisateur). Viser moins de 30 lignes après l'import.
- Les commentaires HTML de bloc sont retirés avant l'envoi à Claude : garder seulement le dernier commentaire du fichier.
-->

# [Nom de l'espace de travail] : consignes de Claude

Les règles communes à tous les agents sont dans AGENTS.md, importé ci-dessous ; ce qui suit ne vaut que pour Claude.

@AGENTS.md

<!-- Section à supprimer sans satellite importé. Remplacer `consignes/` par le dossier de consignes validé à l'étape 3. AGENTS.md cite le même fichier en pointeur pour les autres agents. -->
## Satellites importés

@consignes/contexte.md

## Procédures (skills)

- Pour [tâche récurrente], utiliser `/[nom-du-skill]`.
- [En version minimale seulement, la ligne d'entretien du maître (SKILL.md, étape 5) : « Relancer `/architecte-consignes` en mode audit pour revoir ces consignes ; une règle devenue fausse est supprimée. » Elle cite un skill : jamais dans AGENTS.md.]

<!-- Seulement pour une règle avec paths ; une règle sans paths se charge à chaque session et ne se cite pas. -->
## Règles par chemin

- Les règles propres à `[dossier]` se chargent seules quand un fichier de ce dossier est lu ou modifié (`.claude/rules/[sujet].md`).

## Réglages appliqués par l'outil

- Pour Claude Code, `.claude/settings.json` bloque (deny) [interdit sans exception d'AGENTS.md, nommé en mots, restreint selon SKILL.md, étape 5, « Mentions au maître » : par exemple, la lecture des fichiers .env de ce dossier par mes outils de lecture].
- Il me fait demander l'autorisation (ask) avant [action sensible retenue au bloc F, par exemple : supprimer un fichier, ou lancer une commande dans le terminal de l'application] ; j'accepte ou je refuse.

## Commandes et pièges propres à Claude Code

- [Connecteur, outil ou commande propre à Claude Code, et quand s'en servir : par exemple, proposer `/context all` dans un terminal pour vérifier les consignes chargées au lancement.]
- [Comportement inattendu propre à Claude Code, et la bonne façon de faire.]
- [Si une commande qui exécute du code du dépôt est gardée en allow, statut « risque accepté » (controle-qualite.md C16 ; déduction de mecanismes.md §6) : « Un script du dépôt modifié puis lancé par `[commande]` échappe aux deny de lecture et aux règles Bash (risque accepté). » Cette ligne garde la section, même en version minimale ; jamais dans AGENTS.md.]

## Mémoire automatique

- N'y confier que des apprentissages ; une règle va dans AGENTS.md ou dans ce fichier, l'état dans `[chemin du suivi]`. Quand je demande de retenir une règle, proposer de l'écrire ici ou dans AGENTS.md.

<!-- Section à garder seulement s'il existe des tâches programmées ou des automatisations de Claude. Une tâche programmée créée sans l'option « Only on this computer » ne lit pas ce fichier (mecanismes.md §14). Pour chaque tâche, lister les accords d'AGENTS.md qu'elle rencontre (valeurs par défaut de D1 et de F1 comprises) et ceux des règles par chemin et des CLAUDE.md de sous-dossier des dossiers où elle écrit (leur exception s'écrit aussi ici, avec sa portée) ; appliquer à chacun le choix de G4b comme dans `modele-CLAUDE-projet.md` : l'exception ci-dessous, propre à Claude, ou l'arrêt de la tâche avec un compte rendu, écrit dans sa procédure. Un arrêt laisse un compte rendu : citer son fichier dans la clause (« La session programmée [nom] écrit son compte rendu dans `[emplacement]` sans accord. »), sinon l'accord de D1 l'arrête aussi. Un interdit ne reçoit jamais d'exception. -->
## Sessions sans surveillance

- Une session programmée suit seulement son prompt et `[procédure]` ; elle ne modifie pas [fichiers protégés].
- La session programmée [nom] crée sans accord les fichiers que fixe sa procédure ; elle ne fait jamais [interdits].

<!-- Propriétaire : [nom ou rôle] · Revue : [fréquence, la même que celle d'AGENTS.md] · Créé avec le kit Architecte consignes v1.1.2 -->
