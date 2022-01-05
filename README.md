# Amour_Chadi--Amour_Redouane--Lebelguet_Hugo--Benchehida_Yacine--Beyah_Sami--Bouisson_Arnaud
Capteur de gaz connecté - UF SMART DEVICE

Introduction : Ce projet s'inscrit dans le cadre de notre formation d'ingénieur à l'INSA Toulouse sur les objets connectés. Plus précisément, l'objectif était de pouvoir comprendre toute l'architecture IoT associée à un système connecté, de sa fabrication jusqu'à son implémentation sur le réseau sans fil. A ce titre nous avons conçu un capteur de gaz connecté capable de détecter plusieurs substances telles que de l'ammoniac, de l'éthanol ou même de l'air synthétique. Pour ce faire, nous avons d'abord fabriqué le capteur à base de nanoparticules en salle blanche dans un laboratoire de nano-micro-fabrication (AIME) à l'INSA Toulouse. Afin de récupérer la mesure du capteur, nous avons aussi conçu le circuit électrique sur LT-Spice permettant d'acquérir le signal analogique. Ce circuit a ensuite été embarqué et intégré sur une carte électronique conçue sur le logiciel KiCad. Nous avons connecté la sortie de cette carte à un microcontrôleur Arduino et branché sur les ports UART (TX/RX) un module LoRa permettant de communiquer les valeurs du capteur sur le réseau TTN (The Things Network). Nous avons programmé le tout sur l'IDE Arduino et NodeRed afin d'afficher cette donnée sur un dashboard web et élaboré la fiche technique (datasheet) expliquant l'utilisation typique de ce capteur : 

![image](https://user-images.githubusercontent.com/74780897/148228389-c45cbe69-aad9-4a1f-9217-174bfb960774.png)

******** Micro-Nano-fabrication en salle blanche ********


![image](https://user-images.githubusercontent.com/74780897/148229191-f5715afd-bd67-4975-93c8-f305f55eaef4.png) ![image](https://user-images.githubusercontent.com/74780897/148229293-9518c67d-b960-4d03-aa35-a8cddb975baa.png)

![image](https://user-images.githubusercontent.com/74780897/148229457-456d84f2-1b6b-40bd-b0bf-65f2c80dd207.png)



