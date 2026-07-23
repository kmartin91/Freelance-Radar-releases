# 📡 Freelance Radar

> **Ton radar personnel à missions freelance.** Il scanne une trentaine de sources (posts LinkedIn,
> Free-Work, Codeur, boards remote…), ne garde que les vraies offres dev qui matchent ton profil et
> ton TJM, et t'accompagne jusqu'à la candidature — analyse IA, message personnalisé, pipeline kanban,
> relances. 100 % local : tes clés, tes cookies et tes données ne quittent pas ta machine.

---

## 🧭 À quoi ça sert

Chercher des missions freelance, c'est ouvrir 15 onglets par jour pour retomber sur les mêmes
annonces périmées, noyées au milieu d'offres CDI ou de posts marketing qui citent « JavaScript »
au détour d'une phrase. **Freelance Radar inverse le rapport de force** :

1. **Il scanne pour toi** — en un clic ou toutes les N minutes, sur ~27 sources en parallèle.
2. **Il filtre à ta place** — rôles dev uniquement, TJM minimum, fraîcheur de publication, remote.
3. **Il priorise** — score de matching avec ton profil, urgence, concurrence, scoring IA.
4. **Il t'aide à conclure** — analyse de l'offre, message de candidature généré, suivi des relances,
   stats de conversion.

---

## ✨ Fonctionnalités

### 🔎 Veille multi-sources
| | |
|---|---|
| **Posts LinkedIn** ⭐ | Recherche « mission + techno » directement **dans le feed** — là où les gens publient les vraies missions FR (« Mission React, TJM 550, ASAP… »). Nécessite le cookie `li_at` (guide intégré). |
| **LinkedIn Jobs** | Listings classiques (API guest, vraie date de publication, filtre fraîcheur serveur). Désactivable en un clic si tu ne veux que les posts. |
| **Free-Work** | Le plus gros board freelance IT français : TJM min/max réels, remote, durée, société. |
| **Codeur.com / Freelance-informatique / LeHibou** | Projets et missions FR (LeHibou via navigateur furtif). |
| **~20 boards remote** | RemoteOK, Remotive, WeWorkRemotely, Jobicy, Himalayas, HackerNews « Who is hiring », Indeed (furtif)… |

Chaque source tourne en parallèle, rate-limitée par domaine, avec un statut visible
(OK / erreur / désactivée + explication) — et **chaque source peut être activée/désactivée
individuellement** depuis « Statut des sources ».

### 🧠 Filtrage intelligent
- **Matching strict « profils dev »** — élimine les annonces non-dev qui mentionnent une techno en
  passant (commercial, marketing, PM, designer…), cascade mot-clé → blacklist → signaux dev.
- **Parsing TJM robuste** — devises, `/jour`, `/mois`, `k€`, « TJM : 600 »… converti en €/jour ;
  les offres sans TJM publié sont gardées et marquées, pas jetées.
- **Fraîcheur** — vraie **date de publication** extraite partout ; « Âge max publi » rejette au scan
  les offres trop vieilles ; purge définitive au-delà d'un seuil ; le cache entier est re-validé avec
  tes filtres à chaque scan.
- **Dédup cross-sources** — la même mission vue sur 3 boards = 1 carte, avec liens « aussi sur X ».
- **Feedback 👍/👎** — un rejet pénalise l'offre ; deux rejets sur la même société la masquent
  automatiquement.

### 📊 Priorisation & stats
- **Score de matching** (profil + mots-clés) et **score d'urgence** (fraîcheur, signaux « ASAP »).
- **Concurrence LinkedIn** — « Plus de 100 candidatures » détecté → badge + pénalité de score.
- **Scoring IA en batch** — après chaque scan, l'IA note le top 40 (match 0-100 + justification).
- **Stats TJM** — médiane par techno et évolution dans le temps (clic sur la tuile TJM).
- **Conversion** — candidatures envoyées → réponses → entretiens → gagnées, avec taux.

### 📋 Pipeline & organisation
- **Kanban drag & drop** — Nouveau / Shortlist / Postulé / Entretien / Gagné / Perdu.
- **Relances** — badge « ⏰ postulé il y a X j » dès 3 jours sans réponse + rappel au lancement.
- **Archivage éclair** — touche `E`, l'offre disparaît, la suivante est sélectionnée.
- **Profils de recherche** — sauvegarde tes combos de filtres (« React remote 600+ », « PHP Paris »)
  et switche en un clic.
- **Enrichissement au clic** — la page de l'offre est fetchée une fois : descriptif complet,
  TJM caché dans le corps de l'annonce, emails de contact, date exacte.

### ✉️ Candidature
- **Analyse IA de l'offre** — résumé, points forts/faibles, recommandation (onglet dédié).
- **Message de candidature généré par IA** — personnalisé sur la mission et ton profil.
- **Extraction de contacts** — emails et liens LinkedIn trouvés sur la page de l'offre.
- **Pré-remplissage de formulaire** — Playwright ouvre la page et remplit nom/email/téléphone/message
  (tu vérifies et envoies toi-même, jamais d'envoi automatique).

### 🔔 Alertes & notifications
- **Alertes ciblées** — ne notifie que si TJM ≥ X **et** score ≥ Y (fini le « 300 nouvelles offres »).
- **Digest email quotidien** — top 10 du jour dans ta boîte à l'heure choisie (SMTP configurable).
- **Discord / Telegram** — webhooks avec bouton de test.
- **Notifications macOS / navigateur** en local.

### 🤖 IA au choix
OpenAI, **Anthropic (Claude)**, Mistral, OpenRouter, ou **tout endpoint compatible OpenAI**
(Ollama en local sans clé, Groq…). Clé, modèle et URL configurés dans l'UI, stockés uniquement
dans `config.json`.

### 🎛 Confort
- Guide de démarrage intégré (cookie LinkedIn pas à pas, clé IA) — bouton `?`.
- Recherche instantanée, filtres par source / étape / âge, tri, navigation clavier `↑` `↓`.
- **Export CSV / JSON** de la vue filtrée (CSV compatible Excel).
- Thème sombre / clair, design accessible (`prefers-reduced-motion`, focus visibles).

## ⌨️ Raccourcis

| Touche | Action |
|---|---|
| `↑` / `↓` | Naviguer dans la liste |
| `E` | Archiver / désarchiver l'offre sélectionnée |
| `Échap` | Fermer les modales |

---

## 🔌 API locale (extraits)

| Endpoint | Rôle |
|---|---|
| `POST /refresh` · `GET /jobs` | Lancer un scan · lire les offres + statuts |
| `POST /config` · `GET /config` | Configuration |
| `POST /enrich` · `POST /job-analysis` · `POST /ai-message` | Enrichir · analyser · rédiger |
| `POST /pipeline` · `POST /feedback` · `POST /archive` | Organiser |
| `POST /purge` | Supprimer les offres plus vieilles que N jours |
| `GET /stats/tjm` · `GET /stats/pipeline` | Stats TJM · conversion |
| `POST /digest/send` · `POST /notify/test` | Tester email · webhooks |

---

## ⚠️ À savoir

- **LinkedIn** : l'usage du cookie `li_at` pour scraper est **contraire aux CGU LinkedIn**.
  Usage personnel, rate-limité, à tes risques. Le cookie reste sur ta machine.
- [Dernières releases](https://github.com/kmartin91/Freelance-Radar-releases/releases)
