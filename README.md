# GraphRAG Epidemiological Assistant — Démo en ligne

Application **Streamlit** de démonstration : routage d'un patient vers un cluster
épidémiologique via un modèle **KNN**, extraction du contexte depuis un graphe
**Neo4j**, génération d'un rapport de risque par **Mistral AI**, et mesure du
**taux d'hallucination numérique** du rapport.

Ce dossier est **auto-suffisant** et prêt à être déployé sur
**Streamlit Community Cloud**.

## Contenu

```
demoEnligne/
├── appH.py                     # l'application (chemins relatifs, secrets)
├── models/
│   ├── modele_knn_diabete.pkl  # modèle KNN entraîné
│   └── scaler_knn.pkl          # StandardScaler associé
├── requirements.txt            # dépendances (versions figées)
├── .gitignore                  # exclut .env et secrets.toml
├── .env.example                # modèle pour un lancement LOCAL
├── .streamlit/
│   └── secrets.toml.example    # modèle de secrets (Streamlit Cloud)
└── README.md
```

## Prérequis avant la démo

1. **Neo4j Aura** (base EN LIGNE, gratuite) : créer une instance sur
   https://console.neo4j.io, y **réimporter les données** du projet, puis lancer
   le script d'index. L'URI ressemble à `neo4j+s://xxxx.databases.neo4j.io`.
   > ⚠️ Une instance Aura Free **se met en pause** après quelques jours
   > d'inactivité : **réveille-la le matin de la conférence**.
2. **Clé API Mistral** avec du crédit (régénère-la sur https://console.mistral.ai
   avant de rendre le dépôt public).

## Déploiement sur Streamlit Community Cloud

1. Pousser ce dossier sur un dépôt **GitHub** (privé possible).
2. Aller sur https://share.streamlit.io → **New app** → choisir le dépôt,
   la branche, et `appH.py` comme fichier principal.
3. Dans **Advanced settings › Secrets**, coller le contenu de
   `.streamlit/secrets.toml.example` **avec les vraies valeurs** (clé Mistral +
   identifiants Aura).
4. **Deploy** → tu obtiens une URL publique `https://<nom>.streamlit.app`
   à ouvrir depuis n'importe quel PC/vidéoprojecteur.

## Lancement en local (test)

```bash
pip install -r requirements.txt
copy .env.example .env        # puis remplir .env (Windows)
streamlit run appH.py
```

## Sécurité

- Ne **jamais** committer `.env` ni `.streamlit/secrets.toml` (déjà dans `.gitignore`).
- Les seuls secrets sont la clé Mistral et le mot de passe Neo4j — ils vont
  dans les *Secrets* de Streamlit Cloud, pas dans le code.
