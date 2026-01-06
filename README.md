# Projet DevOps - Jenkins et GitHub Actions

## Description
Ce projet met en œuvre un pipeline CI/CD complet en utilisant Jenkins et GitHub Actions pour un projet Java Maven. L'objectif est d'automatiser les étapes de construction, de test, de déploiement et de notification pour garantir une livraison continue et fiable.

## Structure du Projet
```
Projet-DevOps-elkhattabimohamedamine/
├── README.md
├── pom.xml
└── src/
    ├── main/
    │   └── java/
    │       └── com/
    │           └── devops/
    │               └── Main.java
    └── test/
        └── java/
            └── com/
                └── devops/
                    └── MainTest.java
```

### Détails des Fichiers
- **`pom.xml`** : Contient les dépendances Maven, y compris JUnit pour les tests.
- **`Main.java`** : Classe principale qui affiche un message de bienvenue.
- **`MainTest.java`** : Classe de test unitaire pour valider le fonctionnement de l'application.

## Pipelines CI/CD

### Jenkins Pipeline
Le fichier `Jenkinsfile` contient les étapes suivantes :
1. **Checkout** : Récupération du code source depuis GitHub.
2. **Build** : Compilation du projet avec Maven.
3. **Test** : Exécution des tests unitaires avec Maven.
4. **Archive** : Archivage des artefacts générés.
5. **Deploy** : Déploiement de l'application.
6. **Notify Slack** : Notification des résultats du pipeline sur Slack.

#### Points Clés :
- **Gestion des Artefacts** : Les fichiers générés sont archivés pour une utilisation future.
- **Notifications** : Les notifications Slack permettent de suivre l'état du pipeline en temps réel.
- **Rapports de Tests** : Les résultats des tests sont publiés sous forme de rapports JUnit.

### GitHub Actions Workflow
Le fichier `.github/workflows/maven-build.yml` contient les étapes suivantes :
1. **Checkout** : Récupération du code source.
2. **Setup JDK** : Configuration de Java 17.
3. **Cache Maven** : Mise en cache des dépendances Maven.
4. **Build et Test** : Exécution de `mvn clean test`.
5. **Package** : Création du package avec `mvn package`.

#### Points Clés :
- **Automatisation** : Le workflow est déclenché automatiquement sur les branches `main` et `dev`.
- **Optimisation** : Utilisation de la mise en cache pour réduire le temps de build.
- **Compatibilité** : Fonctionne sur un environnement Ubuntu.

## Commandes Maven
- `mvn clean install -DskipTests` : Build sans exécuter les tests.
- `mvn test` : Exécuter les tests unitaires.
- `mvn package` : Générer le fichier JAR.

## Notifications
- **Slack** : Notifications configurées pour les succès et échecs du pipeline Jenkins.
  - Exemple de message en cas de succès :
    ```
    ✅ Build #42 terminé avec succès!
    Projet: devops-project
    Durée: 2m 30s
    Lien: http://jenkins.local/job/devops-project/42/
    ```
  - Exemple de message en cas d'échec :
    ```
    ❌ Build #42 échoué!
    Projet: devops-project
    Vérifiez les logs ici: http://jenkins.local/job/devops-project/42/console
    ```

## Bonnes Pratiques
- **Tests Unitaires** : Toujours écrire des tests pour valider les fonctionnalités.
- **Automatisation** : Utiliser des pipelines CI/CD pour réduire les erreurs humaines.
- **Notifications** : Configurer des notifications pour être informé rapidement des problèmes.
- **Versioning** : Utiliser des branches `main` et `dev` pour séparer les environnements de production et de développement.

## Auteur
- **Nom** : Mohamed Amine El Khattabi
- **Date** : 6 janvier 2026
- **Contact** : [medamine4elkhattabi@gmail.com](mailto:medamine4elkhattabi@gmail.com)

## Licence
Ce projet est sous licence MIT.

# Projet DevOps - El Khattabi Mohamed Amine
Branch dev - En cours de développement


