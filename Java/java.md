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

# Classi (*classes*)

Le classi sono una struttura fondamentale di Java che incapsula il codice attraverso metodi (*methods*) e attributi (*attributes*). La sintassi è la seguente:
```java
class Dog {
    // ...
}
```

## Attributi (*attributes*)
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
## Metodi (*methods*)
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

## Istanze (*instances*) e Riferimenti (references)
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
## Visibilità (*visibility*)
In Java si può decidere la visibilità (scope) di classi, attributi e metodi mediante i **modificatori di visibilità** `public`, `protected`, `private`, che si inseriscono all'inizio di una dichiarazione.

| Modificatore | Visibilità |
|--------------|------------|
| `public` | Ovunque |
| `protected` | Stesso [*package*](#costruttori-constructors) e *sottoclassi* della classe in questione |
| - (friendly) | Stesso [*package*](#costruttori-constructors) |
| `private` | Stessa [classe](#classi-classes) |

```java
package Pets;

// la classe `Dog` è accessibile ovunque.
public class Dog {
    public String name; // Accessibile ovunque.
    protected int age; // Accessibile da sottoclassi di `Dog`
                       // o nello stesso package.
    private String secretSnack; // non accessibile al di
                                // fuori di `Dog`.
}

// la classe `Cat` è accessibile solo nel package `Pets`.
class Cat { // visibilità = friendly
    // ...
}

// la classe `Fish` e i suoi attributi/metodi non
// saranno MAI accessibili! Non ha senso avere classi private.
private class Fish {
    // ...
}
```

## Costruttori (*constructors*)
Una [classe](#classi-classes) può richedere dei parametri quando viene istanziata, e per fare ciò si usa un metodo speciale detto **costruttore** che ha lo stesso nome della classe a cui appartiene:
```java
class Dog {
    // attributi
    private String name;
    private int age;

    // costruttore
    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
        // Altre operazioni da eseguire quando
        // viene istanziata la classe
    }
}
```

### `this`
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
Posso anche importare *tutti* i componenti di un package usando la *wildcard* '`*`' come segue:
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
A differenza di C, Java permette di gestire le stringhe attraverso la classe `String`, che disponde di propri metodi come:

- `length()` (restituisce la lunghezza della stringa)
- `charAt(int index)` (restituisce il `char` alla posizione `index`)
- `substring(int beginIndex)` (restituisce una porzione della stringa a partire dalla posizione `beginIndex`)

# Attributi e Metodi Statici

In Java è possibile accedere ad attributi o metodi senza la necessità di dovere istanziare una classe a priori mediante la parola chiave `static`.

`Static` è da usare dopo i modificatori di visibilità.

I metodi e gli attributi statici saranno allocati al momento dell'esecuzione del programma. C'è *una e una sola* allocazione per ogni variabile statica, il che vuol dire che quando essa viene modificata il suo valore è aggiornato in ogni punto del codice.

```java
// File 1
package school;

public class Math {
    // Dichiaro un metodo statico
    public static sum(int a, int b) {
        return a + b;
    }
    // Dichiaro un attributo statico
    public static int grade;
}
```
```java
// File 2
import school.*;

public class Student {
    public void doHomework() {
        // Non ho bisogno di un istanza di `Math`
        // per usare `Math.sum()`.
        int result = Math.sum(2 + 2);
        if (result == 4) {
            // Posso accedere a una variabile
            // statica senza avere un istanza
            // di `Math`.
            Math.grade = 10;
        }
    }
}
```
# Classi e metodi astratti
In Java si possono define classi per le quali non è possibile creare un'istanza mediante la keyword `abstract`. Una classe è `abstract` se ha almeno un metodo *astratto*, cioè di cui viene data solo la *dichiarazione* ma non l'*implementazione*.

Sarà un'altra classe a dover estendere e a implementare i metodi di una classe astratta.
```java
new Shape(); // ERRORE: non si può istanziare una
             //         classe astratta.
```
```java
abstract Shape {
    static int sides;
    abstract void draw();
}
```

# Ereditarietà (inheritance)
In Java è possibile avere **sottoclassi (*subclass*)** di una classe, ovvero una versione estesa o moficata di una classe esistente.
Una sottoclasse può estendere *al massimo* una classe, mediante la keyword `extends`. La classe da cui viene *estesa* una sottoclasse si dice **sopraclasse (*superclass*)**.

```java
class Animal {
    private int numberOfLegs;
    public void eat() {
        // ...
    }
    public boolean hasLegs() {
        // Restituisce vero se l'animale ha più di 0 gambe.
        return numberOfLegs > 0;
    }
}

class Dog extends Animal {
    public void bark() {
        // ...
    }
}
```

Dall'esempio sopra, è possibile, data un'istanza di `Dog`, poter chiamare sia `eat()` sia `bark()`.

`Dog` è una sottoclasse di `Animal`, cioè implementa tutti i metodi e attributi di `Animal` ed eventualmente di nuovi. `Animal` è la sopraclasse di `Dog`.

## `super`
È possibile accedere ai metodi della sopraclasse *da un **metodo** della sottoclasse* usando la pseudo-variabile `super`:
```java
class Dog extends Animal {
    public void walk() {
        // `Dog` non descrive nessun metodo `hasLegs()`, ma
        // lo eredita da `Animal`
        if (super.hasLegs()) {
            // Cammina
        } else {
            // Questo cane ha qualche problema
        }
    }
}
```
## Costruttori e superclassi
I costruttori **non** vengono ereditati a differenza degli altri metodi, perchè c'è la necessità di inizializzare i nuovi membri di una sottoclasse. Si può però evitare di inizializzare manualmente i membri della sopraclasse chiamando invece il costruttore della stessa mediante `super();`
```java
class Animal {
    private int numberOfLegs;

    public Animal(int numberOflegs) {
        this.numberOfLegs = numberOfLegs;
    }
}

class Dog extends Animal {
    private String name;
    public Dog(String name) {
        super(4) // super(int numberOfLegs) è il
                 // costruttore di `Animal`.
        // Nuovo attributo da inizializzare non
        // presente in `Animal`.
        this.name = name;
    }
}
```


## Override
Data una sottoclasse, è possibile modificare quello che fa un metodo ereditato dalla sopraclasse eseguendo un *override* (ridefinizione). Si indica al compilatore mediante digitando `@Override` prima del metodo di cui si effettua un override.
```java
class Snake extends Animal {
    @Override
    public void eat() {
        // ...
    }
}
```

## `final`
Java permette di impedire la creazione di ulteriori sottoclassi mediante la keyword `final`.
```java
final class Chihuahua extends Dog {
    // ...
}

class TalkingChihuahua extends Chihuahua {
    // ERRORE: non si può estendere una classe final.
}
```
Si possono anche avere metodi `final`...
```java
class Bird extends Animal {
    final void fly() {
        // ...
    }
}

class Hawk extends Bird {
    @Override
    void fly() {
        // ERRORE: non si può fare override
        //         di un metodo final!
        // È già presente in `Bird` come `final`.
    }
}
```
... e attributi `final`, in questo caso si comportano come *costanti*:
```java
class Bird extends Animal {
    public final int numberOfEyes = 2;
    
    public void flyOverNuclearPlant() {
        numberOfEyes = 3; // ERRORE: non si può modificare
                          //         un attributo `final`!
    }

}
```

## Interfacce (*interfaces*)
Java non permette di ereditare da più di una classe, ma in certe situazioni fa comodo avere la possibilità di ereditare da più classi: esistono dunque le **interfacce (*interfaces*)**.

Le interfacce sono come delle classi i cui attributi sono di default `public static final`, cioè **costanti** e i metodi sono `public abstract` (possono anche essere `static`).

```java
interface flying {
    int LEGS = 2; // public, static, final
    void fly(); // public, abstract
}
```

Un'interfaccia può estendere altre interfacce mediante la keyword `extends` come per le classi.
```java
interface flying extends /* <altre interfacce> */ {
    // ...
}
```

Una classe può implementare un'interfaccia mediante la keyword `implements`.
```java
class Bird extends Animal implements flying {
    // ...
    @Override
    public void fly() {
        // ... (implemento `fly()`)
    }
}
```

# Object (classe)

TODO
