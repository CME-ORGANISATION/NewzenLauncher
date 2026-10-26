# Personnaliser l’icône d’un serveur dans la navbar Newzen

La liste à gauche du launcher utilise désormais le champ `icon` de chaque serveur dans le fichier `distribution.json`. Le champ doit contenir une URL HTTP(S) directe vers une image PNG, par exemple :

```json
{
  "id": "Newzen-1.20.1",
  "name": "Newzen Semi-RP",
  "icon": "https://votre-domaine.fr/assets/icons/newzen.png"
}
```

Remplacez seulement la propriété `icon` de votre entrée existante ; conservez les autres propriétés du serveur. Hébergez l’image à une URL publique et directe, idéalement en HTTPS. Le launcher essaie cette image en premier, puis plusieurs noms de fichiers locaux en secours.

## Icône locale de secours

Vous pouvez aussi placer une image PNG dans `app/assets/images/servers/`. Le launcher cherchera notamment un fichier correspondant à l’identifiant ou au nom du serveur, par exemple `Newzen-1.20.1.png`, puis `newzen.png`. Les noms sont vérifiés avec plusieurs variantes afin de mieux gérer les majuscules et les points dans les identifiants.

Une icône définie dans `distribution.json` peut être modifiée côté serveur sans republier le launcher ; les icônes locales nécessitent une nouvelle version distribuée du launcher.

## Lien « Problème lors de la connexion ? » du loader

Le lien d’aide du loader est configuré indépendamment dans `app/assets/lang/_custom.toml`, sous `[ejs.loading]` :

```toml
[ejs.loading]
connectionHelpURL = "https://discord.gg/newzen"
connectionHelpText = "PROBLÈME LORS DE LA CONNEXION ?"
```

Remplacez `connectionHelpURL` par votre page d’assistance. Les liens HTTP(S) sont ouverts dans le navigateur par défaut du joueur. La version affichée en bas à droite est automatiquement lue depuis la version de l’application définie dans `package.json`.
