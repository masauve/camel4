
# Outils requis
## JBang
https://docs.redhat.com/en/documentation/red_hat_build_of_apache_camel/4.10/html/tooling_guide_for_red_hat_build_of_apache_camel/camel-cli-cq#installing-camel-jbang-cq

jbang:  https://www.jbang.dev/download/

## Maven

## OpenJDK 17+

## client openshift (oc)


# Répertoires
## camel
example de route d'intégration Camel:
- data : Ingestion de données à partir d'un topic kafka vers une BD postgres
- load : Générateur d'événements pour Kafka
- REST : API Rest pour interagir avec le système

## database
manifests pour déployer une base de données Postgres requise pour cette démonstration

## kafka
manifests pour déployer kafka sur OpenShift incluant la console, les roles et un single node KRaft cluster

## local
Fichier Podman compose pour mettre en place un environnement local
podman-compose -f kafka-postgres.compose.yaml up -d


# Utilisation

## pour lancer la route data en mode local:
`camel run data-ingestion.camel.yaml local.properties`

## Pour exporter sur OpenShift (déjà fait dans le github)
```
camel export --runtime=quarkus --gav=com.demo:data:1.0-SNAPSHOT --directory=./myproject
quarkus extension add 'quarkus-openshift'
quarkus ext add io.quarkus:quarkus-jdbc-postgresql
```

##Pour déployer:
`./mvnw install -Dquarkus.openshift.deploy=true`

