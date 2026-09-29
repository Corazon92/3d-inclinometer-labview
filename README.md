# Inclinomètre 3D — LabVIEW

> Acquisition d'un capteur 3 axes, calibration, calcul du tangage/roulis et visualisation 3D.  
> **English version below.**

## Contexte

Projet académique réalisé en binôme (**Samy Hammadi / Hiram Jordan**) autour d'un instrument virtuel LabVIEW capable de mesurer l'inclinaison d'un objet.

## Chaîne de mesure

`capteur 3 axes → acquisition analogique → mise à zéro → calibration → Gx/Gy/Gz → pitch/roll → affichage → visualisation 3D`

L'acquisition est configurée en mode **RSE** afin de référencer les tensions à la masse.

## Calibration

Mesures documentées :

| Axe | -90° | 0° | +90° | Sensibilité utilisée |
|---|---:|---:|---:|---:|
| X | 1.46845 V | 1.26454 V | 1.07082 V | 0.214 V/g |
| Y | 1.45837 V | 1.24432 V | 1.06085 V | 0.214 V/g |

Le rapport indique une sensibilité de **0.207 V/g pour Z** et précise que le zéro de Z est relevé avec la carte à 90°.

Pour X et Y, le traitement documenté est :
1. soustraction de la tension mesurée à plat ;
2. division par 0.214 V/g ;
3. rapport avec la composante Z ;
4. arctangente ;
5. conversion radians → degrés avec `180 / π`.

## Calcul des angles

Équations utilisées dans le projet :

`α = atan(Gx / Gz)` — tangage

`β = atan(Gy / Gz)` — roulis

## Validation physique

Le VI a été comparé à des angles physiques de **30° et 60°** à l'aide d'une équerre.

Le rapport relève une disparité de **7° sur le roulis à 60°**, tandis que les autres mesures testées restent cohérentes. Cette erreur expérimentale est conservée ici : elle montre la limite réelle de la calibration et non un résultat idéal reconstruit.

## Visualisation

Une seconde version du VI réutilise les calculs d'angles pour animer une représentation 3D de l'orientation.

## Limites et améliorations

Le rapport recommande :
- une calibration plus fine ;
- une fonction de mise à zéro ;
- une meilleure prise en compte des sensibilités différentes des axes ;
- une analyse des sources d'erreur expérimentale.

## Artefacts

Le compte rendu confirme le fonctionnement du VI final, mais le fichier binaire `Inclino3D_final.vi` n'a pas été retrouvé avec une correspondance suffisamment sûre lors de la récupération ciblée. Il n'est donc pas remplacé par un faux VI.

---

# English version

Academic LabVIEW project measuring **pitch and roll** from a three-axis sensor.

The processing chain is: analog acquisition → zero-offset correction → axis calibration → Gx/Gy/Gz → angle computation → gauges/numeric display → 3D visualization.

The documented equations are:

`pitch = atan(Gx / Gz)`

`roll = atan(Gy / Gz)`

X/Y calibration used 0.214 V/g while Z used 0.207 V/g. Physical checks were performed at 30° and 60°. A **7° roll error at 60°** was observed and is reported transparently as an experimental limitation.

The final VI is documented in the archived report, but the matching binary VI could not be recovered with enough certainty to publish it as the original.
