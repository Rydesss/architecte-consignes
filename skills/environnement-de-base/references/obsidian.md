# Volet Obsidian et accueil

Ce fichier guide l'installation d'Obsidian, l'ouverture du dossier de travail comme coffre et la note `Accueil.md`. Il est lu à l'étape 4 du `SKILL.md` de ce skill (« 4. Obsidian ») ; sa règle se pose à l'étape 9 et ses tests se font à l'étape 10.

Obsidian est un logiciel gratuit, y compris pour un usage professionnel, utilisable sans compte ; Obsidian Sync, payant, est facultatif. Il affiche les fichiers `.md` (Markdown : texte simple) d'un dossier comme des notes reliées entre elles. Un coffre (vault) est un dossier ouvert dans Obsidian ; il porte le nom du dossier. Obsidian y crée un dossier caché `.obsidian`, qui contient ses réglages.

Ce volet demande une session locale de Claude Code : onglet Code de l'application de bureau, ou terminal. Dans Cowork, les commandes tournent dans un environnement isolé et n'installent rien sur l'ordinateur ; computer use (Pro, Max, Ultra) peut y piloter des applications : non testé pour une installation. Sur claude.ai, ce volet ne se fait pas. Les mentions viennent de la table « Mentions au maître » de [architecte-consignes/SKILL.md](../../architecte-consignes/SKILL.md) ; les faits sur les règles, de [mecanismes.md](../../architecte-consignes/references/mecanismes.md) §6 et §16.

### Rôles

C : Claude, dans le périmètre accepté au plan : demande d'autorisation pour chaque commande qui modifie en mode manuel ; sinon, accord dans la conversation (E2). U : le participant.

| Action | Qui | Pourquoi |
|---|---|---|
| Relever Obsidian et les `.obsidian` existants | C, lecture seule | Sans effet. |
| Lire le mode de permission (onglet Code : sélecteur sous la zone de saisie) | U | Claude n'a pas de moyen documenté de le lire. |
| Créer un dossier de travail neuf, s'il en faut un | C, après accord (étape 3) | Écriture sur sa machine. |
| Ouvrir une nouvelle session dans ce dossier | U | Claude ne démarre pas de session. |
| Installer par winget (Windows) ou par Homebrew déjà présent (macOS) | C, après accord dans la conversation | Commande sur sa machine ; en mode auto ou Bypass, elle peut passer sans demande d'autorisation. |
| Accepter des conditions, saisir un mot de passe, répondre au contrôle de compte | U | Claude n'accepte rien et ne saisit rien à sa place. |
| Télécharger l'installeur officiel (repli) | U | Téléchargement et installation sur sa machine. |
| Lancer Obsidian la première fois | U | Ce lancement enregistre le lien `obsidian://`. |
| Ouvrir le gestionnaire de coffres (`obsidian://choose-vault`) | C | Ouvre une fenêtre, sans toucher aux fichiers. |
| Cliquer « Open folder as vault » et choisir le dossier | U | Aucune méthode officielle ne le fait sans clic. |
| Régler Obsidian | U, guidé par C | Réglage dans l'interface seulement : Claude n'écrit rien dans `.obsidian` et n'y copie aucun modèle. |
| Créer ou compléter `Accueil.md`, créer la note d'essai | C, après accord sur le texte | Fichiers du dossier de travail. |
| Vérifier ces notes dans Obsidian | U | Preuve que Claude et Obsidian voient le même dossier. |
| Poser la règle, écrire les lignes du `CLAUDE.md` | C, après accord (étapes 9 et 10) | `.claude/settings.json` est un chemin protégé (demande d'autorisation en mode manuel et en Accept edits) ; `CLAUDE.md` ne l'est pas. |
| Refuser la demande d'autorisation du test, supprimer les fichiers d'essai | U | Le test porte sur sa décision. |

### Pas à pas

1. (C) Annoncer : « Nous allons installer Obsidian et y ouvrir votre dossier de travail. Je ne lance rien sans votre accord. Accepter des conditions, télécharger un fichier et cliquer dans Obsidian restent de votre côté. Pour ce volet, je vous conseille le mode manuel : il vous demande l'autorisation avant les modifications de fichiers et avant les commandes, sauf celles qui ne font que lire. »
   - Onglet Code : « Cliquez sur le sélecteur sous la zone de saisie et choisissez le mode manuel (libellé à vérifier à l'écran). »
   - Terminal : « Appuyez sur Maj+Tab jusqu'à lire « manual mode on » sous la zone de saisie. » Au lancement, `claude --permission-mode default` donne le même mode (sinon, mode auto par défaut).
2. Dossier du coffre. Par défaut, le coffre est le dossier de la session, fixé à l'étape 3 (`references/stockage.md`, partie A). Il n'y a jamais qu'un seul coffre : un coffre existant au-dessus ou en dessous se garde (pas 3). Noter au brouillon, sous « Obsidian », la racine de la session et le coffre retenu, qui diffèrent seulement dans ces cas.
   - Jamais dans un autre coffre, ni dans le dossier système d'Obsidian (Windows : `%APPDATA%\Obsidian` ; macOS : `~/Library/Application Support/obsidian`).
   - Ne jamais déplacer le dossier actuel hors de OneDrive ou de Google Drive (règle E3). Dire : « Ne glissez pas votre dossier hors de OneDrive ou de Google Drive : selon le service et le système, il peut être retiré du cloud ou mis à la corbeille en ligne. Nous copierons les fichiers. »
   - Dossier synchronisé gardé à l'étape 3 : une seule synchronisation, jamais Obsidian Sync en plus ; fichiers gardés sur l'appareil (gestes : `references/stockage.md`, partie A), sinon Obsidian peut croire une note manquante (aide d'Obsidian). Dire : « Un défaut signalé (source tierce, sans correctif connu) a déjà fait perdre des fichiers modifiés par Claude dans un dossier OneDrive sous Windows ; un dossier local reste plus sûr. »
   - Dossier neuf choisi mais pas encore créé : revenir à l'étape 3 (`references/stockage.md`, partie A, pas 4 à 6). La suite se fait dans la nouvelle session.
3. (C, lecture seule) Relever Obsidian et les coffres existants. Reprendre le relevé de l'étape 1, en faisant toujours la recherche « coffre en dessous » ; tout refaire si le dossier a changé. winget est l'outil d'installation de Microsoft, en ligne de commande. Commandes déduites, non documentées par Obsidian.
   - Windows, installé : `winget list --id Obsidian.Obsidian -e --source winget`. Si winget manque, ou demande d'accepter les conditions d'une source, même ici : ne pas répondre ; demander au participant s'il voit Obsidian dans le menu Démarrer.
   - Windows, coffre ici ou au-dessus : `$d = Get-Item .; while ($d) { if (Test-Path (Join-Path $d.FullName '.obsidian')) { $d.FullName }; $d = $d.Parent }`
   - Windows, coffre en dessous : `Get-ChildItem -Directory -Recurse -Force -Filter .obsidian -ErrorAction SilentlyContinue | ForEach-Object FullName` (ignorer `.\.obsidian` lui-même).
   - macOS, installé : `ls -d /Applications/Obsidian.app ~/Applications/Obsidian.app`
   - macOS, coffre ici ou au-dessus : `d="$PWD"; while [ "$d" != "/" ]; do [ -d "$d/.obsidian" ] && echo "$d"; d=$(dirname "$d"); done`
   - macOS, coffre en dessous : `find . -mindepth 2 -type d -name .obsidian`
   - Que faire selon le résultat :
     - Aucun `.obsidian` : coffre retenu, la racine de la session.
     - `.obsidian` dans le dossier lui-même : c'est déjà un coffre, et le coffre retenu. Garder ses réglages ; au pas 6, l'ouvrir seulement s'il manque à la liste des coffres d'Obsidian.
     - `.obsidian` dans un dossier au-dessus : le dossier fait déjà partie d'un coffre. Ouvrir la racine en ferait un coffre dans un coffre, ce qui peut casser la mise à jour des liens (aide d'Obsidian). Le participant choisit :
       - réutiliser ce coffre : coffre retenu, le dossier au-dessus. Au pas 6, ne pas ouvrir la racine ; (U) ouvre ce coffre s'il manque à la liste, avec son chemin. `Accueil.md` et la note d'essai s'écrivent à la racine de la session : ils apparaissent dans ce coffre, dans le dossier de la session ; le dire. La règle `Edit(./.obsidian/**)` ne vise pas ce `.obsidian`, hors du dossier de la session : pas de règle ni de mention, la ligne sur `.obsidian` reste une consigne. Sauter les points 1 à 5 du test et noter au brouillon, sous « À confirmer » : « `.obsidian` du coffre parent : non couvert par la règle » ;
       - un autre emplacement : retour à l'étape 3 ; appelé par `architecte-consignes`, le dossier ne change pas pendant l'appel (SKILL.md, étape 3), donc reporter ce volet, « à confirmer ».
     - `.obsidian` dans un sous-dossier : ouvrir la racine ferait un coffre dans un coffre. Le dire. Le participant choisit :
       - garder ce seul coffre : coffre retenu, ce sous-dossier. Dire d'abord : « Obsidian ne montrera que `<sous-dossier>` : vos autres dossiers, et ceux copiés ensuite, n'y apparaîtront pas ; l'accueil les citera en texte seulement. » Au pas 6, ne pas ouvrir la racine ; (U) ouvre ce coffre s'il manque à la liste, avec son chemin ; le pas 7 se règle dans ce coffre, s'il le souhaite. L'accueil et la note d'essai s'écrivent à la racine de ce coffre (`<sous-dossier>/Accueil.md`), pour qu'il les montre ; l'accueil y donne les chemins depuis la racine de la session, et la ligne du `CLAUDE.md` nomme ce chemin. La règle `Edit(./.obsidian/**)` ne vise pas ce `.obsidian` : pas de règle ni de mention, la ligne sur `.obsidian` reste une consigne. Sauter les points 1 à 5 du test et noter à « À confirmer » : « `.obsidian` du coffre `<sous-dossier>` : non couvert par la règle » ;
       - reporter ce volet : rien n'est ouvert ; noter « Obsidian : à confirmer, coffre existant dans `<sous-dossier>` ».
     - Dans tous les cas, ne jamais supprimer, déplacer ni modifier un `.obsidian` existant.
   - Après chaque lot de copie (étape 5), refaire la recherche « coffre en dessous ». Un `.obsidian` copié se signale au participant, qui choisit ; ne pas le supprimer, le déplacer ni le modifier.
4. Installer, si besoin.
   - Windows. Dire : « Je vous propose d'installer Obsidian pour votre seul compte utilisateur, sans droits d'administrateur. Obsidian est gratuit ; ses conditions sont sur obsidian.md/terms, à lire par vous. Êtes-vous d'accord ? » Puis (C, après accord) : `winget install --id Obsidian.Obsidian -e --scope user --source winget`.
     - `-e` exige l'identifiant exact (`Obsidian.Obsidian`) ; `--scope user` installe pour ce compte, sans élévation (manifeste winget, source tierce) ; `--source winget` limite la recherche au dépôt communautaire, où se trouve ce manifeste.
     - Ne jamais ajouter `--accept-package-agreements` ni `--accept-source-agreements`, ni contourner une erreur d'empreinte.
     - winget demande un accord : (U) « Ouvrez PowerShell (menu Démarrer, tapez PowerShell), tapez `winget install --id Obsidian.Obsidian -e --scope user --source winget`, lisez les conditions et répondez vous-même. Si winget vous demande d'accepter des conditions, regardez de quelle source elles viennent (à vérifier à l'écran) ; vous seul décidez, sinon nous passons au téléchargement. »
     - Une fenêtre demande des droits d'administrateur : le participant décide ; Claude ne relance pas.
     - winget absent, ou en échec (par exemple « Installer hash does not match », forum, source tierce) : passer au repli.
   - macOS. (C, lecture seule) `command -v brew || ls /opt/homebrew/bin/brew /usr/local/bin/brew`. Homebrew est un outil d'installation pour Mac, absent par défaut : ne jamais l'installer pour l'occasion. S'il est présent, dire : « Je vous propose d'installer Obsidian avec Homebrew, déjà présent sur votre Mac, dans le dossier Applications, commun à tous les comptes du Mac. Obsidian est gratuit ; ses conditions sont sur obsidian.md/terms, à lire par vous. Homebrew se mettra d'abord à jour lui-même ; je l'empêche de faire le ménage dans vos autres logiciels. Êtes-vous d'accord ? »
     - (C, après accord) `HOMEBREW_NO_INSTALL_CLEANUP=1 "<chemin de brew>" install --cask obsidian`, avec le chemin trouvé (macOS 12 au moins, source tierce). Sans cette variable, `brew install` lance `brew cleanup`, qui retire d'anciennes versions d'autres logiciels installés par Homebrew.
     - brew demande un mot de passe : ne rien saisir, jamais `sudo`. Arrêter ; passer au repli, ou le participant tape lui-même la commande dans Terminal.
   - Repli (U) : « Tapez l'adresse obsidian.md/download dans la barre d'adresse, sans passer par un moteur de recherche, et prenez la version « Universal ». »
     - Windows : ouvrir le `.exe` et suivre l'assistant. Dire : « Si l'assistant propose d'installer pour vous seul ou pour tous les utilisateurs, choisissez pour vous seul (libellé à vérifier à l'écran) ; si une fenêtre demande des droits d'administrateur, c'est à vous de décider. »
     - macOS : ouvrir le `.dmg` et glisser Obsidian dans Applications. Dire : « Si le Mac demande un mot de passe d'administrateur, c'est vous qui le saisissez ou qui annulez : je ne le vois pas et je ne le tape pas. »
5. (U) « Lancez Obsidian. Ne vous connectez à aucun compte : il n'en faut aucun. Ne créez pas de coffre de démonstration. » Ce premier lancement enregistre le lien `obsidian://`.
   - Windows : menu Démarrer > Obsidian.
   - macOS : dossier Applications > Obsidian. Si macOS demande de confirmer l'ouverture d'une application téléchargée : « C'est à vous de choisir. » (non vérifié).
6. Ouvrir le dossier comme coffre, seulement si le coffre retenu est la racine de la session (pas 3). Coffre au-dessus réutilisé ou coffre de sous-dossier gardé : même geste, avec le chemin de ce coffre, seulement s'il manque à la liste.
   - (C) Ouvrir le gestionnaire de coffres. Windows : `Start-Process "obsidian://choose-vault"`. macOS : `open "obsidian://choose-vault"`.
   - (C) Donner au participant le chemin absolu développé du coffre retenu, noté au brouillon, sous « Obsidian ». Racine de la session : Windows, `(Get-Location).Path` (forme `C:\Users\<nom>\Claude\<Dossier>`) ; macOS, `pwd` (forme `/Users/<nom>/Claude/<Dossier>`). Coffre au-dessus : le chemin trouvé par la recherche « ici ou au-dessus » du pas 3. Coffre de sous-dossier : Windows, `(Resolve-Path -LiteralPath '<sous-dossier>').ProviderPath` ; macOS, `(cd '<sous-dossier>' && pwd -P)`. Jamais la racine de la session quand le coffre retenu est ailleurs. Jamais `~` ni `$env:USERPROFILE`, que la fenêtre ne comprend pas.
   - (U) « Si le nom du dossier figure déjà dans la liste des coffres, cliquez simplement dessus. Sinon, en face de « Open folder as vault », cliquez sur « Open ». »
     - Windows : « Cliquez dans la barre en haut de la fenêtre, là où s'affiche l'emplacement, collez le chemin que je vous ai donné, Entrée, puis le bouton de validation (probablement « Sélectionner un dossier »). »
     - macOS : « Appuyez sur Cmd+Maj+G, collez le chemin que je vous ai donné, Entrée, puis « Ouvrir ». »
   - Libellés d'Obsidian cités en anglais d'après l'aide (libellé français : non documenté, à vérifier à l'écran) ; libellés du système : non documentés, à vérifier à l'écran.
   - Obsidian crée alors `.obsidian`. Ce dossier est masqué dans Obsidian (source tierce) et dans le Finder ; sous Windows, il reste probablement visible dans l'Explorateur (déduit).
7. (U, guidé par C) Réglages. Dire : « Ouvrez les réglages d'Obsidian : roue dentée en bas à gauche (à vérifier à l'écran). » Libellés en anglais d'après l'aide (libellé français : non documenté, à vérifier à l'écran).
   - Files and links :
     - « Default location for new notes » : choisir « In the folder specified below », puis la zone d'entrée de l'arborescence, si elle existe ;
     - « Default location for new attachments » : choisir « In the folder specified below », puis un dossier choisi avec le participant, plutôt que la racine (« Vault folder », choix par défaut) ;
     - « Automatically update internal links » : activé ;
     - « Show all file types » : activé, pour voir les `.docx`, `.xlsx`, etc. ;
     - « Excluded files » : bouton « Manage », puis la zone d'archives ; elle reste visible dans la liste des fichiers (source tierce), ce n'est pas un moyen de la cacher ;
     - « Deleted files » : « Move to system trash » ;
     - « Use [[Wikilinks]] » : activé (choix par défaut).
   - Community plugins : laisser « Restricted mode » actif. Dire : « Un plugin communautaire est un module ajouté par un tiers ; il a tous les accès d'Obsidian, à vos fichiers comme à Internet. Le mode restreint les empêche de fonctionner. Ne cliquez pas sur « Turn on community plugins » : ce bouton désactive le mode restreint. »
   - Coffre existant (pas 3) dont le mode restreint est déjà désactivé : le dire au participant, qui décide ; Claude ne change rien dans `.obsidian`.
8. (C, après accord sur le texte) Accueil : la note d'entrée du dossier, qui décrit le classement validé. Créer `Accueil.md` depuis `modeles/modele-accueil.md`, en suivant ses consignes de remplissage, là où le coffre retenu le montre : à la racine de la session si le coffre est la racine ou un dossier au-dessus ; à la racine du coffre s'il est un sous-dossier gardé (`<sous-dossier>/Accueil.md`). Noter ce chemin au brouillon, sous « Obsidian ». Dire où le participant la verra : à la racine du coffre ; coffre au-dessus réutilisé, dans le dossier de la session.
   - S'il existe : ne pas l'écraser ; montrer l'ajout et l'écrire après accord.
   - Dossiers listés : ceux du plan validé de `_entretien-claude-md.md`, avec les chemins de l'arborescence réelle. Sans plan validé (skill lancé seul, sans `_entretien-claude-md.md` « Plan validé : oui ») : les dossiers de premier niveau, que le participant valide un par un.
   - Chaque chemin s'écrit en texte, jamais en lien vers un dossier (non documenté dans Obsidian). Un rôle inconnu reste « à confirmer », jamais inventé.
9. (C crée, U vérifie) Note d'essai, selon E9 (SKILL.md) : vérifier que la note n'existe pas dans le dossier de l'accueil noté au pas 8 (`.`, ou `<sous-dossier>` pour un coffre de sous-dossier gardé) : Windows `Test-Path -LiteralPath '<dossier de l'accueil>\essai-claude-AAAAMMJJ-HHMM.md'`, attendu `False` ; macOS `test -e '<dossier de l'accueil>/essai-claude-AAAAMMJJ-HHMM.md' && echo existe`, attendu : rien. Puis la créer dans ce même dossier, avec une ligne : « Note créée par Claude pour l'essai. » Noter son chemin au brouillon, sous « Tests ». Dire : « Regardez la liste des fichiers d'Obsidian, à gauche : la note d'essai et l'accueil doivent apparaître sans rien faire » (coffre au-dessus réutilisé : dans le dossier de la session). Noter le résultat au brouillon.
10. Préparer l'étape 9, sans rien écrire ici : noter au brouillon la règle retenue (section suivante) et les lignes du `CLAUDE.md`. La ligne sur `.obsidian` attend le test de l'étape 10.

### Réglages à poser dans .claude/settings.json

Seulement si le coffre retenu est la racine de la session (pas 3). Règle de `modeles/modele-settings-environnement.json`, fusionnée à l'étape 9 avec le fichier existant, sans rien en retirer :

```json
{
  "permissions": {
    "ask": ["Edit(./.obsidian/**)"]
  }
}
```

- Effet (« confirmation ») : avant que les outils d'édition de Claude (Edit, Write) créent, modifient ou écrasent un fichier du `.obsidian` du dossier de la session, Claude Code affiche une demande d'autorisation. Cela vaut dans tous les modes, auto et Bypass compris, sauf `dontAsk`, où l'appel est refusé (mecanismes.md §6).
- Limites :
  - ce n'est pas un blocage : le participant peut accepter ;
  - un script (Python, Node) n'est pas couvert, ni, par déduction, l'outil de terminal de l'application (`mcp__terminal__run_in_terminal`) ;
  - effet sur une commande PowerShell (`Set-Content`, `Copy-Item`) ou une redirection Bash : non documenté, à vérifier dans l'application ;
  - la règle ne vaut que dans une session ouverte dans ce dossier ; un `.obsidian` de sous-dossier : non documenté, à vérifier dans l'application.
- Phrase à dire à l'étape 9 : « Je vais ajouter une confirmation : quand j'utiliserai mes outils d'édition de fichiers sur le dossier `.obsidian`, Claude Code vous affichera une demande d'autorisation ; vous accepterez ou refuserez. Limite : une commande ou un script que je lancerais n'est pas couvert de façon sûre, et ce réglage ne vaut que dans une session ouverte dans ce dossier. »
- Pas de règle `Write(...)` : elle n'est pas appliquée, et `Edit(...)` couvre déjà la création. L'écrire laisserait croire à une protection de plus.
- Un ask plutôt qu'un deny (choix du kit) : l'interdit reste dans la consigne, et la demande d'autorisation laisse la décision au participant si Claude essaie quand même. Un deny déjà posé sur `.obsidian` se garde. Pas de règle de lecture : Claude peut lire `.obsidian`.

### Ligne à proposer pour le CLAUDE.md

Lignes montrées à l'étape 9 (vocabulaire du maître : l'utilisateur parle à la première personne) :

- « Ne jamais modifier le dossier `.obsidian` : je règle Obsidian moi-même, dans Obsidian (demande d'autorisation, restreinte aux outils d'édition). »
- « Ne jamais renommer ni déplacer une note ou un dossier du coffre par une commande ou par les outils de fichiers : me demander de le faire dans Obsidian, qui met à jour les liens internes. »
- « Écrire les liens entre notes au format choisi dans Obsidian (Wikilinks par défaut : `[[Nom de la note]]`). »
- « Pour retrouver un document, partir de `Accueil.md`, qui donne le rôle et le chemin de chaque dossier. » (coffre de sous-dossier gardé : `<sous-dossier>/Accueil.md`, chemin noté au pas 8)

Conditions :
- La ligne sur `.obsidian` ne s'écrit pas à l'étape 9. Elle s'écrit à l'étape 10, après le test de la règle, et après accord. Sinon, Claude pourrait refuser d'essayer en suivant la consigne, et le test ne prouverait rien.
- Sa mention (table « Mentions au maître », ligne « Interdit sur un chemin couvert par un ask `Edit(…)` ») ne s'écrit que si `Edit(./.obsidian/**)` figure en ask dans le `.claude/settings.json` du dossier, si le coffre retenu est la racine de la session (ni un dossier au-dessus, ni un sous-dossier : pas 3), et si le test a réussi. Sinon, la ligne reste une consigne, sans mention.
- Les trois autres lignes sont des consignes sans mention, écrites à l'étape 9 (aucune règle ne couvre `mv`, `Move-Item` ou `Rename-Item`). Jamais « (bloqué par les réglages) » dans ce volet.
- Sans `CLAUDE.md` : garder les lignes pour le récapitulatif et proposer `/architecte-consignes` à l'étape 11.

### Tests à l'étape 10

Dans la nouvelle session de l'étape 10 (règle E6). Tester la règle en premier, avant d'écrire la ligne sur `.obsidian`. Ordre dans cette session : ce test, puis le retour au mode manuel confirmé (point 5), puis seulement les tests du blocage `Edit` et l'ajout de l'original (`references/stockage.md`, partie B, Test, point 3, et pas 11). En Accept edits, des commandes comme mv, cp ou Remove-Item passent sans demande dans tout dossier de travail, dossier ajouté compris (mecanismes.md §6). Ci-dessous, `<chemin>` est le chemin absolu développé du dossier, donné comme au pas 6 : jamais `~` ni `$env:USERPROFILE`.

1. (C) Vérifier d'abord qu'aucun autre dossier n'est ajouté à la session. Demander : « Avez-vous ajouté un dossier à cette session, par le « + » à côté de la zone de saisie ou par `/add-dir` ? » Lire aussi la clé `additionalDirectories` des `.claude/settings.json` et `.claude/settings.local.json` du dossier. Un dossier ajouté : ne pas passer en Accept edits ; noter le test « à confirmer » et le faire dans une nouvelle session sans dossier ajouté. Sinon, (U) passer en mode Accept edits : onglet Code, sélecteur sous la zone de saisie ; terminal, Maj+Tab jusqu'à « accept edits on ». En mode manuel, toute écriture demande une autorisation, règle ou non : le test ne prouverait rien. Dire : « Pendant ce test seulement, Claude Code laisse passer sans demande les modifications de fichiers et des commandes comme mkdir, mv, cp ou rm ; nous revenons au mode manuel juste après. »
2. (C) Noms des deux fichiers, selon E9 (SKILL.md) : `temoin-claude-AAAAMMJJ-HHMM.txt` à la racine et `.obsidian/essai-claude-AAAAMMJJ-HHMM.txt`. Vérifier d'abord qu'aucun des deux n'existe (Windows `Test-Path -LiteralPath '<fichier>'`, attendu `False` ; macOS `test -e '<fichier>' && echo existe`, attendu : rien) ; sinon, changer l'heure. Témoin : le créer avec l'outil Write, avec une ligne : « Témoin de l'essai Obsidian. » Noter son chemin au brouillon, sous « Tests ». Attendu : créé sans demande. Si une demande s'affiche, le mode n'est pas Accept edits : refuser, corriger le mode, recommencer.
3. (C) Dire : « C'est l'essai du réglage de confirmation, que vous avez accepté. Je vais créer avec mon outil d'écriture, sans commande, le fichier `.obsidian/essai-claude-AAAAMMJJ-HHMM.txt`. Une demande d'autorisation doit s'afficher : refusez-la, sans choisir d'option qui autorise pour toute la session. » Puis appeler Write, jamais une commande.
   - Réussite : la demande s'est affichée et l'outil revient refusé. L'absence du fichier est nécessaire, pas suffisante.
4. (C, lecture seule) Vérifier l'absence du fichier.
   - Windows : `Test-Path -LiteralPath '.\.obsidian\essai-claude-AAAAMMJJ-HHMM.txt'` (attendu : `False`).
   - macOS : `ls '.obsidian/essai-claude-AAAAMMJJ-HHMM.txt'` (attendu : « No such file or directory »).
   - Fichier présent (créé sans demande, ou accepté par erreur) : noter son chemin au brouillon, sous « Tests » ; il se nettoie au point 10.
5. (U) Revenir au mode manuel (terminal : Maj+Tab jusqu'à « manual mode on ») et le confirmer à Claude. (C) Attendre cette confirmation avant tout autre test et avant l'ajout de l'original. Puis (U) supprimer le témoin noté au brouillon, après que (C) a vérifié qu'il ne contient que sa ligne (E9).
   - Windows : « Dans l'Explorateur, cliquez dans la barre d'adresse, collez `<chemin>`, Entrée, puis supprimez le fichier. »
   - macOS : « Finder > Aller > Aller au dossier (Cmd+Maj+G), collez `<chemin>`, Entrée, puis mettez le fichier à la Corbeille. »
6. (C, après accord) Test réussi : écrire au `CLAUDE.md` la ligne sur `.obsidian`, avec sa mention. Test échoué : la ligne sans mention, et « à confirmer » au brouillon (voir Dépannage).
7. Note d'essai : visible au pas 9 (étape 4) ; la cocher.
8. (U, si les lignes sont au `CLAUDE.md`) Demander à Claude comment il renommerait la note d'essai. Attendu : il propose de le faire dans Obsidian et ne renomme rien.
9. Accueil : test fait au point 1 de l'étape 10 du `SKILL.md`, en premier message de la session, avant la reprise. Noter ici son résultat.
10. (U) Nettoyer, selon E9 : seulement les fichiers notés au brouillon, et après que (C) a vérifié qu'ils ne contiennent que leur ligne d'essai. Supprimer la note d'essai dans Obsidian (clic droit sur la note > « Delete », libellé à vérifier à l'écran ; elle va à la corbeille du système). Si le fichier d'essai de `.obsidian` a été noté au point 4 :
    - Windows : « Dans l'Explorateur, cliquez dans la barre d'adresse, collez `<chemin>\.obsidian`, Entrée, puis supprimez `essai-claude-AAAAMMJJ-HHMM.txt`. » Ce geste marche même si le dossier est caché ;
    - macOS : « Finder > Aller > Aller au dossier (Cmd+Maj+G), collez `<chemin>/.obsidian`, Entrée, puis mettez `essai-claude-AAAAMMJJ-HHMM.txt` à la Corbeille. »

### Dépannage

- winget demande un accord : le participant tape lui-même la commande (pas 4) ou choisit le repli. winget absent ou erreur d'empreinte : repli du pas 4.
- `obsidian://choose-vault` n'ouvre rien : Obsidian n'a jamais été lancé (pas 5). Sinon, lancer Obsidian : sans coffre ouvert, son écran d'accueil propose « Open folder as vault » ; avec un coffre ouvert, icône du coffre en bas à gauche > « Manage vaults… » (à vérifier à l'écran).
- La note d'essai n'apparaît pas : le coffre ouvert n'est pas le coffre retenu (comparer son nom, en bas à gauche, au brouillon ; coffre au-dessus réutilisé : chercher la note dans le dossier de la session ; coffre de sous-dossier gardé : la note doit être dans `<sous-dossier>/`, à côté de l'accueil, et non à la racine de la session). Un fichier dans un format qu'Obsidian n'ouvre pas lui-même (`.docx`, `.xlsx`…) n'apparaît qu'avec « Show all file types ».
- Liens cassés après un renommage fait hors d'Obsidian (forum, source tierce) : rendre au fichier son ancien nom, puis le renommer dans Obsidian (déduit).
- Test, le témoin demande une autorisation : le mode n'est pas Accept edits.
- Test, aucune demande pour `.obsidian` et fichier créé :
  - Claude a écrit par une commande (PowerShell, Bash) : la règle ne couvre pas ce cas de façon sûre. Faire d'abord supprimer le fichier par le participant (point 10 du test), vérifier son absence (point 4 du test), puis recommencer au point 2 du test, avec l'outil Write ;
  - sinon : session ouverte dans un autre dossier, `.claude/settings.json` mal placé ou JSON invalide, ou règle écrite `Write(...)` au lieu de `Edit(...)`.
- Test, Claude refuse d'essayer en citant une consigne : c'est la consigne, pas le réglage ; refaire avec la phrase d'essai du point 3 du test.
- Test, refus sans demande : un deny couvre déjà `.obsidian` (`Edit(…)`, ou `Read(…)`, qui refuse aussi l'écriture). Il se garde. Aucune ligne de la table ne correspond à ce cas : la ligne sur `.obsidian` reste une consigne, sans mention, jamais « bloqué » dans ce volet.

### Limites et points à confirmer

- Aucune méthode officielle n'ouvre un dossier comme coffre sans clic (forum, source tierce : demandes ouvertes de mars à octobre 2026). Ne pas modifier `obsidian.json` (format non documenté). Ne pas utiliser l'interface en ligne de commande d'Obsidian : sa commande `eval` exécute du code, et elle demande les droits d'administrateur sous macOS. Computer use pourrait faire le clic (onglet Code, Windows ou macOS 14 ou plus, offres Pro, Max, Ultra) : non testé.
- Claude ne copie aucun `.obsidian` modèle et n'écrit pas `app.json` : ses clés ne sont pas documentées, et un plugin communautaire y hérite de tous les accès d'Obsidian.
- winget : manifeste du dépôt communautaire de Microsoft (source tierce) ; premier usage dans une session Claude non testé ; sans `--source`, winget interroge toutes les sources configurées, dont le Microsoft Store (`msstore`), et une demande d'accord de celle-ci au premier usage n'est pas documentée sur la page lue (à vérifier dans l'application) ; fausses mises à jour signalées (forum, source tierce). Installeur Windows lancé à la main : portée et dossier non documentés. Aucune exigence système publiée pour Windows.
- Homebrew : son installation demande un compte administrateur (déduit) ; prise en charge officielle à partir de macOS 15 sur Apple Silicon, à vérifier pour un Mac Intel. `command -v brew` peut ne rien trouver si la session ne charge pas le profil du shell (déduit) : d'où les deux chemins du pas 4. Avant `brew install`, Homebrew se met à jour lui-même ; `HOMEBREW_NO_INSTALL_CLEANUP` évite le nettoyage qui suit (page Manpage de Homebrew).
- Masquage de `.claude` et `.obsidian` dans Obsidian : source tierce seulement.
- Même note modifiée par Claude et le participant au même moment : non documenté. Capture des modifications de Claude par la récupération de fichiers d'Obsidian : non documentée ; prévoir une autre sauvegarde.
- Règle ask : documentée, mais l'essai réel du 25/11/2026 (onglet Code, Windows) n'a testé que des deny. Effet d'un ask, macOS et Cowork : non testés ; le test de l'étape 10 fait foi.
- Écriture de `.claude/settings.json` : demande d'autorisation en mode manuel et en Accept edits ; en mode auto, un classifieur décide ; en Bypass, écriture sans demande. L'accord se demande donc aussi dans la conversation (étape 9). Dans l'onglet Code, ce fichier ne se modifie pas dans l'éditeur intégré.
- En mode auto ou Bypass, winget et brew peuvent passer sans demande d'autorisation : l'accord se demande toujours d'abord dans la conversation.
- Libellés d'Obsidian cités en anglais d'après l'aide, version 1.15.1 au 25/11/2026.

### Sources

- https://obsidian.md/download — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/install — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/license — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/terms — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/Extending+Obsidian/Obsidian+URI — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/manage-vaults — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/data-storage — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/sync/switch — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/sync-notes — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/settings — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/file-formats — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/attachments — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/plugin-security — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/links — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/plugins/file-recovery — lue le 25/11/2026 — officielle (Obsidian)
- https://obsidian.md/help/cli — lue le 25/11/2026 — officielle (Obsidian)
- https://learn.microsoft.com/en-us/windows/package-manager/winget/install — lue le 25/11/2026 — officielle (Microsoft)
- https://code.claude.com/docs/en/permissions.md — lue le 25/11/2026 — officielle (Anthropic)
- https://code.claude.com/docs/en/permission-modes.md — lue le 25/11/2026 — officielle (Anthropic)
- https://code.claude.com/docs/en/security — lue le 25/11/2026 — officielle (Anthropic)
- https://code.claude.com/docs/en/desktop.md — lue le 25/11/2026 — officielle (Anthropic)
- https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork — lue le 25/11/2026 — officielle (Anthropic)
- https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork — lue le 25/11/2026 — officielle (Anthropic)
- https://raw.githubusercontent.com/microsoft/winget-pkgs/master/manifests/o/Obsidian/Obsidian/1.15.1/Obsidian.Obsidian.installer.yaml — lue le 25/11/2026 — source tierce (dépôt communautaire)
- https://formulae.brew.sh/cask/obsidian — lue le 25/11/2026 — source tierce
- https://docs.brew.sh/Installation — lue le 25/11/2026 — source tierce
- https://docs.brew.sh/Manpage — lue le 25/11/2026 — source tierce
- https://forum.obsidian.md/t/open-a-folder-as-a-new-obsidian-vault-using-its-filepath-via-the-uri/112323 — lue le 25/11/2026 — source tierce (forum)
- https://forum.obsidian.md/t/open-folder-as-an-obsidian-vault-from-terminal-command-line-cli/111805 — lue le 25/11/2026 — source tierce (forum)
- https://forum.obsidian.md/t/links-do-not-update-when-renaming-a-file/80455 — lue le 25/11/2026 — source tierce (forum)
- https://forum.obsidian.md/t/bug-winget-installer-hash-does-not-match/69117 — lue le 25/11/2026 — source tierce (forum)
- https://forum.obsidian.md/t/obsidian-doesnt-update-version-in-register-when-auto-updating/90667 — lue le 25/11/2026 — source tierce (forum)
- https://forum.obsidian.md/t/rename-excluded-files-setting-to-reduce-misunderstandings/110052.md — lue le 25/11/2026 — source tierce (forum)
- https://community.obsidian.md/plugins/hidden-folders-access — lue le 25/11/2026 — source tierce
- https://github.com/anthropics/claude-code/issues/65229 — lue le 25/11/2026 — source tierce (GitHub)
- `../../architecte-consignes/references/mecanismes.md` §6 (règles `Edit` et `Write`, modes, chemins protégés) — référence interne, d'après code.claude.com
- Essais réels du 25/11/2026, onglet Code de l'application de bureau, Windows — observés, sans URL
