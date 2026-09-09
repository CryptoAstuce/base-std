# Parcours français — Base Std

## Intention
Ce dépôt rassemble les interfaces Solidity des précompilés Base. Pour CryptoAstuce, il sert de référence ABI lors de l’intégration de contrats DeFi et NFT.

## Architecture
Repérer interfaces, bibliothèques et mocks, puis relier chaque signature au comportement réseau attendu.

## Flux de données
Suivre un appel depuis le contrat utilisateur jusqu’au précompilé, en notant encodage, retour et gestion d’erreur.

## Sécurité
Contrôler permissions, types, valeurs limites, reentrance et hypothèses sur l’adresse du précompilé.

## Compatibilité Base
Comparer les adresses, versions d’ABI et différences entre Base mainnet, Sepolia et tests locaux.

## Lecture guidée
Lire README, interfaces, mocks et tests dans cet ordre pour transformer l’ABI en intégration vérifiable.

## Exploitation
Conserver versions, paramètres RPC, journaux et procédure de diagnostic lors d’une évolution.

## Glossaire
Définir précompilé, ABI, mock, calldata et compatibilité sans reprendre un autre parcours.

Parcours documentaire : aucun test ni déploiement exécuté.
