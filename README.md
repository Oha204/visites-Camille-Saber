# TP 1 - DevOps

Application fil rouge du module Intro DevOps. À compléter au TP01.

## étape 1 : Configurer Git, la clé SSH et la signature
Q: Que contient le fichier ~/.ssh/allowed_signers et à quoi sert-il pour git log --show-signature ?

R: Le fichier ~/.ssh/allowed_signers contient la liste des clés publiques SSH autorisées à signer des commits ou des tags Git. Lorsqu'on exécute git log --show-signature, Git utilise ce fichier pour vérifier que la signature SSH d'un commit a été réalisée avec une clé de confiance. Si la clé ayant signé le commit est présente dans allowed_signers, Git affiche que la signature est valide ("Good SSH signature").

## étape 2 : Créer le dépôt depuis le modèle et lancer les tests
Q: qu'est-ce qui distingue « créer depuis un modèle » d'un fork ? 

R: Créer depuis un modèle consiste à créer un nouveau dépôt à partir d'un dépôt modèle (template). Les fichiers et la structure sont copiés, mais le nouveau dépôt démarre avec son propre historique Git, indépendant du projet d'origine.
Le fork, lui, est une copie d'un dépôt qui conserve un lien avec le dépôt source. L'historique complet des commits est conservé et il est possible de proposer des modifications au projet d'origine via des pull requests.

## étape 4 : Revue croisée et fusion par squash
Q: après le squash, que devient la branche locale feat/... et pourquoi git branch -d peut refuser de la supprimer ?

R: Après un squash merge, les modifications de la branche feat/... sont intégrées dans la branche principale sous la forme d'un seul commit. La branche feat/... existe toujours en local, mais ses commits d'origine ne font plus partie de l'historique de la branche principale.
La commande git branch -d feat/... peut refuser de supprimer la branche si Git considère que ses commits n'ont pas été fusionnés. En effet, après un squash, l'historique des commits est réécrit en un seul commit, donc Git ne reconnaît pas qu'il s'agit d'une fusion classique.

## étape 5 : Provoquer et résoudre un conflit
Q: pourquoi --force-with-lease et pas --force ? Que vérifie-t-il ?

R: L'option --force-with-lease est plus sûre que --force lors d'un git push. Avec --force, Git écrase la branche distante sans vérifier si quelqu'un d'autre y a ajouté des commits entre-temps. Cela peut donc supprimer involontairement le travail d'un autre développeur.

Avec --force-with-lease, Git vérifie que la branche distante est toujours dans l'état attendu. Si de nouveaux commits sont apparus sur le dépôt distant, le push est refusé.

## étape 6 : pre-commit, CONTRIBUTING.md et tag v0.1.0
Q: que se passe-t-il si vous committez avec un fichier Python mal formaté ? Et avec git commit --no-verify ?

R: Si je tente de faire un commit avec un fichier Python mal formaté et que des hooks de pré-commit sont configurés, le commit est bloqué. Les outils signalent les erreurs de formatage et demandent de les corriger avant de pouvoir valider le commit.

# TP 2 : Protéger le dépôt

## étape 1 : Règles de protection de main
Q: pourquoi « dismiss stale approvals » ? Quel scénario évite-t-il ?

R: L'option dismiss stale approvals permet d'annuler automatiquement les validations déjà données lorsqu'une nouvelle modification est ajoutée à la pull request. Elle évite qu'une PR soit fusionnée avec des changements qui n'ont jamais été relus par les reviewers après leur approbation initiale

## étape 2 : CODEOWNERS
Q: que se passe-t-il si un propriétaire de code est le seul à pouvoir approuver et qu'il est absent ? Quelle règle de l'organisation faut-il prévoir ?

R: Si le propriétaire du code est le seul autorisé à approuver une modification et qu'il est absent (congés par exemple), la PR peut rester bloquée et ne jamais être fusionnée. Il faut donc prévoir une règle avec plusieurs CODEOWNERS afin qu'au moins une autre personne puisse approuver.

## étape 3 : Dependabot
Q: une PR Dependabot est ouverte par un robot ; avec vos règles, qui doit l'approuver et pourquoi est-ce justement une bonne chose ?

R: La PR Dependabot doit être approuvée par l'un des membres du groupe (A ou B). C'est important car même si la modification est proposée automatiquement, un humain doit vérifier qu'elle est correcte et sans impact négatif (régression) avant la fusion.

## étape 4 : gitleaks en pre-commit : planter un faux secret
Q: gitleaks a-t-il détecté le secret grâce au nom de la variable ou grâce à la valeur ? Testez en renommant la variable

R: Après avoir renommé la variable, Gitleaks détecte toujours le secret. La détection se fait donc grâce à la valeur du secret plutôt qu'au nom de la variable.test
test2
test3
