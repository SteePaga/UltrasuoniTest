Documentazione Test Ultrasuoni 
=========

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
