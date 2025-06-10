---
lab:
  title: "Exercice\_1\_: gérer les rôles de conformité et de sécurité"
  module: Module 1 - Implement Information Protection
---
## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation.

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder.

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment.

# Labo 1 - Exercice 1 : gérer les rôles de conformité et de sécurité

En tant qu’administrateur de sécurité des informations récemment engagé pour Contoso Ltd., vous (Joni Sherman) devez vous assurer que le nouveau locataire Microsoft 365 est conforme à diverses normes légales et réglementaires. Contoso Ltd. se développe et votre rôle est essentiel pour maintenir la conformité dans ses régions.

**Tâches :**

1. Attribuer des rôles de conformité et de sécurité
1. Explorer le portail Microsoft Purview

## Tâche 1 : attribuer des rôles de conformité et de sécurité

Dans cette tâche, vous allez attribuer le rôle Administrateur de conformité à Joni Sherman.

1. Connectez-vous à la machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.

1. Ouvrez **Microsoft Edge** et accédez au Centre d’administration Microsoft 365, `https://admin.microsoft.com`, et connectez-vous en tant qu’**administrateur MOD**, `admin@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe d’administrateur doit être fourni par l’hébergeur de votre labo.

1. Développez **Utilisateurs** dans la barre latérale de gauche, puis sélectionnez **Utilisateurs actifs**.

1. Dans la page **Utilisateurs actifs**, recherchez `Joni`, puis sélectionnez **Joni Sherman**.

1. Les propriétés du compte de Joni sont affichées dans un panneau volant à droite. Sélectionnez **Gérer les rôles** dans le panneau volant.

1. Dans le panneau **Gérer les rôles d’administration**, sélectionnez **Accès au centre d’administration**, puis faites défiler vers le bas pour développer **Tout afficher par catégorie**.

1. Sous la catégorie **Sécurité et Conformité**, cochez la case **Administrateur de conformité** et **Administrateur de sécurité**, puis sélectionnez **Enregistrer les modifications** en bas du panneau volant.

1. Un message doit s’afficher : **Rôles d’administration mis à jour**.

1. Dans la page **Gérer les rôles d’administration**, sélectionnez le **X** dans le coin supérieur droit du panneau volant pour fermer le panneau.

1. Déconnectez-vous du compte d’administration MOD en sélectionnant l’icône **MA** en haut à droite, puis sélectionnez **Se déconnecter**.

   ![Capture d’écran montrant le chemin de navigation pour se déconnecter du compte Administrateur MOD.](../Media/sign-out.png)

Vous avez attribué à Joni Sherman les rôles d’administrateur de conformité et de sécurité, ce qui est nécessaire pour effectuer les tâches de ce labo.

## Tâche 2 : explorer le portail Microsoft Purview

Dans cette tâche, vous allez vous connecter en tant que Joni Sherman pour explorer le portail Microsoft Purview.

1. Vous devez toujours avoir une connexion active à votre machine virtuelle Client 1 (SC-401-CL1) en tant que compte **SC-401-CL1\admin**.

1. Dans **Microsoft Edge**, accédez à **`https://purview.microsoft.com`**.

1. Dans la fenêtre **Choisir un compte** qui s’affiche, sélectionnez **Utiliser un autre compte**.

1. Lorsque la fenêtre **Connexion** s’affiche, connectez-vous en tant que `JoniS@WWLxZZZZZZ.onmicrosoft.com` (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de Joni a été défini dans un exercice précédent.

1. Un message à propos du nouveau portail Microsoft Purview s’affiche à l’écran. Sélectionnez **Démarrer** pour accéder au nouveau portail.

1. Familiarisez-vous avec le nouveau portail Microsoft Purview. Lorsque vous avez terminé, laissez la fenêtre du navigateur ouverte.

Vous avez basculé vers le compte de Joni Sherman et êtes maintenant en mesure de démarrer le labo.
