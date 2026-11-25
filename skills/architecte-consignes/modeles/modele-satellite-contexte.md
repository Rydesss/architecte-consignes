<!--
MODÈLE : fichier satellite « contexte » (kit Architecte consignes, v1.1.2).
Pour Claude, au remplissage :
- Créer ce fichier seulement si le contexte utile à chaque session dépasse une quinzaine de lignes ; sinon, l'écrire dans le CLAUDE.md maître. Emplacement par défaut : `consignes/contexte.md`, dans le dossier de consignes validé à l'étape 3.
- Remplir avec les réponses validées du bloc A et les termes relevés à l'étape 1. Remplacer chaque [crochet] ; une valeur inconnue devient « à confirmer » et rejoint la liste remise à l'utilisateur. Supprimer toute section restée vide.
- Ce fichier est importé (ligne `@consignes/contexte.md` dans le maître ; avec plusieurs agents, dans le CLAUDE.md voisin d'AGENTS.md, AGENTS.md le citant en pointeur) : il est chargé à chaque session. Viser moins de 40 lignes. Ne garder que ce que Claude ne trouverait pas en lisant le dossier.
- Test de chaque ligne : elle reste vraie dans six mois. Ne rien écrire qui change chaque semaine ou chaque mois (statuts, priorités du moment, chiffres en cours, dates d'événements) : cela va dans le suivi.
- Interlocuteurs : par rôle, sans coordonnées. Un nom seulement si l'utilisateur le demande ; jamais d'adresse, de téléphone ni d'autre donnée personnelle.
- La façon de répondre à l'utilisateur (langue, registre, longueur) va dans la section « Façon de travailler avec moi » du maître ; le ton des documents pour tiers a un seul lieu : en refonte, une règle sans `paths` existante qui le porte déjà ; sinon `consignes/conventions.md` s'il existe ; sinon la section « Documents destinés à des tiers » du maître (routage.md section 2).
- Retirer ce commentaire et les autres commentaires de consigne ; garder seulement le dernier.
-->

# Contexte : [nom de l'espace de travail]

Rôle et moment de lecture : importé depuis le CLAUDE.md maître (avec plusieurs agents, depuis le CLAUDE.md voisin d'AGENTS.md ; AGENTS.md le cite en pointeur), donc lu à chaque session de Claude. Contexte durable seulement : ni état, ni échéance, ni coordonnées.

## Qui

- [Personne ou équipe qui travaille ici, et son rôle.]
- [Cadre durable de l'activité, s'il change ce que Claude produit : statut, organisation, contraintes permanentes.]

## Quoi

- [Activité de l'espace, en une ou deux phrases.]
- [Ce qu'on y produit : types de livrables ou de documents.]
- Hors périmètre : [ce qui ne se traite pas ici, et où cela se traite].

## Pour qui

- [Destinataires des productions : clients, public, équipe, usage personnel.]

## Objectifs durables

- [Objectif encore vrai dans six mois, sans échéance datée.]

## Vocabulaire et sigles propres

<!-- Seulement les termes propres à l'espace, ou employés dans un sens inhabituel. Pas les mots courants. -->

| Terme ou sigle | Sens dans cet espace |
|---|---|
| [terme] | [définition courte ; « ne pas confondre avec … » si utile] |

## Interlocuteurs par rôle

| Rôle | Relation avec l'espace | Ce qu'il attend |
|---|---|---|
| [rôle, par exemple « personne qui valide les livrables »] | [ce qu'il reçoit ou fournit] | [attente durable] |

- Coordonnées : jamais ici ; elles se trouvent dans `[annuaire ou fichier de contacts]`.

<!-- Propriétaire : [nom ou rôle] · Créé avec le kit Architecte consignes v1.1.2 -->
