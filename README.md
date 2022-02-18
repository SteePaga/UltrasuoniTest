Documentazione Test Ultrasuoni 
=========

Introduzione teorica SFR05
---------------------

L'SRF05 è un’evoluzione dell'SRF04 ed è stato progettato per aumentarne la flessibilità, aumentare la portata e ridurre ulteriormente i costi. In quanto tale, l'SRF05 è completamente compatibile con l'SRF04. La portata è aumentata da 3 metri a 4 metri. Una nuova modalità operativa (che collega il pin della modalità a massa) consente all'SRF05 di utilizzare un singolo pin sia per il trigger che per l'eco, risparmiando così preziosi pin sul controller. Quando il pin della modalità viene lasciato scollegato, l'SRF05 funziona con trigger separati e pin di eco, come l'SRF04. L'SRF05 include un piccolo ritardo prima dell'impulso di eco per dare ai controller più lenti come il Basic Stamp e il Picaxe il tempo di eseguire il loro impulso nei comandi.

![image](https://user-images.githubusercontent.com/97526576/154640828-0f4533c5-5116-4888-8693-2733be6a6fb4.png)


Specifiche SFR05
---------------------

Tensione Operativa           5V
Corrente Operativa Tipica    4mA
Frequenza                    40 Khz
Portata                      1cm - 4mt
Dimensioni                  43 x 20 x H 17 mm

Impulso di ritorno: Segnale TTL positivo, di durata proporzionale alla distanza rilevata.
Trigger di Input: Impulso TTL di durata minima di 10 uS.
Modalità di funzionamento: Pin singolo per trig/echo o 2 Pin SRF04 compatibile.


Funzionamento della task
---------------------

Questa task si occupa di rilevare la presenza di un oggetto sul rullo, tramite l’ultrasuoni. Abbiamo configurato il timer PB6 per il Trig e il timer PA5 per Echo. Grazie ad un impulso iniziale del Trig possiamo iniziare la misurazione; scriviamo la interrupt service routine (ISR) che viene eseguita dopo l’impulso, qui misuriamo inizialmente in uS e dopodichè trasformiamo in cm (misura in uS / 58). 
Dopo aver rilevato l’oggetto mentre transita sul nastro, modificherà un bit dell’event group (EVENT_RILEVA_OGGETTO) per indicare a task successivi di essere eseguiti; il buzzer suonerà emettendo un "beep" e nel frattempo il sensore ad infrarossi inizierà la misurazione per rilevare il colore dell'oggetto e poterlo comunicare alle task per servomotore e display LCD.

Schema elettrico
---------------------

![ultrasuoni](https://user-images.githubusercontent.com/97526576/154546792-01854a83-a27f-4cdd-9cee-2ec075bfbca7.PNG)


Download Test Ultrasuoni
---------------------

git clone https://github.com/SteePaga/UltrasuoniTest.git

Compilazione
--------------------

Il programma è stato testato con Keil uVision V5

### Note
Questo programma va unito insieme agli altri test delle rispettive task, per poter implementare il progetto completo del rullo trasportatore.
Link al progetto completo : https://drive.google.com/drive/folders/1DELfbtvsyqDubmVxufoYO7MtyMC3l895?usp=sharing
