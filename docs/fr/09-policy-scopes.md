# Chapitre 9 -- Rattacher une policy à un token

Une policy ne fait rien tant qu’elle n’est pas rattachée à un emplacement précis sur un token. C’est le rôle de `updatePolicy(policyScope, newPolicyId)`, réservé à `DEFAULT_ADMIN_ROLE` : il branche un `policyId` du registre sur un `policyScope` du token, un peu comme on brancherait un hook sur une fonction spécifique.

`IB20` expose six scopes : `TRANSFER_SENDER_POLICY` et `TRANSFER_RECEIVER_POLICY`, vérifiés sur chaque transfert respectivement contre l’expéditeur et le destinataire ; `TRANSFER_EXECUTOR_POLICY`, vérifié uniquement sur `transferFrom` quand l’appelant diffère du propriétaire des fonds ; `MINT_RECEIVER_POLICY`, vérifié sur chaque mint ; et les deux scopes de saisie du chapitre précédent. Un slot jamais configuré répond `0`, le sentinel intégré "toujours autorisé" -- donc un token fraîchement créé sans aucune policy attachée se comporte comme un ERC-20 ordinaire.

Quand une opération touche un scope configuré, le token interroge le registre via `isAuthorized(policyId, account)` ; en cas de refus, l’appel revert avec `PolicyForbids(policyScope, policyId)`, une erreur qui identifie précisément quel slot a bloqué l’opération. C’est le même mécanisme qui explique pourquoi la fenêtre de bootstrap du chapitre 4 doit impérativement continuer à vérifier `MINT_RECEIVER_POLICY` : sans cette exception, la protection de conformité deviendrait contournable à la création.

Fichier central : `src/interfaces/IB20.sol`, section POLICY ; `docs/overview.md`.

[Chapitre suivant : IB20Asset et le multiplicateur d’affichage](10-b20-asset-multiplier.md)
