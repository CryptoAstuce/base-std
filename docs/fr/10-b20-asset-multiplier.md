# Chapitre 10 -- IB20Asset et le multiplicateur d’affichage

`IB20Asset` étend `IB20` pour l’émission généraliste d’actifs, RWA compris, avec trois ajouts majeurs. Le premier est le multiplicateur UI, standardisé par ERC-8056 (`IScaledUIAmount` et ses extensions) : chaque token garde ses soldes bruts inchangés, mais expose un `uiMultiplier` (précision WAD, `1e18` = 1.0) qui redimensionne uniquement la vue affichée, via `toUIAmount` / `fromUIAmount`. Le principe rappelle wstETH qui enveloppe stETH -- sauf qu’ici, aucun wrapping n’est nécessaire : c’est le token lui-même qui expose sa vue mise à l’échelle. `updateUIMultiplier` planifie un changement à une date future (usage visé : splits d’actions, réinvestissement de dividendes) ; un seul changement peut être en attente à la fois, annulable via `cancelUIMultiplierUpdate`.

Le second ajout est `announce` : une fonction qui poste un événement `Announcement`/`EndAnnouncement` autour d’une série d’appels internes exécutés par self-delegatecall, idéale pour grouper une annonce corporate (par exemple un split) avec l’opération qui l’accompagne, de façon atomique et traçable.

Le troisième est `batchMint`, qui émet vers plusieurs destinataires en un seul appel tout-ou-rien, et `extraMetadata`, un magasin clé/valeur libre pour des champs comme `"category"` ou `"region"` que l’émetteur définit lui-même.

Fichier central : `src/interfaces/IB20Asset.sol`, `src/interfaces/IERC8056.sol`.

[Chapitre suivant : IB20Stablecoin, la variante simplifiée](11-b20-stablecoin.md)
