# Chapitre 2 -- Précompiles contre contrats classiques

Un contrat Solidity ordinaire est du bytecode EVM stocké à une adresse ; l’interpréteur EVM le lit et l’exécute instruction par instruction. Une précompile est différente : c’est du code compilé dans le client lui-même (ici, le node Base, écrit en Rust). Sur chaque `CALL` ou `STATICCALL`, le node vérifie d’abord si l’adresse cible figure dans un registre de précompiles. Si oui, le code natif tourne directement, sans jamais charger ni interpréter de bytecode. Sinon, le chemin EVM classique s’applique.

Les précompiles historiques d’Ethereum (`ecrecover`, `sha256`, `modexp`, etc.) suivent déjà ce mécanisme -- elles sont pures et sans état. B20 est différent : c’est la première précompile à état persistant de Base. Le Factory, le Policy Registry, l’Activation Registry et chaque token B20 lisent et écrivent dans le même modèle d’état EVM que n’importe quel contrat classique, avec le même layout de stockage ERC-7201 (une racine de namespace, des champs à des offsets fixes, des mappings hashés comme le ferait Solidity). La seule chose qui change, c’est que le code qui lit et écrit cet état n’est pas interprété depuis du bytecode -- il est natif.

Deux catégories de précompiles B20 existent : les singletons (Factory, Policy Registry, Activation Registry), à adresse fixe et enregistrés dans la table statique du node, et les tokens B20 eux-mêmes, créés dynamiquement à l’exécution et reconnus par un mécanisme différent (chapitre 5).

Fichier central : `docs/architecture.md` section 1.

[Chapitre suivant : IB20Factory et createB20](03-factory-createb20.md)
