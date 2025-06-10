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

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et connectez-vous à Microsoft 365 avec le compte administrateur MOD.

1. Dans Microsoft Edge, accédez au portail Microsoft Purview, `https://purview.microsoft.com`, et connectez-vous.

1. Un message à propos du nouveau portail Microsoft Purview s’affiche à l’écran. Sélectionnez **Démarrer** pour accéder au nouveau portail.

    ![Capture d’écran de l’écran Bienvenue sur le nouveau portail de conformité Microsoft Purview.](../Media/welcome-purview-portal.png)

1. Sélectionnez **Solutions** dans la barre latérale de gauche, puis **Audit**.

1. Sur la page **Recherche**, sélectionnez la barre **Démarrer l’enregistrement de l’activité des utilisateurs et des administrateurs** pour activer la journalisation d’audit.

    ![Capture d’écran montrant le bouton Démarrer l’enregistrement de l’activité des utilisateurs et des administrateurs.](../Media/enable-audit-button.png)

1. Après que vous avez sélectionné cette option, la barre bleue doit disparaître de cette page.

<!----- PowerShell instructions

1. Open an elevated Terminal window by selecting the Windows button with the right mouse button and then select **Terminal (Admin)**.

1. Run the **Install Module** cmdlet in the terminal window to install the latest **Exchange Online PowerShell** module version:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. Confirm the NuGet provider prompt  by typing **Y** for Yes and press **Enter**.

1. Confirm the Untrusted repository security dialog with **Y** for Yes and press **Enter**.  This process may take some time to complete.

1. Run the **Set-ExecutionPolicy** cmdlet to change your execution policy and press **Enter**

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

1. Close the PowerShell window.

1. Open a regular (non-elevated) PowerShell window by right-clicking the Windows button and selecting **Terminal**.

1. Run the **Connect-ExchangeOnline** cmdlet to use the Exchange Online PowerShell module and connect to your tenant:

    ```powershell
    Connect-ExchangeOnline
    ```

1. When the **Sign in** window is displayed, sign in as `admin@WWLxZZZZZZ.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider). Admin's password should be provided by your lab hosting provider.

1. To check if Audit is enabled, run the **Get-AdminAuditLogConfig** cmdlet:

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. If _UnifiedAuditLogIngestionEnabled_ returns false, then Audit is disabled.

1. To enable the Audit log, run the **Set-AdminAuditLogConfig** cmdlet and set the **UnifiedAuditLogIngestionEnabled** to _true_:

    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```

1. To verify that Audit is enabled, run the **Get-AdminAuditLogConfig** cmdlet again:

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. _UnifiedAuditLogIngestionEnabled_ should return _true_ to let you know Audit is enabled.

-->

Vous avez activé l’audit dans Microsoft 365.

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

## Tâche 4 : activer l’analytique et le partage de données des risques internes

Dans cette tâche, vous allez activer l’analytique et le partage de données pour la gestion des risques internes.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active en tant qu’administrateur ou administratrice MOD dans Microsoft Purview.

1. Dans Microsoft Purview, accédez à **Paramètres** > **Gestion des risques internes** > **Analytique**.

1. Basculez ces paramètres sur **Activé** :

   - **Afficher des insights au niveau du locataire**

   - **Afficher des insights au niveau de l’utilisateur**

1. Sélectionnez **Enregistrer** au bas de la page.

1. Dans le volet de navigation de gauche, sélectionnez **Partage de données**.

1. Dans la section Partage de données, basculez **Partager les détails des risques utilisateur avec d’autres solutions de sécurité** sur **Activé**.

1. Sélectionnez **Enregistrer** au bas de la page.

Vous avez activé l’analytique et le partage de données pour la gestion des risques internes.

## Tâche 5 : initialiser Microsoft Defender XDR

Dans cette tâche, vous allez ouvrir Microsoft Defender et attendre que Microsoft Defender XDR termine l’initialisation.

1. Vous devez toujours avoir une connexion active à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin** et une connexion active en tant qu’administrateur ou administratrice MOD dans Microsoft Purview.

1. Dans **Microsoft Edge**, accédez à **`https://security.microsoft.com/`** l’ouverture de Microsoft Defender.

1. Dans le volet de navigation, sélectionnez **Investigation et réponse** > **Incidents et alertes** > **Incidents**.

1. Vous verrez un message indiquant que Microsoft Defender XDR est en cours de préparation. Ce processus s’exécute automatiquement et peut prendre quelques minutes.

   ![Capture d’écran montrant l’intégration de Microsoft Defender XDR.](../Media/enable-defender-xdr.png)

Microsoft Defender XDR est en cours d’initialisation. Vous pouvez continuer avec d’autres tâches pendant sa configuration.
