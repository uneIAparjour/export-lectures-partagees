# Lectures partagées — Une IA par jour

Outil de consultation et d'export multi-format pour les ressources de la rubrique **« Lectures partagées »** de la newsletter [Une IA par jour](https://www.uneiaparjour.fr/).

🔗 **Accès direct** : [uneiaparjour.github.io/export-lectures-partagees](https://uneiaparjour.github.io/export-lectures-partagees/)

## Présentation

Cet outil permet de consulter, filtrer et exporter les ressources partagées chaque semaine dans la newsletter. Les ressources sont organisées en 10 catégories thématiques et exportables en 7 formats.

### Consultation

- Navigation par catégorie avec accès rapide
- Titre cliquable vers la source originale
- Lien vers la lettre d'origine sur Substack
- Description, source et date pour chaque ressource
- Retour au menu en fin de chaque catégorie

### Export (7 formats)

| Format | Usage | Compatible avec |
|--------|-------|-----------------|
| OPML | Lecteurs de flux | Feedly, Inoreader, NetNewsWire |
| XML | Données structurées | Traitement automatisé |
| Markdown | Documentation | Obsidian, Notion, GitHub |
| Bookmarks | Favoris navigateur | Chrome, Firefox, Edge, Safari |
| BibTeX | Bibliographie | Zotero, Mendeley, JabRef |
| JSON | Développement | APIs, scripts, intégrations |
| CSV | Tableurs | Excel, Google Sheets, LibreOffice |

## Architecture

```
├── index.html    # Interface SPA (consultation + export)
├── data.json     # Données des ressources
├── README.md
├── LICENSE
└── .gitignore
```

## Mise à jour des données

Les ressources sont mises à jour chaque semaine après la publication de la newsletter :

1. Les nouvelles ressources de la rubrique « Lectures partagées » sont identifiées et classées
2. Elles sont ajoutées à `data.json` avec un nouvel ID incrémental
3. Le fichier est poussé sur GitHub → mis en ligne automatiquement via GitHub Pages

### Format d'une ressource dans data.json

```json
{
  "id": 110,
  "title": "Titre de la ressource",
  "desc": "Description courte.",
  "url": "https://example.com/article",
  "date": "2026-02-07",
  "letter": 23,
  "cat": "etudes",
  "source": "Nom de la source"
}
```

### Catégories disponibles

`etudes` · `ethique` · `travail` · `securite` · `creation` · `technique` · `philosophie` · `education` · `droit` · `geopolitique`

## Intégration WordPress

L'outil est intégré dans la page WordPress via une iframe avec redimensionnement automatique et navigation synchronisée.

### Code à insérer dans la page WordPress

```html
<iframe id="lectures-iframe"
  src="https://uneiaparjour.github.io/export-lectures-partagees/" 
  width="100%" 
  frameborder="0" 
  style="border:none; border-radius:16px; box-shadow:0 4px 20px rgba(0,0,0,0.1); min-height:800px;">
</iframe>
<script>
window.addEventListener('message', function(e) {
  var iframe = document.getElementById('lectures-iframe');
  if (!iframe) return;
  if (e.data.type === 'iframeResize') {
    iframe.style.height = e.data.height + 'px';
  }
  if (e.data.type === 'iframeScrollTo') {
    var iframeTop = iframe.getBoundingClientRect().top + window.scrollY;
    window.scrollTo({top: iframeTop + e.data.offset - 20, behavior: 'smooth'});
  }
});
</script>
```

Le script gère deux événements envoyés par l'iframe via `postMessage` :

- **`iframeResize`** : ajuste automatiquement la hauteur de l'iframe au contenu (plus besoin de hauteur fixe)
- **`iframeScrollTo`** : scrolle la page WordPress quand l'utilisateur clique sur un menu ou sur « ↑ Retour au menu »

## Développement local

L'interface charge `data.json` via `fetch`, un serveur HTTP local est nécessaire :

```bash
python3 -m http.server 8000
# ou
npx serve .
```

Puis ouvrir [http://localhost:8000](http://localhost:8000).

## Licence

MIT — [Une IA par jour](https://www.uneiaparjour.fr/)
