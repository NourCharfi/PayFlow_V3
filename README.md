# PayFlow_V3

Statut : Prototype étudiant — Application de gestion des paiements et factures (architecture microservices)

---

## Résumé du projet

PayFlow_V3 est un projet académique qui illustre une architecture microservices pour la gestion des produits, factures, paiements et authentification. Le projet combine des services Java (backend), une interface/clients en TypeScript/HTML/CSS et des scripts PowerShell pour la construction et l'orchestration via Docker Compose.

Objectifs pédagogiques :
- Concevoir et déployer une application distribuée (microservices)
- Utiliser la découverte de services (Eureka), un gateway, et une configuration centralisée
- Automatiser la construction et le déploiement avec Docker / scripts PowerShell
- Travailler avec une base de données SQL (script `setup.sql` fourni)

---

## Analyse rapide du dépôt

Structure principale (dossiers/services importants) :
- authentificationservice/ — service d'authentification
- client-service/ — gestion des clients
- produit-service/ — gestion des produits
- factureservice/ — gestion des factures
- reglement-service/ — gestion des paiements/règlements
- eureka-discoveryservice/ — serveur de découverte (Eureka)
- gatewayservice/ — API Gateway
- config-service/ — configuration centralisée
- PayFlow_Manager/ — composant manager / orchestration côté applicatif
- cloud-conf/ — configurations cloud (si utilisées)
- Fichiers utiles à la racine :
  - `docker-compose.yml` — orchestre les services en containers
  - `setup.sql` — script de création/population de la base de données
  - `build-and-run.ps1`, `build-all.ps1`, `start-services.ps1`, `update-dockerfiles.ps1` — scripts PowerShell pour construire/metter à jour et lancer les services

Technologies dominantes : TypeScript, Java, Docker, SQL, HTML/CSS, PowerShell.

Points forts :
- Architecture microservices complète (discovery, config, gateway, services métier)
- Scripts d'automatisation et orchestration Docker prêts
- Script SQL de setup fourni

## Installation / Exécution (rapide)

1. Cloner le dépôt
   ```
   git clone https://github.com/NourCharfi/PayFlow_V3.git
   cd PayFlow_V3
   ```

2. Préparer la base de données
   - Importer `setup.sql` dans votre instance SQL (MySQL/Postgres selon config attendue).
   - Exemple (MySQL) :
     ```
     mysql -u root -p < setup.sql
     ```
   - Alternativement, si `docker-compose.yml` contient un service DB, laissez Docker initialiser la base via volume / script.

3. Lancer avec Docker Compose (recommandé)
   ```
   docker-compose up --build
   ```
   - Sur Windows PowerShell, vous pouvez utiliser `./start-services.ps1` ou `./build-and-run.ps1` si les scripts sont configurés pour votre environnement.

4. Vérifier les services
   - Eureka (Discovery) : http://localhost:<eureka-port> (vérifier `docker-compose.yml`)
   - Gateway : http://localhost:<gateway-port>
   - Autres services : ports exposés listés dans `docker-compose.yml`

Remarque : les ports et variables dépendent de la configuration dans `docker-compose.yml` et fichiers de configuration dans `config-service`.

---

## Scripts fournis (racine)

- build-all.ps1 — construit tous les composants (PowerShell)
- build-and-run.ps1 — construit puis lance les services
- start-services.ps1 — démarre les services (PowerShell)
- update-dockerfiles.ps1 — met à jour les Dockerfiles (PowerShell)
- docker-compose.yml — composition et orchestration des services
- setup.sql — script SQL de création / population

Conseil : lisez chaque script pour adapter les chemins/versions selon votre environnement.

---

## Architecture & flux (synthèse)

- Config-Service centralise la configuration (Spring Cloud Config ou équivalent)
- Eureka fournit la découverte des services
- Gateway sert de point d'entrée (routage + éventuels filtres/auth)
- Services métiers (produit, client, facture, règlement, authentification) exposent des API REST
- PayFlow_Manager orchestre / surveille ou fournit UI d'administration
- Base de données(s) centralisées ou par service (selon configuration)
