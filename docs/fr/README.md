# Parcours français : base-std (standard B20 de Base)

Lecture commentée du dépôt base/base-std : la bibliothèque Solidity qui documente les précompiles à état B20 de Base (Factory, Policy Registry, Activation Registry) et le standard de token conforme qu’elles font tourner nativement dans le client.

## Sommaire

1. [Présentation de base-std et du standard B20](01-presentation.md)
2. [Précompiles contre contrats classiques](02-precompiles-vs-contrats.md)
3. [IB20Factory et createB20](03-factory-createb20.md)
4. [La fenêtre de bootstrap et les initCalls](04-fenetre-bootstrap-initcalls.md)
5. [Comment un token B20 est reconnu](05-reconnaissance-token-0xb2.md)
6. [IB20, le socle ERC-20 et les rôles](06-ib20-socle-roles.md)
7. [Les quatre vecteurs de pause et la saisie](07-pause-vectors.md)
8. [Le Policy Registry et les listes de conformité](08-policy-registry.md)
9. [Rattacher une policy à un token](09-policy-scopes.md)
10. [IB20Asset et le multiplicateur d’affichage](10-b20-asset-multiplier.md)
11. [IB20Stablecoin, la variante simplifiée](11-b20-stablecoin.md)
12. [L’Activation Registry et l’évolution du protocole](12-activation-registry-hardforks.md)
13. [Limites et périmètre de ce parcours](13-limites-perimetre.md)

Ce parcours est une lecture pédagogique du code source et de la documentation du dépôt, sans installation ni exécution du projet.
