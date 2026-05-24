# AZTRADER — Déploiement sur Vercel

## Structure du projet
```
aztrader/
├── api/
│   └── analyze.js      ← Proxy backend (cache la clé API)
├── public/
│   └── index.html      ← Application frontend
├── vercel.json         ← Configuration Vercel
└── README.md
```

## Déploiement (5 minutes)

### Étape 1 — Créer un compte Vercel
Aller sur https://vercel.com → Sign up (gratuit avec GitHub)

### Étape 2 — Obtenir une clé API Anthropic
Aller sur https://console.anthropic.com/keys → Create Key
Copier la clé (commence par sk-ant-...)

### Étape 3 — Déployer via Vercel CLI

```bash
# Installer Vercel CLI
npm install -g vercel

# Aller dans le dossier du projet
cd aztrader

# Déployer
vercel

# Suivre les instructions :
# ? Set up and deploy? → Y
# ? Which scope? → ton compte
# ? Link to existing project? → N
# ? Project name → aztrader
# ? Directory → ./
# → Deployment done!
```

### Étape 4 — Ajouter la clé API dans Vercel

```bash
vercel env add ANTHROPIC_API_KEY
# Coller ta clé sk-ant-...
# Select: Production + Preview + Development
```

Ou via le dashboard web :
→ Dashboard → Project → Settings → Environment Variables
→ Name: ANTHROPIC_API_KEY
→ Value: sk-ant-api03-xxxxxxx
→ Save

### Étape 5 — Redéployer pour appliquer les variables

```bash
vercel --prod
```

## ✅ Résultat
Ton application sera accessible sur :
`https://aztrader-xxxx.vercel.app`

Tu peux aussi configurer un domaine personnalisé dans :
Dashboard → Project → Settings → Domains

## Alternative — GitHub + Vercel (auto-deploy)

1. Créer un repo GitHub et uploader les fichiers
2. Aller sur vercel.com → New Project → Import Git Repository
3. Ajouter la variable ANTHROPIC_API_KEY
4. Chaque push sur main redéploie automatiquement

## Coût
- Vercel : **Gratuit** (100GB bandwidth/mois, serverless functions incluses)
- Anthropic API : pay-per-use (~$0.003 par analyse avec claude-sonnet)
