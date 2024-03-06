# GEO7630
TP2 GEO7630
<!-----

You have some errors, warnings, or alerts. If you are using reckless mode, turn it off to see inline alerts.
* ERRORs: 0
* WARNINGs: 0
* ALERTS: 17

Conversion time: 3.693 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β35
* Wed Mar 06 2024 11:44:34 GMT-0800 (PST)
* Source doc: Document sans titre
* This document has images: check for >>>>>  gd2md-html alert:  inline image link in generated source and store images to your server. NOTE: Images in exported zip file from Google Docs may not appear in  the same order as they do in your doc. Please check the images!

----->


<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 0; ALERTS: 17.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>
<a href="#gdcalert6">alert6</a>
<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>
<a href="#gdcalert10">alert10</a>
<a href="#gdcalert11">alert11</a>
<a href="#gdcalert12">alert12</a>
<a href="#gdcalert13">alert13</a>
<a href="#gdcalert14">alert14</a>
<a href="#gdcalert15">alert15</a>
<a href="#gdcalert16">alert16</a>
<a href="#gdcalert17">alert17</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>


UNIVERSITÉ DU QUÉBEC À MONTRÉAL

Travail pratique #2

Visualisation et intégration de données géospatiales (GEO7630)

Responsable : Clément Glogowski

Par Émile Heppell-Dion (HEPE23079708) et Marc-Antoine Lévesque (LEVM23069205)

5 mars 2024

--------------------------------------------------------------

**Mise en contexte**

Les données de comptage des véhicules, cyclistes et piétons aux intersections équipées de feux de circulation à Montréal permettent d’établir une vue détaillée du flux de circulation. Collectées aux feux de circulation à des intervalles de 15 minutes pendant les périodes de pointe, ces données incluent des informations sur le nombre, la provenance et la direction des véhicules, des cyclistes et des piétons. Grâce à ces données, il est possible d'identifier les mouvements directionnels spécifiques des différents types de véhicules à travers les intersections, constituant une ressource essentielle pour la compréhension du trafic à Montréal. Ici, nous avons sommés tous les mouvements des véhicules dans chaque direction spécifique à chaque tronçon pour chiffrer le nombre de véhicules se déplaçant sur un tronçon de rues à chaque heure.

Le jeu de données du réseau routier (geobase) consiste en un ensemble de segments de routes appelés tronçons. Chaque tronçon est caractérisé par un toponyme officiel, incluant notamment le nom de la rue, des plages d'adresses et une référence aux limites administratives telles que les arrondissements ou les quartiers. Ces données ont été retravaillé dans un flux de transformers dans FME pour permettre d’ajouter la composante d’orientation aux tronçons de rues selon s’ils sont Est-Ouest ou Nord-Sud afin de leur attribuer les bonnes données de circulation.

Les tronçons qui sont connexes à un feu de circulation ont été isolés par sélection spatiale avec les feux et se sont vu attribués le nombre de véhicules se dirigeant sur ce tronçon et provenant de ce tronçon dans leur table attributaire. Il est ainsi possible de chiffrer le nombre de véhicules traversant un tronçon à chaque heure de la journée en affichant uniquement la sélection pour chaque laps de temps.

Ces étapes ont suffi à la création d’une carte avec une symbologie qui permet d’illustrer le flux général du trafic à chaque heure de la journée et pour chaque type de véhicule. Pour la suite, il faudra s’assurer de faire une interpolation permettant d’estimer le nombre de véhicules sur les tronçons qui ne sont pas adjacents à un feu de circulation.

Le travail sur le chemin de transformations de ces données pour les rendre utiles à l'analyse du flux de trafic est confronté à plusieurs défis majeurs. D’abord, la nécessité d'isoler les tronçons de rues orientés Est-Ouest par rapport à ceux orientés Nord-Sud, en utilisant une dérivée des coordonnées y (dy/dx). Cette tâche demande une bonne compréhension des données pour assurer une classification correcte des tronçons selon leur orientation. De plus, attribuer les données de comptages directionnels cumulés aux bons tronçons de rues en fonction de leur position relative aux feux de circulation représente un défi supplémentaire qui a nécessité une analyse minutieuse des emplacements des feux et des tronçons de rues adjacents. Enfin, l'idée de créer des polygones pour représenter les quadrilatères a été abandonnée en raison de la complexité à construire des polygones qui pourraient recevoir des données de comptages cohérentes, soulignant ainsi la nécessité de trouver des approches alternatives pour modéliser efficacement le flux de trafic dans la ville.

La visualisation de ce flux de trafic sera plutôt via l’interpolation sur les tronçons qui ne se trouvent pas près d’une intersection et une symbologie potentiellement tridimensionnelle qui pourra démontrer l’ampleur du nombre de véhicules pour chaque mode de transport par tranche d’heure. De plus, une composante d’émission de gaz à effet de serre sera ajoutée aux tronçons et sera observable grâce à un clic menant à un tableau de bord qui illustrera et chiffrera ces émissions. Ces derniers éléments seront 

produits au moment de la création de l’application web puisqu’ils nécessitent premièrement l’interpolation du trafic sur les tronçons omis pour le moment, et de simples calculs mathématiques sur les valeurs d’attributs par la suite.

**Explications des Bookmark : **



<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")


**BookMark 1 :** Le but ici est de créer huit attributs pour chaque entité des feux de circulation. Il y a deux groupes d’attributs, une moitié qui somme le trafic de chaque direction respectivement (_vers_nose_), l’autre moitié somme le trafic provenant de chaque direction respectivement (_de_nose_). Les entités sont ensuite sommées par heure et par type de transport (summary du _statistic calculator)_, leur géométrie leur est ensuite attribuée grâce à un _feature merger_.



<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")


**Bookmark 2: **Fait essentiellement la même chose que celui présenté précédemment, mais spécifiquement pour les comptages de piétons puisque ceux-ci n’ont pas les mêmes attributs de comptages que les autres modes de transport.



<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")


**Bookmark 3 :** On utilise les propriétés des listes pour réduire le nombre d’entités de feux de circulation afin d’alléger la jointure spatiale en aval.



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")




<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.png "image_tooltip")


**Bookmarks 4-5 :** Sélection spatiale de tous les tronçons ayant au moins un feu de circulation sur l’axe dont ils font partie. Le premier bookmark sélectionne les tronçons aux intersections ayant un feu de circulation, de ces tronçons, on crée une liste ayant comme critères de sélection (Odonyme, Nom, Arrondissements gauches et droits). De cette liste, on sélectionne tous les tronçons qui possèdent ces mêmes critères de sélection, mais qui ne sont pas à ces intersections.

<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.png "image_tooltip")


**Bookmark 6 :** Permet d’attribuer l’orientation (NS vs EW) à chaques tronçons retenus précédemment. Étant donné l’orientation générale de l’île de Montréal et donc de ses rues, on remarque que les axes nord-sud ont une dérivée négative par rapport aux coordonnées X (dy/dx&lt;0). L’inverse est vrai pour les tronçons Est-Ouest. Fait à noter, on conserve les attributs Xmax et Y-Xmax



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image7.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image7.png "image_tooltip")


**Bookmark 7 :** Le but de ce bookmark est d’attribuer les décompte de trafic des feux de circulation en fonction des directions calculées préalablement aux tronçons adjacents aux feux de circulation selon leur position relative à ceux-ci. On sépare les extrants en fonction du mode de transport et on exporte chacun de ces ensembles de données séparément. Ci-dessous, on explicite la démarche pour déterminer la position relative des tronçons pour les cas NS et EW.



<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image8.jpg "image_tooltip")




<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image9.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image9.png "image_tooltip")




<p id="gdcalert10" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image10.jpg). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert11">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image10.jpg "image_tooltip")




<p id="gdcalert11" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image11.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert12">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image11.png "image_tooltip")




<p id="gdcalert12" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image12.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert13">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image12.png "image_tooltip")


**Bookmark 8 :** On _write_ les couches qui seront utiles pour l’habillage de la carte (arrondissements, île de Montréal, Hydrographie).

Les cartes montrées ci-bas représentent les différents modes d’affichage que nous envisageons pour l’application web. De plus, ces cartes pourront être animées par heure. Finalement, elles seront interactives et afficheront des informations supplémentaires en lien avec le trafic du tronçon (visualisation d’émission de GES - histogramme du trafic, etc.). Nous envisageons aussi d'interpoler à la volée les comptages sur les tronçons qui joignent ensemble les tronçons adjacents aux feux de circulation à l’aide du logiciel d’affiche de carte libre qui sera utilisé.



<p id="gdcalert13" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image13.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert14">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image13.png "image_tooltip")


<p id="gdcalert14" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image14.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert15">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image14.png "image_tooltip")


<p id="gdcalert15" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image15.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert16">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image15.png "image_tooltip")


<p id="gdcalert16" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image16.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert17">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image16.png "image_tooltip")


<p id="gdcalert17" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image17.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert18">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image17.png "image_tooltip")

