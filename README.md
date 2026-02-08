# Export des lectures partagées — Une IA par jour

Outil d'export multi-format pour les ressources de la rubrique **« Lectures partagées »** de la newsletter [Une IA par jour](https://www.uneiaparjour.fr/).

🔗 **Accès direct** : [uneiaparjour.github.io/export-lectures-partagees](https://uneiaparjour.github.io/export-lectures-partagees/)

## Présentation

Cet outil permet de parcourir, filtrer et exporter les ressources partagées chaque semaine dans la newsletter. Les ressources sont organisées en 10 catégories thématiques et exportables en 7 formats.

### Formats d'export

| Format | Usage | Compatible avec |
|--------|-------|-----------------|
| OPML | Lecteurs de flux | Feedly, Inoreader, NetNewsWire |
| XML | Données structurées | Traitement automatisé |
| Markdown | Documentation | Obsidian, Notion, GitHub |
| Bookmarks | Favoris navigateur | Chrome, Firefox, Edge, Safari |
| BibTeX | Bibliographie | Zotero, Mendeley, JabRef |
| JSON | Développement | APIs, scripts, intégrations |
| CSV | Tableurs | Excel, Google Sheets, LibreOffice |

### Fonctionnalités

- Filtrage par catégorie (sélection multiple)
- Sélection individuelle des ressources
- Recherche textuelle en temps réel
- Export des ressources filtrées ou sélectionnées

## Architecture

```
├── index.html                          # Interface SPA (monofichier HTML/CSS/JS)
├── data.json                           # Données des ressources (mis à jour automatiquement)
├── .github/workflows/update-data.yml   # Synchronisation WordPress → GitHub Pages
└── README.md
```

### Synchronisation automatique

Un workflow GitHub Actions s'exécute chaque nuit pour :

1. Récupérer la page WordPress [Lectures partagées](https://www.uneiaparjour.fr/lectures-partagees/)
2. Parser le HTML et extraire les nouvelles ressources
3. Les ajouter à `data.json` (mode ajout uniquement, jamais d'écrasement)
4. Créer une issue GitHub si des ressources sont invalides

Le workflow ne supprime jamais de données existantes. Si WordPress renvoie un parsing partiel, les ressources déjà présentes dans `data.json` sont conservées.

## Intégration WordPress

L'outil est intégré dans la page WordPress via une iframe :

```html
<iframe 
  src="https://uneiaparjour.github.io/export-lectures-partagees/" 
  width="100%" 
  height="1100" 
  frameborder="0" 
  style="border-radius:16px; box-shadow:0 4px 20px rgba(0,0,0,0.1);">
</iframe>
```

## Développement

Le projet est hébergé sur GitHub Pages. L'interface est un monofichier `index.html` qui charge les données depuis `data.json` au démarrage.

### Exécution locale

Ouvrir `index.html` nécessite un serveur HTTP local (le `fetch` de `data.json` ne fonctionne pas en `file://`) :

```bash
# Python
python3 -m http.server 8000

# Node.js
npx serve .
```

Puis ouvrir [http://localhost:8000](http://localhost:8000).

### Labels GitHub

Le workflow utilise deux labels pour les issues automatiques :

- `sync-error` (rouge) — échecs du workflow de synchronisation
- `données-invalides` (orange) — ressources avec des données manquantes ou incorrectes

## Licence

MIT — [Une IA par jour](https://www.uneiaparjour.fr/)
