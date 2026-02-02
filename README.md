# Export des "lectures partagées" de la lettre d'infos du site uneIAparjour.fr

Outil d'export multi-format pour les ressources de la page [Lectures partagées](https://www.uneiaparjour.fr/lectures-partagees/) de la lettre d'infos **Une IA par jour**.



## Fonctionnalités

- **7 formats d'export** : OPML, XML, Markdown, Bookmarks HTML, BibTeX, JSON, CSV
- **Filtrage par catégorie** : 10 thématiques (Études, Éthique, Travail, Sécurité, Création, Technique, Philosophie, Éducation, Droit, Géopolitique)
- **Sélection individuelle** : Choisir des articles spécifiques à exporter
- **Recherche** : Filtrer par mots-clés dans les titres et descriptions
- **Mise à jour automatique** : Synchronisation quotidienne avec la page WordPress

## Mise à jour automatique

Ce dépôt utilise **GitHub Actions** pour se synchroniser automatiquement avec la page WordPress :

- **Chaque nuit à 3h** (heure de Paris) : récupération et parsing du contenu
- **Déclenchement manuel** : possible via l'onglet "Actions" → "Run workflow"

Le flux de travail :
1. Récupère le HTML de la page WordPress
2. Parse et extrait les ressources (titre, description, URL, date, catégorie)
3. Met à jour le fichier `index.html`
4. Publie automatiquement les changements

## Structure du projet

```
export-lectures-partagees/
├── index.html                    # Application d'export
├── README.md                     # Documentation
└── .github/
    └── workflows/
        └── update-data.yml       # Workflow de mise à jour automatique
```

## Installation

### Prérequis
- Un compte GitHub
- Un dépôt GitHub Pages activé

### Étapes

1. **Cloner ou forker ce repository**

2. **Activer GitHub Pages**
   - Settings → Pages
   - Source : Deploy from a branch
   - Branch : `main` / `root`

3. **Configurer les permissions Actions**
   - Settings → Actions → General
   - Workflow permissions : "Read and write permissions"

4. **Intégrer dans WordPress** (optionnel)
   ```html
   <iframe 
     src="https://VOTRE-USERNAME.github.io/export-lectures-partagees/" 
     width="100%" 
     height="750" 
     frameborder="0" 
     style="border-radius:16px; box-shadow:0 4px 20px rgba(0,0,0,0.1);">
   </iframe>
   ```

## 📊 Formats d'export

| Format | Extension | Usage |
|--------|-----------|-------|
| **OPML** | `.opml` | Lecteurs de flux RSS (Feedly, Inoreader) |
| **XML** | `.xml` | Format structuré universel |
| **Markdown** | `.md` | Documentation, notes |
| **Bookmarks** | `.html` | Import navigateurs (Chrome, Firefox, Safari) |
| **BibTeX** | `.bib` | Gestionnaires de références (Zotero, Mendeley) |
| **JSON** | `.json` | Développeurs, intégrations API |
| **CSV** | `.csv` | Tableurs (Excel, Google Sheets) |

## Catégories

- 📊 Études et recherche
- ⚖️ Éthique et société
- 💼 IA et travail
- 🔒 Sécurité et désinformation
- 🎨 Création, art et médias
- ⚙️ Technique et infrastructure
- 🤔 Philosophie et réflexions
- 📚 Éducation
- ⚖️ Droit
- 🌍 Géopolitique et international

## Personnalisation

### Modifier l'URL source

Dans `.github/workflows/update-data.yml`, modifier la variable `PAGE_URL` :

```javascript
const PAGE_URL = 'https://votre-site.fr/votre-page/';
```

### Ajouter une catégorie

1. Dans `index.html`, ajouter la catégorie dans l'objet `C` :
```javascript
const C={
  // ...
  nouvelle_cat: { l: "Nouvelle catégorie", c: "#COULEUR" }
};
```

2. Dans `update-data.yml`, ajouter la même catégorie dans `categoriesConfig`

3. Sur la page WordPress, utiliser un `<h2 id="nouvelle_cat">` pour la section

## Licence

Ce projet est partagé sous licence CC BY.

## Auteur

**Bertrand Formet** — [Une IA par jour](https://www.uneiaparjour.fr/)

- Newsletter : [uneiaparjour.substack.com](https://uneiaparjour.substack.com/)
- Site : [uneiaparjour.fr](https://www.uneiaparjour.fr/)

## Assistance

Outil développé avec l'assistance de Claude (Anthropic).

---

<p align="center">
  <a href="https://www.uneiaparjour.fr/">
    <img src="https://img.shields.io/badge/Une%20IA%20par%20jour-Newsletter-orange" alt="Newsletter">
  </a>
</p>
