# STT-1900 Méthodes statistiques pour l'ingénierie

Ce dépôt contient le site Quarto du cours. Pour l'instant, seules les
**diapositives** (LaTeX/Beamer, classe `BeamerTemplate.cls`) dans `diapos/`
y sont intégrées ; elles ont été reprises telles quelles depuis `Global/`.

À chaque `push` sur `main`, GitHub Actions compile les diapos, régénère le
site et le publie sur GitHub Pages. Les PDF ne sont **pas** versionnés : ils
sont produits par la compilation.

## Structure

| Chemin | Contenu |
|---|---|
| `index.qmd` | Page d'accueil du site |
| `diapos.qmd` | Page du site qui liste automatiquement les PDF des diapos |
| `diapos/Module *.tex` | Sources des diapos (un fichier par module) |
| `diapos/compiler.sh` | Compile les diapos (version présentation + version imprimable) |
| `diapos/latexmkrc` | Configuration de `latexmk` |
| `R/` | Fonctions R utilisées par la page Diapositives |
| `.github/workflows/publish.yml` | Compilation et publication automatiques |

## Mise en place (une seule fois)

1. Créer un dépôt vide sur GitHub (ex. `stt1900`).
2. Dans ce dossier :
   ```bash
   git init -b main
   git add .
   git commit -m "Diapos STT-1900"
   git remote add origin git@github.com:VOTRE-UTILISATEUR/stt1900.git
   git push -u origin main
   ```
3. Sur GitHub : *Settings → Pages → Build and deployment → Source :*
   **GitHub Actions**.
4. Remplacer `VOTRE-UTILISATEUR` dans `_quarto.yml`.

Le site sera ensuite à `https://VOTRE-UTILISATEUR.github.io/stt1900/`, avec
les diapos sous l'onglet *Diapositives*.

## Travailler au quotidien

Modifier un `.tex`, puis :

```bash
git commit -am "Module 5 : correction de l'exemple 4"
git push
```

Le suivi se fait dans l'onglet **Actions** du dépôt (environ 3 à 5 minutes).
Si la compilation LaTeX échoue, rien n'est publié et le journal de l'étape
« Compiler les diapos » indique la ligne fautive.

**Ajouter un module :** créer `diapos/Module 12 - Titre.tex`. Il est compilé
et ajouté à la page *Diapositives* automatiquement (le titre vient du nom du
fichier).

## Compiler localement

```bash
sh diapos/compiler.sh                              # tous les modules
sh diapos/compiler.sh "Module 1 - Introduction aux probabilités.tex"  # un seul module
quarto preview                                     # aperçu du site avec les PDF
```

Prérequis : une distribution TeX complète (TeX Live ou MiKTeX) avec
`latexmk`, Quarto et R (paquets `knitr`, `rmarkdown`).

## À faire

- Ajouter les notes de cours (chapitres Quarto), sur le même modèle que
  [STT-1920](https://github.com/JulienMiron/STT-1920).
