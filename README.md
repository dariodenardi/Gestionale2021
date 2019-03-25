# Gestionale1819
Dubbi frequenti presentati durante le esercitazioni

Questa guida verrà aggiornata dopo ogni esercitazione e fungerà come punto di raccolta dei dubbi più frequenti.

Sito del corso disponibile [qui](http://www-db.deis.unibo.it/courses/FITA-LZ/).

**N.B.** Eventuali dubbi potranno essere segnalati anche via e-mail.

## Installazione del JDK e di Eclipse
Facendo riferimento alle slide presenti sul **sito del corso** i passi da seguire in sequenza sono i seguenti:
1. Installare il JDK
2. Installare Eclipse

**Importante Windows**: la versione da scaricare è stata aggiornata (**controllare [slide](http://www-db.deis.unibo.it/courses/FITA-LZ/LABORATORIO/slide/2018-19/01_esercitazione_2019_02_27.pdf)**), in quanto la versione indicata precedentemente presentava delle incompatibilità con eclipse dando il seguente errore: **exit code = 13**

**Importante Mac**: le ultime versioni di MacOs non prevedono l'istallazione by default del jdk, quindi bisognerà installare il tutto a mano prima di eclipse. Le slide sono state aggiornate con la guida relativa.

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
Quindi nel caso in cui vogliamo eseguire più di una singola istruazione bisognerà **obbligatoriamente** usare le parentesi graffe.

```java
if(condizione){
    /*Tutte le istruzioni inserite in questo blocco verranno 
    eseguite solo se la condizione è soddisfatta*/
}
else if(condizione2){
    /*Tutte le istruzioni inserite in questo blocco verranno 
    eseguite solo se la condizione è soddisfatta*/
}else{
    /*Tutte le istruzioni inserite in questo blocco verranno 
    eseguite se le precendeti istruzioni non sono soddisfatte*/
}

```