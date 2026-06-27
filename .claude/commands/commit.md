# /commit

> Commande pour sauvegarder l'état du workspace avec Git.

---

## Mission

Quand je lance `/commit`, exécute la séquence suivante :

### Étape 1 : Initialiser Git si nécessaire

Vérifie si le dossier est déjà un dépôt Git avec `git status`.

Si ce n'est pas le cas :
1. Lance `git init`
2. Vérifie que `.gitignore` est bien en place (sinon le créer)
3. Informe-moi que le dépôt a été initialisé

### Étape 2 : Vérifier ce qui a changé

Lance `git status` pour lister les fichiers modifiés ou nouveaux.

Résume-moi en quelques lignes ce qui va être sauvegardé, en français, de façon lisible. Pas de jargon technique inutile.

### Étape 3 : Construire le message de commit

Génère automatiquement un message de commit clair et daté qui décrit ce qui a changé. Format :

```
[DATE] - [Résumé court de ce qui a changé]
```

Exemple : `2026-06-27 - Ajout structure livrables et gestion des secrets`

Si j'ai passé un argument à la commande (ex: `/commit mise à jour business IA`), utilise cet argument comme message.

### Étape 4 : Sauvegarder

Lance dans l'ordre :
1. `git add .` (tout ajouter sauf ce qui est dans .gitignore)
2. `git commit -m "[message construit à l'étape 3]"`

### Étape 5 : Confirmer

Affiche un court résumé de ce qui a été sauvegardé et le message de commit utilisé.

---

## Règles importantes

- Ne jamais ajouter le fichier `.env` au commit (il est dans .gitignore)
- Si `git commit` échoue parce qu'il n'y a rien à sauvegarder, dis-le simplement
- Le message de commit doit toujours être en français
- Pas de tirets longs dans les réponses
