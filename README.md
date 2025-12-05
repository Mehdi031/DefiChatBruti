DefiChatBruti — Chat Perché 🤡🐱

Un chatbot volontairement à côté de la plaque : drôle, confiant, “philosophe du dimanche”, parfois inutile… mais toujours vivant.
Interface type iMessage, avec mode LOCAL (réponses fake) ou OPENAI (réponses générées via API).

Prérequis

Node.js (idéalement 18+ / 20+)

npm

Installation

1) Cloner le repo

git clone https://github.com/RobertGriffaton/DefiChatBruti.git
cd DefiChatBruti/chat-perche

2) Installer le front

npm install

Lancer le projet (2 terminaux)

Terminal A — Serveur (OpenAI) : localhost:3001

cd /Users/mehdi/DefiChatBruti/chat-perche/server
npm install
npx tsx index.ts

✅ Test rapide :

curl -i http://localhost:3001/health

Doit renvoyer :

{"ok":true}

Si le serveur crashe avec require is not defined in ES module scope : utilise des imports ESM dans server/index.ts (pas de require).

Clé OpenAI (obligatoire pour le mode OPENAI)

Crée un fichier .env dans chat-perche/server/ :

OPENAI_API_KEY=sk-...

Terminal B — Front (Vite) : localhost:5173

cd /Users/mehdi/DefiChatBruti/chat-perche
npm run dev

Ouvre ensuite :

http://localhost:5173

Utilisation

LOCAL : réponses “bruitées” et absurdes (pas d’API).

OPENAI : streaming SSE via le serveur Express.

Styles :

CYNIC : sarcasme / cynisme

POET : métaphores lunaires

GURU : pseudo-sagesse, max confiance

Fonctions UI :

Répondre à un message (quote)

Copier

Éditer ses messages

Supprimer (soft delete)

Réactions emoji

Recherche dans la conversation

Bouton Stop (interrompt le stream)

Endpoints serveur

GET /health → { ok: true }

POST /api/chat/stream → streaming SSE

Exemple :

curl -N -X POST http://localhost:3001/api/chat/stream \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"Salut"}],"style":"CYNIC"}'

Dépannage

Page blanche côté front

Ouvre la console navigateur (Chrome: ⌥⌘J, Safari: ⌥⌘C) et regarde la première erreur.

Vérifie que src/main.tsx importe bien :

import './index.css';
import './App.css';

“Cannot GET /” sur localhost:3001

Normal : le serveur n’a pas de route /. Utilise /health.

OpenAI ne répond pas / erreur SSE

Vérifie .env dans server/

Vérifie que le serveur tourne (/health)

Vérifie que l’app appelle bien http://localhost:3001/api/chat/stream

Structure

chat-perche/
  src/
    App.tsx
    brain.ts
    main.tsx
    index.css
    App.css
  server/
    index.ts
    tsconfig.json (si TS/NodeNext)

Licence

Projet de défi.
