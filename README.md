# Capteur de gaz connecté - UF SMART DEVICE - INSA Toulouse 

Introduction : Ce projet s'inscrit dans le cadre de notre formation d'ingénieur à l'INSA Toulouse en 5ème année sur les objets connectés. Plus précisément, l'objectif était de pouvoir comprendre toute l'architecture IoT associée à un système connecté, de sa fabrication à son implémentation sur un réseau sans fil basse consommation. A ce titre nous avons conçu un capteur de gaz connecté capable de détecter plusieurs substances telles que de l'ammoniac, de l'éthanol ou même de l'air synthétique. Pour ce faire, nous avons d'abord fabriqué le capteur à base de nanoparticules en salle blanche dans un laboratoire de nano-micro-fabrication (AIME) à l'INSA Toulouse. Afin de récupérer la mesure du capteur, nous avons aussi conçu le circuit électrique sur LT-Spice permettant d'acquérir le signal analogique. Ce circuit a ensuite été embarqué et intégré sur une carte électronique conçue sur le logiciel KiCad. Nous avons connecté la sortie de cette carte à un microcontrôleur Arduino et branché sur les ports UART (TX/RX) un module LoRa permettant de communiquer les valeurs du capteur sur le réseau TTN (The Things Network). Nous avons programmé le tout sur l'IDE Arduino et NodeRed afin d'afficher cette donnée sur un dashboard web et élaboré la fiche technique (datasheet) expliquant l'utilisation typique de ce capteur : 

**Apperçu du capteur de gaz à base de nanoparticules**
![image](https://user-images.githubusercontent.com/74780897/148231435-45145006-497f-4275-be46-3ff1465b531f.png)


**Chronologie du projet**

![image](https://user-images.githubusercontent.com/74780897/148228389-c45cbe69-aad9-4a1f-9217-174bfb960774.png)



**Organisation de l'équipe**

![image](https://user-images.githubusercontent.com/74780897/148241799-a8798eab-e498-44a4-9889-47ead873832f.png)


# *** 1. Micro-Nano-fabrication en salle blanche ***

Aujourd’hui les capteurs de gaz présentent un réel potentiel pour répondre aux problématiques environnementales. Pour rappel, l’objectif était de développer un capteur de gaz chimique à base de nanoparticules de trioxyde de tungstène (WO3), de l’intégrer dans un circuit électronique afin de mesurer la concentration de gaz et de la communiquer ensuite sur un Dashboard web en utilisant le protocole de communication LoRa.  Ce projet nous permet d’étudier et de déployer toute l’architecture IoT associée à un système connecté. Il nous a aussi permis de comprendre les enjeux liés aux objets connectés : le faible encombrement, la faible consommation énergétique et le faible coût. 

---> Ce capteur de gaz répond à la problématique de faible encombrement puisqu’il intègre quatre éléments de mesure sur seulement quelques millimètres (voir figure- ci-dessous) : 
-	Deux capteurs en aluminium symétriques, sous forme de peignes interdigités séparés de 5 µm. Ces peignes permettent de piéger et d’intégrer des nanoparticules WO3, constituant des chemins de conduction électriques parallèles au sein des peignes et sensibles à certains gaz. Lorsqu’une réaction d’oxydoréduction a lieu entre les nanoparticules et un gaz d’intérêt, la résistance électrique au sein des peignes est modifiée. Cette variation de résistance électrique est liée à la concentration de gaz. 
-	Une résistance chauffante de poly silicium enfouie et isolée électriquement par une couche de SiO₂. Elle permet de chauffer la puce et d’y réguler la température autour de 250°C, température optimale pour une meilleure sensibilité des capteurs d’aluminium.
-	Un résistance d’aluminium en serpentin pour mesurer la température à la surface.
-	Des électrodes pour la connexion aux appareils de mesure extérieurs. Pour mesurer cette résistance électrique, nous avons réalisé les contacts électriques par métallisation à l'aluminium. Plus précisément nous avons utilisé la technique de photogravure consistant à déposer une couche de résine photosensible sur l'aluminium, à insoler cette résine au niveau des zones d'aluminium que l'on souhaite retirer et à les attaquer chimiquement dans un bain acide.

![image](https://user-images.githubusercontent.com/74780897/148229191-f5715afd-bd67-4975-93c8-f305f55eaef4.png) 



Une fois les contacts faits, nous avons réalisé la synthèse chimique des nanoparticules WO3 pour ensuite les intégrer par diélectrophorèse au sein des peignes interdigités. Cette technique consiste à déposer une fine goutte de nanoparticules sur le capteur et à appliquer pendant 60s un champ électrique alternatif oscillant à la fréquence de 100 KHz avec une amplitude de 10V, entre les électrodes des peignes interdigités afin d’y attirer et d’y piéger les nanoparticules. 

---> Ce capteur répond aussi à la problématique de faible coût et de respect de l’environnement puisque la synthèse chimique des batônnets de nanoparticules n’implique que quelques millilitres de solution réutilisables chaque année afin d’éviter tout gaspillage. La quantité a même été diminuée de moitié cette année par rapport aux années précédentes. Les produits de la synthèse sont également triés afin de ne pas polluer les eaux usées. Voici une image au microscope optique de notre capteur après intégration des nanoparticules :

![image](https://user-images.githubusercontent.com/74780897/148247050-023a153e-0810-49ff-a663-37364674bb5f.png) ![image](https://user-images.githubusercontent.com/74780897/148247278-50ccd44b-96d9-4411-911e-44d410e7235c.png)


---> Enfin, ce capteur répond à la problématique de faible consommation puisque la résistance électrique de chaque peigne interdigité est théoriquement de l’ordre de la centaine de MΩ, ce qui correspond à une consommation en courant électrique de quelques micro-ampères voire nanoampères. 


# *** 2. CAO Electronique et réalisation du circuit ***

Une fois le capteur fabriqué, l'objectif était d'établir le circuit électronique suivant permettant de traduire la variation de résistance électrique du capteur (Isens), en tension analogique (ADC). Ce circuit inclut la puce fabriquée en AIME avec le boîtier TO5, un filtre RC passif passe-bas à l’entrée pour couper le bruit à hautes fréquences (50Hz) ainsi que le couplage capacitif avec le réseau à 230V, un amplificateur opérationnel Trans-impédance LTC1050 à deux étages, une résistance de Shunt, un filtre passe-bas actif en sortie de l’amplificateur et enfin un filtre passif anti-repliement en sortie du circuit côté ADC pour retirer le bruit introduit en cours de traitement.  

![image](https://user-images.githubusercontent.com/74780897/148254694-57e4d97a-c8c7-4885-8672-b3a68aa8baac.png)



Nous avons dans un second temps conçu la carte électronique permettant d'intégrer l'ensemble du circuit. Nous avons pour cela utilisé le logiciel KiCad en deux étapes : 

1) Réalisation schématique du circuit visant simplement à positionner les symboles de chaque composant, à les connecter et à leur associer leur empreinte (footprint). Ce schéma électrique est constitué de trois parties : le circuit pour le capteur de gaz, l'arduino permettant de récupérer la valeur analogique côté ADC en sortie du circuit et le module RF de communication LoRa connecté aux pins digitaux de l'arduino : 

![image](https://user-images.githubusercontent.com/74780897/148240620-57bdce98-2a73-4cca-b73d-4eb1045c4272.png)

2) Réalisation du PCB visant à positionner les empreintes de chaque composant sur la carte non plus de manière symbolique mais de manière réelle. Y sont ainsi déssinés le routage des pistes de cuivre interconnectant les empreintes ainsi que les deux couches de cuivre (TOP et BOTTOM) et le plan de masse. Nous y avons appliqué les règles de conception de classe 2 en prenant en compte les moyens de fabrication de notre établissement (largeur des pistes et isolation minimum à 0.6 mm). Voici une image 2D et 3D de notre carte PCB simple face intégrant les composants électroniques traversants du côté TOP et les pistes du côté  BOTTOM avec quelques vias : 

PCB et Routage
![image](https://user-images.githubusercontent.com/74780897/148241474-2ae13e45-672a-42c7-8ce5-e8f0fbf2911f.png)

TOP et BOTTOM VIEW
![image](https://user-images.githubusercontent.com/74780897/148248571-5c3752bf-bf55-4adc-965c-9175450625c6.png)


Voici la liste compléte des composants principaux avec leur symbole et leur empreinte, que nous avons utilisés pour ce circuit. (cf. fichier csv pour plus d'informations "bills of materials") :

- Capteur de gaz à nanoparticules

![image](https://user-images.githubusercontent.com/74780897/148249846-beb5565d-c839-41f4-b874-8f9406897837.png)


- un commutateur à glissière trois pattes afin de sélectionner au choix l'un des deux capteurs de gaz : 
![image](https://user-images.githubusercontent.com/74780897/148246720-a0ab246a-a4dc-416b-b20c-f2f431c89d14.png) ![image](https://user-images.githubusercontent.com/74780897/148246759-e756ce92-98fc-422f-8817-e6daa4441621.png)

- Un bornier à vis 2 pattes pour l'alimentation externe de 0 à 15V pour la résistance chauffante : 
![image](https://user-images.githubusercontent.com/74780897/148249086-0fc0fce7-8f0a-4d01-a988-1b0626394b62.png)

- un amplificateur transimpédance : 
![image](https://user-images.githubusercontent.com/74780897/148249265-d36b3cd6-2994-4987-9736-ac52a10a52e8.png)

- Le module LoRa et son breakout board. Nous avons nous-mêmes édité le footprint en prenant soin d'y placer les pads à un pas de 2.54 mm et les trous de perçage permettant de fixer le module : 

![image](https://user-images.githubusercontent.com/74780897/148250001-f208fb54-d1c8-46aa-91dd-d67bbd0dfa7a.png)


# *** Datasheet ***

Dans l’industrie électronique, il est standard d’accompagner chaque composant d’une fiche technique fournissant les caractéristiques de fonctionnement standard, les résultats d’essais, les recommandations d’usage et d’autres renseignements. Vous trouverez dans le dépôt, la datasheet que l'on a réalisé.

        



