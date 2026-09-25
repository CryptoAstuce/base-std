# Chapitre 8 -- Le Policy Registry et les listes de conformité

Le Policy Registry est un singleton partagé par tous les tokens B20 : au lieu que chaque émetteur code sa propre logique de conformité, il crée une policy dans ce registre central et la référence par un `uint64 policyId`. Deux types simples existent, `BLOCKLIST` (autorisé par défaut, sauf figuration sur la liste) et `ALLOWLIST` (refusé par défaut, sauf figuration sur la liste), plus deux types composites qui combinent jusqu’à quatre policies simples existantes : `UNION` (autorise si au moins une policy enfant autorise) et `INTERSECT` (autorise seulement si toutes les policies enfant autorisent). Un composite ne peut jamais référencer un autre composite -- seulement des policies simples.

Chaque policy a un administrateur, transférable en deux étapes : `stageUpdateAdmin` propose un nouvel administrateur, qui doit ensuite appeler lui-même `finalizeUpdateAdmin` pour prendre effet. Un administrateur peut aussi renoncer définitivement via `renounceAdmin` : le set de membres se fige alors pour toujours, mais les requêtes `isAuthorized` continuent de fonctionner normalement.

Point important pour l’intégrateur : `isAuthorized(policyId, account)` ne revert jamais, même pour un `policyId` inexistant ou malformé -- il retombe silencieusement sur la sémantique d’un ensemble vide (`false` pour une allowlist, `true` pour une blocklist). C’est aux appelants qui stockent des `policyId` de valider `policyExists` au moment de l’écriture.

Fichier central : `src/interfaces/IPolicyRegistry.sol`.

[Chapitre suivant : rattacher une policy à un token](09-policy-scopes.md)
