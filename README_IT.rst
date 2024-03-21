.. _italian_readme:

Questo repository è un insieme di guide, immagini e idee riguardanti la modifica dei sensori Xiaomi/Aqara.

Le modifiche sono solamente lato hardware, l'idea è di poter utilizzare i sensori modificati con il gateway Lumi e l'app MiHome.

E' possibile "hackerare"/modificare alcuni sensori Xiaomi per poterli utilizzare in modo alternativo.
Dal sensore originale è possibile creare altri tipi di sensori, utilizzabili con MiHome e/o con qualsiasi sistema di home automation (Domoticz, Home Assistant, OpenHAB...).
Con l'utilizzo di questi sistemi c'è molta più libertà nelle automazione, nella customizzazione e nell'utilizzo in generale del sensore modificato


Al momento, l'unico sensore su cui ho testato la modfica è il Door/Window Sensor, per cui la guida rigurderà principalmente questo.
L'hack funziona in modo analogo anche sugli altri sensori. Ogni sensore ha la possibilità di essere utilizzato in modi differenti.

=========================
Xiaomi Door/Window Sensor
=========================

Ci sono alcuni motivi per cui preferisco questo sensore al posto di altri, come per esempio lo switch.

Vantaggi:

- è il più piccolo tra tutti i sensori Xiaomi

- è il più economico (arriva a costare anche € 3,5 circa)

- essendo un sensore binario, il sistema di funzionamento è molto semplice 


La modifica vera e propria consiste nel saldare due cavetti (o direttamente un componente) ai due pin sulla board del sensore.

Nel sensore originale ai due pin è saldato un reed switch, un sensore a lamine magnetico.
Andando a saldare uno switch esterno sui due pin, è possibile utilizzarlo per chiudere e aprire il circuito e quindi inviare il segnale al gateway.

Volendo si potrebbe anche dissaldare il componente originale, ma è generalmente sconsigliato, tranne nel caso in cui dobbiate posizionare il sensore vicino a magneti.


  **IMPORTANTE**

  Questa è la parte interessante.
  Con switch non si intende solamente il semplice interruttore, ma un insieme di interruttori che aprono e chiudono il circuito in base a diverse condizioni.
  Questa parte riguardante gli switch sarà vista in dettaglio in seguito, vi lascio qui solo alcuni dei possibili utilizzi:
  
  - sensore di pioggia/allagamento
  - sensore di temperatura (superata una certa temperatura apre/chiude il circuito)
  - sensore di vibrazione
  - sensore a mercurio (utilizzabile per accelerazione e come tilt switch)


Funzionamento
-------------

Vi spiego semplicemente (sono abbastanza ignorante in materia) come funziona il sensore originale.

Il reed switch è composto da due lamine, di materiale ferromagnetico, sigillate all'interno di un contenitore riempito di gas inerte.
Le due lamine fuoriescono dal contenitore formando i due pin terminali.
Nel caso del sensore porta/finestra i due terminali sono saldati ai due pin sulla scheda.

Normalmente le lamine sono divise da pochi decimi di millimetro, il sensore rileva che il circuito è aperto e invia lo stato di "Aperto" al gateway.
Avvicinando il magnete al sensore, nel caso il campo magnetico sia abbastanza forte, la forza di attrazione farà toccare le due lamine, che chiuderanno il circuito.
A questo punto il sensore rileverà la chiusura del circuito inviando al gateway lo stato di "Chiuso".

Modifica
--------

Per realizzare la modifica avrete bisogno di alcuni strumenti e componenti:

- saldatore e stagno
- sensore porta/finestra xiaomi
- filo elettrico (nè troppo piccolo nè troppo grande, dimensione consigliata: 22 gauge AWG)

Opzionali:

- switch/interruttore (**andremo a vedere in seguito i diversi tipi**)
- trapano e punta, poco più grande del diametro del filo elettrico

Lo switch è opzionale poichè per testare il corretto funzionamento basterà cortocircuitare i due estremi dei fili.
Il trapano servirà per bucare il case e continuare a utilizzarlo anche dopo la modifica.


Apertura
--------

L'apetura è relativamente facile.
Prima di tutto localizzate la scanalatura sul lato corto del sensore.

.. image:: teardown/door_sensor.jpg

Fate leva con un cacciavite, senza impiegare troppa forza, in modo da non rovinare il case.

.. image:: teardown/opening.jpg

Ora rimuovete la batteria CR1632.

.. image:: teardown/opened.jpg

Potete vedere ora la scheda. Per rimuoverla fate nuovamente leva in una delle fessure tra il case e la board. 
Magari utilizzate uno stuzzicadenti, basterà poca forza per farla saltare via.

.. image:: teardown/door_sensor_board.png

Saldatura
---------

Ora posizionate la scheda in modo che stia ferma, nel caso non abbiate una terza mano aiutatevi con dello scotch.

Localizzate i due pin a cui è collegato il reed switch.

.. image:: soldering/reed_switch_pins.png

Ora prendete il filo elettrico e tagliatene due sezioni di 10cm, non preoccupatevi della lunghezza, andremo ad aggiustarla in seguito.
Ora spellate i due estremi dei fili, attorcigliate i filamenti e tagliate nuovamente in modo da lasciare 3/4 mm in rame.
Saldate un po' di stagno su entrambi i pin e poi andando a risciogliere lo stagno presente sui pin, posizionate e saldate i due fili.

.. image:: soldering/soldered_door_sensor.png

Controllate di non aver fatto ponti e che i cavi siano ben collegati.
Nel caso risciogliete la saldatura e, a seconda dei casi, aggiungete o togliete un po' di stagno.

Test
----

A questo punto spellate gli altri estremi, reinserite la batteria e fate toccare i due estremi in rame.
Aprite la vostra app e/o intefaccia (nel caso di HA, Domoticz, OpenHAB..) e vedrete la "porta/finestra" chiusa.

Nel caso non dovesse funzionare, controllate:

- di aver saldato correttamente i due cavetti
- di non aver premuto il tasto di reset per sbaglio


Forare il case
--------------

Reinserite la scheda nel case e fate un segno con la matita in corrispondenza dei due pin.

.. image:: drill/drill_door_sensor.png

A questo punto andate a forare il case con una punta poco più grande del filo.

.. image:: drill/wire_through.png

Ora potete collegare qualsiasi bottone, switch, interruttore della luce e un'altra infinità di sensori-switch.

.. image:: sensors/door_sensor_in_place.png

Andiamo a vedere ora alcune tra le moltissime possibilità.

------------------------------------------------------------------------------------------------------------

**TIPI DI SWITCH UTILIZZABILI**
-------------------------------

Interruttore della luce
-----------------------

Avendo lampadine Yeelight o altre lampadine Xiaomi in casa vi sarete sicuramente dimenticati una volta di non dover premere l'interruttore della luce, oppure qualcun'altro in casa l'ha fatto al posto vostro.

Utilizzando il sensore da voi modificato è possibile ovviare a questo problema.

Staccate l’alimentazione elettrica dell’abitazione, smontate l'interruttore e scollegate le due fasi dall'interruttore.

Collegate i due cavetti dal sensore all'interruttore, ricordatevi la batteria. Ora avete un interruttore della luce wireless.
Ricordatevi di mettere in corto circuito le due fasi con un morsetto, in modo da mantenere la lampadina alimentata.

.. image:: sensors/door_sensor_lights_switch.JPG

(DEVIATORI)
^^^^^^^^^^^
  
Per quanto riguarda i deviatori dovreste trovare quali cavi, se collegati, accendono la luce, a quel punto cortocircuitarli con un morsetto e isolare il rimanente. Tutto questo con l'alimentazione elettrica scollegata. 
In questo modo la lampadina sarà sempre alimentata.
  
Non avendo il sensore esposto all'esterno potete evitare, in questo caso, di forare il case.

------------------------------------------------------------------------------------------------------------

Sensore pioggia/allagamento
---------------------------

Questo switch consiste in una semplice scheda su cui sono stampate due serpentine.

L'acqua posta sulla scheda agirà da conduttore chiudendo il circuito.

In questo caso quando non piove il nostro sensore risulterà aperto e quando piove chiuso.

Può essere utilizzato anche come sensore di allagamento e per altri scopi.

.. image:: sensors/rain_sensor.jpg
.. image:: sensors/rain_sensor_connected.png

------------------------------------------------------------------------------------------------------------

Sensore temperatura
-------------------

Per quanto riguarda la temperatura è possibile utilizzare i termofusibili che a una certa temperatura si chiudono/aprono.

E' possibile scegliere la temperatura alla quale lo switch aprirà o chiuderà il circuito.
E' anche possibile scegliere se normalmente rimangono aperti o chiusi.

Con alcuni è anche possibile regolare a quale temperatura si attiverà.

.. image:: sensors/termofusibile.jpg

------------------------------------------------------------------------------------------------------------

Sensore touch/bottone
---------------------

E' possibile collegare qualsiasi tipo di pulsante, da quelli più semplici fino ai panic button.

E' inoltre possibile collegare sensori touch capacitivi, che funzionano allo stesso modo dei pulsanti normali, 
semplicemente al posto del bottone fisico c'è una superficie touch che, toccandola con un dito, fa chiudere il circuito.

Le sue funzioni sono abbastanza limitate utilizzando MiHome.

.. image:: sensors/push_button_red.jpg
.. image:: sensors/touch_module.jpg

------------------------------------------------------------------------------------------------------------

Sensore inclinazione
--------------------

Esistono sia con una semplice pallina di metallo sia con una goccia di mercurio.
A una certa inclinazione la pallina, a causa della gravità, scivolera in uno dei due estremi del contenitore connettendo i due pin e quindi chiudendo il circuito.

.. image:: sensors/mercury_tilt_switch.jpg

------------------------------------------------------------------------------------------------------------

Sensore vibrazione
------------------

Sono dei piccoli cilindri al centro dei quali è posto un pin, vi è poi una molla avvolta attorno al pin.
Nel caso di vibrazioni la molla farà contatto con il pin chiudendo il circuito.
Ne esistono diversi tipi con diverse sensibilità e alcuni anche regolabili.

Può essere utilizzato per segnalare una scossa sisimica, se abbastanza sensibile.

.. image:: sensors/vibration_sensor.jpg

-----------------------------------------------------------------------------------------------------

| Questi sono solo alcuni dei possibili sensori utilizzabili, cercherò di aggiornare la lista nel tempo.
| Se avete alcune idee aprirò un issue apposito per suggerirle.


Ringrazio Enrico__ per l'idea

.. __: https://t.me/Illoso
