# Chapitre 7 -- Les quatre vecteurs de pause et la saisie

La pause d’un token B20 n’est pas globale : elle se découpe en quatre vecteurs indépendants, `TRANSFER`, `MINT`, `BURN` et `SEIZE`, chacun contrôlable séparément. Un émetteur peut ainsi geler uniquement les nouvelles émissions (`MINT`) pendant qu’un audit se termine, sans bloquer les transferts existants. `pause` exige `PAUSE_ROLE`, `unpause` exige `UNPAUSE_ROLE` -- deux rôles distincts, pour qu’un compte puisse avoir le pouvoir de geler sans avoir celui de dégeler.

Le mécanisme le plus spécifique à la conformité reste `seizeWithMemo` : une opération d’administrateur qui réassigne de force un solde d’un compte `from` vers un compte `to`, gatée par `SEIZE_ROLE`. Elle contourne volontairement l’allowance et les policies de transfert habituelles, mais reste soumise à deux vérifications de membership inversées par rapport au transfert normal : `from` doit être non autorisé sous `SEIZE_EXEMPT_POLICY` (c’est l’inverse d’une policy normale -- être "autorisé" sous ce slot rend un compte protégé contre la saisie, pas éligible à une opération), et `to` doit être autorisé sous `SEIZE_RECEIVER_POLICY`. Trois événements sont émis dans l’ordre : `Transfer`, `Memo`, puis `Seized`, qui trace explicitement l’appelant, la source et la destination.

Une méthode `burnBlocked`, marquée deprecated, subsiste pour compatibilité : elle brûle le solde d’un compte déjà bloqué sous `TRANSFER_SENDER_POLICY`, sans consommer d’allowance. La documentation recommande désormais `seizeWithMemo` suivi d’un `burn` classique.

Fichier central : `src/interfaces/IB20.sol`, sections PAUSE et MINT / BURN.

[Chapitre suivant : le Policy Registry et les listes de conformité](08-policy-registry.md)
