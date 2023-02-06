# Intro

Ce tuto montre comment soummettre des interruptions de service (Traps) à Centreon via son API.

Si vous avez une application et vous voulez envoyer des évènements à Centreon via son API, cet article est fait pour vous.

Dans le cadre de ce tuto, nous allons utiliser le client api postman pour construire nos requêtes et l'envoyer au serveur.

# Télécharger puis installer le client post via le lien :

https://www.postman.com/downloads/

**Sur Centreon** 

1. Autoriser à votre utilisateur centreon l'accès à l'api

Créer un user puis donner lui les accès à l'api depuis : Configuration  >  Users  >  Contacts / Users puis sélectionner le contact et aller à l'onglet authentification

![image](https://user-images.githubusercontent.com/61230711/217044167-457f07b4-0b16-4f55-84f6-368c8109305a.png)

2. Créer le service devant constistuer la trap

![image](https://user-images.githubusercontent.com/61230711/217050526-833ba13b-3675-457d-9425-13322c237cba.png)


**Sur Postman**

# 1. Récupération de token

Pour interragir avec l'api centreon, nous avons besoin d'un token. Pour le générer nous allons construire notre requête comme ceci :

# Url vers l'api v1 Centreon

{{protocol}}://{{server}}:{{port}}/centreon/api/index.php?action=authenticate

# L'onglet body => form-data

![image](https://user-images.githubusercontent.com/61230711/217046507-00af0be8-83a0-4d8d-9565-5519e40446a2.png)

**Remarque** : l'onglet params est rempli automatiquement si vous avez construit le lien correctement

![image](https://user-images.githubusercontent.com/61230711/217046738-7c7bda90-50ed-4eba-b497-fc12cbb5538f.png)

# Cliquer sur send pour envoyer la requête et copier ensuite le token :

![image](https://user-images.githubusercontent.com/61230711/217048220-cf0bf853-bec9-473b-9dc4-c967d4bed118.png)


# 2. Envoi de la trap

{{baseUrl}} = {{protocol}}://{{server}}:{{port}}/centreon/api/

**Params** : prérempli automatiquement

![image](https://user-images.githubusercontent.com/61230711/217051536-75db2878-2aa3-47f5-80b9-7647e18cfeec.png)

**Autorization** : Bearer Token

![image](https://user-images.githubusercontent.com/61230711/217051754-73bdec55-6c23-4795-9941-5d2f67fc861e.png)


**Header**

Ajouter :

**Content-type** : **application/json**

**centreon-auth-token** : **LE_TOKEN_GENERE_EN_1**

![image](https://user-images.githubusercontent.com/61230711/217052066-748ab7db-6016-4f9d-bdcc-12aa57982265.png)


**Body**

![image](https://user-images.githubusercontent.com/61230711/217050912-3dda5389-5e43-4e92-b340-ecd9578d1083.png)


La partie la plus importante c'est le body. C'est là que vous envoyez la donnée que vous avez choisi d'envoyer à Centreon sous forme de trap.

Dans l'onlget body, choisissez raw puis construiser votre donnée avec les champs comme ceci :


        // OK
        {
            "results": [
                {
                    "host": "Centeon-central",
                    "service": "event_api_test",
                    "status": "0",
                    "output": "OK: Centreon API TRAP TEST ",
                    "updatetime": "1675700194"

            }
        ]

        }


        //Critical
        {
            "results": [
                {
                    "host": "Centeon-central",
                    "service": "event_api_test",
                    "status": "2",
                    "output": "Critical: Centreon API TRAP TEST ",
                    "updatetime": "1675700194"

            }
        ]

        }


**Les champs obligatoires** : 

    host : le nom de l'équipement
    service : le nom de l'indicateur de l'évènement
    status :  le statut (0,1,2 ou 3)
    output : le message affiché en cas d'alerte
    updatetime : la date de l'évènement
    
**Cliquer ensuite sur send**

Sur postman vous pouvez constater que l'évènement a bien été envoyé avec ce retour :


![image](https://user-images.githubusercontent.com/61230711/217054947-83c9f038-3e19-453b-a62c-29f59b8456b8.png)


# Vérification de la réception de l'évènement sur centreon:

**EVENEMENT CRITIQUE**

![image](https://user-images.githubusercontent.com/61230711/217054839-47f499b8-51ca-40c0-b018-97c2a50776d3.png)

**EVENEMENT OK**

![image](https://user-images.githubusercontent.com/61230711/217055232-0c63181f-e38d-4e36-a943-652dc7fcc296.png)



# BRAVO : vous venez d'envoyer votre évènement à centreon via l'api v1

# Remarque :
 
 Cette manipulation peut être faitre via l'api v2 (latest ou beta) en utilisant les id des objets. 
 
 La documentation des champs via l'api v2
 
 https://docs-api.centreon.com/api/centreon-web/#tag/Submit/paths/~1monitoring~1hosts~1%7Bhost_id%7D~1submit/post
