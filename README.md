# TP 1 · Todo-list : MVC puis MVVM — Andriamihamina

Tags : `v-mvc` (filtre en MVC) et `v-mvvm` (passage en MVVM). Tests : `node --test seance1-presentation/tp1-andriamihamina/TodoModel.test.js` et `.../TodoViewModel.test.js`.

## Comparaison MVC / MVVM

- **Logique du filtre.** En MVC, la règle est dans le Model (`filtrer(nom)`, `restantes()`). Le Controller mémorise le filtre courant et transmet à la View la liste déjà filtrée et le compteur. En MVVM, la règle reste dans le Model, mais le filtre courant est un observable du ViewModel (`filtre`). C'est `#recalculer()` qui met à jour `visibles` et `restantes`. La page ne fait que s'abonner.
- **Tests sans navigateur.** En MVC, seul le Model se teste sans navigateur. La View dépend de `document`, et le Controller ne fonctionne pas sans une View. En MVVM, on teste en plus tout le ViewModel : filtre courant, compteur, messages d'erreur, recalcul de la liste (5 tests dans `TodoViewModel.test.js`).
- **Fichiers modifiés pour le filtre en MVC.** Quatre : `index.html` (boutons et style `.actif`), `TodoModel.js` (`filtrer`, `restantes`), `TodoView.js` (`bindFilter`, `showFiltre`, `render(todos, restantes)`) et `TodoController.js` (filtre courant, `#afficher()`), plus `TodoModel.test.js`. Une seule fonctionnalité touche donc les trois rôles.
- **Tableau de bord QueenBee en temps réel : MVVM.** Les mesures arrivent en continu. Avec des observables, chaque nouvelle valeur met à jour automatiquement tous les éléments affichés, sans Controller qui rappelle `render()` à chaque fois. Le ViewModel se teste avec un flux de mesures simulé, sans navigateur. Enfin, c'est le modèle des frameworks actuels (signals d'Angular, `ref()` de Vue), ce qui facilitera le passage à un vrai framework.
