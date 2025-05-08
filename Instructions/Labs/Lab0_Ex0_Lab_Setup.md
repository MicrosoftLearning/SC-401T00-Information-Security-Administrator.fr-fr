---
lab:
  title: "Configuration du labo\_: préparer votre environnement pour l’administration"
  module: Lab setup
---

## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation.

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder.

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment.

# Configuration du labo : préparer votre environnement pour l’administration

Dans ce labo, vous allez configurer et préparer votre environnement pour les tâches d’administration. Vous allez activer les fonctionnalités nécessaires, configurer les autorisations d’administration et vous assurer de la bonne configuration des éléments essentiels.

**Tâches :**

1. Activer l’audit dans le portail Microsoft Purview
1. Définir des mots de passe d’utilisation pour les exercices de labo
1. Activer l’intégration des appareils
1. Activer l’analytique des risques internes

## Tâche 1 : activer l’audit dans le portail Microsoft Purview

Dans cette tâche, vous allez activer l’audit dans le portail Microsoft Purview pour surveiller les activités du portail.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active à Microsoft 365 avec le compte d’administration MOD.

1. Ouvrez une fenêtre Terminal à privilèges élevés en sélectionnant le bouton Windows avec le bouton droit de la souris, puis sélectionnez **Terminal (Admin)**.

1. Exécutez le cmdlet **Install Module** pour installer la dernière version du module **Exchange Online PowerShell** :

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. Confirmez l’invite du fournisseur NuGet en tapant **Y** pour Oui, puis appuyez sur **Entrée**.

1. Confirmez la boîte de dialogue de sécurité du référentiel non approuvé en appuyant sur **Y** pour Oui, puis appuyez sur **Entrée**.  Ce processus peut prendre un certain temps.

1. Exécutez le cmdlet **Set-ExecutionPolicy** pour modifier votre stratégie d’exécution et appuyez sur **Entrée**.

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

1. Fermez la fenêtre PowerShell.

1. Ouvrez une fenêtre PowerShell standard (sans élévation de privilèges) en cliquant avec le bouton droit sur le bouton Windows et en sélectionnant **Terminal**.

1. Exécutez le cmdlet **Connect-ExchangeOnline** pour utiliser le module Exchange Online PowerShell et vous connecter à votre locataire :

    ```powershell
    Connect-ExchangeOnline
    ```

1. Lorsque la fenêtre de **Connexion** s’affiche, connectez-vous en tant que `admin@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.

1. Pour vérifier si l’audit est activé, exécutez le cmdlet **Get-AdminAuditLogConfig** :

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. Si _UnifiedAuditLogIngestionEnabled_ renvoie false, l’audit est désactivé.

1. Pour activer le journal d’audit, exécutez le cmdlet **Set-AdminAuditLogConfig** et configurez **UnifiedAuditLogIngestionEnabled** sur _true_ :

    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```

1. Pour vérifier que l’audit est activé, réexécutez le cmdlet **Get-AdminAuditLogConfig** :

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. _UnifiedAuditLogIngestionEnabled_ doit renvoyer _true_ pour vous informer que l’audit est activé.

<!---

1. In Microsoft Edge, navigate to the Microsoft Purview portal, `https://purview.microsoft.com`, and log in.

1. A message about the new Microsoft Purview portal will appear on the screen. Select the option to agree with the terms of data flow disclosure and the privacy statement, then select **Try now**.

    ![Screenshot showing the Welcome to the new Microsoft Purview portal screen.](../Media/welcome-purview-portal.png)

1. Select **Solutions** from the left sidebar, then select **Audit**.

1. On the **Search** page, select the **Start recording user and admin activity** bar to enable audit logging.

    ![Screenshot showing the Start recording user and admin activity button.](../Media/enable-audit-button.png)

1. Once you select this option, the blue bar should disappear from this page.

-->

## Tâche 2 : définir les mots de passe d’utilisation pour les exercices de labo

Dans cette tâche, vous allez définir des mots de passe pour les comptes d’utilisation nécessaires pour les labos.

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.

1. Ouvrez **Microsoft Edge** et accédez à **`https://admin.microsoft.com`** pour vous connecter au Centre d’administration Microsoft 365 en tant qu’administrateur MOD, `admin@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo).

1. Dans le volet de navigation de gauche, développez **Utilisateurs**, puis sélectionnez **Utilisateurs actifs**.

1. Cochez la case à gauche de **Joni Sherman**, **Lynne Robbins** et **Megan Bowen**.

   Ces comptes seront utilisés tout au long des exercices de labo.

   ![Capture d’écran montrant les comptes d’utilisation qui doivent être réinitialisés.](../Media/user-accounts.png)

1. Sélectionnez le bouton **Réinitialiser le mot de passe** dans la navigation supérieure pour réinitialiser les trois mots de passe.

   ![Capture d’écran montrant le bouton Réinitialiser le mot de passe dans le Centre d’administration Microsoft 365.](../Media/reset-password-button.png)

1. Dans la page de menu volant **Réinitialiser le mot de passe** à droite, vérifiez que les deux cases sont désélectionnées.

   Cela garantit que vous pouvez sélectionner un mot de passe pour les trois utilisateurs utilisés pour les exercices, et que ces mots de passe n’auront pas besoin d’être réinitialisés lorsque vous vous connectez pour la première fois.

1. Dans le champ **Mot de passe**, entrez un mot de passe que vous pouvez mémoriser pour réinitialiser les mots de passe d’utilisation à utiliser dans les exercices futurs.

1. Sélectionnez le bouton **Réinitialiser le mot de passe** au bas de la page **Réinitialiser le mot de passe**.

1. Sur la page de **Les mots de passe ont été réinitialisés**, vous devez voir les trois comptes d’utilisation qui ont été réinitialisés. En bas de cette page volante, sélectionnez **Fermer**.

Vous avez correctement réinitialisé les mots de passe pour les exercices de labo.

## Tâche 3 : activer l’intégration des appareils

Dans cette tâche, vous allez activer l’intégration des appareils pour votre organisation.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active en tant qu’administrateur ou administratrice MOD dans Microsoft 365.

1. Dans **Microsoft Edge**, accédez à **`https://purview.microsoft.com`** pour vous connecter à Microsoft Purview, puis sélectionnez **Paramètres** dans la barre latérale gauche.

1. Dans la barre latérale gauche, développez **Intégration de l’appareil**, puis sélectionnez **Appareils**.

1. Dans la page **Appareils**, sélectionnez **Activer l’intégration des appareils**, puis sélectionnez **OK** pour activer l’intégration de l’appareil.

1. Lorsque vous en recevez l’invitation, sélectionnez **OK** pour confirmer que la surveillance de l’appareil est activée.

Vous avez maintenant activé l’intégration d’appareils et pouvez commencer à intégrer des appareils à protéger avec des stratégies DLP de point de terminaison. Le processus d’activation de la fonctionnalité peut prendre jusqu’à 30 minutes.

## Tâche 4 : activer l’analytique des risques internes

Dans cette tâche, vous allez activer l’analytique pour la gestion des risques internes.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active en tant qu’administrateur ou administratrice MOD dans Microsoft Purview.

1. Dans Microsoft Purview, accédez à **Paramètres** > **Gestion des risques internes** > **Analytique**.

1. Basculez **Analytique** sur **Activé**, puis sélectionnez **Enregistrer**.

Vous avez activé l’analytique pour la gestion des risques internes.

## Tâche 5 : initialiser Microsoft Defender XDR

Dans cette tâche, vous allez ouvrir Microsoft Defender et attendre que Microsoft Defender XDR termine l’initialisation.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active en tant qu’administrateur ou administratrice MOD dans Microsoft Purview.

1. Dans **Microsoft Edge**, accédez à **`https://security.microsoft.com/`** l’ouverture de Microsoft Defender.

1. Dans le volet de navigation, sélectionnez **Investigation et réponse** > **Incidents et alertes** > **Incidents**.

1. Vous verrez un message indiquant que Microsoft Defender XDR est en cours de préparation. Ce processus s’exécute automatiquement et peut prendre quelques minutes.

   ![Capture d’écran montrant l’intégration de Microsoft Defender XDR.](../Media/enable-defender-xdr.png)

Microsoft Defender XDR est en cours d’initialisation. Vous pouvez continuer avec d’autres tâches pendant sa configuration.
