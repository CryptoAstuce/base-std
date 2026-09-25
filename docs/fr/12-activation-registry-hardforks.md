# Chapitre 12 -- L’Activation Registry et l’évolution du protocole

L’Activation Registry est le plus simple des trois singletons, et le plus politique : un unique administrateur d’activation peut activer ou désactiver des fonctionnalités identifiées par un `bytes32` opaque, via `activate` et `deactivate`. `isActivated` ne revert jamais ; `checkActivated` est un simple raccourci qui revert avec `FeatureNotActivated` si besoin, pour éviter que chaque appelant ne redéfinisse cette même erreur. C’est ce registre que `createB20` interroge avant d’autoriser la création d’une nouvelle variante -- désactiver une variante bloque les nouvelles créations, sans jamais toucher aux tokens déjà émis.

Ce contrôle d’activation s’inscrit dans un mécanisme plus large : B20 évolue par hardforks, les mêmes moments de changement de consensus que le reste de Base. Un hardfork peut introduire une toute nouvelle précompile (l’Activation Registry lui-même n’existe qu’à partir du hardfork Beryl) ou publier une nouvelle version de la logique d’une précompile existante. La contrainte absolue est que chaque version déjà livrée reste figée pour toujours : un bloc produit sous la logique Beryl doit continuer, indéfiniment, à s’exécuter avec cette même logique Beryl, même après qu’un hardfork Cobalt a introduit une nouvelle version. C’est ce qui permet à un node qui resynchronise depuis le bloc zéro d’aboutir exactement au même état qu’un node resté en ligne en continu -- aucune réécriture rétroactive n’est possible.

Fichier central : `src/interfaces/IActivationRegistry.sol`, `docs/architecture.md` section 3.

[Chapitre suivant : limites et périmètre de ce parcours](13-limites-perimetre.md)
