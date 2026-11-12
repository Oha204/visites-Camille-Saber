# Guide de contribution
Ce document décrit les bonnes pratiques à respecter pour participer au développement, proposer des modification et garantir la qualité du code.

## 1. Flux de travail Git

### a. Partir d'une branche principale à jour
Chaque nouvelle fonctionnalité doit être récupérée dans la branche principale :
```
git switch main
git pull
````

### b. Création d'une branche courte
Lors de la conception d'une nouvelle fonctionnalité, il faut toujours créer une branche afin de ne pas affecter la branche principale :
```
git switch -c feat/<sujet>
```
(préfixes : feat, fix, docs, chore, ci)

### c. Commits conventionnels
[Voir site commits](https://www.conventionalcommits.org/fr/v1.0.0/), signés (SSH)

### d. Ouvrir une pull request
Une fois le développement terminée, il faut créer une pull request vers la branche 'main' afin qu'un membre du groupe relise et approuve.

### e. Fusion par squash
Suppression d'une branche

### f. Confilts
- Récupération
```
git rebase origin/main
```

- Résout des conflits terminés
```
git add .
```

- Poursuite de la récupération
```
git rebase --continue
```

- Push
```
git push --force-with-lease
````

# Qualité
Avant de proposer une pull request, il est obligatoire de vérifier que les tests passent.
```
pip install -e ".[dev]"
pre-commit install
```

- Lancement des différents tests :
```
pytest -q # Unitaire
pytest -m # Intégration
```
