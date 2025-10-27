---
cover: >-
  https://images.unsplash.com/photo-1515922912707-dbc512030899?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHxzcGhlcmV8ZW58MHx8fHwxNzI5MzA4NTk3fDA&ixlib=rb-4.0.3&q=85
coverY: 0
---

# Expert Fullstack

Que signifie réellement être un « développeur FullStack » ?

Cela ne signifie pas que vous savez programmer un peu sur le serveur et écrire un peu de HTML/Javascript/CSS sur le front-end.

Il y a beaucoup plus à maîtriser pour maîtriser l'ensemble des modules nécessaires au fonctionnement d'une application web.

Pour intégrer ce programme, vous avez sans doute déjà développé des applications web, et ce premier cours servira à la fois de grande **révision** de ce que vous devriez déjà savoir, mais vous poussera également à considérer et à apprécier toutes les nuances du développement et du déploiement full-stack.

De plus, dans l'esprit d'un futur Tech-Lead et CTO, vous serez amené à réfléchir de manière stratégique à des questions transversales essentielles à tout projet ou déploiement :
- sécurité
- maintenabilité
- disponibilité
- coordination
- ...


## Objectifs


## Contexte


## Projet

Votre entreprise va se positionner sur le nouveau marché émergent de la facturation électronique.

Vous devez créer un SaaS permettant la création de factures B2B, prêtes à être transmises à une PA (Plateforme agréée).

Votre SaaS doit disposer des fonctionnalités suivantes :
- permettre la création de nouveaux comptes clients (vos clients)
- chacun de vos clients peut avoir :
  - plusieurs utilisateurs, avec le rôle « Admin » ou « Utilisateur »
  - une liste de leurs clients (les clients de nos clients)
  - une liste d'« Articles », c'est-à-dire les produits ou services vendus par les clients, y compris l'unité, le prix unitaire, la TVA applicable.
  - une liste de « Factures »

Votre logiciel doit :
- permettre à l'utilisateur de créer des factures
- personnaliser leur contenu
- finaliser et publier les factures
- télécharger le PDF
- inclure dans le PDF les métadonnées Factur-X permettant le transfert électronique vers une administration publique

Tout cela doit être fait tout en veillant à ce que la facture soit conforme à la réglementation française en termes de contenu, de stockage et de traçabilité du cycle de vie.

[Vous trouverez plus d'informations sur la facturation ici](./invoicing/intro.md).

Pour ce projet, vous devez créer et déployer un système informatique distribué (client-serveur) afin de fournir ce service. La pile architecturale requise est la suivante :
- Côté serveur
  - Une base de données SQL (MariaDB obligatoire)
  - Une API en NodeJS (Nest JS obligatoire)

Côté client (dans le navigateur d'un utilisateur)
- Une application frontale à page unique (SPA) - Angular obligatoire

Votre projet doit être déployé sur un véritable serveur hébergé dans le cloud (fourni par l'intervenant). Vous devrez donc maîtriser toutes les compétences requises pour vous connecter à ce serveur et le configurer.

Le projet final sera évalué au cours de la semaine du 12 janvier 2026. Vous disposez donc d'environ deux mois pour le mener à bien.

Toutefois, vous bénéficierez tout au long de votre parcours de cours spécifiques sur des thèmes pertinents liés à l'ingénierie, qui sont tous répertoriés ici.

Vous passerez également plusieurs évaluations intermédiaires afin de mesurer vos progrès et votre compréhension des différents thèmes abordés.