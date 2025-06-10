---
lab:
  title: "Exercice\_1\_: implémenter la gestion des risques internes"
  module: Module 3 - Implement Insider Risk Management
---

## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation.

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder.

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment.

# Labo 3 - Exercice 1 : implémenter la gestion des risques internes

Vous êtes Joni Sherman, administrateur de la sécurité des informations pour Contoso Ltd. Votre rôle consiste à garantir la conformité réglementaire et à protéger les informations sensibles au sein de l’organisation. Récemment, Contoso Ltd. a remarqué des activités de navigation inhabituelles susceptibles d’exposer des données sensibles. Pour résoudre de manière proactive ce risque interne, vous allez implémenter la gestion des risques internes Microsoft Purview en vous concentrant sur l’identification, l’analyse et la réponse aux menaces internes potentielles efficacement.

**Tâches :**

1. Attribuer des autorisations de gestion des risques internes
1. Configurer les indicateurs de risque internes
1. Créer une stratégie de risque interne
1. Personnaliser la stratégie de fuites de données
1. Activer l’intégration Microsoft Defender pour point de terminaison avec la gestion des risques internes
1. Activer les indicateurs et configurer les utilisateurs prioritaires
1. Créer une stratégie pour les violations de stratégie de sécurité par les utilisateurs prioritaires
1. Créer un modèle de notification

## Tâche 1 : attribuer des autorisations de gestion des risques internes

Dans cette tâche, vous allez affecter Joni Sherman au rôle Gestion des risques internes afin de pouvoir accéder aux fonctionnalités de risque internes dans Microsoft Purview et les gérer.

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-cl1\admin**.

1. Dans Microsoft Edge, accédez à **`https://purview.microsoft.com`** et connectez-vous au portail Microsoft Purview en tant qu’administrateur MOD, `admin@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.

1. Sélectionnez **Paramètres** > **Rôles et étendues** > **Groupes de rôles**.

1. Sur la page **Groupes de rôles pour les solutions Microsoft Purview**, sélectionnez **Gestionnaire des risques internes**.

1. Dans le panneau volant **Gestion des risques internes** à droite, sélectionnez **Modifier**.

1. Dans la page **Modifier les membres du groupe de rôles**, sélectionnez **+ Choisir des utilisateurs**.

1. Dans le panneau volant **Choisir des utilisateurs**, recherchez `Joni`, puis sélectionnez la case à cocher pour **Joni Sherman**.

1. Sélectionnez le bouton **Sélectionner** en bas du panneau.

1. Dans la page **Modifier les membres du groupe de rôles**, sélectionnez **Suivant**.

1. Dans la page **Vérifier le groupe de rôles et terminer**, sélectionnez **Enregistrer**.

1. Une fois que vous avez ajouté Joni au groupe de rôles, sélectionnez **Terminé** sur la page **Vous avez mis à jour le groupe de rôles**.

1. Déconnectez-vous du compte **Administrateur ou administratrice MOD** en sélectionnant l’icône MA en haut à droite de la fenêtre, puis sélectionnez **Se déconnecter**.

Vous avez attribué à Joni les autorisations nécessaires pour travailler avec la gestion des risques internes dans le portail Microsoft Purview.

## Tâche 2 : configurer les indicateurs de risque internes

Avant de créer une stratégie de risque interne, vous allez activer les indicateurs nécessaires à la détection. Ces indicateurs définissent les types d’activité à risque que le système recherche.

1. Dans **Microsoft Edge**, accédez à **`https://purview.microsoft.com`** et connectez-vous au portail Microsoft Purview en tant que `JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo).

1. Sélectionnez **Paramètres** > **Gestion des risques internes**.

1. Sélectionnez l’onglet situé à gauche pour les **Indicateurs de stratégie**.

1. Dans la page **Indicateurs de stratégie**, développez et sélectionnez **Sélectionner tout** pour activer tous les indicateurs dans ces catégories :

   - Indicateurs Office
   - Détection cumulative d’exfiltration

1. Sélectionnez **Enregistrer** au bas de la page.

Vous avez activé les indicateurs de stratégie clés afin que le système puisse détecter des actions sensibles telles que l’exfiltration de fichier ou l’activité Office risquée.

## Tâche 3 : créer une stratégie de risque interne

Dans cette tâche, vous allez créer une stratégie rapide de fuites de données pour détecter et répondre automatiquement au comportement de l’utilisateur à risque lié à l’exfiltration des données. Les stratégies rapides utilisent des modèles intégrés et des seuils par défaut pour simplifier la configuration.

1. Dans Microsoft Purview, sélectionnez **Solutions** > **Gestion des risques internes** > **Stratégies**.

1. Dans la page **Stratégies**, sélectionnez **Créer une stratégie**, puis sélectionnez **Stratégie rapide**.

1. Dans le menu volant **Créer des stratégies rapides**, sélectionnez **Prise en main** sous **Fuites de données**.

1. Passez en revue les paramètres de création d’une stratégie rapide de fuite de données, puis sélectionnez **Créer une stratégie**.

1. Dans la page **Votre stratégie de fuite de données est en cours de création**, cochez les cases suivantes :

   - M’envoyer un e-mail lorsque les stratégies ont des avertissements non résolus.
   - M’envoyer un e-mail lorsque de nouvelles alertes de gravité élevée sont générées.

     Sélectionnez ensuite **Mettre à jour les paramètres de notification**.

1. En bas de la page **Votre stratégie de fuite de données est en cours de création**, sélectionnez **Terminé**.

Vous avez créé une stratégie rapide pour détecter les fuites de données potentielles à l’aide des paramètres par défaut. Ensuite, vous allez la personnaliser pour résoudre l’avertissement de configuration.

## Tâche 4 : personnaliser la stratégie de fuites de données

Certaines stratégies de risque internes nécessitent des indicateurs supplémentaires pour fonctionner correctement. Dans cette tâche, vous allez modifier votre stratégie pour activer les indicateurs de séquence et mettre la stratégie dans un état sain.

Dans la page **Stratégies** de **Gestion des risques internes**, vous remarquerez que votre stratégie de fuites de données présente une recommandation.

1. Sélectionnez la **Stratégie rapide de fuites de données** que vous venez de créer.

1. Passez en revue la recommandation dans la page volante de la stratégie. Vous avez un avertissement indiquant que **Les indicateurs requis du déclencheur de séquence ne sont pas sélectionnés**. Pour résoudre cet avertissement, sélectionnez **Modifier la stratégie**.

1. Dans la page **Sélectionner un modèle de stratégie**, sélectionnez **Suivant**.

1. Sur la page **Nommer votre stratégie**, sélectionnez **Suivant**.

1. Dans la page **Choisir des utilisateurs, des groupes et des étendues adaptatives**, sélectionnez **Suivant**.

1. Dans la page **Exclure les utilisateurs et les groupes (facultatif) (préversion)**, sélectionnez **Suivant**.

1. Dans la page **Décider s’il faut hiérarchiser le contenu**, sélectionnez **Suivant**.

1. Dans la page **Choisir l’événement déclencheur de cette stratégie**, passez en revue **Sélectionnez les séquences qui déclenchent cette stratégie** et affichez les informations indiquant **Certaines séquences nécessitent l’activation d’indicateurs spécifiques dans « Paramètres » avant de pouvoir être sélectionnées ci-dessous**.

1. Sélectionnez l’option **Activer les indicateurs** pour activer les indicateurs de séquence nécessaires pour cette stratégie.

1. Les fuites de données sont principalement une stratégie de risque interne d’exfiltration des données. Dans la boîte de dialogue pour activer les indicateurs de séquence, sélectionnez **Sélectionner tout** pour activer tous les **Indicateurs exfiltrés** requis, puis sélectionnez **Enregistrer**.

1. Sélectionnez **Suivant** dans la page **Choisir un événement déclencheur pour cette stratégie**.

1. Dans la page **Choisir des seuils pour déclencher des événements**, sélectionnez **Suivant**.

1. Dans la page **Indicateurs**, sélectionnez **Suivant**.

1. Dans les **Options de détection**, sélectionnez **Suivant**.

1. Dans la page **Choisir un type de seuil pour les indicateurs**, sélectionnez **Suivant**.

   Cette stratégie utilise un événement déclencheur et des indicateurs intégrés. Elle commence à évaluer l’activité des utilisateurs uniquement quand Microsoft Defender pour point de terminaison détecte les menaces telles que l’évasion de défense ou les logiciels indésirables.

1. À la page **Vérifier les paramètres et terminer**, sélectionnez **Envoyer**.

1. Sélectionnez **terminé** dans la page **Votre stratégie a été créée**.

1. De retour sur la page **Stratégies**, votre stratégie doit maintenant avoir un état **Sain**.

Votre stratégie de risque interne est désormais saine et prête à détecter les activités à risque en fonction des déclencheurs de séquence et des indicateurs activés.

## Tâche 5 : activer l’intégration de Microsoft Defender pour point de terminaison à la gestion des risques internes

Dans cette tâche, vous allez activer l’intégration entre Microsoft Defender pour point de terminaison et Microsoft Purview afin que les alertes de sécurité puissent être utilisées dans les stratégies de risques internes.

1. Dans Microsoft Edge, accédez à Microsoft Defender en accédant à `https://security.microsoft.com`.

1. Dans le volet de navigation de gauche, sélectionnez **Paramètres** > **Points de terminaison** > **Fonctionnalités avancées**.

1. Faites défiler vers le bas et basculez le bouton sur **Activé** pour **Partager les alertes des points de terminaison avec le Centre de conformité Microsoft**.

   ![Capture d’écran montrant les points de terminaison de partage avec le bouton bascule du centre de conformité Microsoft.](../Media/enable-irm-in-mde.png)

1. Au bas de l’écran, sélectionnez **Enregistrer les préférences**.

Vous avez activé Defender pour points de terminaison pour partager des alertes avec Microsoft Purview.

## Tâche 6 : activer les indicateurs et configurer les utilisateurs prioritaires

Dans cette tâche, vous allez configurer les indicateurs de stratégie et créer un groupe d’utilisateurs prioritaires qui peut être utilisé dans les stratégies de risques internes.

1. Dans **Microsoft Edge**, accédez à `https://purview.microsoft.com`.

1. Sélectionnez **Paramètres** > **Gestion des risques internes**.

1. Sélectionnez l’onglet situé à gauche pour les **Indicateurs de stratégie**.

1. Dans la page **Indicateurs de stratégie**, développez et sélectionnez **Sélectionner tout** pour activer tous les indicateurs dans ces catégories :

   - Indicateurs dans Microsoft Defender pour point de terminaison (préversion)
   - Indicateurs de navigation à risque (préversion)

1. Sélectionnez **Enregistrer** au bas de la page.

1. Sélectionnez l’onglet **Groupes d’utilisateurs prioritaires**, puis sélectionnez **+ Créer un groupe d’utilisateurs prioritaires**.

1. Dans la page **Nommer et décrire le groupe d’utilisateurs prioritaires**, entrez :

   - **Nom :** `Finance team`
   - **Description** : `Team members who manage financial operations, budgeting, and payroll systems.`

1. Cliquez sur **Suivant**.

1. Sur la page **Membres**, sélectionnez **+ Membres**.

1. Dans le menu volant **Membres**, recherchez et sélectionnez :

   - `Lynne Robbins`
   - `Debra Berger`
   - `Megan Bowen`

1. Sélectionnez **Ajouter** pour ajouter les trois membres au groupe de priorité de l’équipe Finance.

1. Cliquez sur **Suivant**.

1. Dans la page **Choisir qui peut afficher les données impliquant des utilisateurs dans ce groupe prioritaire**, sélectionnez **+ Choisir des utilisateurs et des groupes de rôles**.

1. Dans le menu volant, cochez la case **Gestion des risques internes**, puis sélectionnez **Ajouter**.

1. Cliquez sur **Suivant**.

1. **Passez en revue** et **Envoyez** vos paramètres, puis sélectionnez **Terminé** une fois que votre groupe d’utilisateurs prioritaires a été créé.

Vous avez configuré des indicateurs de stratégie et créé un groupe prioritaire pour surveiller les utilisateurs à haut risque.

## Tâche 7 : créer une stratégie pour les violations de stratégie de sécurité par les utilisateurs prioritaires

Dans cette tâche, vous allez créer une stratégie de risque interne qui détecte les alertes Defender pour point de terminaison pour l’activité à risque par les utilisateurs prioritaires.

1. Dans Microsoft Purview, sélectionnez **Solutions** > **Gestion des risques internes** > **Stratégies**.

1. Dans la page **Stratégies**, sélectionnez **Créer une stratégie**, puis sélectionnez **Stratégie personnalisée**.

1. Dans la page **Choisir un modèle de stratégie**, sélectionnez **Violations de stratégie de sécurité par utilisateurs prioritaires (préversion)**, puis sélectionnez Suivant.

1. Sur la page **Nommer votre stratégie**, saisissez :

   - **Nom :** `Security policy violations - Priority users`
   - **Description** : `Detects Defender for Endpoint alerts for risky activity by priority users, such as malware or disabled protections.`

1. Cliquez sur **Suivant**.

1. Dans la page **Choisir des utilisateurs, des groupes et des étendues adaptatives**, sélectionnez **Ajouter ou modifier des groupes d’utilisateurs prioritaires**.

1. Dans le menu volant **Choisir les groupes d’utilisateurs prioritaires**, cochez la case du groupe **Équipe Finance**, puis sélectionnez Ajouter.

1. Cliquez sur **Suivant**.

1. Dans la page **Décider s’il faut hiérarchiser le contenu**, sélectionnez **Suivant**.

1. Dans la page **Choisir un événement déclencheur pour cette stratégie**, sélectionnez **Suivant**.

1. Dans la page **Indicateurs**, sélectionnez **Suivant**.

1. Dans la page **Choisir un type de seuil pour les indicateurs**, conservez l’option par défaut **Appliquer les seuils fournis par Microsoft** sélectionnée, puis sélectionnez **Suivant**.

1. À la page **Vérifier les paramètres et terminer**, sélectionnez **Envoyer**.

1. Dans la page **Votre stratégie a été créée**, sélectionnez **Terminé**.

Vous avez créé une stratégie de risque interne personnalisée qui utilise les signaux Defender pour point de terminaison pour détecter l’activité à risque des utilisateurs prioritaires.

## Tâche 8 : créer un modèle de notification

Dans cette tâche, vous allez créer un modèle de notification dans Microsoft Purview pour avertir les utilisateurs lorsqu’une alerte de risque interne est déclenchée.

1. Dans Microsoft Purview, sélectionnez **Solutions** > **Gestion des risques internes** > **Modèles de notification**.

1. Dans la page **Modèles de notification**, sélectionnez **+ Créer un modèle de notification**.

1. Renseignez les informations nécessaires dans le panneau volant **Créer modèle de notification** à droite.

    - **Nom du modèle** : `Security Violation Alert`
    - **Envoyer de** : `Joni Sherman`
    - **Objet** : `Unusual activity detected - please review`
    - **Corps du message** :

        ````html
        <!DOCTYPE html>
        <html>
        <body>
        <h2>Security Alert</h2>
        <p>We've detected activity from your account that might violate our organization's security policies. This could be due to malware, disabled protections, or other risky behavior.</p>
        <p>Please review your recent actions and ensure your device security settings are up to date. If you believe this alert was generated in error, contact the IT Security team for assistance.</p>
        <p>To avoid future issues, refer to the <a href="https://contoso.com/security-guidelines">Contoso Security Guidelines</a>.</p>
        <p>Thank you,</p>
        <p><em>Compliance and Security Team</em></p>
        </body>
        </html>
        ````

1. Sélectionnez **Créer**.

1. De retour sur la page **Modèles de notification**, vous verrez le modèle **Alerte de violation de sécurité** que vous venez de créer.

Vous avez créé un modèle de notification permettant à la gestion des risques internes d’informer les utilisateurs des violations de stratégie de sécurité.
