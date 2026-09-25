# Chapitre 1 -- Présentation de base-std et du standard B20

base-std est la bibliothèque Solidity officielle qui documente et teste les précompiles B20 de Base : des interfaces, des bibliothèques d’aide et des mocks, pas une implémentation de token à déployer soi-même. B20 est le standard natif de Base pour émettre et gérer des actifs programmables on-chain -- une extension d’ERC-20 pensée dès le départ pour l’émission d’actifs du monde réel (RWA) et de stablecoins, avec la conformité comme brique de base plutôt que comme ajout.

La différence clé avec un ERC-20 classique : un token B20 ne tourne pas comme bytecode EVM ordinaire. Il s’exécute comme précompile native dans le client Base lui-même. Cela veut dire que ce dépôt ne contient pas le token, seulement la surface Solidity (interfaces) qui permet d’appeler ce token, plus les mocks utilisés pour tester sans dépendre d’une vraie précompile.

Trois précompiles composent le système : la Factory (création des tokens), le Policy Registry (listes de conformité partagées) et l’Activation Registry (interrupteur de fonctionnalités contrôlé par Base). Ce parcours suit ces trois pièces puis le token B20 lui-même et ses deux variantes, Asset et Stablecoin.

Fichiers centraux : `src/StdPrecompiles.sol`, `src/interfaces/IB20.sol`, `src/interfaces/IB20Factory.sol`, `src/interfaces/IPolicyRegistry.sol`, `src/interfaces/IActivationRegistry.sol`, `src/interfaces/IB20Asset.sol`, `src/interfaces/IB20Stablecoin.sol`, `src/lib/B20Constants.sol`, `src/lib/B20FactoryLib.sol`, ainsi que `docs/overview.md` et `docs/architecture.md` pour le contexte.

Rien n’a été installé, compilé ni exécuté pour écrire ces chapitres.

[Chapitre suivant : précompiles contre contrats classiques](02-precompiles-vs-contrats.md)
