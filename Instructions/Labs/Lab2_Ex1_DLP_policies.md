---
lab:
  title: "Exercice\_1\_: implémenter et gérer des stratégies DLP"
  module: Module 2 - Implement Data Loss Prevention
---
## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation.

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder.

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment.

# Labo 2, exercice 1 : implémenter et gérer des stratégies DLP

Joni Sherman, nouvelle employée et administratrice responsable de la sécurité de l’information chez Contoso Ltd., a pour mission de configurer des stratégies de protection contre la perte de données (DLP) afin de protéger les données client sensibles dans Microsoft 365. Dans ce labo, vous allez utiliser Microsoft Purview et Microsoft Defender afin de créer et de gérer des stratégies DLP qui détectent et limitent le partage d’informations sensibles, telles que les numéros de carte de crédit et les ID des employés.

**Tâches :**

1. Créer une stratégie DLP en mode simulation
1. Modifier une stratégie DLP
1. Créer une stratégie DLP dans PowerShell
1. Activer une stratégie en mode simulation
1. Modifier la priorité de stratégie
1. Activer l’inspection des fichiers dans Microsoft 365 Defender
1. Créer une stratégie pour Microsoft 365 Defender

## Tâche 1 - Créer une stratégie DLP en mode simulation

Dans cette tâche, vous allez créer une stratégie DLP en mode simulation qui cible les numéros de carte de crédit dans les messages Teams. La stratégie avertit les utilisateurs lorsqu’ils tentent de partager du contenu sensible et les autorise à ignorer l’avertissement en fournissant une justification.

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin**.

1. Dans **Microsoft Edge**, accédez à l’adresse **`https://purview.microsoft.com`** et connectez-vous au portail Microsoft Purview en tant que **Joni Sherman**. Connectez-vous en tant que `JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de Joni a été défini dans un exercice précédent.

1. Sélectionnez **Solutions** > **Protection contre la perte de données** > **Stratégies**.

1. Sur la page **Stratégies**, sélectionnez **+ Créer une stratégie** pour commencer la configuration de la création d’une stratégie de protection contre la perte de données.

1. Sur la page **Démarrer avec un modèle ou créer une stratégie personnalisée**, sélectionnez **Personnalisé** pour la catégorie, puis sélectionnez **Stratégie personnalisée** dans **Réglementations**.

1. Cliquez sur **Suivant**.

1. Dans la page **Nommer votre stratégie DLP**, entrez :

   - **Nom :** `DLP - Credit Card Protection`
   - **Description** : `Detect and restrict sharing of credit card numbers in Teams messages.`

1. Cliquez sur **Suivant**.

1. Sur la page **Affecter des unités d’administration**, sélectionnez **Suivant**.

1. Sur la page **Choisir les emplacements où appliquer la stratégie**, activez uniquement l’emplacement **Messages de conversation et de canal Teams**. Si d’autres emplacements sont sélectionnés, désélectionnez-les.

1. Cliquez sur **Suivant**.

1. Dans la page **Définir les paramètres de stratégie**, sélectionnez **Créer ou personnaliser des règles DLP avancées**, puis **Suivant**.

1. Sur la page **Personnaliser les règles DLP avancées**, sélectionnez **+ Créer une règle**.

1. Dans le menu volant **Créer une règle** :
    - Dans le champ **Nom**, entrez `Credit card information`.

1. Sous **Conditions**, sélectionnez **+ Ajouter une condition** > **Contenu partagé à partir de Microsoft 365**.

1. Dans la section **Contenu partagé à partir de Microsoft 365** :
    - Sélectionnez l’option **avec personnes extérieures à mon organisation**.

1. Sélectionnez **+ Ajouter une condition** > **Le contenu inclut**.

1. Dans la nouvelle section **Le contenu inclut** :
    - Sélectionnez **Ajouter** > **Types d’informations sensibles**.
    - Dans la page **Types d’informations sensibles**, recherchez et sélectionnez `Credit Card Number`, puis sélectionnez **Ajouter**.

1. Sous **Actions**, sélectionnez **+ Ajouter une action** > **Restreindre l’accès ou chiffrer le contenu dans les emplacements Microsoft 365**.

1. Dans la section **Restreindre l’accès ou chiffrer le contenu** :
    - Sélectionnez **Bloquer uniquement les personnes extérieures à votre organisation**.

1. Sous **Notifications d’utilisation** :
    - Activez le bouton bascule pour **Utiliser les notifications pour informer vos utilisateurs et leur enseigner la bonne utilisation des informations confidentielles**.
    - Cochez la case **Informer les utilisateurs dans le service Office 365 avec un conseil de stratégie**.

1. Sous **Remplacements d’utilisation** :
    - Cochez la case **Autoriser les utilisateurs à contourner les restrictions de stratégie** (Fabric, Exchange, SharePoint, OneDrive et Teams).
    - Cochez la case **Exiger une justification professionnelle pour contourner**.

1. Dans **Rapports d’incidents**, dans le menu déroulant **Utiliser ce niveau de gravité dans les alertes et les rapports d’administration** :
    - Sélectionnez **Faible**.

1. En bas du panneau volant **Créer une règle**, sélectionnez **Enregistrer**.

1. De retour sur **Personnaliser les règles DLP avancées**, sélectionnez **Suivant**.

1. Sur la page **Mode de stratégie**, sélectionnez **Exécuter la stratégie en mode simulation** et cochez la case **Afficher les conseils de stratégie en mode simulation**.

1. Cliquez sur **Suivant**.

1. Sur la page **Vérifier les paramètres et terminer**, vérifiez vos paramètres, puis sélectionnez **Envoyer**.

1. Dans la page **Nouvelle stratégie créée**, sélectionnez **Terminé**.

Vous avez créé une stratégie DLP qui analyse le contenu Teams pour les numéros de carte de crédit et autorise les remplacements par justification métier.

## Tâche 2 - Modifier une stratégie DLP

Dans cette tâche, vous allez étendre l’étendue de votre stratégie DLP existante pour inclure le courrier Exchange. Cela permet de garantir une protection cohérente sur des canaux de communication supplémentaires.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et vous devez avoir une connexion active à Microsoft 365 en tant que **Joni Sherman**.

1. Vous devriez toujours vous trouver sur la page **Stratégies** de Microsoft Purview. Si ce n’est pas le cas, ouvrez **Microsoft Edge** et accédez à `https://purview.microsoft.com`. Sélectionnez **Solutions** > **Protection contre la perte de données** > **Stratégies**.

1. Sur la page **Stratégies**, cochez la case de la **stratégie DLP de protection de carte de crédit** récemment créée, puis sélectionnez **Modifier la stratégie** pour ouvrir la configuration de la stratégie.

1. Dans la page **Nommer votre stratégie DLP**, modifiez la description en `Detect and restrict sharing of credit card numbers in Teams and Exchange messages.`.

1. Cliquez sur **Suivant**.

1. Sur la page **Affecter des unités d’administration**, sélectionnez **Suivant**.

1. Sur la page **Choisir les emplacements où appliquer la stratégie**, cochez la case **E-mail Exchange** pour ajouter cet emplacement à votre stratégie DLP.

1. Sélectionnez **Suivant** jusqu’à atteindre la page **Vérifier et terminer**.

1. Sélectionnez **Envoyer** sur la page **Vérifier et terminer** pour appliquer la modification que vous avez apportée à la stratégie.

1. Une fois la stratégie mise à jour, sélectionnez **Terminé** sur la page **Stratégie mise à jour**.

Vous avez correctement mis à jour la stratégie pour analyser les e-mails avec les messages Teams.

## Tâche 3 - Créer une stratégie DLP dans PowerShell

Dans cette tâche, vous allez créer une stratégie DLP à l’aide de PowerShell pour bloquer le partage des ID d’employés par e-mail. Cette approche montre comment définir et appliquer des paramètres de stratégie par le biais de scripts.

1. Vous devez toujours être connecté à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin**.

1. Sur votre bureau, ouvrez une fenêtre PowerShell à privilèges élevés en cliquant avec le bouton droit sur le bouton **Démarrer** dans la barre des tâches, puis en sélectionnant **Terminal (Admin)**.

1. Exécutez le cmdlet **Connect-IPPSSession** pour vous connecter au PowerShell de Sécurité et conformité :

    ```powershell
    Connect-IPPSSession
    ```

1. Connectez-vous en tant que **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo) dans la fenêtre indépendante **Connexion à votre compte**. Le mot de passe de Joni a été défini dans un exercice précédent.

1. Exécutez le cmdlet **New-DlpCompliancePolicy** pour créer une stratégie DLP qui analyse toutes les boîtes aux lettres Exchange :

    ```powershell
    New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
    ```

1. Exécutez le cmdlet **New-DlpComplianceRule** pour ajouter une règle DLP à la stratégie DLP que vous avez créée lors de l’étape précédente. Cette stratégie utilise le type d’informations sensibles **Contoso Employee IDs** créé dans un exercice précédent :

    ```powershell
    New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
    ```

1. Exécutez le cmdlet **Get-DLPComplianceRule** pour vérifier la **règle DLP EmployeeID** :

    ```powershell
    Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
    ```

Vous avez utilisé PowerShell pour créer une stratégie DLP qui bloque le partage des ID des employés.

## Tâche 4 - Activer une stratégie en mode simulation

Maintenant que votre stratégie DLP a été testée dans la simulation, vous l’activerez pour commencer à appliquer ses actions.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et vous devez avoir une connexion active à Microsoft 365 en tant que **Joni Sherman**.

1. Dans **Microsoft Edge**, accédez aux stratégies DLP via `https://purview.microsoft.com` > **Solutions** > **Protection contre la perte de données**, puis sélectionnez **Stratégies** dans la barre latérale de gauche.

1. Dans la page **Stratégies**, sélectionnez la **stratégie DLP de protection de carte de crédit**.

1. En bas du menu volant situé à droite, sélectionnez **Afficher la simulation**.

1. Sur la page de simulation, prenez un moment pour explorer :

   - Onglet **Vue d’ensemble de la simulation**, qui affiche la progression de l’analyse, les correspondances totales et l’état d’analyse par emplacement.
   - L’onglet **Éléments de révision**, où toutes les correspondances prédites s’affichent une fois disponibles.
   - L’**onglet Alertes**, où toutes les alertes déclenchées en mode simulation sont répertoriées.

1. Après avoir exploré les informations en mode simulation, sélectionnez **Activer la stratégie**, puis **Confirmer** pour activer la stratégie DLP.

   Un menu volant de confirmation s’affiche indiquant que la stratégie a été publiée avec succès.

La stratégie est désormais active et applique des restrictions sur les informations de carte de crédit dans Teams et Exchange.

## Tâche 5 : modifier la priorité de la stratégie

Lorsqu’il existe plusieurs stratégies, leur priorité détermine celle qui s’applique en premier. Dans cette tâche, vous allez déplacer la stratégie d’ID d’employés vers la priorité la plus élevée.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et vous devez avoir une connexion active à Microsoft 365 en tant que **Joni Sherman**.

1. Dans **Microsoft Edge**, l’onglet du portail Microsoft Purview devrait encore être ouvert à la page **Stratégies**. Si ce n’est pas le cas, ouvrez **Microsoft Edge** et accédez à `https://purview.microsoft.com`. Sélectionnez **Solutions** > **Protection contre la perte de données** > **Stratégies**.

1. Dans la page **Stratégies**, sélectionnez la **stratégie DLP EmployeeID**.

1. Sélectionnez **Redéfinir les priorités** dans le ruban de navigation supérieur, puis sélectionnez **Déplacer vers le haut (priorité la plus élevée)**.

1. Dans la fenêtre **Protection contre la perte de données**, sélectionnez **Actualiser** et passer en revue la priorité dans la colonne **Ordre** de la table de stratégie.

1. Déconnectez-vous du compte de Joni en sélectionnant son icône en haut à droite, puis sélectionnez **Se déconnecter**.

Vous avez mis à jour la priorité de stratégie afin que la stratégie d’ID d’employés soit prioritaire sur les autres.

## Tâche 6 : activer l’inspection des fichiers dans Microsoft 365 Defender

Certaines stratégies de fichiers nécessitent l’accès pour inspecter le contenu des fichiers protégés. Dans cette tâche, vous accorderez les autorisations nécessaires pour permettre à Microsoft Defender d’analyser le contenu des fichiers OneDrive et SharePoint pour obtenir des informations sensibles.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active en tant que Joni Sherman.

1. Dans **Microsoft Edge**, accédez à Microsoft Defender en accédant à `https://security.microsoft.com`. Connectez-vous en tant qu’**administrateur ou administratrice MOD** `admin@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.

1. Dans la barre latérale gauche, sélectionnez **Système** > **Paramètres**, puis **Applications cloud**.

1. Dans le volet gauche de la fenêtre **Applications cloud**, faites défiler jusqu’à la section **Protection des données**. Sous **Inspecter les fichiers protégés**, sélectionnez **Accorder l’autorisation** pour activer l’inspection des fichiers.

1. Suivez l’invite pour autoriser les autorisations requises dans Microsoft Entra ID. Vous devez voir que l’inspection des fichiers est **active** dans Microsoft Defender for Cloud Apps.

1. Déconnectez-vous du compte d’administration MOD en sélectionnant l’icône **MA** en haut à droite, sélectionnez **Se déconnecter**, puis fermez votre fenêtre de navigateur.

L’inspection des fichiers est désormais activée dans Defender, ce qui permet aux stratégies de fichiers d’analyser le contenu sensible.

## Tâche 7 : créer une stratégie de fichier pour Microsoft 365 Defender

Dans cette tâche, vous allez créer une stratégie de fichier dans Microsoft Defender qui identifie et met en quarantaine les fichiers contenant des numéros de carte de crédit dans OneDrive et SharePoint.

1. Vous devez toujours être connecté à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin**.

1. Ouvrez **Microsoft Edge**, accédez à **`https://security.microsoft.com`** et connectez-vous au portail Microsoft Defender tant que **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de Joni a été défini dans un exercice précédent.

1. Dans le portail **Microsoft Defender**, dans le menu de navigation de gauche, sélectionnez **Applications cloud** > **Stratégies**, puis sélectionnez **Gestion des stratégies**.

1. Dans la page **Stratégies**, sélectionnez **+ Créer une stratégie**, puis sélectionnez **Stratégie de fichier**.

1. Dans la page **Créer une stratégie de fichier**, configurez :

   - **Nom de la stratégie** : `Credit card information for files`
   - **Gravité de la stratégie** : **faible**
   - **Catégorie** : **DLP**
   - **Description** : `Protect credit card numbers from being shared in files.`
   - Dans la **section Fichiers remplissant toutes les conditions suivantes** :
      - Pour le premier filtre, configurez les listes déroulantes sur : **le niveau d’accès est égal à Public (Internet), Externe, Public** et ajoutez **Interne**.
      - Pour le deuxième filtre, configurez les listes déroulantes sur : **Dernière modification après (date)** et utilisez la date du jour.

          ![Capture d’écran montrant la liste déroulante des fichiers correspondants avec l’option interne ajoutée.](../Media/files-matching-internal.png)

   - Dans la liste déroulante **Méthode d’inspection**, sélectionnez **Service de classification des données**.
   - Dans le menu déroulant **Choisir le type d’inspection...**, sélectionnez **Type d’informations sensibles...**.
   - Dans la boîte de dialogue **Sélectionner un type d’informations sensibles**, recherchez la case à cocher `Credit Card Number` et cochez-la.
      - Sélectionnez **Terminé** en haut à droite de la boîte de dialogue **Sélectionner un type d’informations sensibles**.

   - Sous **Actions de gouvernance**, développez **Microsoft OneDrive Entreprise** :
      - Cochez la case **Mettre en quarantaine des utilisateurs**.
   - Répétez le même processus pour **Microsoft SharePoint Online**.
      - Cochez la case **Mettre en quarantaine des utilisateurs**.

1. Sélectionnez **Créer** en bas de la page pour créer la stratégie de fichier.

Vous avez créé une stratégie de fichier qui détecte et met en quarantaine les fichiers avec des données de carte de crédit sensibles.
