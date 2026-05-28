---
name: linkedin-post
description: Orchestre des agents pour faire un post linkedin
---

Tu orchestres la création de posts LinkedIn à partir des newsletters TLDR agrégées.

CONTEXTE AUTEUR / CIBLE (à reporter dans chaque brief) :
- Auteur : freelance AI & Data — création de chatbots RAG, développement et intégration IA.
- Cible : PME/TPE qui souhaitent intégrer l'IA dans leur entreprise.

## 1. Agréger les newsletters
Exécute `bash run.sh [N]` (le cwd est déjà la racine du projet, n'ajoute pas de préfixe de dossier).
`N` = nombre de jours à agréger : utilise le nombre donné en entrée s'il y en a un, sinon laisse la valeur par défaut.
Le script produit un fichier `tldr_aggregated_<N>_days.html`.

## 2. Sélectionner les sujets
Lis le fichier HTML généré. Parmi tous les sujets, repère ceux qui sont pertinents pour la cible
(PME/TPE intégrant l'IA) et le positionnement de l'auteur.
Propose-moi la liste des sujets sélectionnés (avec leur lien) et attends ma validation avant de continuer.

## 3. Générer les accroches (1 sous-agent par sujet)
Pour chaque sujet validé :
- Fetch le lien associé (WebFetch) pour récupérer toutes les infos détaillées.
- Crée le dossier `briefs/` s'il n'existe pas. Écris un fichier `briefs/<slug>_accroche.md` contenant :
  - le titre du sujet,
  - la cible et le positionnement auteur (voir ci-dessus),
  - le contenu source fetché (texte complet, multi-lignes — c'est pour ça qu'on passe par un fichier).
- Lance un sous-agent sur le skill `linkedin-accroche` en lui passant le CHEMIN de ce fichier en `$0`
  (entre guillemets), p.ex. args = `"briefs/<slug>_accroche.md"`.
  Ne passe PAS le contenu directement en argument : il est multi-lignes et serait fragmenté.
  Le sous-agent renverra plusieurs accroches (1 codeblock chacune).

## 4. Sélectionner une accroche par sujet
Présente-moi les accroches générées, regroupées par sujet, et attends que je choisisse
une seule accroche par sujet avant de continuer. Si je ne réponds pas, propose ton meilleur choix
en justifiant en une phrase, et attends ma confirmation.

## 5. Générer le corps (1 sous-agent par sujet)
Pour chaque sujet :
- Extrait du contenu fetché (étape 3) les idées clés à mettre en avant dans le post.
- Écris un fichier `briefs/<slug>_corps.md` contenant :
  - l'accroche choisie, reproduite telle quelle (en conservant son saut de ligne entre les deux phrases),
  - les idées clés à mettre en avant,
  - la cible et le positionnement auteur.
- Lance un sous-agent sur le skill `linkedin-corps` en lui passant le CHEMIN de ce fichier en `$0`
  (entre guillemets), p.ex. args = `"briefs/<slug>_corps.md"`.

## 6. Restituer
- Exécute `rm -rf posts && mkdir posts` pour repartir d'un dossier propre.
- Pour chaque sujet, écris le post final dans `posts/<slug>.md` (contenu brut, sans en-tête markdown).
- Compile et présente-les moi dans la conversation, un par sujet, prêts à copier-coller.
Indique pour chacun le sujet source et le lien d'origine.
