# Kona Energy Card — version locale à tester

Adaptation de la distribution Lumina fournie par l'utilisateur (le code déclare 3.6.10). Le fichier original et cette copie utilisent des noms de cartes distincts.

## Installation manuelle dans Home Assistant

1. Décompresser le ZIP. Copier le dossier `kona-energy-card` dans le dossier `www/community` de votre configuration HA. Le résultat habituel est `/config/www/community/kona-energy-card/`.
2. Dans les ressources du tableau de bord, ajouter `/local/community/kona-energy-card/kona-energy-card.js?v=1`, de type **Module JavaScript**. Selon votre interface, activer le mode avancé de votre profil pour voir les ressources. Si le dossier `www` vient d'être créé, redémarrer HA pour qu'il soit servi.
3. Recharger complètement le navigateur. Ajouter une carte manuelle avec `configuration-exemple.yaml`.
4. Remplacer tous les identifiants fictifs `sensor.*` par vos entités. Ne pas coller cet exemple dans le fichier général `configuration.yaml` : c'est une configuration de carte Lovelace.

Pour conserver votre configuration Lumina actuelle, dupliquer la carte, remplacer son type par `custom:kona-energy-card`, puis définir les lignes suivantes :

```yaml
type: custom:kona-energy-card
image_style: real
background_image: /local/community/kona-energy-card/kona-background.png
battery_overlay_enabled: true
battery_overlay_image: /local/community/kona-energy-card/battery_real.png
car_label: KONA 2020
show_pv_strings: true
```

Conserver ensuite vos capteurs et les positions que vous avez déjà réglées. La nouvelle carte ne remplace pas automatiquement la carte HACS originale.

## Votre configuration visuelle

- Kona Electric 2020 gris foncé, représentation générée, sur la droite.
- Trois zones de panneaux : deux groupes au sol à gauche et un sur le toit. Ce placement est une proposition visuelle ; il ne décrit pas nécessairement votre installation réelle.
- Batterie stationnaire au premier plan, ajoutée par la carte, avec jauge de charge dynamique.
- Maison, pompe à chaleur, onduleur et réseau conservés.

Le fichier `kona-background.png` ne contient volontairement pas la batterie : celle-ci est superposée à partir de `battery_real.png`. L'image d'aperçu fournie séparément est une illustration et ne doit pas remplacer le fond, sous peine d'afficher deux batteries.

## Trois zones et total

`sensor_pv1`, `sensor_pv2`, `sensor_pv3` doivent recevoir les puissances des trois zones. La carte affiche leurs valeurs séparément et calcule le total. Les lignes Zone 1/2/3 sont regroupées dans le bloc solaire ; le flux principal représente la production agrégée. Les flux personnalisés permettent ensuite de tracer un chemin distinct par zone.

Ne pas affecter simultanément les mêmes mesures à plusieurs groupes. `sensor_pv_total`, lorsqu'il est renseigné, remplace la somme des chaînes du premier groupe. Pour utiliser la somme des trois zones, laisser ce paramètre absent/vide.

`sensor_daily` doit être l'énergie journalière totale. Il ne s'agit pas d'une puissance : utiliser Wh/kWh, pas W/kW. La carte ne crée aucun capteur ni aucune intégration HA.

## Fonctions avancées

Les réglages locaux sont disponibles sans mot de passe dans cette adaptation : 20 flux personnalisés, 20 textes personnalisés, 10 images superposées, fenêtres personnalisées et leurs styles, mini-caméras, affichage selon le mouvement, personnes, prévisions solaires fondées sur vos capteurs, aperçu de placement et autres réglages existants.

Disponibles ne signifie pas tous activés : chaque fonction doit être reliée à des entités existantes. Les caméras, commandes de lumières, alarmes ou véhicules utilisent les capacités et autorisations de HA. Cette copie n'ajoute pas une intégration Hyundai/Bluelink.

Non inclus : galerie distante et service IA proxy de l'auteur. Les demandes d'activation, notifications de licence et envois de statistiques d'installation à ce service ont été désactivés. Import/export local conservé. Les appels directs à un fournisseur IA avec votre propre clé peuvent rester payants ; aucun crédit ni abonnement n'est fourni. Des ressources externes de présentation (polices/GSAP) et les cartes géographiques de certains popups restent présentes dans le code.

## Vérifications et limites

Validation syntaxique du JavaScript et neuf vérifications isolées : enregistrement de la carte, valeurs par défaut, présence des réglages avancés, somme des trois zones, conversion W/kW, batterie, réseau, nuit, capteur indisponible et énergie journalière (certaines vérifications couvrent plusieurs points).

Pas de validation du rendu navigateur : l'accès à l'aperçu local a été refusé. Pas de test dans votre HA ni sur vos appareils. C'est une première version à tester sur une copie de votre carte. Le code hérité traite certaines mesures indisponibles comme zéro ; contrôler les entités dans les diagnostics plutôt que d'interpréter systématiquement zéro comme une mesure réelle.

Les textes et tracés peuvent nécessiter un ajustement avec le nouveau fond. Utiliser l'aperçu de placement dans l'éditeur. La représentation générée du véhicule n'est pas un modèle constructeur exact.

## Provenance

Les mentions d'origine sont conservées : `LICENSE`, `README.original.md`, `privacy.original.md`. L'archive reçue contient une contradiction : `LICENSE` indique MIT, tandis que le README annonce PolyForm Noncommercial. Cette adaptation ne résout pas cette incohérence et ne constitue pas une licence PRO officielle de l'auteur.

Documentation HA : https://developers.home-assistant.io/docs/frontend/custom-ui/custom-card/
