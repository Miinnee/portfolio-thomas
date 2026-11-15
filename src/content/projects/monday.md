---
title: "M.O.N.D.A.Y"
category: "Application de bureau · Projet Chronos"
summary: "L'application de gestion interne de Projet Chronos : pôles, tâches, planning, messagerie, IA et bot Discord qui rédige les comptes rendus de réunion."
cover: "/projects/monday.svg"
tags: ["Tauri", "Vue 3", "TypeScript", "Node.js", "MariaDB", "Discord"]
featured: true
---

## Le projet

**M.O.N.D.A.Y** est l'application de bureau que j'ai conçue pour gérer l'équipe de **[Projet Chronos](../projet-chronos/)**, l'association d'événements Minecraft que j'ai fondée. Elle réunit au même endroit tout ce dont le staff a besoin pour préparer et faire vivre nos événements : organisation par pôles, suivi des tâches, planning, communication interne et comptes rendus de réunion.

Elle tourne sur **Windows et Linux** et elle est **en production depuis novembre 2026**, utilisée au quotidien par l'équipe.

Je l'ai développée avec **Claude Code**, l'assistant de développement d'Anthropic, comme une partie de l'écosystème Projet Chronos. Je suis parti de maquettes Figma complètes (design system, écrans, modèle de données), puis j'ai avancé par petites étapes vérifiables : je définissais les besoins et les règles métier, je relisais et testais chaque fonctionnalité.

## Les fonctionnalités

- **Comptes et rôles** : hiérarchie Admin → Responsable de pôle → Staff, avec une matrice de permissions configurable par pôle. Les comptes sont créés par un admin, avec un mot de passe temporaire à changer à la première connexion.
- **Pôles et tâches** : chaque pôle (Build, Dev, Com, Anim…) a son **Kanban** avec glisser-déposer, des sous-tâches, des mises à jour d'avancement, des abonnés et des filtres par projet.
- **Projets en parallèle** : plusieurs événements peuvent être préparés en même temps, avec un compte à rebours jusqu'à l'ouverture.
- **Planning** : créneaux par pôle ou réunions staff, en vues jour, semaine, mois ou « event ».
- **Communication en temps réel** : messagerie privée et de groupe, tickets vers les admins, centre de notifications, notifications Windows, préférences et mode « Ne pas déranger ».
- **Chronos IA** : une palette `Ctrl K` pour poser des questions sur ses tâches et ses projets, le résumé d'une conversation et la proposition d'actions à transformer en tâches en un clic. L'IA propose et l'humain valide.
- **Bot Discord et comptes rendus** : le bot rejoint le salon vocal pendant une réunion, transcrit les échanges avec Gemini (aucun son n'est conservé), puis rédige un compte rendu. La personne qui a lancé la réunion le relit, et les actions validées deviennent automatiquement des tâches. Un export PDF est disponible.
- **Mises à jour automatiques** : les nouvelles versions sont signées et l'application se met à jour toute seule.

## L'architecture

```
Appli de bureau (Tauri + Vue)  ·  Bot Discord
            │  REST + WebSocket
        API M.O.N.D.A.Y (Fastify)
            │
   MariaDB  ·  Gemini (IA)
```

- **Application** : Tauri 2, Vue 3 et TypeScript, sans framework CSS. Le design system vient directement de Figma (thème clair et sombre).
- **API** : Node.js, Fastify 5, Drizzle ORM sur MariaDB et validation avec zod. Les droits sont vérifiés côté serveur, les mots de passe hachés avec argon2 et le temps réel passe par WebSocket.
- **Bot** : discord.js et @discordjs/voice, relié à l'API par WebSocket.
- **Code partagé** : un monorepo avec un paquet commun (rôles, permissions, types d'API) utilisé par l'appli, l'API et le bot.
- **Hébergement** : un Raspberry Pi 4 sous Debian, des services systemd, Caddy en HTTPS et un script de déploiement avec retour arrière automatique.
- **Qualité** : des tests unitaires et de bout en bout avec Vitest, ainsi que des revues de code.

## Ce que j'y ai appris

Mener un vrai produit de bout en bout : du design Figma à la mise en production, en passant par la conception d'une base de données, la gestion fine des permissions, le temps réel, l'intégration d'une IA et le déploiement sur mon propre serveur. Travailler avec Claude Code m'a aussi appris à bien découper un projet, à formuler des besoins précis et à garder un œil critique sur le code produit.
