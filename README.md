# wvd-github-arm-deployment

Chaîne de déploiement d'un template ARM Windows Virtual Desktop.<br/>
Integration à un domaine AD avec gestion de l'OU. </br>
Workflow GitHub Actions en 3 jobs:<br/>

- Test + What-If template ARM
    - Génération du "Token Expiration Time"
    - Test + What-If du Template ARM
- Déploiement du template ARM
    - Génération du "Token Expiration Time"
    - Déploiement du template ARM
- Assignation d'un groupe utilisateurs sur l'application group WVD
    - Via Powershell

# Step 1 - Générer les informations d'identification du déploiement

Azure CLI: 

<b>az ad sp create-for-rbac --name {myApp} --role contributor --scopes /subscriptions/{subscription-id}/resourceGroups/{MyResourceGroup} --sdk-auth</b>

# Step 2 - Creer les secrets dans le repo GitHub

a/ Copier l'output de la commande ci-dessus dans un secret GitHub <b>AZURE_CREDENTIALS</b>

{<br>
  "clientId": "<GUID>",<br>
  "clientSecret": "<GUID>",<br>
  "subscriptionId": "<GUID>",<br>
  "tenantId": "<GUID>",<br>
  (...)<br>
}<br>
<br>
  
b/ Créer un 2nd secret <b>AZURE_SUBID</b> contenant l'ID de la souscription Azure

# Step 3 - Creer un dossier ARM

Déposer le template ARM à l'intérieur

# Step 4 - Modeliser le workflow GitHub Actions

Créer un dossier .github/workflows à la racine du repository<br>
Créer un fichier azurewvd.yml à l'intérieur pour coder le workflow<br>
Initialiser les variables d'environnement et les secrets additionels suivants:<br><br>
USERNAME --> Compte administrateur local<br>
USER_PWD --> Mot de passe compte administrateur local<br>
DOMAINEUSERNAME --> Compte de service pour la jonction au domaine AD<br>
DOMAINUSERPWD --> Mot de passe du compte de service<br>
TEAMS_WEBHOOK --> Webhook URL du connecteur Teams<br>
 