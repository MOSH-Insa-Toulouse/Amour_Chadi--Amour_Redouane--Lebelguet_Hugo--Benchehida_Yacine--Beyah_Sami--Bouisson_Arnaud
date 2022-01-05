# Amour_Chadi--Amour_Redouane--Lebelguet_Hugo--Benchehida_Yacine--Beyah_Sami--Bouisson_Arnaud
Capteur de gaz connecté - UF SMART DEVICE

Introduction : Ce projet s'inscrit dans le cadre de notre formation d'ingénieur à l'INSA Toulouse sur les objets connectés. Plus précisément, l'objectif était de pouvoir comprendre toute l'architecture IoT associée à un système connecté, de sa fabrication à son implémentation sur un réseau sans fil basse consommation. A ce titre nous avons conçu un capteur de gaz connecté capable de détecter plusieurs substances telles que de l'ammoniac, de l'éthanol ou même de l'air synthétique. Pour ce faire, nous avons d'abord fabriqué le capteur à base de nanoparticules en salle blanche dans un laboratoire de nano-micro-fabrication (AIME) à l'INSA Toulouse. Afin de récupérer la mesure du capteur, nous avons aussi conçu le circuit électrique sur LT-Spice permettant d'acquérir le signal analogique. Ce circuit a ensuite été embarqué et intégré sur une carte électronique conçue sur le logiciel KiCad. Nous avons connecté la sortie de cette carte à un microcontrôleur Arduino et branché sur les ports UART (TX/RX) un module LoRa permettant de communiquer les valeurs du capteur sur le réseau TTN (The Things Network). Nous avons programmé le tout sur l'IDE Arduino et NodeRed afin d'afficher cette donnée sur un dashboard web et élaboré la fiche technique (datasheet) expliquant l'utilisation typique de ce capteur : 

******* Apperçu du capteur de gaz à base de nanoparticules *********
![image](https://user-images.githubusercontent.com/74780897/148231435-45145006-497f-4275-be46-3ff1465b531f.png)











******* Chronologie du projet ********

![image](https://user-images.githubusercontent.com/74780897/148228389-c45cbe69-aad9-4a1f-9217-174bfb960774.png)











******* Organisation de l'équipe *******
![image](https://user-images.githubusercontent.com/74780897/148234312-cdb1ea1d-7880-4edd-8436-8709f02fa41b.png)











******** Etape 1 : Micro-Nano-fabrication en salle blanche ********

Aujourd’hui les capteurs de gaz présentent un réel potentiel pour répondre aux problématiques environnementales. Pour rappel, l’objectif était de développer un capteur de gaz chimique à base de nanoparticules de trioxyde de tungstène (WO3), de l’intégrer dans un circuit électronique afin de mesurer la concentration de gaz et de la communiquer ensuite sur un Dashboard web en utilisant le protocole de communication LoRa.  Ce projet nous permet d’étudier et de déployer toute l’architecture IoT associée à un système connecté. Il nous a aussi permis de comprendre les enjeux liés aux objets connectés : le faible encombrement, la faible consommation énergétique et le faible coût. 

---> Ce capteur de gaz répond à la problématique de faible encombrement puisqu’il intègre quatre éléments de mesure sur seulement quelques millimètres (voir figure- ci-dessous) : 
-	Deux capteurs en aluminium symétriques, sous forme de peignes interdigités séparés de 5 µm. Ces peignes permettent de piéger et d’intégrer des nanoparticules WO3, constituant des chemins de conduction électriques parallèles au sein des peignes et sensibles à certains gaz. Lorsqu’une réaction d’oxydoréduction a lieu entre les nanoparticules et un gaz d’intérêt, la résistance électrique au sein des peignes est modifiée. Cette variation de résistance électrique est liée à la concentration de gaz. 
-	Une résistance chauffante de poly silicium enfouie et isolée électriquement par une couche de SiO₂. Elle permet de chauffer la puce et d’y réguler la température autour de 250°C, température optimale pour une meilleure sensibilité des capteurs d’aluminium.
-	Un résistance d’aluminium en serpentin pour mesurer la température à la surface.
-	Des électrodes pour la connexion aux appareils de mesure extérieurs. Pour mesurer cette résistance électrique, nous avons réalisé les contacts électriques par métallisation à l'aluminium. Plus précisément nous avons utilisé la technique de photogravure consistant à déposer une couche de résine photosensible sur l'aluminium, à insoler cette résine au niveau des zones d'aluminium que l'on souhaite retirer et à les attaquer chimiquement dans un bain acide.
![image](https://user-images.githubusercontent.com/74780897/148229191-f5715afd-bd67-4975-93c8-f305f55eaef4.png) 



Une fois les contacts faits, nous avons réalisé la synthèse chimique des nanoparticules WO3 pour ensuite les intégrer par diélectrophorèse au sein des peignes interdigités. Cette technique consiste à déposer une fine goutte de nanoparticules sur le capteur et à appliquer pendant 60s un champ électrique alternatif oscillant à la fréquence de 100 KHz avec une amplitude de 10V, entre les électrodes des peignes interdigités afin d’y attirer et d’y piéger les nanoparticules. Voici une image au microscope optique de notre capteur après intégration des nanoparticules :
![image](https://user-images.githubusercontent.com/74780897/148229293-9518c67d-b960-4d03-aa35-a8cddb975baa.png)



![image](https://user-images.githubusercontent.com/74780897/148229457-456d84f2-1b6b-40bd-b0bf-65f2c80dd207.png)


---> Il répond aussi à la problématique de faible coût et de respect de l’environnement puisque la synthèse chimique des batônnets de nanoparticules n’implique que quelques millilitres de solution réutilisables chaque année afin d’éviter tout gaspillage. La quantité a même été diminuée de moitié cette année par rapport aux années précédentes. Les produits de la synthèse sont également triés afin de ne pas polluer les eaux usées.

---> Enfin, ce capteur répond à la problématique de faible consommation puisque la résistance électrique de chaque peigne interdigité est théoriquement de l’ordre de la centaine de MΩ, ce qui correspond à une consommation en courant électrique de quelques micro-ampères voire nanoampères. 
        



