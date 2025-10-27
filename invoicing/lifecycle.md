# Cycle de vie

Les factures ont un cycle de vie très strict selon la réglementation française, et votre logiciel doit respecter ce cycle afin d'éviter toute erreur de la part de vos utilisateurs.



## La phase de brouillon

En général, une nouvelle facture commence par un statut de brouillon.

Dans cet état, nous pouvons modifier la facture, préciser le client, ajouter des articles, etc.

Dans cet état, le numéro de facture n'est pas encore défini. Il ne sera attribué qu'une fois la facture publiée.

## Publication de la facture

Au moment de la publication, le numéro de facture est attribué de manière définitive.

Ce numéro est soumis à une contrainte très stricte : il doit contenir un numéro incrémentiel quelque part. Par exemple, nous pourrions utiliser un système de numérotation tel que 

```
FAC-2025-01
FAC-2025-02
FAC-2025-03
...
```

Le numéro ne peut jamais être répété et doit toujours augmenter.

La date d'émission est également définie lorsque nous publions une facture.

Une fois publiée, le PDF final est généralement rendu disponible au téléchargement. Un utilisateur peut alors l'imprimer ou l'envoyer par e-mail au client.

**Une facture publiée est figée : elle ne peut plus jamais être modifiée !!**

Il s'agit d'une règle très stricte. Une fois qu'une facture est publiée, son existence doit être garantie (par le numéro de facture croissant).

Mais que se passe-t-il en cas d'erreur ?

Une facture publiée n'est pas obligatoirement envoyée à un client. Si nous commettons une erreur, nous pouvons émettre un « avoir », un type spécial de facture avec un total négatif qui équilibre le compte du client. Nous devons alors créer une nouvelle facture dans laquelle nous corrigeons notre erreur.

Un auditeur peut alors consulter notre historique, qui sera le suivant :

- FAC-2025-66 pour un montant de 100 € (erreur)
- AVOIR-2025-67 pour un montant de -100 € (annule la dernière facture)
- FAC-2025-68 pour un montant de 150 € (remplace la facture 66)

Comme vous pouvez le constater, le numéro augmente toujours.


## Suivi du statut de paiement

Le contenu d'une facture publiée ne peut être modifié, mais à partir de septembre 2026, nous devrons suivre le statut de paiement de chaque facture et envoyer des rapports au gouvernement.

Le suivi du statut peut être effectué par votre banque (automatiquement lors du paiement), par votre logiciel de comptabilité ou manuellement.

Dans tous les cas, nous devons suivre si une facture a été payée, est toujours en attente de paiement, est considérée comme impayée (litigieuse), etc. Idéalement, vous devriez également pouvoir indiquer le moyen de paiement (espèces, chèque, virement, etc.).

## Conservation

Les factures émises doivent être conservées [pendant 10 ans](https://yousign.com/fr-fr/blog/delais-conservation-facture) par les entreprises en cas d'audit. Cela signifie que votre système ne doit pas permettre leur suppression et doit offrir un stockage sécurisé.

Toutefois, cela ne s'applique pas aux brouillons de factures, qui peuvent bien sûr être supprimés.