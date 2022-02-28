Documentazione Test Ultrasuoni 
=========

1. [Introduzione teorica](#Introduzione-teorica-SFR05)
2. [Specifiche](#Specifiche-SFR05)
3. [Funzionamento della task](#Funzionamento-della-task)
4. [Schema elettrico](#Schema-elettrico)
5. [Download](#Download-Test-Ultrasuoni)
6. [Compilazione](#Compilazione)
7. [Note](#Note)

Introduzione teorica SFR05
---------------------

L'SRF05 è un’evoluzione dell'SRF04 ed è stato progettato per aumentarne la flessibilità, aumentare la portata e ridurre ulteriormente i costi. In quanto tale, l'SRF05 è completamente compatibile con l'SRF04. La portata è aumentata da 3 metri a 4 metri. Una nuova modalità operativa (che collega il pin della modalità a massa) consente all'SRF05 di utilizzare un singolo pin sia per il trigger che per l'eco, risparmiando così preziosi pin sul controller. Quando il pin della modalità viene lasciato scollegato, l'SRF05 funziona con trigger separati e pin di eco, come l'SRF04. L'SRF05 include un piccolo ritardo prima dell'impulso di eco per dare ai controller più lenti come il Basic Stamp e il Picaxe il tempo di eseguire il loro impulso nei comandi. È sufficiente fornire un breve impulso da 10uS all'ingresso trigger per avviare la misurazione. L'SRF05 invierà una serie di 8 cicli di ultrasuoni a 40 kHz e alzerà la sua linea di eco alta (o la linea di trigger in modalità 2). Quindi ascolta un eco e non appena ne rileva uno abbassa nuovamente la linea dell'eco. La linea dell'eco è quindi un impulso la cui larghezza è proporzionale alla distanza dall'oggetto. Misurando la durata dell'impulso è possibile calcolare la distanza. L'SRF05 può essere attivato ad intervalli di 50 ms (20 volte al secondo). È necessario quindi attendere 50 ms prima del trigger successivo, anche se l'SRF05 rileva un oggetto vicino e l'impulso dell'eco è più breve. Questo per garantire che il "segnale acustico" ultrasonico sia svanito e non causi una falsa eco alla successiva misurazione.

![image](https://user-images.githubusercontent.com/97526576/154640828-0f4533c5-5116-4888-8693-2733be6a6fb4.png) <br>
Per altri approfondimenti : [fblabs](https://docs.google.com/presentation/d/1ncb6Ci0HxQNQlsVwNXdWsPh6nSv_9QuoiDdvp6g8AaI/edit#slide=id.p)


Specifiche SFR05
---------------------

* Tensione Operativa           5V <br>
* Corrente Operativa Tipica    4mA <br>
* Frequenza                    40 Khz <br>
* Portata                      1cm - 4mt <br>
* Dimensioni                   43 x 20 x H 17 mm <br>

Impulso di ritorno: Segnale TTL positivo, di durata proporzionale alla distanza rilevata. <br>
Trigger di Input: Impulso TTL di durata minima di 10 uS. <br>
Modalità di funzionamento: Pin singolo per trig/echo o 2 Pin SRF04 compatibile. <br>


Funzionamento della task
---------------------

Questa task si occupa di rilevare la presenza di un oggetto sul rullo, tramite l’ultrasuoni. Abbiamo configurato il timer PB6 per il Trig e il timer PA5 per Echo. Grazie ad un impulso iniziale del Trig possiamo iniziare la misurazione; Dopo aver configurato i due pin in alternate function scriviamo la interrupt service routine (ISR) che viene eseguita dopo l’impulso, qui misuriamo inizialmente in uS e dopodichè trasformiamo in cm (misura in uS / 58). 
Dopo aver rilevato l’oggetto mentre transita sul nastro, modificherà un bit dell’event group (EVENT_RILEVA_OGGETTO) per indicare a task successivi di essere eseguiti; il buzzer suonerà emettendo un "beep" e nel frattempo il sensore ad infrarossi inizierà la misurazione per rilevare il colore dell'oggetto e poterlo comunicare alle task per servomotore e display LCD. <br>
![ultrasuoni](https://user-images.githubusercontent.com/97526576/155041009-ffcc8fe4-6552-45b0-a0a0-50336b2feb6c.png)


Schema elettrico
---------------------

![ultrasuoni](https://user-images.githubusercontent.com/97526576/154546792-01854a83-a27f-4cdd-9cee-2ec075bfbca7.PNG) <br>
Utilizziamo il timer PB6 (TIM4_CH1_PWM) per il Trigger e il timer PA5 (TIM2_CH1_InCapt_SM) per l'Echo.


Download Test Ultrasuoni
---------------------

Per scaricare il programma eseguire questo comando; <br>
git clone https://github.com/SteePaga/UltrasuoniTest.git

Compilazione
--------------------

Il programma è stato testato con Keil uVision V5.

### Note
Questo programma va unito insieme agli altri test delle rispettive task, per poter implementare il progetto completo del rullo trasportatore. <br>

![IMG_2635](https://user-images.githubusercontent.com/97526576/155039762-2a09c052-3a0a-4c58-9748-8a378ccf16a5.jpg)

