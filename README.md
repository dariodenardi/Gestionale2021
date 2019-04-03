# Gestionale1819
Dubbi frequenti presentati durante le esercitazioni

Questa guida verrà aggiornata dopo ogni esercitazione e fungerà come punto di raccolta dei dubbi più frequenti.

Sito del corso disponibile [qui](http://www-db.deis.unibo.it/courses/FIT1-LZ/).

**N.B.** Eventuali dubbi potranno essere segnalati anche via e-mail.

## Installazione del JDK e di Eclipse
Facendo riferimento alle slide presenti sul **sito del corso** i passi da seguire in sequenza sono i seguenti:
1. Installare il JDK
2. Installare Eclipse

**Importante Windows**: la versione da scaricare è stata aggiornata (**controllare [slide](http://www-db.deis.unibo.it/courses/FITA-LZ/LABORATORIO/slide/2018-19/01_esercitazione_2019_02_27.pdf)**), in quanto la versione indicata precedentemente presentava delle incompatibilità con eclipse dando il seguente errore: **exit code = 13**

**Importante Mac**: le ultime versioni di MacOs non prevedono l'istallazione by default del jdk, quindi bisognerà installare il tutto a mano prima di eclipse. Le slide sono state aggiornate con la guida relativa.

## Risoluzione problemi Eclipse
### Mancanza librerie
È possibile che la versione usata del JDK a casa sia diversa da quella del laboratorio. Questo potrebbe provocare (se la versione del JDK di casa è più recente rispetto a quella del laboratorio) un'incongruenza di librerie nel progetto e una conseguente eliminazione delle librerie dal progetto. Quindi il risultato sarà un progetto pieno di errori.

<img src="img/img1.png" width="" height="60">

Ci toccherà aggiungere nuovamente la libreria.

Per fare ciò occorre configurare il **build Path** (tasto destro sul progett --> Build Path --> Configure Build Path).

<img src="img/img2.png" width="400" height="">

Selezionando la sezione **libraries**, potremo aggiungere la nostra libreria.

<img src="img/img3.png" width="" height="">

Selezioniamo **Modulepath** e successivamente **Add Library**

La scheramata successiva sarà la seguente.

<img src="img/img4.png" width="500" height="">

Selezioniamo **JRE System Library** clicchiamo su **Next**.

<img src="img/img5.png" width="500" height="">

Lasciamo tutto così com'è e clicchiamo su **Finish**

Al termine di questa operazione clicchiamo su **Apply** e la libreria sarà nuovamente presente.

## Input Stringhe
Errore comune quando si vuole leggere una stringa da input risiede nella *nextLine()* della scanner.
Questo è dovuto al comportamento anomalo della *nextLine()* che va a consumare l'invio della lettura precedente.
```java
Scanner tastiera = new Scanner(System.in);

// NextLine senza alcun comprtamento anomalo
System.out.println("Inserisci una stringa: ");
String s1 = tastiera.nextLine();

tastiera.close();
```
In questo caso non avremo nessuno comportamento anomalo, in quanto non viene effettuata alcuna lettura prima della nextLine().

```java
Scanner tastiera = new Scanner(System.in);

System.out.println("Inserisci un intero: ");
int in1 = tastiera.nextInt();

//NextLine con comportamento anomalo
System.out.println("Inserisci una stringa: ");
String s1 = tastiera.nextLine();

tastiera.close();
```

In questo caso, la *nextLine()* andrà a consumare l'**enter** inserito al termine dell'input *tastiera.nextInt()*. Questo significa che dentro s1 ci sarà una stringa vuota.

Quindi la sequenza di istruzioni **corretta** diventa la seguente

```java
Scanner tastiera = new Scanner(System.in);

System.out.println("Inserisci un intero: ");
int in1 = tastiera.nextInt();

tastiera.nextLine(); //consumo il tasto enter

//NextLine senza comportamento anomalo
System.out.println("Inserisci una stringa: ");
String s1 = tastiera.nextLine();

tastiera.close();
```

## Istruzioni di selezione
Uno dei problemi più frequenti sull'istruzione di selezione **if/else** riguarda la struttura. In particolare

```java

if(condizione);{
    //il codice inserito all'interno di questo blocco non verrà mai eseguito
}else
{
    //altre istruzioni
}
```
L'errore in questo caso risiede nell'inserimento del terminatore '**;**' presente al termine della condizione. Questo terminatore infatti impedirà, nel caso in cui siano soddisfatte le condizioni, l'esecuzione delle istruzioni presenti dentro il blocco dell'if.

Un altro dubbio riguardante la struttura riguarda il numero di istruzioni inseribili all'interno del blocco.

```java
if (condizione)
    //una sola istruzione
else if(condizione2)
    //una sola istruzione
else
    //una sola istruzione
```
In questo caso non ho specificato le parentesi graffe, quindi posso inserire una sola istruzione all'interno dell'istruzione **if/else**, tutte le altre istruzioni saranno considerate esterne all'istruzione di selezione.
Quindi nel caso in cui vogliamo eseguire più di una singola istruzione bisognerà **obbligatoriamente** usare le parentesi graffe.

```java
if(condizione){
    /*Tutte le istruzioni inserite in questo blocco verranno 
    eseguite solo se la condizione è soddisfatta*/
}
else if(condizione2){
    /*Tutte le istruzioni inserite in questo blocco verranno 
    eseguite solo se la condizione2 è soddisfatta*/
}else{
    /*Tutte le istruzioni inserite in questo blocco verranno 
    eseguite se le precendenti condizioni non sono soddisfatte*/
}

```

### Assegnamento VS Uguaglianza
Uno degli errori più comuni riguarda la distinzione tra questi due operatori '**=**' e '**==**'.
L'operatore '**=**' è usato per assegnare un valore ad una variabile. Quindi ricordando la struttura di una variabile
```java
    tipo nome = valore
```
Questo permetterà di inserire il valore dentro la **cella di memoria** alla quale è stato assegnato il nome *nome*.

Diverso è il caso di'**==**'. È un operatore di comparazione. Questo significa che potrà essere usato per verificare l'ugualianza di due valori (come illustrato di seguito).

```java
int n1 = 10;
int n2 = 11;

if(n1 == n2){
    //esegui queste istruzioni
}else
    //esegui questa istruzione
```

In conclusione, non bisogna **MAI** scrivere una cosa del genere
```java
int n1 = 10;
int n2 = 11;

if(n1 = n2){ //SBAGLIATO
    //esegui queste istruzioni
}else
    //esegui questa istruzione
```
Il compilatore comunque segnalerà questa tipologia di errore, in quanto riconoscerà l'errore nella sintassi.
