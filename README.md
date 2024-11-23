# ScartSwitcher
Scart switcher for old gaming stuff

## Mes ambitions

Créer une multiprise pour prises péritels afin de pouvoir y brancher toutes mes vielles consoles utilisant une péritel :
- Master system II
- NES
- SNES
- GameCube
- Wii
- PS1
- PS2
- Dreamcast

Soit 8 entrées pour une sortie unique.

L'objectif est bien de faire du PassThrought d'une des 8 entrées vers la sortie unique.

Je ne cherche pas obligatoirement à détecter quelle péritel est active sur les 8 (donc pas de switch automatique). Toutefois si
je trouve une solution simple et efficace, pourquoi pas !


## Inspiration

Cf. [Maker.pro](https://maker.pro/forums/projectlogs/wall-mounted-8-way-scart-switch.156/).

Pistes à creuser (et valdier) :

1) Architecture principale :

    Vous aurez besoin de plusieurs multiplexeurs en parallèle car une péritel contient différents types de signaux :

    3 voies pour le RGB (rouge, vert, bleu)
    1 voie pour la vidéo composite
    2 voies pour l'audio (gauche/droite)
    1 voie pour le signal de commutation (slow switch -> 12v)
    1 voie pour le blanking (fast switch)

NOTE : Ajouter les connecteurs YUV et composite + audio sur chaque entrée et sur la sortie ?
NOTE 2 : Cable rouge/blanc pour la sortie audio est super bien...

Bouton ON/OFF à mettre

Alim par USB-C ou par prise jack ?

Une led indiquant la scart sélectionnée

Un bouton par scart pour la sélectionner ?

2 scarts output (permet de brancher sur un télé en // d'un OSSC par exemple)

Auto switching ??


2) Composants recommandés :

    Pour la vidéo : (R, G, B, Composite IN)
        4 x MAX4358 (multiplexeur vidéo 8:1 haute performance)
        Ou 8 x AD8184 (alternative de qualité), mais 4:1 (avec usage d'une porte NOT - 74HC1G04 ou 74HC04 par exemple)
               ATTENTION : Ajouter un AD8009 derrière !! (adaptation d'impédance toussa toussa... Cf. page 8 de la datasheet)
    Pour l'audio :
        2 x CD4051B (pour les signaux audio G/D)
    Pour les signaux de contrôle : PAS DU TOUT CONVAINCU
        1 x 74HC151 (pour le signal de commutation)
        1 x 74HC151 (pour le blanking)

Amplificateur vidéo : THS7374 (Cf. projet ossw)

3) Points importants sur l'implémentation :

Chaque signal vidéo nécessite une adaptation d'impédance 75Ω
Les masses doivent être en étoile pour éviter les boucles de masse
Prévoir des découplages sur les alimentations
Routage PCB : séparer les signaux vidéo, audio et contrôle


## Composants sympa

- [LM1881](https://www.ti.com/lit/ds/symlink/lm1881.pdf?ts=1731942361153&ref_url=https%253A%252F%252Fwww.google.com%252F)
    Permet de récupérer le signal de synchro d'un flux vidéo quelque soit le format vidéo
- [74HC238](https://www.mouser.fr/datasheet/2/408/74HC238D_datasheet_en_20160804-981082.pdf)
    Démultiplexer 3bits -> 8 lines
- [SN74HCS138](https://www.ti.com/lit/ds/symlink/sn74hcs138.pdf?HQS=dis-mous-null-mousermode-dsf-pf-null-wwe&ts=1731962390690&ref_url=https%253A%252F%252Fwww.mouser.fr%252F)
    Démultiplexer 3bits -> 8 lines avec trigger de schmitt 2v à 6v
- [CD4051](https://www.ti.com/lit/ds/symlink/cd4051b.pdf?ts=1731962650237&ref_url=https%253A%252F%252Fwww.google.com%252F)
    CMOS Single 8-Channel Analog Multiplexer or Demultiplexer With Logic-Level Conversion


Prises péritel :
- chez [Conrad](https://www.conrad.fr/fr/p/peritel-scart-embase-femelle-verticale-tru-components-1578891-noir-1-pc-s-1578891.html?utm_source=google&utm_medium=surfaces&utm_campaign=shopping-feed&utm_content=free-google-shopping-clicks&utm_term=1578891&utm_source=google&utm_medium=cpc&utm_campaign=SH+-+FR+-+Performance+max+-+High&utm_id=17690685297&gad_source=1&gbraid=0AAAAADmQbYcd405LsN948qm0M79RfCtU4&gclid=Cj0KCQiA6Ou5BhCrARIsAPoTxrAfOL7CZ34AvQYkkeM5-62B2O11hZUXFyEjKZ9d-doIfBiJoMxznwYaAhi_EALw_wcB).
- chez [console5](https://console5.com/store/female-scart-jp21-through-hole-pcb-mount-21-pin-connector-straight-angle-180-no-mounting-tabs.html).
