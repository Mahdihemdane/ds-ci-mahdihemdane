# ds-ci-mahdihemdane

Ce dépôt contient trois microservices Spring Boot pour l'exercice CI/CD :

## 1. api-gateway
**Rôle :**point d'entrée unique pour tous les clients. Il route les requêtes vers les services backend, applique l'authentification, le throttling, et la gestion des erreurs.
**Exemples d'outils :**
- Spring Cloud Gateway (recommandé pour les applications Spring Cloud)
- Netflix Zuul (historique, moins maintenu)
- Kong ou Traefik (solutions API gateway standalone)

## 2. client-service
**Rôle :** service orienté "front-facing" (BFF — Backend For Frontend). Il adapte les réponses des microservices aux besoins d'une interface cliente (web/mobile).
**Exemples d'outils/technos :**
- Spring Boot (Spring Web / WebFlux) pour le backend BFF
- Node.js / Express ou Next.js si on choisit une solution JavaScript côté serveur

## 3. account-service
**Rôle :** service métier gérant les comptes utilisateurs (CRUD, authentification, profil).
**Exemples d'outils/technos :**
- Spring Boot + Spring Data JPA + PostgreSQL ou MySQL pour la persistance
- Spring Security pour l'authentification / autorisation

## CI/CD
Le workflow GitHub Actions (`.github/workflows/ci.yml`) :
- Se déclenche manuellement (`workflow_dispatch`) ou lors d'une Pull Request vers `main`.
- Build des trois microservices et publication des images Docker sur DockerHub.
- Variables sensibles stockées dans les GitHub Secrets : `DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`.

## Commandes utiles
- Compiler sans tests : `mvn clean package -DskipTests`
- Build image Docker : `docker build -t <dockerhub-username>/<image-name>:latest .`
- Push image Docker : `docker push <dockerhub-username>/<image-name>:latest`
