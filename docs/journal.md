# Questions d'observation TP1

## Q1. Combien de temps s'est écoulé entre votre premier commit et sa fusion sur main ?
premier commit à ..., fusion à ...

## Q2. Qu'est-ce qui, dans ce TP, ne dépend pas de GitHub ?
Indépendant : configuration Git, signature SSH, branches, rebase, pre-commit, commits conventionnels.
Dépendant : commandes `gh`, règles de protection, interface de PR.

## Q3. Pourquoi signer les commits si la forge vérifie déjà qui pousse ?
l'auteur d'un commit est une chaîne libre ; la forge vérifie qui *pousse*, pas qui a *écrit*. Un miroir ou une migration perd l'information de push ; la signature suit le commit.

## Q4. Qu'est-ce qui nous a prit le plus de temps ?
Camille : Configuration du poste avec la VM. Utilisation d'un langage et d'une méthode de travail totalement différente de ce que l'on fait en entreprise. Synchronisation équipe.

## Questions d'observation TP2
### Q1. Quelles règles de protection auraient empêché le secret d'arriversur main ?
La revue obligatoire des PR, les contrôles automatiques (Gitleaks) et la protection de la branche main auraient pu empêcher le secret d'être fusionné.

### Q2. gitleaks en pre-commit protège-t-il un collègue qui n'a pas installé pre-commit ?
Non. Le hook pre-commit est local à chaque développeur. Un collègue qui ne l'a pas installé n'est pas protégé. Il faut donc également un contrôle Gitleaks côté serveur (CI/PR)

### Q3. Combien de temps un secret poussé sur une forge publique reste-t-il privé?
Quelques secondes à quelques minutes au maximum. Sur une forge publique, un secret doit être considéré comme compromis dès sa publication.

### étape 5 : commit fautif + Discussion en binôme + Rotation
cf rendu PDF

## Questions d'observation TP3

### Q1. Combien de temps dure votre pipeline, et qu'est-ce qui prend le plus de temps ?
Notre pipeline dure environ 1m4s. L'étape qui nous prends le plus de temps est l'étape "Run pre-commit run --all-files" (environ 40s) car elle doit initialiser puis exécuter les différents hooks (Ruff, Gitleaks, vérifications YAML, etc.).

### Q2. Qu'est-ce qui empêche un membre de contourner le pipeline ?
Ce qui empêche un membre de contourner le pipeline est la protection de la branche main via un ruleset GitHub. Les checks test (py3.12) et test (py3.13) ont été définis comme obligatoires. Tant qu'un de ces contrôles échoue, GitHub bloque la fusion de la Pull Request et empêche l'intégration du code dans main.

Seuls les administrateurs disposant du droit de bypass peuvent exceptionnellement contourner cette protection.

### Q3. Quelles lignes de ci.yml changeriez-vous pour GitLab CI ou Gitea Actions ?
Je conserverais les commandes (pip install, pre-commit, ruff, pytest) mais je remplacerais les lignes spécifiques à GitHub Actions (on, runs-on, actions/checkout, actions/setup-python, actions/upload-artifact) par leur équivalent GitLab CI ou Gitea Actions.

### étape 3 : Matrice 3.12 / 3.13 et cache pip : mesurer
Notez la durée du job actuel (page de l'exécution) : 1m1s

1e run (cache miss) : 1m4s
2e run (cache hit)  : 1m4s
