# Todo List - TP1

Ce projet est une simple application de liste de tâches (todo list) développée avec Vue 3 et Vite pour un travail pratique dans le cadre d'un cours sur Vue.js.

## Fonctionnalités

- Ajouter de nouvelles tâches.
- Filtrer les tâches par état (Toutes les tâches, À faire, En cours, Terminées).
- Éditer les tâches existantes.
- Supprimer une ou plusieurs tâches sélectionnées.
- Validation des formulaires pour éviter les entrées incorrectes.
- Sécurité sur le nombre de tâches en cours et le total des heures par utilisateur.

## Configuration de l'IDE recommandée

- [VSCode](https://code.visualstudio.com/)
- [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (désactiver Vetur)
- [Plugin TypeScript Vue (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin)

## Configuration du projet
Installez les dépendances avec la commande suivante :

```sh
npm install
```

### Compilation et rechargement à chaud pour le développement
Lancez l'application en mode développement avec cette commande :

```sh
npm run dev
```

### Compilation et minification pour la production

```sh
npm run build
```

## Utilisation
Après avoir démarré l'application, vous pouvez commencer à ajouter des tâches à l'aide du bouton "Ajouter une todo". Les tâches peuvent être modifiées en cliquant sur le titre de la tâche. Cochez les tâches et cliquez sur "Supprimer les tâches sélectionnées" pour les supprimer.