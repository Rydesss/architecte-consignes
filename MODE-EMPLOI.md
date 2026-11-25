# Mode d'emploi : Architecte consignes

Ce plugin vous aide à créer, avec Claude, le fichier de consignes de votre dossier de travail (`CLAUDE.md`), et à ranger ce dossier proprement. Claude vous pose quelques questions et vous montre un plan. Il n'écrit rien sans votre accord, à part un brouillon qui garde vos réponses.

Il peut aussi préparer l'environnement de base de ce dossier : Obsidian, copie de vos dossiers Google Drive ou OneDrive, messagerie en brouillons seulement, stockage en ligne connecté et Claude in Chrome. Voir la section 6.

Ce mode d'emploi vaut pour Windows et pour Mac. Quand un geste diffère, les deux sont indiqués. Les menus sont cités sous leur nom anglais : si votre application est en français, cherchez l'équivalent (Customize : Personnaliser ; Settings : Paramètres ; Connectors : Connecteurs). Leurs noms peuvent aussi changer d'une version à l'autre.

## 1. Ce qu'il vous faut

- **Un compte Claude avec un abonnement payant** : Pro, Max, Ultra, Team ou Enterprise. L'onglet Code n'est pas ouvert à l'offre gratuite. Sur Team ou Enterprise, votre organisation peut interdire l'ajout de plugins : si l'application refuse l'adresse du plugin, adressez-vous à son administrateur.
- **L'application de bureau Claude**, à jour, sur Windows ou sur Mac. Vous la téléchargez sur https://claude.ai/download.
- **Un dossier de travail** : le vôtre, ou une copie pour un premier essai.
- **Pour l'environnement de base**, qui est facultatif : Google Chrome si vous voulez Claude in Chrome et, avec un compte professionnel, l'accord éventuel de votre administrateur (section 6).

Le plugin travaille directement dans votre dossier : il le lit, puis y crée des fichiers. Utilisez-le donc dans l'**onglet Code** de l'application (on l'appelle aussi « Claude Code ») : c'est là qu'il a été essayé. **Cowork**, un autre onglet de l'application, devrait aussi convenir pour l'entretien, mais n'a pas encore été essayé. Dans l'onglet **Chat**, ou sur le site claude.ai, Claude n'a pas accès à vos dossiers : il ne pourrait que vous donner le texte des fichiers à créer vous-même.

Gestes utiles :

| Pour… | Windows | Mac |
|---|---|---|
| Copier, puis coller | Ctrl + C, puis Ctrl + V | Cmd + C, puis Cmd + V |
| Valider | Entrée | Retour ↩ |

## 2. Installer le plugin (une seule fois)

### Méthode simple, depuis l'application (Windows et Mac)

1. Ouvrez l'application Claude et connectez-vous.
2. Dans la barre latérale, à gauche, ouvrez **Customize**, puis **Plugins**. Si la barre latérale affiche directement **Plugins**, cliquez dessus.
3. Cliquez sur **Add**, puis sur **Add marketplace**.
4. Copiez le texte ci-dessous, collez-le dans le champ qui s'affiche, puis validez :

   ```text
   Rydesss/architecte-consignes
   ```

5. Ouvrez l'onglet **Discover** : le plugin y apparaît avec les autres. Choisissez **architecte-consignes**, puis cliquez sur **Add** (ou **Install**, selon la version). Si l'application vous demande où l'installer, choisissez votre compte utilisateur (**your user account**) : le plugin sera disponible dans tous vos dossiers. Installé pour « ce projet » ou en « local », il ne marche que dans le dossier ouvert à ce moment-là.

**Pour vérifier :**
1. Ouvrez une nouvelle session dans l'onglet Code, puis tapez `/archi` : **architecte-consignes** doit être proposé.
2. S'il ne l'est pas, ouvrez encore une nouvelle session : le plugin se télécharge au démarrage d'une session.
3. Toujours rien ? Mettez l'application à jour :
   - Mac : menu **Claude**, puis **Check for Updates…** ;
   - Windows : menu **Help**, puis **Check for Updates…**.

   Si cela ne suffit pas, utilisez la méthode avec le terminal ci-dessous.

Pour Cowork, il faut aussi que **Code execution and file creation** soit activé : **Settings**, puis **Capabilities**. Sur Team ou Enterprise, c'est le propriétaire du compte qui l'active.

### Autre méthode, avec le terminal

Cette méthode installe le plugin pour l'onglet Code et le terminal seulement, pas pour Cowork. Elle demande que Claude Code soit aussi installé pour le terminal, ce que l'application seule ne fait pas.

1. Ouvrez le terminal :
   - **Mac** : l'application **Terminal** (dans Applications, puis Utilitaires) ;
   - **Windows** : **PowerShell** (menu Démarrer, tapez « PowerShell »).
2. Copiez la première commande ci-dessous, collez-la dans le terminal, puis validez. Attendez la fin, puis faites de même avec la seconde :

   ```text
   claude plugin marketplace add Rydesss/architecte-consignes
   claude plugin install architecte-consignes@architecte-consignes
   ```

3. Le message « Successfully installed plugin » confirme l'installation, pour votre compte utilisateur : le plugin est disponible dans tous vos dossiers. Ouvrez alors une nouvelle session dans l'onglet Code.

Si le terminal répond que `claude` est introuvable ou n'est pas reconnu, utilisez la méthode depuis l'application.

## 3. Préparer votre dossier

1. **Vérifiez d'abord ce que vous avez le droit de copier, et où.** Avec un compte professionnel, des documents de l'entreprise ne se copient pas toujours sur une clé USB ou sur votre ordinateur.
2. **Ne déplacez et ne supprimez rien.** Si votre dossier contient des fichiers sensibles (mots de passe, codes bancaires, données personnelles de vos clients), laissez-le tel quel : créez à côté un **dossier de travail neuf** et copiez-y seulement les documents que Claude peut lire. Dans un dossier OneDrive ou Google Drive, un fichier déplacé ou supprimé l'est aussi en ligne. Claude cherche à repérer un fichier sensible sans l'ouvrir, mais ce n'est pas une garantie.
3. **Faites ensuite une copie de sauvegarde** de ce dossier de travail, à un endroit permis par la règle du point 1 (un autre dossier de votre ordinateur, par exemple). Elle ne contient que des documents autorisés.

## 4. Lancer l'entretien

1. Dans l'application, ouvrez l'**onglet Code** (à côté de **Chat** et de **Cowork**), puis démarrez une **nouvelle session**.
2. Sous la zone de saisie, choisissez l'environnement **Local**. Cliquez ensuite sur le choix du dossier, juste à côté, puis sur **Open folder…**. Sélectionnez votre dossier de travail lui-même, pas l'un de ses sous-dossiers. Si l'application vous demande si vous faites confiance à ce dossier, acceptez.
3. Sur la même ligne, choisissez le mode de permission **Manual** (**Ask permissions** sur une version plus ancienne) : Claude vous demande votre accord avant de modifier un fichier ou de lancer une commande.
4. Tapez :

   ```text
   /architecte-consignes
   ```

   puis validez. Si rien ne se passe, ou si une ancienne version se lance, tapez plutôt `/architecte-consignes:architecte-consignes`. Vous pouvez aussi écrire simplement : « Crée le CLAUDE.md de ce dossier ».
5. Répondez aux questions. Pour aller vite, choisissez la **version minimale** : environ 15 minutes. La version complète prend de 30 à 60 minutes. Claude vous propose aussi de préparer l'environnement de base (section 6).

## 5. Pendant l'entretien : trois mots à connaître

- **Bloqué** : Claude Code refuse l'action, même si vous la demandez. Si vous en avez besoin, vous la faites vous-même.
- **Confirmation** : avant chaque action de ce type, Claude s'arrête et vous affiche une demande d'autorisation, avec des boutons pour accepter ou refuser. C'est ce que le plugin propose par défaut pour supprimer, déplacer ou renommer un fichier.
- **Consigne** : Claude s'engage à la suivre, mais sans garantie.

Claude vous montre le plan de fichiers avant de créer vos consignes. Seule exception : un brouillon, `_entretien-claude-md.md`, qui garde vos réponses pour reprendre après une interruption. Lisez le plan, puis répondez « oui » ou demandez une correction.

## 6. Préparer l'environnement de base

Cette étape est facultative. Elle prépare les outils autour de votre dossier de travail. Vous choisissez les éléments voulus :

- **Obsidian** (recommandé) : un logiciel gratuit qui affiche les fichiers texte de votre dossier comme des notes reliées entre elles. Votre dossier y devient un « coffre » (vault), c'est-à-dire un dossier ouvert dans Obsidian.
- **Vos dossiers Google Drive ou OneDrive**, copiés dans votre dossier de travail.
- **Gmail ou Outlook en brouillons seulement** : Claude prépare des brouillons dans votre boîte, sans pouvoir les envoyer par le connecteur (essayé avec Gmail ; Outlook pas encore).
- **Google Drive ou OneDrive connecté**, pour que Claude y cherche et lise un document.
- **Claude in Chrome** : l'extension d'Anthropic qui permet à Claude de lire les pages, de cliquer et de remplir des champs dans votre navigateur Google Chrome. Une extension est un petit module ajouté au navigateur.

Un connecteur relie Claude à l'un de vos comptes en ligne : messagerie ou stockage.

### Ce qu'il vous faut avant

- **Une offre payante** (Pro, Max, Ultra, Team ou Enterprise). Elle est déjà nécessaire pour l'onglet Code, et Claude in Chrome la demande aussi. Obsidian est gratuit ; son option payante de synchronisation (Sync) n'est pas utile ici.
- **L'onglet Code ou le terminal.** Cette étape installe et copie sur votre ordinateur : elle ne fonctionne ni dans Cowork, ni dans l'onglet Chat, ni sur le site claude.ai.
- **Google Chrome**, si vous voulez Claude in Chrome. S'il manque, installez-le vous-même depuis le site de Google :
  - Windows : exécutez le fichier téléchargé et répondez Oui à la demande de modification de l'appareil ;
  - Mac : ouvrez `googlechrome.dmg` et glissez Chrome dans le dossier Applications.
- **Avec un compte professionnel**, l'accord éventuel de votre administrateur, c'est-à-dire la personne qui gère les comptes de votre organisation :
  - pour connecter Claude à une messagerie ou à un stockage d'entreprise (Google Workspace, Microsoft 365) ;
  - sur Claude Team ou Enterprise, pour activer les connecteurs et Claude in Chrome ;
  - pour copier des fichiers de l'entreprise sur votre ordinateur.
- **De la place sur le disque**, si vous copiez des dossiers.

Si vous ne savez pas ce que votre entreprise permet, répondez « je ne sais pas ». Claude le note « à confirmer » et garde un parcours qui fonctionne avec un dossier local.

### Comment le lancer

- **Pendant l'entretien.** Après avoir lu votre dossier, Claude vous demande : « Préparer aussi l'environnement de base ? » Répondez : tout, choisir les éléments, ou non. Si vous acceptez, il s'en occupe après avoir rédigé vos consignes, puis il ajoute ses tests à ceux de la fin.
- **Seul**, avant ou après l'entretien. Ouvrez une session de l'onglet Code sur votre dossier de travail (section 4, étapes 1 à 3), puis tapez :

  ```text
  /architecte-consignes:environnement-de-base
  ```

  Vous pouvez aussi écrire : « Prépare l'environnement de base de ce dossier ».

Claude pose d'abord quatre questions au plus : les éléments voulus ; compte personnel ou professionnel ; en entreprise, si la copie et les connecteurs sont permis ; si besoin, quel service de messagerie et de stockage. Il relève ensuite votre situation sans rien modifier. Puis il vous montre un **plan d'installation** : un tableau qui dit, pour chaque action, qui la fait (Claude ou vous), le réglage posé et le test. Rien ne change avant votre accord sur ce plan : c'est une règle que Claude suit, pas un verrou de l'outil. En mode Manual, chaque commande qui modifie vous est en plus soumise.

Si votre dossier semble synchronisé par OneDrive, Google Drive ou iCloud, Claude vous le signale : ce qui y est supprimé l'est aussi en ligne. Il peut vous proposer un dossier local à la place :
- Windows : `C:\Users\<nom>\Claude\<Dossier>` ;
- Mac : `~/Claude/<Dossier>` (`~` désigne votre dossier personnel).

Lancement seul : si vous acceptez, Claude crée ce dossier. Ouvrez alors une nouvelle session dans ce dossier (section 4, étapes 1 à 3), tapez `/archi` pour vérifier que le plugin y est proposé, puis tapez la phrase qu'il vous donne. S'il n'est pas proposé, le plugin a été installé pour l'ancien dossier seulement : installez-le pour votre compte utilisateur (section 2), puis ouvrez encore une nouvelle session dans le nouveau dossier. Pendant l'entretien, ce choix se fait au début, après la lecture de votre dossier : Claude s'arrête, vous créez le dossier local, puis vous relancez `/architecte-consignes` dans une session ouverte dedans. Une fois les consignes écrites, le dossier ne change plus ; Claude vous propose de rendre le dossier disponible hors connexion et note le passage à un dossier local « à confirmer ».

### Ce que vous faites vous-même

Claude ne fait jamais ces gestes à votre place :

- **Choisir** les dossiers à récupérer, leur destination et le compte à utiliser.
- **Vous connecter**, saisir un mot de passe, accepter des conditions.
- **Ouvrir votre dossier dans Obsidian.** Lancez Obsidian une fois, sans créer de coffre, puis fermez-le. Dans la fenêtre que Claude ouvre ensuite, cliquez sur **Open** en face de **Open folder as vault**, choisissez le dossier dont Claude vous donne le chemin (votre dossier de travail, ou le coffre Obsidian existant que vous avez choisi de garder) et validez. Pour aller au dossier dans la fenêtre de choix :
  - Windows : tapez le chemin du dossier dans la barre d'adresse de la fenêtre, appuyez sur Entrée, puis cliquez sur le bouton de validation (libellé à vérifier à l'écran) ;
  - Mac : Cmd + Maj + G, tapez le chemin du dossier, Retour, puis **Ouvrir**.
- **Connecter vos comptes sur claude.ai.** Dans l'application : **Customize**, puis **Connectors** (ou **Plugins**, selon la version). Sur le web : https://claude.ai/customize/connectors. Choisissez le service : Gmail, Google Drive, ou Microsoft 365 (pour Outlook et OneDrive). Cliquez sur **Connect** (selon la version : **Connect to Claude**, ou **Add**), puis connectez-vous dans la page qui s'ouvre. Lisez les autorisations demandées avant de les accepter. Un compte Microsoft personnel (Outlook.com, Hotmail) se connecte seulement sur le site claude.ai, et seulement avec une offre Pro, Max ou Ultra ; Team et Enterprise n'acceptent que les comptes professionnels.
- **Régler les permissions d'outils.** Sur la page du connecteur, rubrique **Tool permissions**, mettez sur **Blocked** les outils que Claude vous indique : envoyer, répondre, transférer ; mettre à la corbeille, partager, déplacer. Avec Microsoft 365, aussi les réponses automatiques, les règles de boîte et, avec un compte professionnel, Teams. Pour l'agenda (créer, modifier ou supprimer un événement, répondre à une invitation), choisissez **Always ask** si l'option existe, sinon **Blocked** : une invitation peut prévenir d'autres personnes. Laissez les brouillons autorisés : ne bloquez pas tout le groupe d'écriture d'un coup. Sur Team ou Enterprise, le propriétaire du compte peut les avoir réglés pour tous ; un membre ne peut pas passer outre.
- **Installer Claude in Chrome :**
  1. dans Chrome, créez un profil réservé au travail avec Claude : icône de profil en haut à droite, puis **Ajouter un profil Chrome**. Ne vous y connectez ni à votre messagerie, ni à votre banque, ni à des services de santé ou d'impôts, ni à un gestionnaire de mots de passe ;
  2. dans ce profil, ouvrez le Chrome Web Store et ajoutez l'extension **Claude** publiée par Anthropic (**Ajouter à Chrome**) ;
  3. connectez-vous avec le même compte que l'application, puis épinglez l'extension (icône en forme de pièce de puzzle) ;
  4. dans Chrome, cliquez sur l'icône Claude pour ouvrir le panneau latéral. Ouvrez le menu déroulant de la zone de saisie et choisissez **Approuver manuellement** (Manually approve) : le mode automatique est celui par défaut. N'accordez jamais **Toujours autoriser les actions sur ce site** (Always allow actions on this site) à un site de messagerie ou de banque.
- **Rendre vos dossiers disponibles hors connexion** avant la copie (voir plus bas).
- **Répondre à chaque demande d'autorisation** de Claude Code. Ne choisissez une option « toujours » ou « pour cette session » que par une décision consciente.
- **Vérifier, puis supprimer vous-même** le brouillon d'essai créé dans votre messagerie.

### Ce que Claude fait

- Il relève, sans rien modifier : votre système, l'emplacement du dossier, Obsidian, les connecteurs déjà branchés, vos réglages existants.
- À votre accord sur le plan, il crée un brouillon `_entretien-environnement.md`, qui garde l'avancement pour reprendre après une interruption.
- **Obsidian** : il vérifie s'il est installé, puis vous propose de l'installer. Sous Windows, il utilise winget, l'outil d'installation de Microsoft. Sur Mac, il utilise Homebrew seulement s'il est déjà installé. Si winget vous demande d'accepter des conditions, Claude vous donne la commande à taper vous-même dans Terminal (menu Démarrer, tapez Terminal). Si winget ou Homebrew manque ou échoue, vous téléchargez Obsidian vous-même sur https://obsidian.md/download. Il ouvre ensuite la fenêtre des coffres d'Obsidian, crée une note d'essai et une note `Accueil.md` qui liste vos dossiers et leur rôle.
- **Copie** : il copie vos dossiers par lots, puis vérifie chaque fichier (voir plus bas).
- **Réglages** : il garde une copie de votre ancien `.claude/settings.json`, puis y ajoute, sans rien retirer :
  - le blocage de l'envoi, de la réponse et du transfert par le connecteur de messagerie ;
  - le blocage de la mise à la corbeille, du partage, du déplacement et du renommage par le connecteur de stockage, et une confirmation avant d'y créer ou d'y copier un fichier (pas encore essayée dans l'onglet Code : on ne sait pas encore si la demande d'autorisation s'y affiche) ;
  - le blocage de l'outil de Claude in Chrome qui exécute du code dans une page, et une règle de confirmation sur les outils qui remplissent un formulaire, envoient un fichier sur une page ou enchaînent plusieurs actions (effet pas encore essayé) ;
  - une confirmation avant de modifier les réglages d'Obsidian (dossier `.obsidian`), seulement si votre dossier de travail est lui-même le coffre ; pas encore essayée elle non plus : un test de la fin la vérifie.
- Claude Code vous demande l'autorisation d'écrire dans `.claude/settings.json`. Acceptez-la, sans choisir l'option qui autorise tout le dossier `.claude` pour la session.
- Il vous montre les lignes à ajouter au `CLAUDE.md`, puis les écrit après votre accord.
- En mode **Manual**, chaque commande qui modifie votre ordinateur vous est soumise par une demande d'autorisation. Claude n'ajoute jamais d'option qui accepte des conditions à votre place, n'utilise jamais `sudo` (la commande qui donne les droits d'administrateur sur Mac), n'installe pas Homebrew et ne touche pas aux réglages de sécurité de votre ordinateur.

### La copie, jamais le déplacement

Claude récupère vos dossiers Google Drive ou OneDrive par **copie**. Il ne déplace rien et ne supprime rien, ni dans la source, ni dans la destination. Il n'écrase jamais un fichier déjà présent sans votre accord.

Pourquoi : sortir un fichier du dossier Google Drive met sa version en ligne à la corbeille (documenté sur Mac). Sortir du dossier OneDrive un fichier présent seulement en ligne le retire de OneDrive (documenté sur Mac). Une copie laisse l'original en place.

1. Vous rendez d'abord le dossier disponible hors connexion, puis vous attendez la fin du téléchargement. Dans l'Explorateur de fichiers (Windows) ou le Finder (Mac), faites un clic droit sur le dossier (Mac : Ctrl + clic, ou deux doigts sur le pavé tactile) :
   - OneDrive : « Toujours conserver sur cet appareil », puis attendez le rond vert plein (sur Mac, libellé à vérifier à l'écran) ;
   - Google Drive : « Available offline » (libellé français : non documenté, à vérifier à l'écran).
2. Claude copie par lots, après votre accord sur la source et la destination. Chaque lot va dans un dossier neuf : Claude vérifie d'abord qu'il n'existe pas. Sa commande n'écrase jamais un fichier déjà copié, et se relance sans risque après une interruption :
   - Windows : `robocopy` ;
   - Mac : `cp -Rn`.
3. Il vérifie chaque fichier par son **empreinte** : un code calculé à partir du contenu du fichier. Deux fichiers identiques ont la même empreinte. Un fichier différent ou manquant se recopie, avec votre accord. Si un fichier ne peut pas être lu (ouvert dans une autre application, par exemple), le contrôle s'arrête et le lot reste « non vérifié » : fermez le fichier, puis Claude recommence.
4. Les fichiers Google Docs, Sheets et Slides (`.gdoc`, `.gsheet`, `.gslides`) ne sont que des liens vers le web. Claude les signale : vous les exportez vous-même depuis Drive sur le web, par exemple en Word ou en PDF. Claude ne suit pas un raccourci sans votre choix.

### Tester, puis finir

Les réglages se lisent au démarrage d'une session. Claude vous demande donc d'ouvrir **une seule nouvelle session** pour tous les tests (une de plus si vous changez de dossier de travail). Avant, il note l'avancement dans son brouillon et vous donne le geste exact :
- onglet Code : nouvelle session, sur le même dossier ;
- terminal : dans le dossier, tapez `claude --permission-mode default` (`claude --chrome --permission-mode default` si les tests comprennent Chrome).

Avant, il prépare aussi avec vous **la question de la pièce** : vous choisissez un document de votre dossier, de préférence un document qui existe en plusieurs versions (un devis et sa version définitive, par exemple), sans lui donner son chemin, son numéro ni son montant. Gardez-la en tête : elle n'est écrite nulle part.

Dans la nouvelle session :
1. **Premier message** : posez cette question, avant toute autre demande. Par exemple : « Où est la version définitive du devis [objet] ? Donnez le fichier, puis le chemin suivi pour le trouver. » Vérifiez la réponse : le bon document, la bonne version, et un chemin qui part de la note d'accueil (`Accueil.md`, ou celle du coffre Obsidian que vous avez gardé, dont Claude vous a donné le chemin). Un nouvel assistant, qui ne connaît pas encore votre entretien, montre ainsi que l'accueil lui suffit.
2. Tapez ensuite la phrase que Claude vous a donnée, par exemple `/architecte-consignes:environnement-de-base`, puis « reprendre », et donnez-lui le résultat du point 1.

Selon les éléments installés, les autres tests sont les suivants. Rien n'est envoyé, même pour un essai.
- Claude liste ses outils : l'envoi, la réponse et le transfert n'y figurent plus ; l'outil de brouillon, si.
- Il crée un vrai brouillon, sans destinataire, avec l'objet « Essai Claude — à supprimer ». Vous le vérifiez dans vos brouillons, puis vous le supprimez vous-même.
- Il cherche un document précis dans Drive ou OneDrive.
- Il ouvre la page neutre https://example.com dans un nouvel onglet de son groupe d'onglets Chrome.
- La note d'essai apparaît dans Obsidian.
- Si la confirmation sur `.obsidian` est posée, passez en mode **Accept edits** (sélecteur sous la zone de saisie). Claude crée d'abord un fichier témoin, `temoin-claude-` suivi de la date et de l'heure, sans demande. Puis il essaie de créer un fichier d'essai dans `.obsidian` : une demande d'autorisation doit s'afficher ; refusez-la, sans choisir d'option valable pour toute la session. Revenez ensuite en mode **Manual** et supprimez le fichier témoin dans l'Explorateur ou le Finder.
- Chaque fichier d'essai porte la date et l'heure dans son nom, et Claude vérifie avant de le créer qu'aucun fichier ne porte déjà ce nom. À la fin, il ne vous propose de supprimer que ces fichiers-là, jamais un de vos documents.
- Il compare les empreintes de la copie.

À la fin, Claude vous remet un récapitulatif :
- ce qui est bloqué par les réglages de Claude Code ;
- ce qui vous demande une autorisation avant d'agir (confirmation) ;
- où se trouvent votre coffre Obsidian et sa note d'accueil ;
- ce que vous avez réglé sur claude.ai ;
- ce qui reste une consigne ;
- ce qui reste « à confirmer ».

Il vous propose ensuite de supprimer, d'archiver ou de garder son brouillon. S'il n'y a pas encore de `CLAUDE.md`, il vous propose `/architecte-consignes` pour ranger votre dossier.

### Ce que ces réglages ne garantissent pas

- Aucun réglage n'est une garantie complète. Chacun a ses limites, que Claude vous dit.
- « Brouillons seulement » vaut pour le connecteur de messagerie, dans Claude Code. Avec Claude in Chrome, Claude pourrait ouvrir votre messagerie dans le navigateur : là, l'interdiction d'envoyer reste une consigne. Choisissez l'approbation manuelle dans l'extension.
- Le réglage **Blocked** que vous posez vous-même sur claude.ai est documenté pour l'onglet Chat et pour Cowork ; son effet dans l'onglet Code ne l'est pas (seul celui posé par une organisation l'est). C'est pourquoi Claude pose aussi un blocage dans les réglages du dossier.
- Le blocage de l'outil qui exécute du code dans une page ne bloque pas toute action dans le navigateur : Claude peut toujours y cliquer et y taper, y compris dans un formulaire, sans règle de confirmation.
- Les réglages du dossier valent dans une session ouverte sur ce dossier, dans l'onglet Code ou le terminal. Cowork n'est pas couvert.
- Les blocages ont été essayés une fois, le 25/11/2026, dans l'onglet Code sous Windows : envoi, réponse et transfert de Gmail ; mise à la corbeille de Google Drive ; outil de Chrome qui exécute du code. Pas encore essayés : le Mac, le terminal, Cowork, Outlook et OneDrive, le partage et le déplacement dans Drive, les confirmations, la création réelle d'un brouillon, et le déroulé complet (installation d'Obsidian, copie, connexion des comptes).

## 7. À la fin

Votre dossier contient au moins :
- **`CLAUDE.md`** : vos consignes, que Claude lira à chaque session ;
- **`.claude/settings.json`** : les réglages que Claude Code applique lui-même (ce qui est bloqué, ce qui demande votre autorisation).

Selon le plan validé, d'autres fichiers s'y ajoutent, par exemple des fichiers de consignes complémentaires. À la fin, Claude vous propose de supprimer, d'archiver ou de garder le brouillon.

Si vous avez préparé l'environnement de base, s'y ajoutent aussi, selon vos choix :
- la note `Accueil.md` et le dossier `.obsidian` (les réglages d'Obsidian) ;
- vos dossiers copiés, et le dossier `_copies` (journaux de copie et provenance des dossiers copiés) ;
- si vous aviez déjà des réglages, leur copie de sauvegarde `settings.ancien-AAAA-MM-JJ.json`, à la racine ;
- le brouillon `_entretien-environnement.md`, tant que vous le gardez.

Pour voir le dossier `.claude` :
- **Mac** : il est masqué. Dans le Finder, appuyez sur **Cmd + Maj + .** (point) ; le même geste le masque de nouveau. `.obsidian` est masqué comme `.claude` (même geste).
- **Windows** : il est visible normalement dans l'Explorateur de fichiers.

**Vérifiez le résultat.** Ouvrez une nouvelle session dans le même dossier et posez les questions de test que Claude vous a données. Il les appelle « questions de recette ». Les bonnes réponses montrent que vos consignes sont bien suivies.

## 8. Mettre à jour ou désinstaller

- **Depuis l'application** (page **Plugins**) :
  - mettre à jour : sur la marketplace **architecte-consignes**, cliquez sur **Check for updates**, ou activez **Sync automatically** ;
  - désinstaller : ouvrez **architecte-consignes**, ouvrez son menu, puis choisissez **Remove**. Pour le couper sans le retirer, choisissez **Disable plugin**.
- **Avec le terminal**, seulement si vous l'avez installé avec le terminal :

  ```text
  claude plugin update architecte-consignes@architecte-consignes
  claude plugin uninstall architecte-consignes@architecte-consignes
  ```

Après une mise à jour, ouvrez une nouvelle session.

## 9. En cas de souci

| Ce que vous voyez | Que faire |
|---|---|
| Vous ne trouvez ni **Plugins** ni **Customize** dans la barre latérale | Mettez l'application à jour (https://claude.ai/download). Sur un compte Team ou Enterprise, demandez au propriétaire du compte d'activer les plugins. |
| `/architecte-consignes` n'est pas reconnu | Ouvrez une nouvelle session de l'onglet Code et essayez `/architecte-consignes:architecte-consignes`. Sinon, mettez l'application à jour, ou installez le plugin avec le terminal (section 2). |
| `/architecte-consignes:environnement-de-base` n'est pas reconnu | Votre plugin date d'avant la version 1.2.0 : mettez-le à jour (section 8), puis ouvrez une nouvelle session. Ou bien il a été installé pour un autre dossier seulement : installez-le pour votre compte utilisateur (section 2), puis ouvrez une nouvelle session. |
| L'application refuse d'ouvrir le dossier | Vérifiez que le dossier existe toujours et que vous avez le droit d'y écrire. Choisissez-le de nouveau, ou redémarrez l'application. Si l'application vous demande si vous faites confiance au dossier, acceptez. |
| Claude dit qu'il ne peut pas créer les fichiers | Vous êtes sans doute dans l'onglet **Chat** ou sur le site claude.ai. Passez à l'onglet **Code**. |
| Claude s'arrête sur une demande d'autorisation | C'est normal : c'est une confirmation. Lisez l'action, puis acceptez ou refusez. |
| La fenêtre des coffres d'Obsidian ne s'ouvre pas | Lancez Obsidian une fois, fermez-le, puis demandez à Claude de recommencer. Sinon, ouvrez Obsidian vous-même : sans coffre ouvert, son écran d'accueil propose **Open folder as vault** ; si un coffre est déjà ouvert, cliquez sur son nom en bas à gauche, puis sur **Manage vaults…** (à vérifier à l'écran). |
| Claude ne voit ni votre messagerie, ni votre stockage, ni Chrome | Vérifiez la connexion sur claude.ai (**Customize**, puis **Connectors**), et que le connecteur est activé par le bouton « + » de la zone de saisie. Pour Chrome, vérifiez que l'extension est activée (page `chrome://extensions`) et connectée au même compte et à la même organisation que l'application. Puis quittez Chrome, quittez complètement l'application (Mac : Cmd + Q ; Windows : si elle reste ouverte, Gestionnaire des tâches, Ctrl + Maj + Échap), relancez Chrome puis l'application, et ouvrez une nouvelle session. |
| Google affiche « Access blocked » à la connexion | Votre compte professionnel attend l'accord de l'administrateur de votre organisation. Transmettez-lui ce message. |
| Vous aviez déjà copié une ancienne version (un « skill ») dans votre ordinateur | Supprimez le dossier `architecte-consignes` de `.claude/skills/`, dans votre dossier personnel et, s'il y en a un, dans votre dossier de travail. Sinon, `/architecte-consignes` lance l'ancienne copie ; le plugin reste accessible par `/architecte-consignes:architecte-consignes`. |

Pour ouvrir le dossier personnel de Claude :
- **Windows** : tapez `%USERPROFILE%\.claude` dans la barre d'adresse de l'Explorateur ;
- **Mac** : dans le Finder, menu **Aller**, puis **Aller au dossier** (Cmd + Maj + G), et tapez `~/.claude`.

## Windows et Mac en un coup d'œil

| Pour… | Windows | Mac |
|---|---|---|
| Copier, puis coller | Ctrl + C, puis Ctrl + V | Cmd + C, puis Cmd + V |
| Valider | Entrée | Retour ↩ |
| Ouvrir un terminal | PowerShell (menu Démarrer) | Terminal (Applications, puis Utilitaires) |
| Voir le dossier `.claude` | Visible sans réglage | Finder, Cmd + Maj + . |
| Ouvrir le dossier personnel de Claude | Barre d'adresse de l'Explorateur : `%USERPROFILE%\.claude` | Finder, Aller, Aller au dossier (Cmd + Maj + G) : `~/.claude` |
| Mettre l'application à jour | Menu Help, puis Check for Updates… | Menu Claude, puis Check for Updates… |
| Quitter complètement l'application | Si elle reste ouverte : Gestionnaire des tâches (Ctrl + Maj + Échap) | Cmd + Q |
| Installer Obsidian vous-même | Fichier `.exe` sur obsidian.md/download, puis suivez l'assistant | Fichier `.dmg` sur obsidian.md/download, puis glissez Obsidian dans Applications |

Projet indépendant, non affilié à Anthropic. Licence MIT.
