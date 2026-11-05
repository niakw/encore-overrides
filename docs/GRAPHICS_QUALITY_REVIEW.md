# Revue des recommandations graphiques Encore R07/R24

5 novembre 2026. Analyse reproductible des fiches sans promotion automatique.
Commande : python3 tools/audit_graphics_recommendations.py

## Inventaire vérifié

8 993 jeux catalogués, dont **8 992 auto-baseline** sans mesure console
propre au jeu et **une seule fiche spécifique FC 27**
(0100C49025D3E000).

- Minimum : Bilinear, AA Off pour les jeux automatiques
- Recommended : Bilinear, FXAA pour tous les jeux
- High : Bicubic, FXAA pour les jeux automatiques
- Ultra : Bilinear, AA Off pour tous les jeux

Le runtime graphique Encore sait lire désormais les clés
lanczos, sgsr, sgsr_edge et fxaa_quality, mais refuse les options
réservées à Vulkan lorsqu'un profil choisit OpenGL. Les anciennes
clés, priorités des overrides manuels et recommandations sont conservées.
Le script d'audit rejette les combinaisons invalides et évite de
promouvoir ces shaders encore non mesurés dans les milliers de
baselines automatiques.

## Revue ciblée et ordre théorique

Qualité spatiale supposée sur jeux 3D (pas de métrique PS5) :
SGSR Edge > SGSR > FSR 1 > Lanczos > Bicubic > Bilinear > Nearest.
AA des contours : SMAA Ultra > FXAA+ > FXAA > Off.
Le classement peut s'inverser sur certaines scènes et Nearest est
souvent préférable pour pixel art.

Priorité 1 **FC 27** : conserver les réglages existants jusqu'à
comparaison de pelouse, tribunes, joueurs, HUD, scintillement,
VRAM et frametime GPU ; sa baseline inclut FSR 1 en Minimum et
Bilinear dans Recommended/High/Ultra, à dessein pour ménager la GPU.
Priorité 2 **BOTW** : scènes de feuillage, silhouettes, panoramiques,
transparence, texture et mesure GPU. Priorité 3 **NS2** : pas
de revendication tant que les images invitées ne sont pas présentées.

Un changement spécifique à un jeu devra être justifié par des
captures A/B, une séquence de mouvement, la version testée,
les mesures de frametime/VRAM et la qualité du HUD, avec
l'override manuel utilisateur toujours prioritaire.

FSR 3.1 temporel et véritable MSAA x2/x4/x8 ne sont pas implémentés ;
ne jamais les activer par profil ni leur attribuer un bénéfice.
**Aucun des 8 993 profils n'a été réécrit dans ce lot.**
