# Locker

Outil TrysCode prévu pour gérer des verrous opérationnels simples autour des
travaux sensibles. Le dépôt reste au stade documentaire tant que le contrat de
verrouillage, le stockage et les preuves de concurrence ne sont pas définis.

## Rôle

Préparer un mécanisme de verrouillage lisible sans fournir un faux runtime de
coordination.

## Responsabilités

- documenter le périmètre du futur verrouillage ;
- éviter les doubles exécutions sur les opérations qui devront être sérialisées ;
- garder la branche `develop` comme état de construction courant ;
- refuser les secrets et les endpoints internes directs dans le dépôt.

## Hors périmètre

Le dépôt ne fournit pas encore de service, CLI, base de données, lock distribué
ou intégration Kubernetes.

## Architecture

Socle documentaire sans runtime. Les accès privés TrysCode doivent passer par
Tailscale ou Services Kubernetes, jamais par une IP privée directe documentée en
dur.

## Prérequis

- Git ;
- accès au remote `origin/develop` ;
- accès Tailscale seulement si une ressource privée doit être consultée.

## Installation

Aucune installation applicative n'est requise à ce stade.

## Configuration

Aucune configuration runtime n'est disponible. Le futur contrat devra préciser
le backend de verrouillage, les expirations, les propriétaires et les règles de
libération.

## Variables d'environnement

Aucun secret ne doit être défini ou versionné dans ce dépôt.

## Commandes

```bash
git status --short --branch
```

Une future implémentation devra exposer une commande locale de validation et une
preuve de non-concurrence reproductible.

## Tests

Le contrôle actuel est documentaire. Les tests de concurrence devront couvrir
expiration, double acquisition, libération et reprise après échec.

## API et messages

Aucune API HTTP, queue RabbitMQ ou événement métier n'est exposé.

## Sécurité

Ne versionner aucun token, mot de passe, clé privée, URL interne directe ou
preuve contenant des chemins personnels.

## Observabilité

Aucune télémétrie runtime n'existe tant qu'aucun processus de verrouillage n'est
implémenté. Le futur outil devra journaliser propriétaire, durée et résultat
sans exposer de secret.

## Déploiement

Pas de déploiement runtime. Les changements courants partent sur `develop`;
`main` reste réservé aux releases cohérentes.

## Migrations

Toute migration vers un backend réel devra inclure rollback, durée maximale des
verrous, nettoyage sûr et compatibilité multi-repository.

## Dépannage

Vérifier l'état Git, la branche `develop` et l'absence de secret avant toute
publication.

## Contribution

Garder les changements atomiques, tester dès qu'un runtime apparaît et pousser
les travaux courants sur `develop`.

## Licence et statut

Statut interne TrysCode. La licence suit le fichier `LICENSE` si présent.

## Propriétaire

Baptiste RENNESON BOUTARD / équipe outillage TrysCode.

## Limitations

Ce dépôt ne prouve pas encore un verrou distribué. Il décrit seulement le futur
cadre de l'outil.
