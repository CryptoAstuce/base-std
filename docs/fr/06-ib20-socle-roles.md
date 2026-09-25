# Chapitre 6 -- IB20, le socle ERC-20 et les rôles

`IB20` est la surface que tout token B20 implémente, quelle que soit sa variante. Elle reprend l’ERC-20 standard (`transfer`, `transferFrom`, `approve`, `balanceOf`, `allowance`) et l’enrichit de variantes memo (`transferWithMemo`, etc.) qui émettent un événement `Memo` juste après le `Transfer` standard, utile pour attacher une référence off-chain à une opération on-chain sans changer sa sémantique.

Le contrôle d’accès suit le modèle `AccessControl` d’OpenZeppelin, mais intégré nativement à la précompile plutôt que comme bibliothèque importée : un unique `DEFAULT_ADMIN_ROLE` accorde et révoque les rôles opérationnels (`MINT_ROLE`, `BURN_ROLE`, `PAUSE_ROLE`, `UNPAUSE_ROLE`, `METADATA_ROLE`, `SEIZE_ROLE`, `BURN_BLOCKED_ROLE`). Chaque fonction privilégiée vérifie d’abord le rôle, puis le vecteur de pause correspondant. Un détail volontaire : `renounceLastAdmin` permet de faire basculer un token dans un état sans administrateur, de façon permanente et irréversible -- utile pour un token dont on veut prouver qu’il ne sera plus jamais administré.

Côté métadonnées, `updateName` et `updateSymbol` sont réservés à `METADATA_ROLE` et émettent respectivement `NameUpdated` et `SymbolUpdated` ; changer le nom déclenche en plus `EIP712DomainChanged`, car le nom entre dans le calcul du domaine EIP-712 utilisé par `permit` (EIP-2612), également supporté nativement.

Fichier central : `src/interfaces/IB20.sol`.

[Chapitre suivant : les quatre vecteurs de pause et la saisie](07-pause-vectors.md)
