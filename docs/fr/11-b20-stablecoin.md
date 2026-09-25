# Chapitre 11 -- IB20Stablecoin, la variante simplifiée

Face à `IB20Asset` et ses options d’émission généraliste, `IB20Stablecoin` prend le chemin inverse : une interface volontairement minimale, qui n’ajoute qu’une seule fonction à `IB20`, `currency()`, retournant un code devise auto-déclaré (`"USD"`, `"EUR"`, `"JPY"`...). Le nombre de décimales n’est plus un choix à la création : il est fixé à 6 pour toute la variante Stablecoin, là où `IB20Asset` autorise n’importe quelle valeur entre 6 et 18 via `B20Constants.MIN_ASSET_DECIMALS` et `MAX_ASSET_DECIMALS`.

Côté création, `B20StablecoinCreateParams` ne demande que le nom, le symbole, l’administrateur initial et la devise -- pas de multiplicateur, pas d’annonces, pas de batchMint. Tout le reste (rôles, policies, pause, permit EIP-2612) vient directement du socle `IB20` commun aux deux variantes, sans duplication de logique.

Le code devise est validé par la Factory à la création : une chaîne non vide doit contenir uniquement des caractères ASCII majuscules `A` à `Z`, sous peine de `InvalidCurrency`. La Factory encode ensuite ce code dans `variantEventParams` du `B20Created` émis à la création, via `B20StablecoinEventParams`, pour que les indexeurs puissent retrouver la devise d’un stablecoin sans avoir à interroger le contrat lui-même.

Fichier central : `src/interfaces/IB20Stablecoin.sol`, `src/interfaces/IB20Factory.sol`.

[Chapitre suivant : l’Activation Registry et l’évolution du protocole](12-activation-registry-hardforks.md)
