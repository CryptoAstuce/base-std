# Chapitre 4 -- La fenêtre de bootstrap et les initCalls

Entre la création d’un token et le retour de `createB20`, une fenêtre courte et unique s’ouvre : celle des `initCalls`. Chaque entrée de ce tableau est exécutée sur le token fraîchement créé, dans l’ordre, avant que quiconque n’en ait le contrôle normal.

Pendant cette fenêtre, la Factory bénéficie d’un contournement partiel des contrôles habituels : les vérifications de rôle et les policies côté transfert (`TRANSFER_SENDER_POLICY`, `TRANSFER_RECEIVER_POLICY`, `TRANSFER_EXECUTOR_POLICY`) sont désactivées pour les appels provenant de la Factory. C’est ce qui permet à un seul `createB20` d’enchaîner `grantRole`, `updatePolicy`, un mint initial et un transfert de bootstrap, sans que la Factory elle-même ait besoin de détenir le moindre rôle.

Ce contournement n’est pas total, et c’est la partie à retenir. Trois garde-fous restent actifs même pendant la fenêtre : `MINT_RECEIVER_POLICY` est toujours évaluée, pour qu’un mint initial ne puisse jamais atterrir sur un compte refusé par la politique de conformité ; la pause n’est jamais court-circuitée, elle démarre à l’état "rien de pausé" donc un token qui doit naître déjà en pause doit placer son `pause(...)` en dernier dans la liste des `initCalls` ; et les invariants du token (comptabilité des soldes, plafond de supply) s’appliquent sans exception.

Dès que `createB20` retourne, la fenêtre se referme définitivement.

Fichier central : `src/interfaces/IB20Factory.sol`, section `createB20`.

[Chapitre suivant : comment un token B20 est reconnu](05-reconnaissance-token-0xb2.md)
