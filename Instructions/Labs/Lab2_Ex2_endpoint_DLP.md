---
lab:
  title: "Exercice\_2\_: implémenter et gérer DLP pour points de terminaison"
  module: Module 2 - Implement Data Loss Prevention
---

# Labo 2 – Exercice 2 : implémenter et gérer DLP pour points de terminaison

Joni Sherman, l’administrateur de sécurité de l’information nouvellement embauché chez Contoso Ltd., a été invité à renforcer les contrôles DLP sur les appareils de l’entreprise. Certains employés ont copié des informations client sensibles sur des lecteurs USB, ce qui augmente le risque d’exposition des données. Dans ce laboratoire, Joni configure une stratégie DLP de point de terminaison pour bloquer ces transferts.

**Tâches :**

1. Intégrer un appareil pour la stratégie DLP de point de terminaison
1. Créer une stratégie DLP de point de terminaison
1. Configurer les paramètres DLP pour les points de terminaison
1. Configurer l’extension Microsoft Purview

## Tâche 1 : intégrer un appareil pour la stratégie DLP de point de terminaison

Dans cette tâche, vous allez intégrer un appareil Windows 11 afin qu’il soit prêt à être protégé par des stratégies DLP de point de terminaison.

1. Connectez-vous à **la machine virtuelle Client 2 (SC-401-CL2)** en tant que compte **SC-401-cl2\admin**.

1. Dans Microsoft Edge, accédez à **`https://purview.microsoft.com`** et connectez-vous au portail Microsoft Purview en tant que **Joni Sherman**. Connectez-vous en tant que `JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de Joni a été défini dans un exercice précédent.

1. Sélectionnez **Paramètres** dans la barre latérale de gauche.

1. Dans la barre latérale gauche, développez **Intégration de l’appareil**, puis sélectionnez **Intégration**.

1. Dans la page **Intégration**, dans le menu déroulant **Méthode de déploiement**, sélectionnez **Script local (pour jusqu’à 10 ordinateurs)** et sélectionnez **Télécharger le package**.

1. Dans la boîte de dialogue **Téléchargements**, placez le curseur sur le téléchargement, puis sélectionnez l’icône de dossier pour **Afficher dans le dossier**.

1. Extrayez le fichier zip sur le **Bureau** de SC-401-CL1. Vous devez voir un script nommé **DeviceComplianceLocalOnboardingScript.cmd**.

1. Sur le bureau, cliquez avec le bouton droit sur le fichier **DeviceComplianceLocalOnboardingScript.cmd** que vous venez d’extraire, puis sélectionnez **Afficher plus d’options**, puis sélectionnez **Propriétés**.

1. En bas de l’onglet **Général** de la fenêtre Propriétés, dans la section **Sécurité**, sélectionnez **Débloquer**, puis **OK** pour enregistrer ce paramètre.

1. De retour sur le bureau, cliquez avec le bouton droit sur **DeviceComplianceLocalOnboardingScript.cmd**, puis sélectionnez **Exécuter en tant qu’administrateur**. Dans la boîte de dialogue **Contrôle de compte d’utilisateur**, sélectionnez **Oui**.

1. Dans l’écran **Invite de commandes**, tapez **Y** pour confirmer, puis appuyez sur Entrée.

1. Une fois le script terminé, vous recevez un message de réussite et une invitation à **Appuyer sur n’importe quelle touche pour continuer**. Appuyez sur n’importe quelle touche pour fermer la fenêtre de ligne de commande. L’exécution de l’intégration peut prendre une minute.

1. Ouvrez le menu Démarrer et recherchez `Access work or school`. Sélectionnez **Accès Professionnel ou Scolaire** sous **Meilleure correspondance**.

1. Dans la fenêtre **Accès Professionnel ou Scolaire** pour **Ajouter un compte professionnel ou scolaire**, sélectionnez **Se connecter**.

1. Dans la boîte de dialogue **Configurer un compte professionnel ou scolaire**, sélectionnez le lien **Joindre cet appareil à Microsoft Entra ID** et connectez-vous en tant que **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de Joni a été défini dans un exercice précédent.

1. Dans la boîte de dialogue **Vérifier qu’il s’agit de votre organisation**, passez en revue l’URL de locataire et sélectionnez **Joindre**.  

1. Une fois que votre appareil est connecté, sélectionnez **Terminé** dans l’écran **You’re all set (C’est terminé !)** .

1. Redémarrez la machine virtuelle Client 2 (SC-401-CL2).

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1).

1. La fenêtre Microsoft Purview doit toujours être ouverte sur la page **Appareils**. Actualisez cette page et vérifiez que l’appareil a été correctement intégré.

Vous avez correctement intégré l’appareil et l’avez joint à Microsoft Entra ID. Il peut désormais être protégé par des stratégies DLP de point de terminaison.

## Tâche 2 : créer une stratégie DLP de point de terminaison

Dans cette tâche, vous allez créer une stratégie DLP qui bloque le transfert d’informations sensibles vers des lecteurs USB. Cela permet de réduire le risque que les données soient extraites du site sans autorisation.

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte SC-401-cl1\admin.

1. Vous devez toujours être sur la page **Appareils** du portail Microsoft Purview, avec une connexion en tant que Joni Sherman.

1. Dans le portail Microsoft Purview, sélectionnez **Solutions** > **Protection contre la perte de données**.

1. Dans le panneau de navigation de gauche, sélectionnez **Stratégies**, puis **+ Créer une stratégie**.

1. Sur la page **Démarrer avec un modèle ou créer une stratégie personnalisée**, sélectionnez **Personnaliser**, puis **Stratégie personnalisée** et enfin **Suivant**.

1. Dans la page **Nommer votre stratégie DLP**, entrez les éléments suivants :

    - **Nom :** `Block USB transfers`
    - **Description** : `Prevent transferring sensitive data to USB devices.`

1. Sur la page **Affecter des unités d’administration**, sélectionnez **Suivant**.

1. Dans la page **Choisir des emplacements pour appliquer la stratégie**, vérifiez que seul l’emplacement **Appareils** est sélectionné. Si un autre emplacement est sélectionné, assurez-vous de les désélectionner, puis sélectionnez **Suivant**.

1. Dans la page **Définir les paramètres de stratégie**, sélectionnez **Créer ou personnaliser des règles DLP avancées**, puis **Suivant**.

1. Sur la page **Personnaliser les règles DLP avancées**, sélectionnez **+ Créer une règle**.

1. Dans la page **Créer une règle**, saisissez les éléments suivants :

    - **Nom :** `USB transfer rule`
    - **Description** : `Block USB transfers of sensitive data.`

1. Dans **Conditions**, sélectionnez **+ Ajouter une condition**, puis **Le contenu inclut**.

1. Dans la nouvelle section **Le contenu inclut** :
    - Sélectionnez **Ajouter** > **Types d’informations sensibles**.
    - Dans la page **Types d’informations sensibles**, recherchez les type d’informations sensibles suivants :
       - `Credit Card Number`
       - `U.S. Social Security Number (SSN)`
       - `U.S. Driver's License Number`
       - `Contoso Employee IDs`

1. Sous **Actions**, sélectionnez **+ Ajouter une action** > **, puis Auditer ou restreindre les activités sur les appareils**.

1. Dans la nouvelle section **Auditer ou restreindre les activités sur les appareils** :
    - Dans la section **Activités de fichier pour toutes les applications**, veillez à sélectionner **Copier vers un périphérique USB amovible**.
    - Sélectionnez la liste déroulante à gauche de **Copier vers un périphérique USB amovible** afin de remplacer l’action **Audit uniquement** par **Bloquer**.

1. Sous **Notifications d’utilisation** :
    - **Activez** le bouton bascule **Utiliser les notifications pour informer vos utilisateurs et leur enseigner la bonne utilisation des informations sensibles**.
    - Cochez la case en regard de **Montrer aux utilisateurs une notification de conseil de stratégie lorsqu’une activité est restreinte**.

1. En bas du panneau volant **Créer une règle**, sélectionnez **Enregistrer**.

1. De retour sur **Personnaliser les règles DLP avancées**, sélectionnez **Suivant**.

1. Dans la page **mode de stratégie**, sélectionnez **Exécuter la stratégie en mode simulation**.
   - Cochez la case en regard de **Montrer les conseils de stratégie en mode simulation**.
   - Activez également la case à cocher en regard de **Activer la stratégie si elle n’est pas modifiée dans les quinze jours suivant la simulation**.

1. Cliquez sur **Suivant**.

1. Sur la page **Vérifiier et terminer**, passez en revue vos paramètres de stratégie, puis sélectionnez **Envoyer** pour créer la stratégie.

1. Une fois la stratégie créée, sélectionnez **Terminé** dans la page **Nouvelle stratégie créée**.

Vous avez créé une stratégie DLP en mode simulation qui bloque les transferts de données sensibles par USB. Si la stratégie n’est pas modifiée, elle est automatiquement activée après 15 jours.

## Tâche 3 : configurer les paramètres DLP du point de terminaison

Dans cette tâche, vous allez affiner les paramètres DLP du point de terminaison en excluant un dossier local, en définissant des restrictions de navigateur et en bloquant un domaine cloud.

1. Vous devez toujours être connecté à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-cl1\admin** et connecté à Microsoft 365 en tant que **Joni Sherman**.

1. Dans Microsoft Purview, dans le volet de navigation gauche, sélectionnez **Paramètres** > **Prévention contre la perte de données**.

1. La page des **paramètres de protection contre la perte de données** doit afficher les **paramètres DLP du point de terminaison**.

1. Dans la page des **paramètres DLP du point de terminaison**, développez **Exclusions de chemin de fichier pour Windows**, puis sélectionnez **+ Ajouter une exclusion de chemin de fichier**.

1. Dans la page volante **Exclure ces chemins de fichiers des appareils Windows**, dans le champ **Exclusion des chemins de fichiers**, entrez `C:\FilePathExclusionTest` et sélectionnez le bouton **+** à droite. Sélectionnez **Enregistrer** pour enregistrer cette entrée.

1. De retour sur la page des **paramètres DLP du point de terminaison**, développez **Restrictions de navigateur et de domaine pour les données sensibles**, puis sélectionnez **+ Ajouter ou modifier des navigateurs non autorisés**.

1. Dans la page **Ajouter des navigateurs non autorisés**, cochez la case en regard de **Google Chrome**, puis sélectionnez **Enregistrer**.

1. De retour sur la page des **paramètres DLP du point de terminaison**, sélectionnez la liste déroulante **Domaines de service** et remplacez **Désactivé** par **Bloquer**.

1. Dans la boîte de dialogue **Mettre à jour le mode application cloud**, sélectionnez **Oui** pour activer le mode bloc.

1. Sous **Domaines de service**, sélectionnez **+ Ajouter un domaine de service cloud**.

1. Dans la page volante **Ajouter un domaine de service cloud**, dans le champ **Domaine**, entrez `dropbox.com` et sélectionnez l’icône **+** (plus) pour ajouter le chemin d’accès. Sélectionnez **Enregistrer** pour enregistrer ce paramètre.

Vous avez appliqué des paramètres DLP du point de terminaison personnalisé qui affinent le comportement de votre stratégie, notamment les exclusions, les restrictions de navigateur et le blocage de l’accès à des domaines spécifiques.

## Tâche 4 : configurer l’extension Microsoft Purview

Dans cette tâche, vous allez installer l’extension Microsoft Purview dans Google Chrome pour tester le comportement de stratégie DLP du point de terminaison dans les navigateurs pris en charge.

1. Ouvrez le navigateur Edge à partir de la barre des tâches.

1. Accédez au téléchargement Google Chrome à l’adresse **`https://chrome.google.com`**.

1. Sélectionnez **Télécharger Chrome** et sélectionnez **Ouvrir le fichier** à partir de la notification **Téléchargements** pour **ChromeSetup.exe**.

1. Sélectionnez **Oui** dans la boîte de dialogue **Contrôle de compte d’utilisation** pour installer le navigateur Chrome.

1. Une fois l’installation terminée, dans l’écran **Se connecter à Chrome**, sélectionnez **Non merci** ou **Ne pas se connecter**.

1. Sélectionnez **Ignorer** dans la page **Définir votre navigateur par défaut**.

1. Lorsque la fenêtre de navigateur Chrome nouvellement installé s’ouvre, accédez à l’**extension Microsoft Purview** dans le **Chrome Web Store** à l’adresse :

   `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`

1. Vérifiez que vous êtes sur la page d’extension correcte, puis sélectionnez **Ajouter à Chrome**.

1. Dans la fenêtre **Ajouter « Extension Microsoft Purview » ?** , sélectionnez **Ajouter l’extension**.

1. Fermez la notification pour l’extension ajoutée à Chrome, puis accédez à **`chrome://extensions`**.

1. Vérifiez que l’**extension Microsoft Purview** est visible et activée.

1. Fermez la fenêtre du navigateur Chrome.

Vous avez correctement installé Chrome et ajouté l’extension Microsoft Purview. L’appareil prend désormais en charge l’application des stratégies DLP dans Edge et Chrome.
