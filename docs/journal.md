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