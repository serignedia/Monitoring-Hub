# Intro

Ce tuto montre comment soummettre des interruptions de service (Traps) à Centreon via son API.

Si vous avez une application et vous voulez envoyer des évènements à Centreon via son API, cet article est fait pour vous.

Dans le cadre de ce tuto, nous allons utiliser le client api postman pour construire nos requêtes et l'envoyer au serveur.

# Télécharger puis installer le client post via le lien : https://www.postman.com/downloads/

# Autoriser à votre utilisateur centreon l'accès à l'api

Créer un user puis donner lui les accès à l'api depuis : Configuration  >  Users  >  Contacts / Users puis sélectionner le contact et aller à l'onglet authentification

![image](https://user-images.githubusercontent.com/61230711/217044167-457f07b4-0b16-4f55-84f6-368c8109305a.png)


# Sur Postman

# Récupération de token

Pour interragir avec l'api centreon, nous avons besoin d'un token. Pour le générer nous allons construire notre requête comme ceci :

# Url vers l'api v1 Centreon

{{protocol}}://{{server}}:{{port}}/centreon/api/index.php?action=authenticate

# L'onglet body => form-data

![image](https://user-images.githubusercontent.com/61230711/217046507-00af0be8-83a0-4d8d-9565-5519e40446a2.png)

**Remarque** : l'onglet params est rempli automatiquement si vous avez construit le lien correctement

![image](https://user-images.githubusercontent.com/61230711/217046738-7c7bda90-50ed-4eba-b497-fc12cbb5538f.png)

# Cliquer sur send pour envoyer la requête et copier ensuite le token :

![image](https://user-images.githubusercontent.com/61230711/217048220-cf0bf853-bec9-473b-9dc4-c967d4bed118.png)



