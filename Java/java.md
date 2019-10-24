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
| `Public` | Ovunque |
| `Protected` | Stesso [*package*](#costruttori-constructors) e *sottoclassi* della classe in questione |
| - (friendly) | Stesso [*package*](#costruttori-constructors) |
| `Private` | Stessa [classe](#classi-classes) |

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
In Java se non si specifica alcuna sopraclasse da cui ereditare si eredita automaticamente dalla classe `Object`. `Object` contiene alcuni metodi particolarmente comodi:
## `public boolean equals(Object)`
Restituisce `true` se i due oggetti sono identici. Spesso conviene fare override di `equals()` per controllare solo certi campi. L'implementazione di default controlla che i riferimenti siano uguali.
```java
class Circle {
    public int x;
    public int y;
    public String color;
    // ...
}
```
```java
Circle a = new Circle();
Circle b = a;
a.equals(b); // => true, hanno lo stesso riferimento.
             // C'è una sola istanza di `Circle`!
```
## `public String toString()`
Restituisce una rappresentazione testuale dei valori dell'oggetto. Si può fare override per stampare quello che si vuole.
```java
Circle a = newCircle(0, 0, "red");
a.toString(); // => Circle@<hash dei valori>
```
Facendo override di `toString()` diventa
```java
class Circle {
    // ...
    @Override
    public String toString() {
        return "It's a " + color + " circle";
    }
}
```
```java
Circle a = newCircle(0, 0, "red");
a.toString(); // => "It's a red circle"
```
## `public Object clone()`
Restituisce un riferimento a una copia dell'oggetto, nella quale vengono copiati i valori dei campi (attenzione: gli attributi che sono una reference copiano la reference allo stesso oggetto!) A volte conviene fare override per avere maggiore controllo su cosa viene clonato.
```java
Circle a = new Circle(0, 0, "red");
Circle b = a;
Circle c = a.clone();
a.equals(b); // => true, è un riferimento alla
             // medesima istanza.
a.equals(c); // => false, c è un riferimento ad
             // un'altra istanza di `Circle`, che
             // ha però gli stessi attributi.
```

# Eccezioni
Java permette di gestire eventuali problemi a runtime senza causare l'arresto inaspettato del programma mediante le **eccezioni**.

Una funzione può "lanciare" un'eccezione anziché restituire il valore atteso. L'eccezione viene "catturata" dal chiamante che può gestire il problema. Si usa la seguente sintassi:
```java
try {
    // ...
    // Blocco che contiene le funzioni che possono
    // lanciare eccezioni.
} catch(ExceptionType e) {
    // ...
    // Gestisco l'eccezione
} finally {
    // ...
    // Viene sempre eseguito.
    // Utile per chiudere i file letti o altri I/O.
}
```
Le eccezioni sono delle speciali classi che quindi definiscono il tipo dell'eccezione. Si possono gestire così eccezioni diverse cambiando il tipo dell'eccezione.
```java
try {
    int y = Integer.parseInt(stdin.readLine());
    x = x/y;
} catch(NumberFormatException e) {
    // gestisco eccezioni da parseInt
} catch (ArithmeticException e) {
    // gestisco tutte le eccezioni aritmetiche, 
    // inclusa DivisionByZero
} catch (IOException e) {
    // gestisco le eccezioni di I/O
}
```
> Il parametro `e` può avere qualsiasi nome: è un oggetto che contiene informazioni sull'eccezione.

Quando occorre un'eccezione, il codice nel `try` block smette di essere eseguito, e viene eseguito il `catch` corrispondente.

## Throw

Java non permette di non gestire le eccezioni: se non vuole gestire un'eccezione in una particolare funzione, si può passare l'eccezione al chiamante definendo nella dichiarazione le eccezioni che essa può generare dopo la keyword `throws`.
```java
public static int divideNumbersFromFile() throws IOException, ArithmeticException {
    // ...
}
```

All'interno di una propria funzione, è possibile "lanciare" un'eccezione mediante `throw`:
```java
public static int sumOnlyPositiveNumbers(a, b) throws NegativeException {
    if (a < 0 || b < 0) {
        throw new NegativeException();
    } else {
        return a + b;
    }
}
```

Le eccezioni sono sottoclassi di `Throwable`, e si dividono in `Error`s (errori gravi) e `Exception`s (gestibili). Le `Exception`s a loro volta si dividono in *checked* e *unchecked*: le eccezioni *checked* devono essere gestite a compile-time altrimenti si ha errore, quelle *unchecked* possono anche non essere gestite da un blocco `catch`, anche se converrebbe.

Se si può evitare un'eccezione con un semplice check, spesso è conveniente.

## Creare nuove eccezioni
Si possono creare nuove eccezioni creando una classe che estende `Exception` e implemente due costruttuori, uno senza parametri e uno che riceve una stringa.
```java
public class MyException extends Exception {
    public MyException() {
        super();
    }
    public MyException(String s) {
        super(s);
    }
}
```
Posso lanciare questa nuova eccezione nel seguente modo:
```java
throw new MyException("Houston, we have a problem!");
```
## Masking
Le eccezioni possono essere usate per evitare un errore in una funzione che deve restituire al chiamante, per esempio restituendo un valore di default.
```java
public static String parseInput() {
    // ...
    String parsedOutput;
    try {
        stdin.readLine()
    } catch(IOException e) {
        // Restituisco una string vuota se ho
        // delle eccezioni, anzichè avere un
        // crash.
        parsedOutput = "";
    } finally {
        // ...
    }
    // ...
    return parsedOutput;
}
```
## Reflection
A volte si vuole propagare al chiamante un'eccezione, che non sempre è dei tipi `throw`-abili da esso: allora si può lanciare un'eccezione compatibile col chiamante nel blocco `catch` dell'eccezione.
```java
public static void feedBaby (Baby baby) throws CryException {
    try {
        feed(baby);
    } catch (NotHungryException e) {
        throw new CryException("WEEE!");
    } catch (IsTiredException e) {
        throw new CryException("WEEE!");
    }
}
```

