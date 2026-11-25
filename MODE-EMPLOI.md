# Mode d'emploi : Architecte consignes

Ce plugin vous aide à créer, avec Claude, le fichier de consignes de votre dossier de travail (`CLAUDE.md`), et à ranger ce dossier proprement. Claude vous pose quelques questions et vous montre un plan. Il n'écrit rien sans votre accord, à part un brouillon qui garde vos réponses.

Ce mode d'emploi vaut pour Windows et pour Mac. Quand un geste diffère, les deux sont indiqués. Les menus sont cités sous leur nom anglais : si votre application est en français, cherchez l'équivalent (Customize : Personnaliser ; Settings : Réglages). Leurs noms peuvent aussi changer d'une version à l'autre.

## 1. Ce qu'il vous faut

- **Un compte Claude avec un abonnement payant** : Pro, Max, Ultra, Team ou Enterprise. L'onglet Code n'est pas ouvert à l'offre gratuite. Sur Team ou Enterprise, votre organisation peut interdire l'ajout de plugins : si l'application refuse l'adresse du plugin, adressez-vous à son administrateur.
- **L'application de bureau Claude**, à jour, sur Windows ou sur Mac. Vous la téléchargez sur https://claude.ai/download.
- **Un dossier de travail** : le vôtre, ou une copie pour un premier essai.

Le plugin travaille directement dans votre dossier : il le lit, puis y crée des fichiers. Utilisez-le donc dans l'**onglet Code** de l'application (on l'appelle aussi « Claude Code ») : c'est là qu'il a été essayé. **Cowork**, un autre onglet de l'application, devrait aussi convenir, mais n'a pas encore été essayé. Dans l'onglet **Chat**, ou sur le site claude.ai, Claude n'a pas accès à vos dossiers : il ne pourrait que vous donner le texte des fichiers à créer vous-même.

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

5. Ouvrez l'onglet **Discover** : le plugin y apparaît avec les autres. Choisissez **architecte-consignes**, puis cliquez sur **Add** (ou **Install**, selon la version).

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

3. Le message « Successfully installed plugin » confirme l'installation. Ouvrez alors une nouvelle session dans l'onglet Code.

Si le terminal répond que `claude` est introuvable ou n'est pas reconnu, utilisez la méthode depuis l'application.

## 3. Préparer votre dossier

1. Faites une **copie de sauvegarde** de votre dossier, par exemple sur une clé USB ou dans un autre dossier.
2. **Retirez de votre dossier de travail les fichiers sensibles** (mots de passe, codes bancaires, données personnelles de vos clients) et rangez-les ailleurs. Claude cherche à repérer un tel fichier sans l'ouvrir, mais ce n'est pas une garantie.

## 4. Lancer l'entretien

1. Dans l'application, ouvrez l'**onglet Code** (à côté de **Chat** et de **Cowork**), puis démarrez une **nouvelle session**.
2. Sous la zone de saisie, choisissez l'environnement **Local**. Cliquez ensuite sur le choix du dossier, juste à côté, puis sur **Open folder…**. Sélectionnez votre dossier de travail lui-même, pas l'un de ses sous-dossiers. Si l'application vous demande si vous faites confiance à ce dossier, acceptez.
3. Sur la même ligne, choisissez le mode de permission **Manual** (**Ask permissions** sur une version plus ancienne) : Claude vous demande votre accord avant de modifier un fichier ou de lancer une commande.
4. Tapez :

   ```text
   /architecte-consignes
   ```

   puis validez. Si rien ne se passe, ou si une ancienne version se lance, tapez plutôt `/architecte-consignes:architecte-consignes`. Vous pouvez aussi écrire simplement : « Crée le CLAUDE.md de ce dossier ».
5. Répondez aux questions. Pour aller vite, choisissez la **version minimale** : environ 15 minutes. La version complète prend de 30 à 60 minutes.

## 5. Pendant l'entretien : trois mots à connaître

- **Bloqué** : Claude Code refuse l'action, même si vous la demandez. Si vous en avez besoin, vous la faites vous-même.
- **Confirmation** : avant chaque action de ce type, Claude s'arrête et vous affiche une demande d'autorisation, avec des boutons pour accepter ou refuser. C'est ce que le plugin propose par défaut pour supprimer, déplacer ou renommer un fichier.
- **Consigne** : Claude s'engage à la suivre, mais sans garantie.

Claude vous montre le plan de fichiers avant de créer vos consignes. Seule exception : un brouillon, `_entretien-claude-md.md`, qui garde vos réponses pour reprendre après une interruption. Lisez le plan, puis répondez « oui » ou demandez une correction.

## 6. À la fin

Votre dossier contient au moins :
- **`CLAUDE.md`** : vos consignes, que Claude lira à chaque session ;
- **`.claude/settings.json`** : les réglages que Claude Code applique lui-même (ce qui est bloqué, ce qui demande votre autorisation).

Selon le plan validé, d'autres fichiers s'y ajoutent, par exemple des fichiers de consignes complémentaires. À la fin, Claude vous propose de supprimer, d'archiver ou de garder le brouillon.

Pour voir le dossier `.claude` :
- **Mac** : il est masqué. Dans le Finder, appuyez sur **Cmd + Maj + .** (point) ; le même geste le masque de nouveau.
- **Windows** : il est visible normalement dans l'Explorateur de fichiers.

**Vérifiez le résultat.** Ouvrez une nouvelle session dans le même dossier et posez les questions de test que Claude vous a données. Il les appelle « questions de recette ». Les bonnes réponses montrent que vos consignes sont bien suivies.

## 7. Mettre à jour ou désinstaller

- **Depuis l'application** (page **Plugins**) :
  - mettre à jour : sur la marketplace **architecte-consignes**, cliquez sur **Check for updates**, ou activez **Sync automatically** ;
  - désinstaller : ouvrez **architecte-consignes**, ouvrez son menu, puis choisissez **Remove**. Pour le couper sans le retirer, choisissez **Disable plugin**.
- **Avec le terminal**, seulement si vous l'avez installé avec le terminal :

  ```text
  claude plugin update architecte-consignes@architecte-consignes
  claude plugin uninstall architecte-consignes@architecte-consignes
  ```

Après une mise à jour, ouvrez une nouvelle session.

## 8. En cas de souci

| Ce que vous voyez | Que faire |
|---|---|
| Vous ne trouvez ni **Plugins** ni **Customize** dans la barre latérale | Mettez l'application à jour (https://claude.ai/download). Sur un compte Team ou Enterprise, demandez au propriétaire du compte d'activer les plugins. |
| `/architecte-consignes` n'est pas reconnu | Ouvrez une nouvelle session de l'onglet Code et essayez `/architecte-consignes:architecte-consignes`. Sinon, mettez l'application à jour, ou installez le plugin avec le terminal (section 2). |
| L'application refuse d'ouvrir le dossier | Vérifiez que le dossier existe toujours et que vous avez le droit d'y écrire. Choisissez-le de nouveau, ou redémarrez l'application. Si l'application vous demande si vous faites confiance au dossier, acceptez. |
| Claude dit qu'il ne peut pas créer les fichiers | Vous êtes sans doute dans l'onglet **Chat** ou sur le site claude.ai. Passez à l'onglet **Code**. |
| Claude s'arrête sur une demande d'autorisation | C'est normal : c'est une confirmation. Lisez l'action, puis acceptez ou refusez. |
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

Projet indépendant, non affilié à Anthropic. Licence MIT.
