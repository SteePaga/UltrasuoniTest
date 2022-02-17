Documentazione Test Ultrasuoni 
=========

Questa task si occupa di rilevare la presenza di un oggetto sul rullo, tramite l’ultrasuoni. Abbiamo configurato il timer PB6 per il Trig e il timer PA5 per Echo. Grazie ad un impulso iniziale del Trig possiamo iniziare la misurazione; scriviamo la interrupt service routine (ISR) che viene eseguita dopo l’impulso, qui misuriamo inizialmente in uS e dopodichè trasformiamo in cm (misura in uS / 58). 
Dopo aver rilevato l’oggetto mentre transita sul nastro, modificherà un bit dell’event group per indicare al task successivo di essere eseguito, sia quello del buzzer sia quello del rilevamento del colore. 

Schema elettrico
---------------------

![alt text](‪C:\Users\Stefano\Desktop\ultrasuoni.PNG)

Download Test Ultrasuoni
---------------------

git clone https://github.com/SteePaga/UltrasuoniTest.git

Compilazione
--------------------

Il programma è stato testato con Keil uVision V5

### Note
lo script clean_project.bat permette di eliminare i file generati dal compilatore
