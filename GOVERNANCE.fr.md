# Gouvernance

ANP est maintenu par un seul auteur à ce stade (v0.1). Ce document explique comment les décisions sont prises aujourd'hui, et comment cela est amené à évoluer à mesure que le projet mûrit.

## Modèle actuel : mainteneur bienveillant, critique ouverte

- **Serge Olivier KITT** est le seul mainteneur et a le dernier mot sur les fusions vers `main`.
- Ce n'est pas destiné à durer. Cela reflète où en est réellement le projet — un draft précoce, pas un standard mature — pas une revendication d'autorité permanente dessus.
- N'importe qui peut ouvrir une issue ou une pull request. Aucune approbation préalable n'est nécessaire pour proposer un changement, seulement pour le fusionner.

## Comment les décisions sont prises

- **Changements éditoriaux / de formulation** (fautes, clarté, traduction) : revus et fusionnés directement, sans discussion nécessaire.
- **Changements structurels** (rôle d'une couche, nouveau mécanisme, changement de nom) : doivent d'abord passer par une issue, ouverte au moins quelques jours, avant qu'une pull request ne soit fusionnée. Cela laisse le temps aux gens de réagir plutôt que de découvrir un changement après coup.
- **Changements contestés ou à fort enjeu** (en particulier tout ce qui touche au modèle sémantique de la Couche 4, aux mécanismes de vérification de la Couche 0, ou aux principes de gouvernance de la Couche T) : le mainteneur résumera publiquement la discussion avant de trancher, et expliquera le raisonnement derrière la décision finale — même quand elle ne suit pas la majorité des commentaires.

## Ce qui se passera si le projet grandit

Si ANP attire un groupe soutenu de contributeurs actifs, l'intention est d'évoluer vers un **modèle de groupes de travail** : des groupes informels organisés autour de couches spécifiques (par exemple un groupe alignement sémantique pour la Couche 4, un groupe vérification pour la Couche 0), chacun pouvant proposer des changements sur son périmètre avec moins de friction qu'un mainteneur unique qui reviserait tout seul.

Un organe de gouvernance formel (comité de pilotage, fondation, ou équivalent) n'est pas mis en place de façon préventive. En créer un avant qu'il existe une vraie communauté à gouverner serait du théâtre de gouvernance, pas de la gouvernance.

## Ce que ce projet ne fera pas

- Il n'acceptera pas de financement ou de conditions de partenariat qui exigeraient de fermer une partie de la spécification du protocole.
- Il n'accordera à aucune entreprise ou organisation unique un droit de veto sur l'orientation d'une couche en échange d'un financement ou d'un soutien.

## Gestion des versions

Les changements substantiels au modèle sont consignés dans la section historique des versions du whitepaper (voir `docs/ANP_whitepaper_draft.md`), pas fusionnés silencieusement sans trace.
