---
lab:
  title: "Exercice\_1\_: rechercher dans le journal d’audit"
  module: Module 6 - Audit and search activity in Microsoft Purview
---

## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation.

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder.

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment.

# Labo 6 - Exercice 1 : rechercher dans le journal d’audit

Vous êtes Joni Sherman, administrateur de sécurité des informations chez Contoso Ltd. Dans le cadre du renforcement de l’examen et de la conformité de votre organisation, vous avez reçu une invitation à utiliser Microsoft Purview Audit pour examiner les modifications de configuration DLP et vous assurer que les enregistrements d’audit pour l’activité sensible sont conservés pendant une période prolongée. Vous allez rechercher des événements d’audit liés aux stratégies DLP, exporter les résultats pour l’analyse hors connexion et configurer une stratégie de rétention d’audit qui conserve les enregistrements clés dans Exchange, SharePoint et l’activité de point de terminaison.

**Tâches :**

1. Rechercher une activité liée à DLP
1. Exporter les résultats d’une recherche dans le journal d’audit
1. Créer une stratégie de rétention des journaux d’audit

## Tâche 1 : rechercher une activité liée à DLP

Dans cette tâche, vous allez utiliser la solution Microsoft Purview Audit pour rechercher les événements d’audit récents liés à la stratégie et aux règles DLP.

1. Dans Microsoft Edge, accédez à `https://purview.microsoft.com` et connectez-vous au portail Microsoft Purview en tant que **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de Joni a été défini dans un exercice précédent.

1. Dans Microsoft Purview, accédez à **Solutions** > **Audit**.

1. Dans la page **Recherche**, configurez votre recherche :

   - **Date et intervalle de temps (UTC)**  :

     - **Date de début** : il y a 3 jours
     - **Date de fin** : aujourd’hui

   - **Activités - Noms conviviaux** : recherchez `DLP` et sélectionnez les activités suivantes sous **Protection des informations et activités DLP** :

     - Création de règle DLP
     - Mise à jour de la règle DLP
     - Règle DLP supprimée
     - Création de stratégie DLP
     - Mise à jour de stratégie DLP
     - Stratégie DLP supprimée

   ![Capture d’écran montrant les activités DLP à sélectionner dans Audit.](../Media/audit-dlp-search.png)

   - **Nom de recherche** : `DLP Policy Activity`

1. Sélectionnez **Rechercher.**.

1. La recherche peut prendre plusieurs minutes. Pendant qu’Audit traite votre recherche, actualisez la page pour vérifier le **Statut des tâches**,la **Progression (%)** et l’**Heure de recherche**.

1. Une fois l’opération terminée, sélectionnez **Activité de stratégie DLP** pour afficher les résultats.

1. Sélectionnez des résultats individuels pour afficher des informations détaillées sur chaque activité DLP.

Vous avez recherché et examiné l’activité d’audit liée à la stratégie DLP et à la configuration des règles.

## Tâche 2 : exporter les résultats de la recherche d’audit

Dans cette tâche, vous allez exporter les résultats de recherche d’audit DLP pour l’analyse hors connexion ou la conservation des enregistrements de conformité.

1. Dans Microsoft Purview, accédez à **Solutions** > **Audit**.

1. Dans la page **Recherche**, sélectionnez la recherche **Activité de stratégie DLP** que vous avez créée dans la tâche précédente.

1. Sélectionnez **Exporter** en haut de la page.

1. Dans la boîte de dialogue de confirmation, sélectionnez **OK** pour démarrer l’exportation.

1. Une fois l’exportation terminée, sélectionnez le lien **Télécharger le fichier** dans la bannière verte **Votre exportation est terminée**.

 > [!Note] **Note** : les fichiers d’exportation Audit sont enregistrés au format CSV et peuvent être ouverts dans n’importe quel éditeur de texte ou application de feuille de calcul. Pour faciliter la révision, utilisez Excel ou un autre outil de feuille de calcul. Dans cet environnement de labo, vous pouvez ouvrir le fichier CSV dans le Bloc-notes pour confirmer que l’exportation s’est terminée correctement.

Vous avez exporté les journaux d’audit liés à DLP, qui peuvent être utilisés pour la révision hors connexion ou la conservation des enregistrements.

## Tâche 3 : créer une stratégie de rétention d’audit

Dans cette tâche, vous allez configurer une stratégie de rétention d’audit pour conserver les journaux liés aux correspondances et actions DLP pour une investigation à long terme.

1. Dans Microsoft Purview, accédez à **Solutions** > **Audit**.

1. Sélectionnez **Stratégies** dans la barre latérale gauche.

1. Sur la page **Stratégies**, sélectionnez **Créer une stratégie de conservation des journaux d’audit**.

1. Dans le panneau **Nouvelle stratégie de rétention d’audit**, entrez :

   - **Nom de la stratégie** : `Retain DLP Audit Logs`
   - **Description** : `Retains audit logs for DLP activities across Exchange, SharePoint, and endpoints to support investigation and compliance.`
   - **Utilisateurs** : laissez vide pour appliquer à tous les utilisateurs.
   - **Type d’enregistrement** :
      - ComplianceDLPEndpoint
      - ComplianceDLPExchange
      - ComplianceDLPExchangeClassification
      - ComplianceDLPSharePoint
      - ComplianceDLPSharePointClassification
   - **Durée** : 1 an
   - **Priorité** : `1`

1. Sélectionnez **Enregistrer** pour créer la stratégie de rétention d’audit.

Vous avez configuré une stratégie de rétention d’audit qui conserve les journaux d’activité et les correspondances DLP pendant un an.
