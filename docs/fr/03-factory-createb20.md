# Chapitre 3 -- IB20Factory et createB20

Un token B20 ne peut naître que d’un seul point d’entrée : `createB20(variant, salt, params, initCalls)` sur la Factory, précompile singleton unique. L’appelant choisit une variante (`ASSET` ou `STABLECOIN`), un salt arbitraire, des `params` encodés en ABI contenant le nom, le symbole, l’administrateur initial et les champs propres à la variante, et une liste optionnelle `initCalls` de rappels exécutés juste après la création.

L’adresse du nouveau token n’est pas aléatoire : elle est déterministe, dérivée de `(variant, sender, salt)` via `getB20Address`, ce qui permet de la prédire avant même d’appeler `createB20`. Si un token existe déjà à cette adresse, l’appel échoue avec `TokenAlreadyExists` -- il faut changer de salt.

`B20FactoryLib` fournit des encodeurs purs pour construire ces `params` et ces `initCalls` sans jamais toucher à la précompile elle-même : `encodeAssetCreateParams`, `encodeStablecoinCreateParams`, et des constructeurs de lots comme `buildRoleGrants` qui transforment un struct `B20RoleHolders` en une liste d’appels `grantRole` prêts à être passés en `initCalls`, en sautant automatiquement les adresses nulles.

Une fois `createB20` terminé, la Factory n’a plus aucun accès persistant au nouveau token : la création est un événement en une seule transaction, sans lien de dépendance après coup.

Fichiers centraux : `src/interfaces/IB20Factory.sol`, `src/lib/B20FactoryLib.sol`.

[Chapitre suivant : la fenêtre de bootstrap](04-fenetre-bootstrap-initcalls.md)
