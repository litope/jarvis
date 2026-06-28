# /check

> Commande pour vérifier que tout est bien en ligne et synchronisé.

---

## Mission

Quand je lance `/check`, vérifie l'état complet de l'infrastructure et donne-moi un rapport clair.

### Étape 1 : Vérifier le site en ligne

Lance une requête HTTP vers le site Netlify :

```powershell
try {
    $response = Invoke-WebRequest -Uri "https://brilliant-begonia-7a75f0.netlify.app" -UseBasicParsing -TimeoutSec 10
    Write-Output "STATUS: $($response.StatusCode)"
} catch {
    Write-Output "ERREUR: $($_.Exception.Message)"
}
```

- Si le code retour est 200 : site en ligne
- Sinon : signaler l'erreur et le code retour

### Étape 2 : Vérifier la synchronisation Git

```powershell
git fetch origin
git status
git log --oneline -5
```

Vérifier :
- Y a-t-il des fichiers non commités ?
- Le dépôt local est-il en avance ou en retard par rapport à GitHub ?
- Quel est le dernier commit ?

### Étape 3 : Vérifier la connexion GitHub

```powershell
$headers = @{ Authorization = "token $env:GITHUB_TOKEN" }
$repo = Invoke-RestMethod -Uri "https://api.github.com/repos/litope/jarvis" -Headers $headers
Write-Output "Repo: $($repo.full_name) | Dernier push: $($repo.pushed_at)"
```

### Étape 4 : Rapport final

Présente un résumé visuel propre, par exemple :

```
RAPPORT DE STATUT — [DATE]

Site Netlify       ✓ En ligne (200)
GitHub (litope/jarvis)  ✓ Accessible
Synchronisation    ✓ Local = Remote / ⚠ X commits non pushés

Dernier commit : [message]
```

---

## Règles importantes

- Si une vérification échoue, explique pourquoi en français simple
- Ne pas afficher les tokens ou clés API dans le rapport
- Toujours lire le GITHUB_TOKEN depuis les variables d'environnement, pas en dur
- Pas de tirets longs dans les réponses
