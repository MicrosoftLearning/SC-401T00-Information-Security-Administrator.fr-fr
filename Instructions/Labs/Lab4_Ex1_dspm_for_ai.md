---
lab:
  title: "Exercice\_1\_: protéger les données dans les environnements IA"
  module: Module 4 - Protect data in AI environments
---

## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation.

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder.

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment.

# Labo 4 - Exercice 1 : protéger les données dans les environnements IA

Vous êtes Joni Sherman, administrateur de la sécurité des informations pour Contoso Ltd. À mesure que les outils IA tels que Microsoft Copilot deviennent plus intégrés aux flux de travail quotidiens, votre équipe a été invitée à évaluer et à améliorer les protections autour des données sensibles. Dans ce labo, vous allez découvrir comment Microsoft Purview DSPM pour l’IA peut vous aider à sécuriser les interactions de données avec les outils d’IA par le biais de l’application des stratégies, de la détection des risques et des évaluations d’exposition.

**Tâches :**

1. Utiliser DSPM pour l’IA pour créer une stratégie DLP pour les sites d’IA générative
1. Créer une stratégie de risque interne pour détecter les interactions avec l’IA risquées
1. (Facultatif) Empêcher Copilot d’accéder au contenu étiqueté
1. Exécuter une évaluation des données pour détecter le contenu sans étiquette

## Tâche 1 : utiliser DSPM pour l’IA pour créer une stratégie DLP pour les sites d’IA générative

Pour réduire le risque de perte de données par le biais d’assistants IA, vous allez commencer par créer une stratégie DLP à l’aide de la recommandation Fortify de sécurité des données. Cette stratégie utilise la protection adaptative pour limiter le collage ou le chargement de données sensibles dans des outils IA tels que ChatGPT et Copilot dans Edge, Chrome et Firefox.

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-cl1\admin**.

1. Dans **Microsoft Edge**, accédez à **`https://purview.microsoft.com`** et connectez-vous en tant que **Joni Sherman**, `JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo).

1. Dans Microsoft Purview, accédez à DSPM pour l’IA en sélectionnant **Solutions** > **DSPM pour l’IA** > **Recommandations**.

1. Sélectionnez la recommandation **Renforcer votre sécurité des données**.

1. Dans la page volante **Sécurité des données pour l’IA**, passez en revue le résumé, puis sélectionnez **Créer des stratégies**. Cela crée une stratégie DLP préconfigurée ciblant des sites d’IA générative.

1. Une fois la stratégie créée, sélectionnez **Afficher la stratégie**.

1. Dans la section **Détails de la stratégie**, sélectionnez **Modifier la stratégie dans la solution** pour ouvrir la solution **Protection contre la perte de données** dans Microsoft Purview.

1. Dans la page **Stratégies**, recherchez et sélectionnez la stratégie **DSPM pour l’IA : bloquer les informations sensibles des sites d’IA**.

1. Dans le menu volant, sélectionnez **Afficher la simulation**.

1. Dans le tableau de bord de simulation, sélectionnez **Modifier la stratégie**.

1. Sélectionnez **Suivant** jusqu’à ce que vous arriviez à la page **Choisir où appliquer la stratégie**. Vérifiez que la stratégie est étendue aux **Appareils**.

1. Cliquez sur **Suivant**.

1. Dans la page **Personnaliser les règles DLP avancées**, sélectionnez l’icône de crayon en regard de **Bloquer avec remplacement pour les utilisateurs à risque élevé** pour afficher la règle.

1. Passez en revue la configuration de la règle créée par DSPM pour l’IA :
   - Sous **Conditions**, notez les types d’informations sensibles inclus et que la règle utilise la **Protection adaptative** en fonction du risque élevé.
   - Sous **Actions**, vérifiez que l’option **Activités de domaine et de navigateur de service** est définie sur **Bloquer avec remplacement** pour les **Sites web d’IA générative**.

1. Sélectionnez **Annuler** pour quitter l’éditeur de règle sans modification.

1. De retour dans la page **Personnaliser les règles DLP avancées**, sélectionnez **Suivant**.

1. Dans la page **Mode de stratégie**, sélectionnez **Activer la stratégie si elle n’est pas modifiée dans les quinze jours suivant la simulation**, puis sélectionnez **Suivant**.

1. Sur la page **Vérifier et terminer**, sélectionnez **Envoyer**, puis **Terminé**.

Vous avez créé une stratégie qui empêche les utilisateurs à haut risque de partager des données sensibles sur des sites d’IA générative et confirmé la configuration de stratégie définie par DSPM pour l’IA.

## Tâche 2 : créer une stratégie de risque interne pour détecter les interactions avec l’IA risquées

Ensuite, vous allez créer une stratégie qui permet de détecter le comportement d’invite à risque dans Copilot.

1. Dans Microsoft Purview, accédez à **DSPM pour l’IA** en sélectionnant **Solutions** > **DSPM pour l’IA** > **Recommandations**.

1. Sélectionnez la recommandation **Détecter les interactions risquées dans les applications IA (prévisualisation)**.

1. Dans la page volante **Détecter les interactions risquées dans les applications IA (prévisualisation)**, passez en revue le résumé, puis sélectionnez **Créer une stratégie**.

1. Une fois la stratégie créée, sélectionnez **Afficher la stratégie**.

1. Dans la section **Détails de la stratégie**, sélectionnez **Modifier la stratégie dans la solution** pour ouvrir la zone **Gestion des risques internes** de Microsoft Purview.

1. Dans la page **Stratégies**, recherchez et sélectionnez la stratégie **DSPM pour l’IA - Détecter l’utilisation de l’IA risquée**.

1. Dans le menu volant, sélectionnez **Modifier la stratégie** pour passer en revue la configuration complète de la stratégie.

1. Dans la page **Choisir un modèle de stratégie**, observez que la stratégie utilise le modèle **Utilisation de l’IA risquée (prévisualisation)**.

1. Sélectionnez **Suivant** jusqu’à atteindre la page **Choisir l’événement déclencheur pour cette stratégie**.
Vérifiez que l’événement déclencheur est **Compte d’utilisation supprimé de Microsoft Entra ID**, ce qui signale les risques potentiels liés au processus de départ qui peuvent précéder ou suivre une activité IA risquée.

1. Cliquez sur **Suivant**.

1. Dans la **page Indicateurs**, développez les catégories d’indicateurs pour examiner les signaux sélectionnés :

   - Accès à des sites web d’IA générative
   - Réponse sensible reçue de Copilot
   - Invite à risque entrée dans Copilot

1. Sélectionnez **Suivant** jusqu’à atteindre la page **Vérifier et terminer**, puis sélectionnez **Annuler** pour quitter l’éditeur sans apporter de modifications.

Vous avez créé une stratégie qui détecte les interactions avec l’IA risquées, y compris les invites et les réponses, pour vous aider à identifier les signes précoces du comportement de l’utilisateur ou de l’utilisatrice à risque.

## Tâche 3 : (facultative) empêcher Copilot d’accéder au contenu étiqueté

Vous pouvez réduire davantage les risques en empêchant Copilot de traiter ou de répondre avec du contenu protégé par des étiquettes de confidentialité.

1. Dans Microsoft Purview, accédez à **DSPM pour l’IA** en sélectionnant **Solutions** > **DSPM pour l’IA** > **Recommandations**.

1. Sélectionnez la recommandation **Protéger les données sensibles référencées dans la recommandation Microsoft 365 Copilot (préversion)**.

1. Passez en revue les conseils fournis dans cette recommandation.

1. Accédez à **Solutions** > **Protection contre la perte de données** > **Stratégies**.

1. Sélectionnez **+ Créer une stratégie**, puis choisissez **Stratégie personnalisée**.

1. Dans la page **Nommer votre stratégie DLP**, entrez les éléments suivants :

   - **Nom :** `DLP - Block Copilot access to labeled content`
   - **Description** : `Prevents Microsoft 365 Copilot from processing or responding with content labeled using sensitivity labels.`

1. Sélectionnez **Suivant** jusqu’à ce que vous arriviez à la page **Choisir où appliquer la stratégie**.

1. Sélectionnez **Microsoft 365 Copilot (préversion)** comme étendue de stratégie, puis sélectionnez **Suivant** jusqu’à atteindre la page **Personnaliser les règles DLP avancées**.

1. Sélectionnez **Créer une règle** et configurez :

   - **Nom :** `Prevent Copilot from accessing labeled data`
   - Sous **Conditions**, sélectionnez **Ajouter une condition** > **Le contenu contient** > **Étiquettes de confidentialité**. Ajoutez ces étiquettes de confidentialité :
     - `Internal`
     - `Confidential`
     - `Highly Confidential`
   - Sélectionnez **Ajouter**
   - Sous **Actions**, sélectionnez **Ajouter une action** > **Empêcher Copilot de traiter le contenu (préversion)**.
   - En bas du panneau volant **Créer une règle**, sélectionnez **Enregistrer**.

1. De retour dans la page **Personnaliser les règles DLP avancées**, sélectionnez **Suivant**.

1. Sur la page **Mode de stratégie**, sélectionnez **Activer immédiatement la stratégie**, puis **Suivant**.

1. Sur la page **Vérifier et terminer**, sélectionnez **Envoyer**, puis **Terminé** sur la page **Votre stratégie a été créée**.

1. Revenez à **Recommandations DSPM pour l’IA** en sélectionnant **Solutions** > **DSPM pour l’IA** > **Recommandations**.

1. Sélectionnez la recommandation **Protéger les données sensibles référencées dans microsoft 365 Copilot (préversion)**, puis sélectionnez **Marquer comme terminé**.

Vous avez créé une stratégie DLP qui empêche l’utilisation du contenu étiqueté dans les invites et réponses Copilot.

## Tâche 4 : exécuter une évaluation des données pour détecter le contenu sans étiquette

Pour comprendre les lacunes potentielles dans la couverture de l’étiquetage, vous allez exécuter une évaluation des données pour identifier les fichiers sans étiquettes de confidentialité accessibles par Copilot.

1. Dans **DSPM pour l’IA**, sélectionnez la recommandation intitulée **Protéger les données sensibles référencées dans les réponses Copilot**.

1. Dans le volet **Protéger les données sensibles référencées dans les réponses Copilot**, passez en revue le résumé, puis sélectionnez **Accéder aux évaluations**.

1. Dans la page **Évaluations des données (préversion)**, sélectionnez **Créer une évaluation (préversion)**.

1. Dans la page **Détails de base**, entrez :

   - **Nom :** `Unlabeled File Exposure Assessment`
   - **Description** : `Identifies files without sensitivity labels that may be exposed in Microsoft 365 Copilot responses and provides recommendations to reduce oversharing risks.`

1. Cliquez sur **Suivant**.

1. Dans la page **Ajouter des utilisateurs**, sélectionnez **Tous**, puis sélectionnez **Suivant**.

1. Dans la page **Ajouter des sources de données pour évaluer**, laissez l’emplacement par défaut de **SharePoint** sélectionné, puis sélectionnez **Suivant**.

1. Dans la page **Vérifier et exécuter l’analyse de l’évaluation des données**, sélectionnez **Enregistrer et exécuter**.

1. Dans la page **Évaluation des données créée avec succès**, sélectionnez **Terminé**.

Vous avez maintenant utilisé Microsoft Purview DSPM pour l’IA pour détecter les risques liés à l’IA, appliquer des stratégies et évaluer l’exposition des données sensibles, ce qui aide votre organisation à utiliser l’IA en toute sécurité.
