# Publier une nouvelle version de Newzen Launcher

Les joueurs reçoivent la mise à jour automatiquement au prochain lancement du launcher (pendant le loading screen). Il suffit de publier une release sur GitHub.

## En 5 étapes

### 1. Change le numéro de version

Dans `package.json` :

```json
"version": "0.0.6",
```

Le numéro doit toujours être **plus haut** que le précédent. Ne réutilise jamais un numéro déjà publié.

### 2. Commit et push

```bat
git add .
git commit -m "Version 0.0.6"
git push origin master
```

### 3. Crée le tag (une seule fois)

```bat
git tag v0.0.6
git push origin v0.0.6
```

Le tag est `v` + le numéro du `package.json`. C'est lui qui déclenche la publication.

### 4. Attends le build

Sur GitHub : onglet **Actions**, attends la coche verte (5 à 15 minutes).
Le job **Windows** est le seul indispensable.

Si deux runs apparaissent pour le même tag, annule le plus récent (**Cancel workflow**).

### 5. Publie la release

1. Va dans **Releases** et ouvre la release `0.0.6` (elle est en **Draft**).
2. Vérifie qu'elle contient :
   - `latest.yml`
   - `Newzen-Launcher-setup-0.0.6.exe`
   - `Newzen-Launcher-setup-0.0.6.exe.blockmap`
3. Clique sur le crayon, puis tout en bas :
   - **Set as the latest release** : coché
   - **Set as a pre-release** : **décoché**
4. Clique sur **Publish release**.

C'est fini. Tant que la release est en Draft, les joueurs ne reçoivent rien.

## Vérifier que ça marche

Lance un launcher installé avec une version plus ancienne. Le loading screen affiche :

1. « Vérification de la version... »
2. « Mise à jour 0.0.6 trouvée... » avec la barre de téléchargement
3. « Installation... le launcher va redémarrer »

Le launcher redémarre et affiche `V0.0.6` en bas à droite du loading screen.

Le test ne marche pas avec `npm start` ni avec le dossier `win-unpacked`. Il faut une version **installée** avec le setup `.exe`.

## Problèmes fréquents

| Problème | Solution |
|---|---|
| `Author identity unknown` au commit | `git config --global user.name "ton_nom"` et `git config --global user.email "ton@email.com"` (une seule fois) |
| `tag 'v0.0.6' already exists` | `git tag -d v0.0.6` puis `git push origin --delete v0.0.6`, et recrée le tag après le commit |
| Aucun build dans Actions | Vérifie que le tag est poussé : `git push origin v0.0.6` |
| Les joueurs ne reçoivent pas la mise à jour | La release est encore en Draft, ou marquée pre-release, ou `latest.yml` manque |
| Mauvais code dans la release | Supprime la release et le tag (`git push origin --delete v0.0.6`), puis refais les étapes 2 à 5 |
| Le job Windows échoue | Ouvre-le dans Actions et lis les dernières lignes rouges |

## Ordre à respecter

Toujours dans cet ordre : **version → commit → push → tag → push du tag**.
Si tu crées le tag avant le commit, la release contient l'ancien code.
