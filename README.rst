**(english coming soon)**

Questo repository è un insieme di guide, immagini e idee riguardanti la modifica dei sensori Xiaomi/Aqara

E' possibile "hackerare"/modificare alcuni sensori Xiaomi per poterli utilizzare in modo alternativo.

Dal sensore originale è possibile creare altri tipi di sensori, utilizzabili con MiHome e con qualsiasi sistema di home automation (Domoticz, Home Assistant, OpenHAB...)


| Ora come ora, l'unico sensore su cui ho testato la modfica è il Door/Window Sensor, per cui la guida rigurderà principalmente questo.
|
| *Domani dovrebbero arrivarmi altri switch, per cui ne potrò sacrificare uno per poterlo modificare.*
| *Nei prossimi giorni aggiungerò una guida anche per lo switch.*
|
| L'hack funziona in modo analogo anche sugli altri sensori, per esempio lo Switch Xiaomi è già stato testato da altri ed è funzionante.
| Nel caso abbiate domande potete contattarmi su Telegram: https://t.me/pisch3

=========================
Xiaomi Door/Window Sensor
=========================

Ci sono alcuni motivi per cui preferisco questo sensore al posto di altri, come per esempio lo switch.

Vantaggi:

- è il più piccolo tra tutti i sensori Xiaomi

- è il più economico (con le offerte arriva a costare € 3,5 circa)

- è possibile utilizzare il case orginale anche dopo la modifica

- essendo un sensore binario, il sistema di funzionamento è semplice 


La modifica vera e propria consiste nel saldare due cavetti (o direttamente un componente) ai due pin sulla board del sensore.

Nel sensore originale ai due pin è saldato un reed switch, un sensore a lamelle magnetico.
Andando a saldare uno switch esterno sui due pin, è possibile utilizzarlo per chiudere e aprire il circuito e quindi inviare il segnale al gateway.

Volendo si potrebbe anche dissaldare il componente originale, ma è generalmente sconsigliato, tranne nel caso in cui dobbiate posizionare il sensore vicino a magneti.


  **IMPORTANTE**

  Questa è la parte interessante.
  Con switch non si intende solamente il semplice interruttore, ma un insieme di interruttori che aprono e chiudono il circuito in base   a certe condizioni.
  Questa parte riguardante gli switch sarà vista in dettaglio più avanti, vi scrivo qui solo alcuni dei possibili utilizzi:
  
  - sensore di pioggia/allagamento
  - sensore di temperatura (superata una certa temperatura apre/chiude il circuito)
  - sensore di vibrazione
  - sensore a mercurio (utilizzabile per accelerazione e come tilt switch)

Funzionamento
-------------

Vi spiego semplicemente (sono abbastanza ignorante in materia) come funziona il sensore originale.

Il reed switch è composto da due lamine, di materiale ferromagnetico, sigillate all'interno di un contenitore riempito di gas inerte.
Le due lamine fuoriescono dal contenitore formando le due pin terminali.
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

- switch/interruttore (**andremo a vedere più avanti i diversi tipi**)
- trapano e punta, poco più grande del diametro del filo

Lo switch è opzionale solo perchè per testare il corretto funzionamento basterà cortocircuitare i due estremi dei fili oppure utilizzare un qualsiasi conduttore.
Il trapano servirà per bucare il case e utilizzarlo anche dopo la modifica.


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
Magari utilizzate uno stuzzicadenti, basterà poco per farla saltare via.

.. image:: teardown/door_sensor_board.png

Saldatura
---------

Ora posizionate la scheda in modo che stia ferma, nel caso non abbiate una terza mano aiutatevi con lo scotch.

*IMG*

Localizzate i due pin a cui è collegato il reed switch.

.. image:: soldering/reed_switch_pins.png

Ora prendete il filo elettrico tagliatene due sezioni di 10cm, non preoccupatevi della lunghezza, andremo ad aggiustarla in seguito.
Ora spellate due estremi dei fili, attorcigliate i filamenti e tagliate nuovamente in modo da lasciare 3/4 mm in rame.
Saldate un po' di stagno su entrambi i pin e poi andandolo a risciogliere lo stagno presente sui pin posizionate e saldate i due fili.

.. image:: soldering/soldered_door_sensor.png

Controllate di non aver fatto ponti e che i cavi siano collegati bene.
Nel caso andate a risciogliere la saldatura e, a seconda dei casi, aggiungete o togliete un po' di stagno.

Test
----

A questo punto spellate gli altri estremi, reinserite la batteria e fate toccare i due estremi in rame.
Aprite la vostra app e/o intefaccia (nel caso di HA, Domoticz, OpenHAB..) e vedrete la "porta/finestra" chiusa.

*IMG*

Nel caso non dovesse funzionare, controllate:

- di aver saldato correttamente i due cavetti
- di non aver premuto il tasto di reset per sbaglio

*IMG RESET*

Forare il case
--------------

Reinserite la scheda nel case e fate un segno con la matita in corrispondenza dei due pin.

.. image:: drill/drill_door_sensor.png

A questo punto andate a forare il case con una punta poco più grande del filo.

.. image:: drill/wire_through.png

Ora potete collegare qualsiasi bottone, switch, interruttore della luce e un'altrà infinità di sensori-switch.

.. image:: sensors/door_sensor_in_place.png

Andiamo a vedere ora alcune tra le moltissime possibilità.

------------------------------------------------------------------------------------------------------------

**TIPI DI SWITCH UTILIZZABILI**
-------------------------------

Interruttore della luce
-----------------------

Avendo lampadine Yeelight o altre lampadine Xiaomi in casa vi sarete sicuramente dimenticati una volta di non dover toccare l'interruttore della luce, oppure qualcun'altro in casa l'ha fatto al posto vostro.

Utilizzando il sensore da voi modificato è possibile ovviare a questo problema.

Staccate l’alimentazione elettrica dell’abitazione, smontate l'interruttore, scollegate le due fasi dall'interruttore.

Collegate i due cavetti dal sensore all'interruttore, ricordatevi la batteria. Ora avete un interruttore della luce wireless.
Ricordatevi di mettere in corto circuito le due fasi con un morsetto, in modo da mantenere la lampadina alimentata.

.. image:: sensors/door_sensor_lights_switch.JPG


(DEVIATORI)
^^^^^^^^^^^

Per quanto riguarda i deviatori non è possibile utilizzare questo sensore dall'app MiHome, in quanto i due interruttori fittizi andrebbero in conflitto.
E' possibile invece utilizzare gli Xiaomi Switch con i deviatori e l'app MiHome.
A breve posterò una guida anche su quelli, me ne stanno arrivando 4 da Gerabest e per ora non posso sacrificarne nessuno.

Nel caso utilizziate un sistema di domotica, è possibile mettendo come condizioni il cambio stato del sensore e lo stato della lampadina, 
di conseguenza se la lampadina è accesa e il sensore cambia stato la lampadina si spegne e viceversa.
Dovreste ovviamente trovare quali cavi se collegati accendono la luce, a quel punto cortocircuitarli con un morsetto e isolare il rimanente. Tutto questo con l'elettricità 

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

**Dove acquistarlo:**

Banggood: https://goo.gl/KnYUva

------------------------------------------------------------------------------------------------------------

Sensore temperatura
-------------------

Per quanto riguarda la temperatura è possibile utilizzare i termofusibili che a una certa temperatura si chiudono/aprono.

E' possibile scegliere la temperatura alla quale lo switch aprirà o chiuderà il circuito.
E' anche possibile scegliere se normalmente rimangono aperti o chiusi.

Con alcuni è anche possibile regolare a che temperatura si attiva.

.. image:: sensors/termofusibile.jpg

**Dove acqusitarlo:**

| Amazon: https://goo.gl/UBRmeo
| Banggood (con regolazione temepratura): https://goo.gl/G8ZETr

------------------------------------------------------------------------------------------------------------

Sensore touch/bottone
---------------------

E' possibile collegare qualsiasi tipo di pulsante, da quelli più semplici ai panic button.

E' inoltre possibile collegare sensori touch capacitivi, che funzionano allo stesso modo dei pulsanti normali, 
semplicemente al posto del bottone fisico c'è una superficie touch che, nel caso venga toccata, fa chiudere il circuito.

Le sue funzioni sono abbastanza limitate utilizzando MiHome.

.. image:: sensors/push_button_red.jpg
.. image:: sensors/touch_module.jpg

**Dove acquistarlo:**

Pulsante:
  - Amazon: https://goo.gl/Q6igYU
  - Banggood: https://goo.gl/Cdtn7V

Sensore Touch: 
  - Amazon: https://goo.gl/RBqrD7
  - Banggood: https://goo.gl/4Qmpqx

------------------------------------------------------------------------------------------------------------

Sensore inclinazione
--------------------

Esistono sia con una semplice pallina di metallo sia con una goccia di mercurio.
A una certa inclinazione la pallina, a causa della gravità, scivolera in uno dei due estremi del contenitore connettendo due pin e quindi chiudendo il circuito.

.. image:: sensors/mercury_tilt_switch.jpg

**Dove acquistarlo:**

Tilt ball:
  - Amazon: https://goo.gl/14N5QR
  - Banggood: https://goo.gl/22jCwY / https://goo.gl/PCYEYB

Mercury switch:
  - Amazon: https://goo.gl/F6v1qo
  - Banggood: https://goo.gl/uYiWaK

------------------------------------------------------------------------------------------------------------

Sensore vibrazione
------------------

Sono dei piccoli cilindri al centro dei quali è posto un pin, attorno al pin vi è una molla avvolta attorno al pin.
Nel caso di vibrazioni la molla farà contatto con il pin chiudendo il circuito.
Ne esistono diversi tipi alcuni più facili/difficili da attivare e alcuni regolabili.

Può essere utilizzato per segnalare una scossa sisimica, se abbastanza sensibile, può essere anche utile controllando i log.

.. image:: sensors/vibration_sensor.jpg

**Dove acquistarlo:**

| Banggood (regolabile): https://goo.gl/VMp7yR
| Banggood (alta sensibilità): https://goo.gl/nBU6zC

-----------------------------------------------------------------------------------------------------

| Questi sono solo alcuni dei possibili sensori utilizzabili, cercherò di aggiornare la lista nel tempo.
| Se avete alcune idee aprirò un issue apposito per suggerirle.
