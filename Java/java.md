Java
====

Java è un linguaggio di programmazione che è compilato in *bytecode* eseguibile su ogni architettura che abbia una propria JVM (Java Virtual Machine).

È un linguaggio orientato agli oggetti, cioè consiste di un insieme di classi che contengono **attributi** (variabili) e **metodi** (funzioni). Lo scopo della struttura a classi è limitare tramite opportuni modificatori la **visibilità** delle componenti di un oggetto, al fine di rendere più agevole e modulare la modifica del codice.

Java è un linguaggio *statico*, cioè ogni elemento deve avere un *tipo* esplicito.

# Tipi Primitivi *(primitives)*

- `byte` (8 bit)
- `short` (16 bit)
- `int` (32 bit)
- `long` (64 bit)
- `float` (32 bit)
- `double` (64 bit)
- `boolean` (*vero* o *falso*)
- `char` (16 bit)

# Visibilità (*scope*)
In Java si può modificare la **visibilità** di una variabile tramite delle keyword da inserire all'inizio di una definizione.

# Classi

Le classi sono una struttura fondamentale di Java che incapsula il codice attraverso metodi (*methods*) e attributi (*attributes*). La sintassi è la seguente:
```java
class Dog {
    // ...
}
```

## Attributi
Gli attributi sono delle variabili che sono contenute all'interno di una classe:
```java
class Dog {
    float height; // Attr. non inizializzato
    int age = 2; // Attr. inizializzato a 2
    boolean isHungry = true;
}
```
Si può accedere ad un attributo mediante la sintassi col `.`
```java
// Dato un cane chiamato "doggo", posso accedere
// all'attr. "age" come segue
Dog doggo = new Dog();

doggo.age // => 2
```
## Metodi
I metodi sono delle funzioni che sono contenute all'interno di una classe.
```java
class Dog {
    // Attributes
    // ...
    boolean isHungry = true;
    int timesPetted = 10;

    // Methods
    void pet() {
        timesPetted += 1; // incrementa "times petted"
    }
    void eat(int numberOfSnacks) {
        if(snacks > 2) {
            isHungry = false; // aggiorna l'attr. "isHungry"
        }
    }
    int getTimesPetted() {
        return timesPetted; // => 10
    }
}
```

## Istanze (*Instances*) e Riferimenti (References)
Una classe rappresenta una struttura di attributi e metodi, ma una volta che il programma è in esecuzione, affinchè possa accedere ad essi ho bisogno di allocare in **memoria** la classe: posso dunque istanziarla tramite la keyword `new`:
```java
Dog scooby = new Dog();
```
Il primo `Dog` specifica il tipo della variabile `scooby`, `new` dice al compilatore che vogliamo creare una nuova **istanza** in memoria, mentre l'ultimo `Dog()` è in realtà un metodo speciale chiamato **costruttore**.

Il risultato è l'allocazione in memoria della nuova istanza di `Dog`, e viene assegnato alla variabile `scooby` il **riferimento** all'istanza in memoria. `scooby` **non** contiene l'istanza, ma solo un indirizzo di essa.

```java
Dog scooby = new Dog(); // nuovo riferimento all'istanza di Dog
Dog cloneOfScooby = scooby; // è la stessa istanza
System.out.println(scooby.age) // => 2
System.out.println(cloneOfScooby) // => 2

scooby.age = 4

System.out.println(scooby.age) // => 4
System.out.println(cloneOfScooby) // => 4
```

## Costruttori (*constructors*)
Una classe può richedere dei parametri quando viene istanziata, e per fare ciò si usa un metodo speciale detto **costruttore** che ha lo stesso nome della classe a cui appartiene:
```java
class Dog {
    // attributi
    private String name;
    private int age;

    // costruttore
    public Dog() {

    }
}
```

## `this`
`this` è una pseudo-variabile che ha come valore il riferimento all'oggetto in uso. È utile quando un parametro di un metodo ha lo stesso nome di un attributo. È opzionale quando non ci sono ambiguità.
```java
class Dog() {
    private String name;

    public void giveName(String name) {
        this.name = name;
        // this.name è l'attributo
        // name è il parametro
    }
}
```

# Packages

Più classi sono raggruppate in un pacchetto (*package*), definito così in cima ad un file `.java`:
```java
package A; // Sono nel package A

public class Dog {
    // ...
}
```
Se volessi accedere alle classi contenute in *A* posso *importare* i contenuti di A in un altro file come segue:
```java
package B; // Sono in un altro package
import A.Dog; // Importo la classe "Dog" dal package A

public class House {
    // ...
    Dog scooby = new Dog(); // Posso usare la classe Dog
}
```
Posso anche importare *tutti* i componenti di un package usando la *wildcard* `*` come segue:
```java
import A.*; // Importa tutte i componenti di A
```
I package si posso annidare come segue:
```java
// File 1
package restaurant.kitchen;
public class Oven {
    public void turnOn();
}
```
```java
// File 2
import restaurant.staff.*;
public class Chef {
    // The Chef class can now use the Oven class
    Oven oven = new Oven();
    Oven.turnOn();
}
```
# Stringhe

Le stringhe sono oggetti immutabili in Java.
A differenza di C, Java permette una gestione delle stringhe attraverso la classe `String`, che disponde di propri metodi come:

- `length()` (restituisce la lunghezza della stringa)
- `charAt(int index)` (restituisce il `char` alla posizione `index`)
- `substring(int beginIndex)` (restituisce una porzione della stringa a partire dalla posizione `beginIndex`)