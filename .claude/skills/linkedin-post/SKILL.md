---
name: linkedin-post
description: Orchestre des agents pour faire un post linkedin
---

1. Utilise tldr_automation/run.sh. Ce script permet d'agréger toutes les newsletters reçues dans les N derniers jours, N étant le chiffre que tu passes en argument de la commande. Ce nombre te sera éventuellement donné en entrée sinon ne met rien
2. Parmi tous les sujets donnés, y en a t-ils qui te paraissent pertinents pour un post linkedin. Ma cible est les PME/TPE qui souhaient intégrer l'IA dans leur entreprise. Si oui sélectionne les et propose les moi pour validation. Je suis freelance AI & Data, création de chatbot RAG, développement et intégration IA
3. Lance un sous agent par sujet sélectionné sur le skill linkedin-accroche, après avoir fetch le lien te permettant d'avoir toutes les infos sur les sujets sélectionnés. Tu pourras comme ça les envoyer aux sous agents en arguments (en le mettant entre ""), qui seront injecté dans le prompt du skill. 
4. Lance un sous agent par sujet sélectionné sur le skill linkedin-corps. Tu mettras en premier argument l'accroche correspondante au post (entre guillemet), puis en second argument les idées évoquées dans le post