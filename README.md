# wvd-github-arm-deployment

Chaîne de déploiement d'un template ARM Windows Virtual Desktop.<br/>
Workflow GitHub Actions en 3 jobs:<br/>

- Test + What-If template ARM
    - Génération du "Token Expiration Time"
    - Test + What-If du Template ARM
- Déploiement du template ARM
    - Génération du "Token Expiration Time"
    - Déploiement du template ARM
- Assignation d'un groupe utilisateurs sur l'application group WVD
    - Via Powershell
 