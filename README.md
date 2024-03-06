# GEO7630
TP2 GEO7630
<!-----

UNIVERSITÉ DU QUÉBEC À MONTRÉAL

Travail pratique #2

Visualisation et intégration de données géospatiales (GEO7630)

Responsable : Clément Glogowski

Par Émile Heppell-Dion (HEPE23079708) et Marc-Antoine Lévesque (LEVM23069205)

5 mars 2024

\--------------------------------------------------------------

**Mise en contexte**

Les données de comptage des véhicules, cyclistes et piétons aux intersections équipées de feux de circulation à Montréal permettent d’établir une vue détaillée du flux de circulation. Collectées aux feux de circulation à des intervalles de 15 minutes pendant les périodes de pointe, ces données incluent des informations sur le nombre, la provenance et la direction des véhicules, des cyclistes et des piétons. Grâce à ces données, il est possible d'identifier les mouvements directionnels spécifiques des différents types de véhicules à travers les intersections, constituant une ressource essentielle pour la compréhension du trafic à Montréal. Ici, nous avons sommés tous les mouvements des véhicules dans chaque direction spécifique à chaque tronçon pour chiffrer le nombre de véhicules se déplaçant sur un tronçon de rues à chaque heure.

Le jeu de données du réseau routier (geobase) consiste en un ensemble de segments de routes appelés tronçons. Chaque tronçon est caractérisé par un toponyme officiel, incluant notamment le nom de la rue, des plages d'adresses et une référence aux limites administratives telles que les arrondissements ou les quartiers. Ces données ont été retravaillé dans un flux de transformers dans FME pour permettre d’ajouter la composante d’orientation aux tronçons de rues selon s’ils sont Est-Ouest ou Nord-Sud afin de leur attribuer les bonnes données de circulation.

Les tronçons qui sont connexes à un feu de circulation ont été isolés par sélection spatiale avec les feux et se sont vu attribués le nombre de véhicules se dirigeant sur ce tronçon et provenant de ce tronçon dans leur table attributaire. Il est ainsi possible de chiffrer le nombre de véhicules traversant un tronçon à chaque heure de la journée en affichant uniquement la sélection pour chaque laps de temps.

Ces étapes ont suffi à la création d’une carte avec une symbologie qui permet d’illustrer le flux général du trafic à chaque heure de la journée et pour chaque type de véhicule. Pour la suite, il faudra s’assurer de faire une interpolation permettant d’estimer le nombre de véhicules sur les tronçons qui ne sont pas adjacents à un feu de circulation.

Le travail sur le chemin de transformations de ces données pour les rendre utiles à l'analyse du flux de trafic est confronté à plusieurs défis majeurs. D’abord, la nécessité d'isoler les tronçons de rues orientés Est-Ouest par rapport à ceux orientés Nord-Sud, en utilisant une dérivée des coordonnées y (dy/dx). Cette tâche demande une bonne compréhension des données pour assurer une classification correcte des tronçons selon leur orientation. De plus, attribuer les données de comptages directionnels cumulés aux bons tronçons de rues en fonction de leur position relative aux feux de circulation représente un défi supplémentaire qui a nécessité une analyse minutieuse des emplacements des feux et des tronçons de rues adjacents. Enfin, l'idée de créer des polygones pour représenter les quadrilatères a été abandonnée en raison de la complexité à construire des polygones qui pourraient recevoir des données de comptages cohérentes, soulignant ainsi la nécessité de trouver des approches alternatives pour modéliser efficacement le flux de trafic dans la ville.

La visualisation de ce flux de trafic sera plutôt via l’interpolation sur les tronçons qui ne se trouvent pas près d’une intersection et une symbologie potentiellement tridimensionnelle qui pourra démontrer l’ampleur du nombre de véhicules pour chaque mode de transport par tranche d’heure. De plus, une composante d’émission de gaz à effet de serre sera ajoutée aux tronçons et sera observable grâce à un clic menant à un tableau de bord qui illustrera et chiffrera ces émissions. Ces derniers éléments seront 

produits au moment de la création de l’application web puisqu’ils nécessitent premièrement l’interpolation du trafic sur les tronçons omis pour le moment, et de simples calculs mathématiques sur les valeurs d’attributs par la suite.

**Explications des Bookmark :** 

![](https://lh7-us.googleusercontent.com/z74OmFphBhZlNqodKCNIi7wvBpUEexgARVJFlelRaNFZ79M7BAdx6OWFPhPyYxjpC-bUexw9lWKGPKi7BdJE6D3bI3GjUMn3ILhsC4DFTI0FpAH6ejSwv9BL4h_YA5u3n3Qfv0vBxmveN0pewQTwVMU)

**BookMark 1 :** Le but ici est de créer huit attributs pour chaque entité des feux de circulation. Il y a deux groupes d’attributs, une moitié qui somme le trafic de chaque direction respectivement (_vers\_nose_), l’autre moitié somme le trafic provenant de chaque direction respectivement (_de\_nose_). Les entités sont ensuite sommées par heure et par type de transport (summary du _statistic calculator)_, leur géométrie leur est ensuite attribuée grâce à un _feature merger_.

![](https://lh7-us.googleusercontent.com/rd7m45FAOOkj9esenDYIR0Mp_l7UphYyoHi0gVWhR45j-w89Nh3h1bajiRbKQEQ7vJDkjaXIt3fSf7prE06rEdM-ZkL7qwO_joOCjySP0ye3Q8AYrgQWhTbJL5YS1aQ8ra1Pl2gQwwUrdyd6b1CxsDM)

**Bookmark 2:** Fait essentiellement la même chose que celui présenté précédemment, mais spécifiquement pour les comptages de piétons puisque ceux-ci n’ont pas les mêmes attributs de comptages que les autres modes de transport.

![](https://lh7-us.googleusercontent.com/GyInQMGBYziAYp_ZDp2C5kE_iJbcCkLr43AynKAsDzYC3ORCbWwkgu5JbTsje-lcBoYZVREPSd08no_ZwlPhEsPcCzOwUKsxGOTycjVnQUAqxc5f-3jo99l_MOjR9_ibamxuc8PRkPGfRRnGX0gwlfo)

**Bookmark 3 :** On utilise les propriétés des listes pour réduire le nombre d’entités de feux de circulation afin d’alléger la jointure spatiale en aval.

![](https://lh7-us.googleusercontent.com/0LGyUhCEwk4v-sEsS9XuHT85HO9kWVs2JmXT2--KsIXCNaUoArmhjm05kUxOXXq7_ouvCQRI2kXmZLL0dJCn-s8M2cR7Z6y9tVKQPy-Dlu57BJY70K7idPgxaohkTvBONtmHIU2JF1_XidWcADggLSg)

![](https://lh7-us.googleusercontent.com/RpMJAtjcjAHufh-tzjzJIdlInyer25lFi2ZKIc4iywZNoBzZxdHzuI7ER2P7u43A-tyqloNMTYgxQFE56ZqVnWPeBJD2xY7zq1IoMDUaOKuuAlaCjYbsqT04ciTEuaNP_RWxCijHUEdSn9-bRlUlc_8)

**Bookmarks 4-5 :** Sélection spatiale de tous les tronçons ayant au moins un feu de circulation sur l’axe dont ils font partie. Le premier bookmark sélectionne les tronçons aux intersections ayant un feu de circulation, de ces tronçons, on crée une liste ayant comme critères de sélection (Odonyme, Nom, Arrondissements gauches et droits). De cette liste, on sélectionne tous les tronçons qui possèdent ces mêmes critères de sélection, mais qui ne sont pas à ces intersections.![](https://lh7-us.googleusercontent.com/K8_duLaGGgj5uFLlwooPCUTSuIqhwhRLHwWRDynneYQ55FPUH_Gbk1MJVfJ0ex_iuyqa6okpIcrYi73fX8qv1QLeayACWS4ZPGKuqYw6WlHYd0XZjrCw43yGSD6r024J3OWh57bYF1hDIvpdlpYzPfk)

**Bookmark 6 :** Permet d’attribuer l’orientation (NS vs EW) à chaques tronçons retenus précédemment. Étant donné l’orientation générale de l’île de Montréal et donc de ses rues, on remarque que les axes nord-sud ont une dérivée négative par rapport aux coordonnées X (dy/dx<0). L’inverse est vrai pour les tronçons Est-Ouest. Fait à noter, on conserve les attributs Xmax et Y-Xmax

![](https://lh7-us.googleusercontent.com/0kZcVg6okjAzBNmjp6l8rMmj1vQz81nLB6LT-MijPKSaTBPeE9_wtUtXaVl10-nc4mFLpaRwVzvLHJ9BOnhPrTp13ih-kYDQxyNxOtBgdeoh-0A1J-yVOg9_PeV7062jnOnLbf1mKAnr2KwwrcFUWt0)

**Bookmark 7 :** Le but de ce bookmark est d’attribuer les décompte de trafic des feux de circulation en fonction des directions calculées préalablement aux tronçons adjacents aux feux de circulation selon leur position relative à ceux-ci. On sépare les extrants en fonction du mode de transport et on exporte chacun de ces ensembles de données séparément. Ci-dessous, on explicite la démarche pour déterminer la position relative des tronçons pour les cas NS et EW.

![](https://lh7-us.googleusercontent.com/UGmRsa7jfFhfddJd07R0RsumdGhZSyXQB2VzOIW-290O30nCDZYAlbJvo_hfNW0KWAOFkUyQX4Nb_8oc1Ry1s4GXj15HQwAQakIYoCFX8aQTkJzSgyP49_MIm57CUymfdFUJ-dOfL2QLb93eX93LRck)

![](https://lh7-us.googleusercontent.com/_M4susGjyyNLl7VuF6aD3z2u-Hnr8x5Z6m3cmKoBs4qh1oL6VzDuqexpRJG4nxZKkZUyKN8RdvX6muZUkm10FfBJwZZCPR7jBPc3z3yR0fyVa6KN-xYpi0tqSg5gS-CwrBEERHcmakjvjBL9kM2h3fY)

![](https://lh7-us.googleusercontent.com/9DOFO7LMJBv1jvVep05MXhlerGgECxFV3tstkVpwfVTS6YyZl3lwB6QbyFFiFdnvfie5gbE0Gzdjvg_cg55wVLd7XnTShwA3vFrSLAsFWOCdceD4QWguUB_4w55FPLRcPSbZcdFOBpCaRrC65Om5DRw)

![](https://lh7-us.googleusercontent.com/m_kEXbVLZnl6tlPjm-TF8mn8CxFa-As-nRfaljxglysYYwJbWwuEpAF0ckv2TRkVI-wP8J5GybLhPHqUHFyLmJJI-YwDcEBD5wr2Hj6dUVjUbPixsiVzn-lo1TrGLA6s4M2BHqiCKia2067Vmz4ZXCk)

![](https://lh7-us.googleusercontent.com/qF7Jx_qzcSdpCjUkYGa299gukIe0a5MBFiffMag1cPumP7OcrtFX7bwsZkoLoc4RLFxoq63Sbk5hCRMIw7ugDK6eN_XA4vGpgQ_heDbYogVoVnTnz-RzcUTXoPKcHD7fAsaz7laUbA0pqKGsmi23ffE)

**Bookmark 8 :** On _write_ les couches qui seront utiles pour l’habillage de la carte (arrondissements, île de Montréal, Hydrographie).

Les cartes montrées ci-bas représentent les différents modes d’affichage que nous envisageons pour l’application web. De plus, ces cartes pourront être animées par heure. Finalement, elles seront interactives et afficheront des informations supplémentaires en lien avec le trafic du tronçon (visualisation d’émission de GES - histogramme du trafic, etc.). Nous envisageons aussi d'interpoler à la volée les comptages sur les tronçons qui joignent ensemble les tronçons adjacents aux feux de circulation à l’aide du logiciel d’affiche de carte libre qui sera utilisé.

![](https://lh7-us.googleusercontent.com/9BmdnJu4VlJSyxF8xUmfBfhxGcstFAgySX_DQ8qmScH7UtGYyWJ6fxMYt4CO1i1EdPbngU-c-DXBEs9pWAfbYRKJSRCjSwMYt2Xp39sczuInXG8XcC9GShbj7uDFrpgatDrU2fNmbAA7QCLucgAM4aU)


