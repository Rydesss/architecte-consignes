# Messagerie en brouillons seulement (Gmail, Outlook)

Référence de l'étape 6 du skill `environnement-de-base`, à lire quand le participant a choisi la messagerie à l'étape 0 : connecter Gmail ou Outlook pour que Claude prépare des brouillons, sans pouvoir envoyer, répondre ni transférer par le connecteur.

Deux protections : le réglage « Blocked » sur claude.ai, posé par le participant ; des règles deny dans le `.claude/settings.json` du dossier, écrites à l'étape 9 et testées à l'étape 10. Claude ne se connecte à aucun compte, ne saisit aucun mot de passe, n'accepte aucune condition et n'envoie aucun message, même pour un essai (E4). Il n'ouvre ni ne pilote, avec Claude in Chrome ou le navigateur intégré, les pages de connexion, les pages de réglages (claude.ai, extension) ni la boîte du participant : il dit où cliquer, et le participant agit.

Les libellés d'interface sont écrits en anglais, tels que les sources les citent ; sauf mention contraire, leur libellé français est non documenté, à vérifier à l'écran (E7).

## Rôles

| Action | Claude (C) ou participant (U) | Pourquoi |
|---|---|---|
| Reprendre les réponses de l'étape 0 : service, offre, compte personnel ou professionnel | C | Toute la suite en dépend. |
| Se connecter à Google ou Microsoft, accepter les autorisations demandées | U | Cela engage le compte du participant. |
| Obtenir l'accord d'un administrateur (compte professionnel) | U | Claude ne contacte personne. |
| Régler les outils un par un sur claude.ai (en Team ou Enterprise : le propriétaire) | U | Réglage du compte en ligne : Claude guide, sans agir. |
| Relever les outils de messagerie de sa liste | C | Lecture seule ; aucun outil de messagerie appelé. |
| Préparer les règles deny, puis les écrire à l'étape 9 | C (après accord) | Fichier local du dossier de travail. |
| Choisir « Manual », et non « Auto », dans le sélecteur de mode sous la zone de saisie | U | Réglage de la session du participant. |
| Régler l'extension Claude in Chrome | U | Réglage du navigateur du participant. |
| Ouvrir la nouvelle session de l'étape 10 | U | Les règles se vérifient dans une nouvelle session. |
| Créer le brouillon d'essai, sans destinataire | C (après accord) | Il ne peut partir chez personne. |
| Vérifier le brouillon dans la boîte, puis le supprimer | U | C'est la boîte du participant. |
| Écrire la ligne du `CLAUDE.md` | C (après accord) | Étape 9 du skill. |

## Pas à pas

Au plan de l'étape 2, ce volet compte : la connexion et les réglages sur claude.ai (U), les règles deny (C, étape 9), le test (étape 10). Avec Microsoft 365, y ajouter OneDrive (`references/stockage.md`, partie C) et l'agenda Outlook (point 7 ci-dessous).

1. (C) Annoncer : « Je vais vous aider à connecter votre messagerie pour que je prépare des brouillons ; l'envoi par ce connecteur sera bloqué. Vous vous connectez vous-même : je ne vois pas votre mot de passe, et je n'envoie aucun message, même pour un essai. »
2. (C) Reprendre les réponses de l'étape 0 et ne demander que ce qui manque : Gmail ou Outlook ; offre Claude ; compte personnel ou professionnel.
   - L'onglet Code exige une offre payante : Pro, Max, Ultra, Team ou Enterprise.
   - Microsoft : un compte personnel (Outlook.com, Hotmail, Live, MSN) n'est accepté qu'en Free, Pro, Max ou Ultra ; Team et Enterprise n'acceptent que des comptes professionnels ; un seul compte Microsoft à la fois.
   - Team ou Enterprise : le propriétaire de l'organisation Claude active d'abord le connecteur.
   - Microsoft, compte professionnel : un administrateur global Entra (la personne qui gère les comptes Microsoft de l'entreprise) donne un consentement unique pour l'organisation, même en Pro ou Max. L'écriture, brouillons compris, est désactivée par défaut : elle demande l'accord de cet administrateur, puis, en Team ou Enterprise, son activation dans Organization settings > Connectors.
   - Google Workspace (comptes Google gérés par une entreprise) : le message « Access blocked » veut dire que l'administrateur doit approuver Claude (« Trusted »).
   - À dire : « Avec un compte professionnel, votre administrateur devra peut-être donner son accord. Je ne peux pas le faire à votre place. »
   - Si le participant gère lui-même les comptes Microsoft de l'entreprise, à dire : « Si vous êtes vous-même l'administrateur de vos comptes Microsoft, la fenêtre de connexion peut vous demander d'accepter pour toute l'organisation. Cet accord vaut pour tous les comptes de l'entreprise, pas seulement pour le vôtre : lisez-le, et ne l'acceptez que si c'est votre décision. » Libellé exact de cette fenêtre : non documenté, à vérifier à l'écran.
3. (C) Reprendre le relevé de l'étape 1, en lecture seule :
   - outils de sa liste dont le nom contient `send_message`, `reply`, `forward`, `draft`, `outlook_` ou `teams_`, recopiés en entier (`mcp__<identifiant>__<outil>`), et un outil de lecture (`search_threads` pour Gmail, `outlook_email_search` pour Outlook), qui montre que le connecteur est chargé ;
   - `mcp__ccd_session_mgmt__send_message`, la messagerie entre les sessions de l'utilisateur, s'il existe : il sert de témoin à l'étape 10 ;
   - une règle de `.claude/settings.json` qui bloque déjà tout le serveur de messagerie : voir « Réglages », dernier point.
   - Messagerie déjà connectée : passer au point 5. Sinon, faire le point 4, puis refaire ce relevé : l'arrivée des outils dans la session en cours est non documentée, à vérifier dans l'application. S'ils manquent encore, les relever à l'étape 10. Dans tous les cas, noter au brouillon, avant le point 6, si les outils d'envoi sont visibles.
4. (U) Connecter la messagerie sur claude.ai, pas depuis Claude Code : Gmail et Microsoft 365 n'acceptent pas la connexion locale depuis Claude Code.
   - Sur le web : ouvrir `https://claude.ai/customize/connectors`, choisir Gmail ou Microsoft 365, cliquer sur Connect (ou Add), se connecter au compte.
   - Application de bureau, même chemin sous Windows et macOS : barre latérale, Customize, puis Connectors (ou Plugins) ; interface en français, d'après l'aide en français : initiales du participant en bas à gauche, puis Paramètres > Personnaliser > Connecteurs. La page de connexion s'ouvre dans le navigateur.
   - Compte Microsoft personnel : seulement sur le web, à l'adresse ci-dessus.
   - À dire : « Connectez-vous vous-même, et lisez les autorisations demandées avant de les accepter. »
   - Microsoft 365, à dire aussi : « En connectant Microsoft 365, vous donnez aussi accès à OneDrive et à votre agenda : nous allons régler les deux. »
5. (C) Avant le réglage, expliquer pourquoi « Needs approval » ne suffit pas : « Dans la conversation de claude.ai et dans Cowork (le mode de l'application où Claude travaille dans les dossiers que vous lui confiez), en mode Auto, c'est-à-dire quand Claude agit sans vous demander à chaque étape, un outil réglé sur “Needs approval” s'exécute sans vous demander, sauf si un contrôle automatique juge l'action risquée. “Blocked” est refusé dans tous les modes. » Le mode Auto est en cours de déploiement comme défaut sur Pro, Max, Ultra et Team ; Manual reste le défaut sur Enterprise.
6. (U) Régler les outils un par un : page du connecteur, onglet Permissions, rubrique Tool permissions. Libellés : « Always allow », « Needs approval », « Blocked » et, chez certains, « Always ask » ; repérer le réglage par sa place, dans l'onglet des autorisations de la page du connecteur. Forme du nom de chaque outil à l'écran (nom technique ou phrase) : non documentée, à vérifier dans l'application. Ne pas bloquer tout le groupe d'écriture : les brouillons seraient bloqués aussi.
   - Gmail : `send_message`, `reply`, `forward` sur « Blocked » ; `create_draft` et `update_draft` sur « Needs approval » ou « Always allow ». En option : `trash_message` et `trash_thread` sur « Blocked » ou « Always ask ».
   - Microsoft 365 : `outlook_send_mail`, `outlook_forward_mail` et `outlook_send_draft` sur « Blocked » ; compte professionnel : aussi `outlook_set_vacation` (réponse automatique), `outlook_create_filter` (règle de boîte), `teams_send_chat_message`, `teams_send_channel_message`, `teams_reply_channel_message` et `teams_create_chat`. `outlook_create_draft` et `outlook_create_reply_draft` autorisés. En option : `outlook_trash_thread` et `outlook_batch_delete_messages` sur « Blocked ».
   - Microsoft 365 apporte aussi OneDrive : régler la suppression, le déplacement, le renommage, la modification et le partage selon `references/stockage.md`, partie C, même si le stockage connecté n'a pas été choisi.
   - Compte Microsoft personnel : les outils d'écriture, OneDrive compris, sont actifs dès la connexion ; ce réglage est donc indispensable.
   - Team ou Enterprise : le propriétaire de l'organisation règle ces outils (Organization settings > Connectors > onglet Tools), et un membre ne peut pas passer outre. Si le participant n'est pas propriétaire : (U) lui demander de mettre les outils d'envoi sur « Blocked » et de laisser les brouillons autorisés ; (C) en attendant, noter « réglage claude.ai à confirmer ». Les règles du dossier de l'étape 9 se posent quand même.
   - « Always ask » est en déploiement progressif : il peut manquer, et un « Always allow » accordé depuis une conversation l'emporte sur lui.
7. (U) Agendas, obligatoire avec Microsoft 365, en option avec Google Agenda : régler la création, la modification et la suppression d'événement, et la réponse aux invitations, sur « Always ask » si l'option existe, sinon sur « Blocked ». Microsoft 365 : `outlook_create_event`, `outlook_update_event`, `outlook_delete_event`, `outlook_respond_to_event`. Google Agenda : noms non publiés. À dire : « Créer un événement avec des invités ou répondre à une invitation peut prévenir d'autres personnes ; le détail n'est pas documenté. Gardez donc la main sur ces actions. Dans l'onglet Code, l'effet de ce réglage n'est pas documenté (sauf blocage par l'organisation), et aucune règle du dossier ne vise l'agenda : c'est une consigne. Gardez le mode Manual. Si une demande d'autorisation pour créer, modifier ou supprimer un événement, ou pour répondre à une invitation, apparaît sans que vous l'ayez demandé, répondez Non. » Agenda gardé en deny au passage d'un blocage entier (« Réglages », dernier point) : remplacer « aucune règle du dossier ne vise l'agenda : c'est une consigne » par « les règles de ce dossier bloqueront ces actions dans Claude Code ».
8. (C) Proposer la deuxième protection, avec les mots du kit (E5) : « Le réglage “Blocked” de claude.ai est documenté pour la conversation et Cowork ; son effet dans l'onglet Code ne l'est pas. Je vous propose de bloquer aussi l'envoi dans les réglages de ce dossier : Claude Code refusera alors ces outils, même si vous me le demandez. » Après accord, noter au brouillon les règles à poser (section « Réglages ») ; Claude les écrit à l'étape 9.
9. Claude in Chrome, si des outils `mcp__claude-in-chrome__…` figurent dans sa liste (détail : `references/chrome.md`) :
   - (C) À dire : « Dans Chrome, je pourrais ouvrir votre messagerie dans le navigateur (le webmail) et cliquer sur “Envoyer” : les réglages du connecteur ne m'en empêchent pas. Gardez le mode manuel et refusez toute action d'envoi. »
   - (U) Dans l'onglet Code, choisir « Manual » (mode manuel ; anciennes versions : « Ask permissions ») dans le sélecteur de mode, dans la rangée sous la zone de saisie, et non « Auto » (libellé français : non documenté, à vérifier à l'écran), pour toute session qui peut ouvrir le webmail : en mode Auto, quand le contrôle automatique approuve une action Chrome, l'extension peut sauter sa propre vérification par site.
   - (U) Dans l'extension, choisir « Approuver manuellement » (Manually approve) : le mode automatique est le défaut du panneau Cowork. Ne jamais accorder « Toujours autoriser les actions sur ce site » (Always allow actions on this site ; panneau Cowork : Allow all for this website) à un site de messagerie, notamment `mail.google.com`, `outlook.live.com`, `outlook.office.com`, `outlook.office365.com` et `outlook.cloud.microsoft` (nouvelle adresse d'Outlook sur le web, vers laquelle Microsoft redirige les anciennes). Effet de ce mode quand Chrome est piloté depuis l'onglet Code : non documenté, à vérifier dans l'application.
10. (C) Usage de l'ordinateur (Claude qui pilote l'écran ; onglet Code : Pro, Max ou Ultra, Windows ou macOS 14 ou plus), si des outils `mcp__computer-use__…` figurent dans sa liste (relevé de l'étape 1 ; noms observés le 25/11/2026, onglet Code, Windows) ou si le participant dit l'avoir activé ; sinon, sauter ce point. À dire : « Je n'ai pas besoin de votre application de messagerie : refusez-la-moi d'avance dans les réglages, ou refusez si je vous la demande. »
   - (U) Dans les réglages (Settings) de l'application de bureau (This computer > System, ou Capabilities), section Computer use, ajouter l'application de messagerie installée (Outlook sous Windows ; Mail ou Outlook sous macOS) à « Denied apps » : elle est refusée sans demande.
   - (U) À défaut, quand la demande d'accès à cette application s'affiche, cliquer sur « Deny » et non sur « Allow for this session ».
   - Limite : Claude peut encore agir sur une application refusée à travers une application autorisée.
11. (C) Sans outil de brouillon (compte Microsoft professionnel sans écriture activée, blocage entier gardé, écriture bloquée sur claude.ai) : écrire le texte du message dans un nouveau fichier du dossier de travail, à l'emplacement que le participant choisit, sans remplacer un fichier existant (nom proposé : `brouillon-mail-AAAA-MM-JJ.md` ; s'il existe déjà, ajouter `-2`, `-3`), puis dire : « Je ne peux pas déposer ce brouillon dans votre boîte. Je l'ai écrit dans [fichier] : copiez-le dans un nouveau message. » Noter le dépôt dans la boîte « à confirmer ».
12. (C) Noter au brouillon les règles à poser, les tests de l'étape 10, la ligne proposée pour le `CLAUDE.md` et les points « à confirmer ». Passer à l'étape suivante du skill.

## Réglages

Claude les écrit à l'étape 9 du skill (copie de l'ancien fichier, fusion sans rien retirer, chemin protégé), d'après `modeles/modele-settings-environnement.json`. Pour chaque outil d'envoi, trois règles deny :
- le nom exact relevé, `mcp__<identifiant>__<outil>` ;
- le motif en forme d'identifiant, `mcp__*-*-*-*-*__<outil>`, qui vise tout nom de serveur à quatre tirets ou plus (vérifié à l'essai 2 sur un poste Windows ; couverture d'un identifiant renouvelé : déduite, non testée) ;
- la forme du terminal, `mcp__claude_ai_*__<outil>`.

Ne jamais écrire `mcp__*__<outil>` : ce motif retire aussi `mcp__ccd_session_mgmt__send_message`, la messagerie entre les sessions de l'utilisateur (essai du 25/11/2026).

| Service | `<outil>` | Effet |
|---|---|---|
| Gmail | `send_message`, `reply`, `forward` | bloqué : envoi d'un nouveau message ou d'un brouillon existant, réponse et transfert directs |
| Outlook (Microsoft 365) | `outlook_send_mail`, `outlook_forward_mail`, `outlook_send_draft` | bloqué d'avance : envoi, transfert, envoi d'un brouillon |
| Outlook (Microsoft 365) | `outlook_set_vacation`, `outlook_create_filter` | bloqué d'avance : réponse automatique, règle de boîte (compte professionnel) |
| Teams (Microsoft 365) | `teams_send_chat_message`, `teams_send_channel_message`, `teams_reply_channel_message`, `teams_create_chat` | bloqué d'avance : message ou conversation Teams (compte professionnel) |

Exemple pour Gmail, `<identifiant>` remplacé par celui relevé :

```json
{
  "permissions": {
    "deny": [
      "mcp__<identifiant>__send_message",
      "mcp__*-*-*-*-*__send_message",
      "mcp__claude_ai_*__send_message",
      "mcp__<identifiant>__reply",
      "mcp__*-*-*-*-*__reply",
      "mcp__claude_ai_*__reply",
      "mcp__<identifiant>__forward",
      "mcp__*-*-*-*-*__forward",
      "mcp__claude_ai_*__forward"
    ]
  }
}
```

- Gmail : essais du 25/11/2026 (onglet Code, Windows). Les trois outils ont disparu de la liste ; `create_draft` et `update_draft` sont restés. Le motif vise le nom complet : `…__reply_to_board_thread` d'un autre serveur est resté. Avec les deux motifs, `mcp__ccd_session_mgmt__send_message` est resté.
- Microsoft 365 : noms tirés du guide de sécurité Microsoft 365, ni observés ni testés, aucun compte Outlook n'étant connecté aux essais. Les comparer au relevé. Compte personnel : pas de Teams, ni réponse automatique, ni règle de boîte (`outlook_set_vacation`, `outlook_create_filter` absents) ; ces règles restent alors sans effet, sans gêne.
- Microsoft 365 apporte aussi OneDrive. Poser aussi les règles `sharepoint_…` de `references/stockage.md`, partie C (deny sur la suppression, le déplacement, le renommage et le remplacement du contenu ; ask sur la création, le dépôt et la copie), même si le stockage connecté n'a pas été choisi à l'étape 0. À l'étape 9, ne pas les retirer comme règles d'un élément non installé.
- Pourquoi trois formes. Dans l'onglet Code, un connecteur est monté sous un identifiant opaque. Une règle `mcp__claude_ai_Gmail__send_message` y est ignorée (source tierce, ticket n°92787 ; l'essai a constaté le nom en identifiant, sans tester cette forme). Un identifiant peut changer (source tierce : rotations signalées, dont le ticket n°82532) : le motif en forme d'identifiant couvrirait le nouveau s'il garde la même forme (déduit, non testé). La forme du terminal doit valoir quand le participant lance `claude` dans ce dossier (déduit : outils nommés `mcp__claude_ai_<serveur>__<outil>` et motifs documentés ; non testé).
- Aucun avertissement : Claude Code ne vérifie pas les noms qui contiennent `_` ou `*`. Une faute de frappe passe donc en silence : seul le test par la liste d'outils la révèle, et seulement si l'outil était visible avant la règle.
- Effet de bord, blocage en trop possible : le motif en forme d'identifiant vise tout nom de serveur qui contient au moins quatre tirets, pas seulement un identifiant de connecteur. Un outil du même nom sur un tel serveur, ou sur un autre connecteur claude.ai en terminal, est retiré aussi. Le dire au participant. L'inverse reste possible : avec un identifiant d'une autre forme, ou un nom exact pas encore relevé, l'outil reste présent ; seul le test par la liste d'outils le montre.
- Noms exacts pas encore visibles à l'étape 9 : poser les deux motifs. À l'étape 10, relever les noms exacts et les ajouter après accord, puis relire le JSON. Si un outil d'envoi restait présent au test, refaire le test dans une nouvelle session après cet ajout.
- Brouillons et agendas : aucune règle locale, sauf les outils gardés en deny au passage d'un blocage entier (dernier point). Les agendas restent réglés sur claude.ai et par une consigne (effet d'une règle ask sur un connecteur : non testé).
- Portée : Claude Code (onglet Code, terminal), dans une session ouverte dans ce dossier, pas dans un sous-dossier. Effet dans Cowork : non documenté. Ni Claude in Chrome ni l'usage de l'ordinateur ne sont couverts ; macOS non testé. Un allow ne lève pas un deny.
- Blocage entier existant. Si `.claude/settings.json` bloque déjà tout le serveur de messagerie (`mcp__<identifiant>__*`, `mcp__<identifiant>`, `mcp__claude_ai_Gmail__*`, ou un motif plus large comme `mcp__*`), ne pas le débloquer sans un accord explicite. À dire : « Votre dossier bloque déjà toute votre messagerie : je ne peux ni la lire ni y préparer de brouillon. Passer en brouillons seulement débloquerait aussi d'autres outils de ce service, par exemple la corbeille ou l'agenda : je vous les liste avant. Voulez-vous garder ce blocage, ou passer en brouillons seulement ? »
  - Garder : ce volet s'arrête là ; Claude écrit les textes dans un fichier local (pas à pas, point 11).
  - Passer, d'abord : lister au participant les outils de ce serveur que le retrait rendrait disponibles, hors envoi et brouillons. Le blocage les retire de la liste d'outils : partir des noms ci-après, puis les vérifier au test de l'étape 10. Gmail (observés le 25/11/2026) : `trash_message`, `trash_thread`, `delete_draft`, libellés et spam. Microsoft 365 (guide de sécurité) : `outlook_trash_thread`, `outlook_batch_delete_messages`, `outlook_delete_draft`, `outlook_delete_filter` ; l'agenda (`outlook_create_event`, `outlook_update_event`, `outlook_delete_event`, `outlook_respond_to_event`) ; OneDrive (règles `sharepoint_…` ci-dessus).
  - Proposer de garder en deny, sous les trois formes, la corbeille et la suppression, et l'agenda si le participant n'en a pas besoin. Il choisit outil par outil.
  - Puis, après accord sur cette liste seulement : retirer la règle du blocage entier, poser les règles ci-dessus et celles qu'il garde, et remplacer au `CLAUDE.md` la ligne qui annonçait ce blocage. Un motif plus large (`mcp__*`) bloque aussi d'autres serveurs : le retirer les débloquerait ; le dire avant.

## Ligne pour le CLAUDE.md

Mention prise dans la table « Mentions au maître » de [architecte-consignes](../../architecte-consignes/SKILL.md), seul lieu de ces mentions. Claude montre les lignes à l'étape 9. Les consignes sans mention s'écrivent alors, après accord. Une ligne avec mention attend le test : elle s'écrit à l'étape 10, après le test et l'accord (étape 9 du skill). Sans `CLAUDE.md`, il garde les lignes pour le récapitulatif. Une ligne par service connecté et testé :
- Gmail : « Ne jamais envoyer, répondre ou transférer un e-mail avec Gmail : préparer des brouillons seulement (bloqué par les réglages pour le connecteur Gmail ; dans le navigateur, consigne). »
- Outlook, compte personnel : « Ne jamais envoyer, répondre ou transférer un e-mail avec Outlook : préparer des brouillons seulement (bloqué par les réglages pour le connecteur Outlook ; dans le navigateur, consigne). »
- Outlook, compte professionnel (`outlook_set_vacation` et `outlook_create_filter` relevés) : « Ne jamais envoyer, répondre ou transférer un e-mail avec Outlook, ni poser de réponse automatique ou de règle de boîte : préparer des brouillons seulement (bloqué par les réglages pour le connecteur Outlook ; dans le navigateur, consigne). » Avec des outils Teams relevés, ajouter « ni envoyer de message dans Teams » avant les deux-points.
- Toujours, sans mention (consigne) : « Ne jamais envoyer un e-mail par une autre voie, messagerie ouverte dans le navigateur ou application de messagerie de l'ordinateur comprises : préparer le brouillon et me laisser l'envoyer. »
- Agendas, sans mention (consigne) : « Demander mon accord avant de créer, modifier ou supprimer un événement d'agenda, ou de répondre à une invitation. »
- Repli sans outil de brouillon, sans mention (consigne) : « Écrire les e-mails à préparer dans un fichier de `[emplacement]` : je les copie moi-même dans ma messagerie. »

Jamais « aucun e-mail ne peut partir » : le navigateur et l'usage de l'ordinateur restent des voies possibles.

La mention demande quatre conditions :
1. les règles deny du service sont dans le `.claude/settings.json` du dossier, sous les trois formes : trois outils pour Gmail, neuf pour Microsoft 365 ;
2. les outils d'envoi ont été vus sous leur nom complet dans la liste d'outils avant ces règles (relevé de l'étape 1, ou pas à pas après la connexion), avec ce compte et dans cette application ;
3. le test par la liste d'outils, dans une nouvelle session ouverte dans ce dossier, montre les outils d'envoi absents et l'outil de brouillon présent ;
4. le service est connecté.

Outils d'envoi déjà absents avant les règles (retirés par l'organisation, ou réglés sur « Blocked » sur claude.ai) : leur absence au test ne prouve pas les règles du dossier. Ligne sans mention ; noter au brouillon la capacité observée (« brouillon possible, envoi absent de la liste ») et, à « À confirmer », « règles du dossier non vérifiées par la liste d'outils ». Ne jamais retirer une protection existante pour faire le test.

Un service bloqué d'avance mais pas encore connecté, ou un compte Microsoft professionnel sans écriture activée, n'est pas nommé : il va dans « à confirmer », avec la question à reposer après la connexion ou l'activation : « Quels outils as-tu pour Outlook ? » Sinon, la ligne s'écrit sans mention : c'est une consigne.

Avec Cowork ou la conversation claude.ai seules, aucune mention tirée de `.claude/settings.json` : la protection est le « Blocked » de claude.ai ([modele-instructions-projet.md](../../architecte-consignes/modeles/modele-instructions-projet.md)).

## Test

À faire à l'étape 10 du skill, dans la nouvelle session (E6), avec les autres tests.

1. (U) Ouvrir une nouvelle session dans le même dossier, pas dans un sous-dossier, avec le geste et la commande de recette de E6 (SKILL.md), seul lieu de cette commande. Onglet Code : « + New » dans la barre latérale (Windows `Ctrl+N`, macOS `Cmd+N`), puis vérifier dans la rangée sous la zone de saisie que le dossier est le même. Puis, dans l'ordre de l'étape 10 : la question de la pièce, puis la phrase de reprise. Le `.claude/settings.json` est lu depuis le dossier de la session, sans repli sur les dossiers parents.
2. (C) Vérifier le dossier de la session. Windows (PowerShell) : `(Get-Location).Path` ; macOS : `pwd`. Attendu : le dossier retenu (relevé de l'étape 1, ou dossier choisi à l'étape 3), par exemple `C:\Users\<nom>\Claude\<Dossier>` ou `/Users/<nom>/Claude/<Dossier>`.
3. (U) Écrire à Claude : « Sans appeler aucun outil, liste les outils de ta liste dont le nom contient send_message, reply, forward, draft, outlook_, teams_ ou search_threads, avec leur nom complet. »
4. (C) Attendu pour Gmail : aucun `…__send_message`, `…__reply` ni `…__forward` du connecteur ; `…__create_draft` et `…__update_draft` présents ; `mcp__ccd_session_mgmt__send_message` présent s'il l'était à l'étape 1. Pour Outlook (non testé) : les neuf outils du tableau absents ; `outlook_create_draft` présent ; `sharepoint_delete_item`, `sharepoint_move_item`, `sharepoint_rename_item` et `sharepoint_update_file` absents (test de `references/stockage.md`, partie C). Outils gardés en deny au passage d'un blocage entier (« Réglages », dernier point) : absents aussi. Si les outils d'envoi manquaient déjà avant les règles du dossier (relevé du point 3 ; blocage de l'organisation, documenté ; « Blocked » personnel, non documenté), leur absence ne prouve pas ces règles : le dire au participant et noter à « À confirmer » : « règles du dossier non vérifiées par la liste d'outils ».
5. (C) Si l'outil de brouillon manque, regarder les outils de lecture (`search_threads`, `outlook_email_search`) :
   - absents aussi : le connecteur n'est pas chargé, et l'absence des outils d'envoi ne prouve rien. (U) Vérifier d'abord le bouton « + » à côté de la zone de saisie, puis Connectors : le connecteur doit y être activé (dans l'onglet Code, « + » ajoute des connecteurs à une session locale, avant ou pendant la session : documenté). Sinon, reconnecter sur claude.ai, puis refaire le test dans une nouvelle session ;
   - présents, avec un compte Microsoft professionnel : l'écriture n'est pas activée. Repli par fichier local (pas à pas, point 11) ; noter « à confirmer » ;
   - présents, autre cas : voir « Dépannage ».
6. (C) Après accord, créer un vrai brouillon sans destinataire, au contenu fictif, objet « Essai Claude — à supprimer ». À dire : « Je crée un brouillon sans destinataire : il reste dans votre dossier Brouillons et ne peut partir chez personne. Si une demande d'autorisation s'affiche, vérifiez qu'aucun destinataire n'y est indiqué, puis acceptez cette fois seulement. » Gmail : destinataire facultatif (définition de l'outil lue le 25/11/2026, sans appel). Outlook : brouillon sans destinataire non documenté, à vérifier dans la définition de l'outil ; à défaut, sa propre adresse, tapée par le participant ; jamais une autre adresse, ni une adresse cherchée dans sa boîte.
7. (U) Ouvrir le dossier Brouillons (Drafts), puis le seul brouillon dont l'objet est « Essai Claude — à supprimer ». Vérifier qu'il n'a aucun destinataire (Outlook : au plus sa propre adresse) et que son contenu est fictif. Ne pas cliquer sur Envoyer. Le supprimer par l'icône de corbeille du brouillon (libellé : non documenté, à vérifier à l'écran), sans supprimer aucun autre brouillon.
8. (C) Ne jamais demander « envoie un e-mail de test » : si une règle était mal écrite, le message partirait vraiment.
9. (U) Sur claude.ai, relire Tool permissions : outils d'envoi sur « Blocked », brouillons non bloqués ; membre d'une organisation : constater le réglage du propriétaire. Avec Chrome : icône de l'extension > trois points > « Paramètres de l'extension » > Permissions > « Vos sites approuvés » : aucun site de messagerie ne doit y figurer.
10. (U, en option) Seulement si Claude Code est installé en ligne de commande. Ouvrir un terminal (Windows : PowerShell ; macOS : Terminal ; ou le panneau Terminal de l'application). Aller dans le dossier retenu (Windows `cd "C:\Users\<nom>\Claude\<Dossier>"`, macOS `cd ~/Claude/<Dossier>`), lancer `claude --permission-mode default`, puis taper `/mcp` dans Claude Code. Avant `claude`, `/mcp` donne une erreur : ce n'est pas une commande du système. Au premier lancement dans un dossier pas encore approuvé, Claude Code demande si l'on fait confiance au dossier : c'est au participant de répondre. `/mcp` ne prouve pas le blocage : un outil bloqué par l'organisation y figure encore ; pour un deny local, non documenté. Seul compte le test par la liste d'outils.
11. (C) Noter les résultats au brouillon, sous « Tests ».

## Dépannage

- Les outils d'envoi apparaissent encore. (C) Vérifier le dossier de la session (sous-dossier ?), que la session est neuve, le JSON (virgule ou guillemet manquant) et la forme des règles : une règle `mcp__claude_ai_Gmail__…` seule ne vaut pas dans l'onglet Code ; un identifiant d'une autre forme que `*-*-*-*-*` demande le nom exact relevé. Corriger après accord ; (U) ouvrir une nouvelle session ; (C) refaire le test.
- L'outil de brouillon a disparu aussi. Causes possibles : connecteur non chargé (non connecté, désactivé par le « + », offre non payante) ; outil bloqué par l'organisation (documenté) ; « Blocked » personnel sur claude.ai (même effet possible, non documenté) ; règle deny trop large dans `.claude/settings.json` (`mcp__*`, `mcp__*__*`, ou une règle qui vise `create_draft`) ; compte Microsoft professionnel sans écriture activée. (C) Chercher la cause ; (U) reconnecter ou régler outil par outil ; (C) corriger la règle après accord.
- `mcp__ccd_session_mgmt__send_message` a disparu. Une règle `mcp__*__send_message` reste dans le fichier (ancienne version du kit, autre source). (C) Proposer de la remplacer par les trois formes, après accord.
- Google affiche « Access blocked: your institution's admin needs to review Claude… » (la fin varie selon le service). (U) Demander à l'administrateur Workspace de passer Claude en « Trusted » (application approuvée) : Security > Access and data control > API controls > Manage third-party app access. Attendre environ 15 minutes, puis se reconnecter.
- Microsoft, compte professionnel : connexion refusée ou outils d'écriture absents. (U) Demander le consentement de l'administrateur global Entra pour l'organisation, puis, en Team ou Enterprise, l'activation de l'écriture par le propriétaire de l'organisation Claude (Organization settings > Connectors). Des permissions ajoutées après coup s'approuvent par le lien de consentement administrateur (administrateur global ou administrateur d'applications) : se reconnecter ne suffit pas. Si le participant est lui-même administrateur, la fenêtre de connexion peut lui proposer d'accepter pour toute l'organisation : le prévenir d'abord (pas à pas, point 2).
- Microsoft, compte personnel : pas de choix pour un compte personnel dans l'application de bureau. (U) Passer par claude.ai sur le web.
- « Always ask » n'apparaît pas. Déploiement progressif : (U) choisir « Blocked ».
- Un outil d'un autre service a disparu. Effet attendu des motifs si son nom est exactement un nom du tableau des réglages : (C) le dire au participant.
- Aucune demande d'autorisation pour `.claude/settings.json` à l'étape 9. Causes possibles : session en « Auto » (le contrôle automatique décide sans demander) ou en « Bypass permissions » (écriture permise sans demande) ; ou l'option qui autorise les modifications du dossier `.claude` pour toute la session a été acceptée plus tôt. (U) Choisir « Manual » (anciennes versions : « Ask permissions ») dans le sélecteur sous la zone de saisie, et non « Auto » (libellé français : non documenté, à vérifier à l'écran), dans une nouvelle session si cette option avait été accordée.

## Limites et points à confirmer

- Essais du 25/11/2026 : onglet Code, Windows, Gmail. Non testés : Outlook et Microsoft 365, macOS, Cowork, effet d'une règle ask, création effective d'un brouillon. En terminal, la forme `mcp__claude_ai_*__…` n'est pas testée. Couverture d'un identifiant renouvelé par `mcp__*-*-*-*-*__…` : déduite, non testée.
- Effet d'un « Blocked » personnel (Pro, Max) de claude.ai dans l'onglet Code et le terminal : non documenté. Seul le réglage de l'organisation l'est : « Blocked » retire l'outil dans l'onglet Code ; « Needs approval » (« ask » dans la documentation de Claude Code) n'y parvient pas, et les règles ordinaires de la session s'appliquent.
- Cowork : effet des deny de `.claude/settings.json` non documenté ; y compter seulement sur « Blocked ».
- Noms des outils Gmail : observés dans une seule session, publiés nulle part par Anthropic. Noms Microsoft 365 : publiés, non observés. Les relever à chaque séance.
- Une règle de boîte (`outlook_create_filter`) peut-elle transférer des messages ? Non documenté, à vérifier dans l'application ; elle est bloquée par prudence.
- Agendas : aucune règle locale. Noms des outils Google Agenda du connecteur d'Anthropic non publiés ; ceux du serveur de Google (`create_event`, `update_event`, `delete_event`, `respond_to_event`) sont probables, non vérifiés.
- Mode Auto : les outils d'envoi sont-ils toujours examinés par le contrôle automatique ? Non documenté.
- Microsoft 365, Team et Enterprise (connecteur ajouté avant le 9/11/2026) : le 9 décembre 2026 ou après, les outils encadrés que l'administrateur n'a pas réglés passent en « Needs approval ». En mode Auto, l'envoi peut alors partir sans demande, sauf si le contrôle automatique le signale. L'administrateur doit poser « Blocked » avant (verdict « à nuancer »).
- Claude in Chrome peut envoyer par le webmail, même avec le connecteur bloqué (déduit) : l'envoi ne figure pas parmi les actions que l'extension confirme toujours. Le deny de `javascript_tool` (règle du volet Chrome) laisse les 19 autres outils Chrome, dont ceux qui cliquent et remplissent des formulaires.
- Usage de l'ordinateur : d'après l'aide de Cowork, il voit les navigateurs sans pouvoir y cliquer ni y taper, mais il a un accès complet à la plupart des autres applications, dont une application de messagerie installée. Onglet Code : mêmes niveaux, documentés (navigateurs en View only, la plupart des autres applications en Full access) ; envoi par une application de messagerie : déduit.
- Libellés français de Tool permissions et de ses réglages : non documentés, à relever à l'écran.
- Les pages claude.com/docs Gmail et Google Agenda disent ces connecteurs en lecture seule et contredisent le centre d'aide : elles paraissent périmées ; ne pas les citer aux participants.
- Un e-mail reçu peut contenir des instructions piégées : raison de plus pour garder « brouillons seulement ».
- Les pages d'aide changent vite, et certaines ne sont pas datées : revérifier avant chaque séance.
- Les adresses d'Outlook sur le web changent (passage à `cloud.microsoft`, en déploiement progressif) : les revérifier avant chaque séance.

## Sources

- https://support.claude.com/en/articles/13345190-get-started-with-claude-cowork — lue le 25/11/2026 — officielle (modes et Tool permissions, « Always ask »)
- https://support.claude.com/en/articles/16761823-claude-cowork-and-chat-are-one-claude — lue le 25/11/2026 — officielle (mode Auto par défaut)
- https://support.claude.com/en/articles/10166901-use-google-workspace-connectors — lue le 25/11/2026 — officielle (Gmail, Agenda, « Access blocked »)
- https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities — lue le 25/11/2026 — officielle (réglages d'organisation)
- https://claude.com/docs/connectors/getting-started.md — lue le 25/11/2026 — officielle (connexion, Tool permissions, bouton « + »)
- https://claude.com/docs/connectors/microsoft/365.md — lue le 25/11/2026 — officielle (offres, comptes, consentement Entra pour toute l'organisation, écriture désactivée par défaut pour un compte professionnel ; compte personnel sans Teams, règles de boîte ni réponses automatiques)
- https://support.claude.com/en/articles/15183774-connect-to-microsoft-365 — lue le 25/11/2026 — officielle (compte personnel, écriture active par défaut, OneDrive)
- https://support.claude.com/en/articles/12542951-set-up-the-microsoft-365-connector — lue le 25/11/2026 — officielle (administrateurs, outils encadrés, échéance du 9 décembre 2026)
- https://support.claude.com/en/articles/12684923-microsoft-365-connector-security-guide — lue le 25/11/2026 — officielle (noms des outils Outlook, agenda et Teams)
- https://support.claude.com/fr/articles/12012173-commencez-avec-claude-dans-chrome — lue le 25/11/2026 — officielle, en français (chemin : initiales en bas à gauche > Paramètres > Personnaliser > Connecteurs)
- https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide — lue le 25/11/2026 — officielle (modes de l'extension, actions toujours confirmées, sites approuvés)
- https://support.claude.com/fr/articles/12902446-claude-in-chrome-permissions-guide — lue le 25/11/2026 — officielle, en français (libellés de l'extension)
- https://support.claude.com/en/articles/14128542-let-claude-use-your-computer-in-cowork — lue le 25/11/2026 — officielle (usage de l'ordinateur : navigateurs sans clic ni saisie, accès aux autres applications)
- https://code.claude.com/docs/en/desktop.md — lue le 25/11/2026 — officielle (offre payante, connecteurs dans l'onglet Code, bouton « + », « + New », sélecteur de mode et ses libellés ; usage de l'ordinateur : demande par application, niveaux d'accès, Denied apps)
- https://code.claude.com/docs/en/mcp.md — lue le 25/11/2026 — officielle (connecteurs dans Claude Code, préfixe `claude_ai_`, pas de connexion locale, `/mcp`, outils bloqués par l'organisation, réglage « ask » de l'organisation sans effet dans l'onglet Code)
- https://code.claude.com/docs/en/security — lue le 25/11/2026 — officielle (demande de confiance au lancement dans un dossier pas encore approuvé)
- https://code.claude.com/docs/en/permissions.md — lue le 25/11/2026 — officielle (deny par motif sur le nom complet, deny avant allow, noms avec `_` ou `*` non vérifiés, `.claude/settings.json` lu depuis le dossier de la session sans repli sur les dossiers parents)
- https://code.claude.com/docs/en/permission-modes.md — lue le 25/11/2026 — officielle (chemins protégés : demande en Manual et Accept edits, contrôle automatique en Auto, écriture sans demande en Bypass permissions, option pour toute la session ; mode auto)
- https://code.claude.com/docs/en/chrome.md — lue le 25/11/2026 — officielle (mode auto et vérification par site de l'extension)
- https://claude.com/docs/cowork/overview.md — lue le 25/11/2026 — officielle (Cowork charge les connecteurs du compte)
- https://claude.com/docs/connectors/google/gmail.md — lue le 25/11/2026 — officielle, paraît périmée
- https://developers.google.com/workspace/calendar/api/guides/configure-mcp-server?hl=en — lue le 25/11/2026 — officielle Google (outils Agenda, instructions piégées)
- https://knowledge.workspace.google.com/admin/apps/control-which-apps-access-google-workspace-data?hl=en — lue le 25/11/2026 — officielle Google (application « Trusted »)
- https://learn.microsoft.com/en-us/microsoft-365/enterprise/cloud-microsoft-domain — lue le 25/11/2026 (page mise à jour le 3/11/2026) — officielle Microsoft (domaine `cloud.microsoft` pour Microsoft 365)
- https://mc.merill.net/message/MC1188995 — lue le 25/11/2026 — source tierce, reprise du message Microsoft MC1188995 publié le 22/11/2025 (Outlook à `outlook.cloud.microsoft`, redirection depuis les anciennes adresses, déploiement progressif)
- https://github.com/anthropics/claude-code/issues/92787 — lue le 25/11/2026 — source tierce (noms en identifiant, motif testé en terminal, rotations d'identifiant signalées, dont le ticket n°82532)
- Essais du 25/11/2026, observés (onglet Code de l'application de bureau, Windows) — essais internes, non publiés (règles en motif, définition de `create_draft` lue sans appel, noms des outils `mcp__computer-use__…`)
- [mecanismes.md](../../architecte-consignes/references/mecanismes.md) §6 et §16 — référence interne (permissions, environnement de base)
