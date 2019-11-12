![banner](../images/java_banner.png)

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

```Java
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

## Object (classe)
In Java se non si specifica alcuna sopraclasse da cui ereditare si eredita automaticamente dalla classe `Object`. `Object` contiene alcuni metodi particolarmente comodi:

- `public boolean equals(Object)` restituisce `true` se i due oggetti sono identici. Spesso conviene fare override di `equals()` per controllare solo certi campi. L'implementazione di default controlla che i riferimenti siano uguali.

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

- `public String toString()` restituisce una rappresentazione testuale dei valori dell'oggetto. Si può fare override per stampare quello che si vuole.

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

- `public Object clone()` restituisce un riferimento a una copia dell'oggetto, nella quale vengono copiati i valori dei campi (attenzione: gli attributi che sono una reference copiano la reference allo stesso oggetto!) A volte conviene fare override per avere maggiore controllo su cosa viene clonato.

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

- `public int hashCode()` restituisce un numero che dipende dallo stato dell’oggetto, in particolare instanze uguali ritornano hash uguali.
Deve essere ridefinito nel caso si ridefinisca il metodo `equals()`.

# Collection

[`Collection`](http://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) è una classe di Java che viene utilizzata da molte sue sottoclassi per rappresentare collezioni di elementi, come `List`, `Set` (non contiene elementi duplicati), `Queue` (ha metodi per inserire/prelevare in testa o coda). Tutte le sottoclassi di `Collection` sono *iterabili*, cioè implementano l'interfaccia `Iterable` e i loro elementi possono essere ciclati da un `forEach` loop.

Si specifica il tipo contenuto nella *collection* all'interno delle parentesi uncinate `<`,`>`. Ad esempio per `Set`

```java
Set<Integer> mySet = new Set<Integer>();
```

### Implementazioni di Collection

- [**Set**](http://docs.oracle.com/javase/8/docs/api/java/util/Set.html): non contiene elementi duplicati
    - [HashSet](http://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html)
    - [TreeSet](http://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html)
    - [LinkedHashSet](http://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html)
- [**List**](http://docs.oracle.com/javase/8/docs/api/java/util/List.html): sequenza di elementi che può contenere duplicati
    - [ArrayList](http://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)
    - [LinkedList](http://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)
    - [Vector](http://docs.oracle.com/javase/8/docs/api/java/util/Vector.html)
- [**Queue**](http://docs.oracle.com/javase/8/docs/api/java/util/Queue.html): coda di elementi che può contenere duplicati
    - [Deque](http://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) (entrambi gli estremi sono manipolabili)
- [**Map**](http://docs.oracle.com/javase/8/docs/api/java/util/Map.html): associa a un valore a una chiave. Non ha duplicati, ma può avere valori nulli.
    - [HashMap](http://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
    - [TreeMap](http://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)
    - [LinkedHashMap](http://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)

## Generics

Le classi in Java possono accettare dei parametri speciali chiamati *generics* che sono *tipi* di una variabile. È quindi possibile utilizzare tali parametri nei metodi della classe come *tipi* dei parametri del metodo.

Si specifica il nome del generics tra le parentesi uncinate dopo il nome della classe.

Più parametri devono essere separati da una virgola.

```java
public class MyList<T> {
    // Attributo di tipo T
    private T myVar;
    // Metodo di tipo T
    public myMethod(T param) {
        // ...
    }
    // Costruttore che accetta un parametro di tipo T
    public MyList(T value) {
        myVar = value;
    }
}
```

Posso quindi utilizzare la classe specificando i parametri *generics* per creare una instance, ad esempio:

```java
MyList<Integer> listOfIntegers = new MyList<Integer>(3);
MyList<String>  listOfStrings  = new MyList<String>("Hi!");
```

Si possono anche creare metodi generici senza dover avere una classe con *generics* nel seguente modo:

```java
public <T> void genericPrint(T param) {
    System.out.format("%s", param);
}

myGenericMethod(33); // => 33
myGenericMethod("Hello!"); // => Hello!
```

Il carattere `?`, detto *wildcard*, permette di rappresentare un tipo non definito.
È comodo per definire dei sottoinsiemi di tipi che possono essere accettati mediante la keyword `extends` o `super`.

Il seguente metodo accetta una `Collection` di `Mammal` o sue sottoclassi, che potrebbero essere `Cat` oppure `Dog`, o una sua sottoclasse, come `Bulldog`, ma non accetta `Fish`, che non è un mammifero.

```java
public void method(Collection<? extends Mammal> collection);
```

Il seguente metodo accetta una `Collection` di `Mammal` o di sue sopraclassi, come `Vertebrate` o la sua sopraclasse `Animal`, ma non `Invertebrate`, che è sottoclasse di `Animal` ma non sopraclasse di `Vertebrate`.

```java
public void method(Collection<? super Mammal> collection);
```

## HashTable

Una *HashTable* è un'implementazione di una *Map*, e **non** ammette valori nulli, ed è [synchronized](#Atomicità-e-synchronized).

`HashTable<K,V>` ha due *generics*, `K` e `V`, che sono la *chiave* e il *valore* ad essa associata.

```java
Hashtable<String, String> postalCode = new Hashtable<String, String>();
numbers.put("Milan", "20100");
numbers.put("Rome", "00194");
```
## Iteratibilità

### `Iterator<E>`
`Iterator<E>` è un'interfaccia che permette di scandire e rimuovere oggetti da collezioni. È composta dai metodi:

- `boolean hasNext();` restituisce `True` se c'è un elemento successivo.
- `E next();` restituisce l'elemento successivo
- `void remove();` rimuove l'elemento corrente.

```java
Iterator<String> i = list.iterator();
while(i.hasNext()) {
    String s = i.next(); // Restituisce l'elemento successivo
    iterator.remove(); //Rimuove l'elemento corrente
}
```

### `Iterable<T>`
`Iterable<T>` è un'interfaccia che permette di implementare il for generalizzato. È composta dal metodo 

```java
Iterator<T> iterator();
```

È possibile usare il for generalizzato su oggetti che implementano tale interfaccia.

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

# Multithreading
In un programma ci interessa la possibilità di svolgere più task in *parallelo* a livello *logico*.

## Processo
Un **processo** è un programma eseguibile che ha un suo spazio in memoria.
A ogni processo corrisponde un programma.
La comunicazione tra processi è gestita dal sistema operativo.
Un processo può contenere più **thread**.

## Thread
Un **thread** è un attività logica sequenziale che condivide gli indirizzi e alcune variabili con altri thread dello stesso **processo**. Ha un suo contesto con variabili locali. È chiamato anche *lightweight process*.

## Classe `Thread`
Per creare un thread in Java si deve:
1. definire una classe che estenda la classe `Thread` e che implementi il metodo `public void run()`
    ```java
    class MyNewThread extends Thread {
        @Override
        public void run() {
            // ...
        }
    }
    ```
2. istanziare il thread
    ```java
    MyNewThread task = new MyNewThread();
    ```
3. far partire il thread col medoto `start()` che si occupa di chiamare `run()` all'interno del thread.
    ```java
    task.start()
    ```

## Interfaccia `Runnable`
Alternativamente si può eseguire un task in parallelo implementando l'interfaccia `Runnable` (che è comunque implementata da `Thread`). È sufficiente:
1. definire una classe che implementi l'interfaccia `Runnable` e che implementi il metodo `public void run()`
    ```java
    class MyNewTask implements Runnable {
        @Override
        public void run() {
            // ...
        }
    }
    ```
2. istanziare la classe
    ```java
    MyNewTask task = new MyNewTask();
    ```
3. creare il thread
    ```java
    Thread myThread = new Thread(task);
    ```
4. far partire il thread col medoto `start()`
    ```java
    task.start()
    ```
## Priorità
Ogni thread ha una priorità che va da `Min_Priority` a `Max_Priority`. La priorità serve allo scheduler per decidere quali thread eseguire.

## Atomicità e `synchronized`
Per evitare che più thread agiscano sulle stesse variabili condivise e si ottengano risultati inattesi (**interferenza**), si può definire una sequenza di azioni che viene eseguita senza interruzioni (**sequenza atomica**) mediante la keyword `syncronized`.

```java
class Jar {
    private int candies;

    syncronized public void take(int howMany) {
        candies += howMany;
    }
    syncronized public void add(int howMany) {
        candies -= howMany;
    }
}
```

In questo modo, quando un thread **A** esegue un metodo `syncronized` su un oggetto **X** un thread **B** che vuole chiamare un metodo su **X** deve aspettare che il metodo invocato da **A** termini.

Quando si cerca di eseguire un metodo `syncronized` Java applica un **lock intrinseco** all'oggetto (in questo caso, l'istanza della classe `Jar`), cioè:
- se l'oggetto è bloccato (*locked*), il task in esecuzione si sospende fino a quando la risorsa (instanza di `Jar`) viene sbloccata.
- se l'oggetto è sbloccato (cioè non ci sono *locks*), viene applicato un *lock* e viene eseguito il metodo. Al completamento del metodo, l'oggetto viene sbloccato nuovamente.

Se una un metodo non ha la keyword `syncronized`, non è mai bloccato.

Eventuali dati `final` possono essere letti da metodi non `syncronized`, dato che sono costanti.

Se si ha un metodo `static syncronized`, viene applicato alla *classe* un lock speciale, diverso da quello usato da un'istanza della classe, che controlla l'accesso ai campi *statici* della classe.

I costruttori non sono *mai* `syncronized`.

## Liveness
Poichè eseguire un applicazione con multithreading richiede il rispetto di alcuni limiti di tempo è importante evitare di usare troppi metodi syncronized, ma conviene usare *lock* più fini. Sono però da evitare situazioni di *deadlock*, *starvation* e *livelock*.

### Deadlock
Si ha un **deadlock** quando due thread si bloccano in attesa l'uno dell'altro.
> Esempio: *Ada e Bob devono salire in ascensore, ma ciascuno vuole lasciare entrare prima l'altro.*

```java
class Person {
    // ...

    public syncronized void waitFor(other) {
        other.getOnTheElevatorBefore(this);
    }

    public syncronized void getOnTheElevator(person) {
        // ...
    }
}

Person ada = new Person("Ada");
Person bob = new Person("Bob");

new Thread(
    new Runnable() {
        public void run() {
            ada.getOnTheElevatorBefore(bob);
        }
    }
).start();

new Thread(
    new Runnable() {
        public void run() {
            bob.getOnTheElevatorBefore(ada);
        }
    }
).start();
```

### Starvation
Si parla di **starvation** quando un thread non riesce a guadagnare accesso frequentemente ad una risorsa condivisa di cui ha bisogno, per esempio a causa di altri thread ingordi (*greedy*) che invocano metodi molto lunghi, di conseguenza termina in tempi lunghi. Lo *scheduler* inoltre dà priorità ai task greedy.

### Livelock
Si ha un **livelock** quando un thread genera una sequenza ciclica di operazioni inutili ai fini dell'effettivo avanzamento della computazione, per esempio creando più task di quanti ne riesca ad eseguire. A differenza del *deadlock* non aspetta lo sblocco di nessuna risorsa.

## Synchronized statements

Si può applicare un *lock* ad un oggetto all'interno di un metodo tramite `synchronized()`, che accetta come parametro l'oggetto da bloccare, e blocca l'oggetto fino al termine del blocco.

```java
class Person {
    private String name;

    public void changeName(String newName) {
        synchronized(this) {
            // ora l'istanza di `Person` che chiama
            // `changeName` è bloccata fino al
            // termine del blocco.
            name = newName;
        }
        // Qui il lock è stato rimosso.
        System.out.println("Name has been changed!");
    }
}
```

## Wait & Notify

A volte si vuole mandare in sospensione un task finchè una certa condizione non viene soddisfatta. Si può quindi chiamare la funzione `wait()` per sospendere il thread, che resterà in tale stato fino a che un altro thread chiama `notify()` (risveglia un task in *wait* a caso) o `notifyAll()` (risveglia tutti i task che sono in *wait*).

Conviene usare `notifyAll()`, anche se meno performante, per evitare di creare *deadlocks* o altre situazioni dove la *liveness* è a rischio.

```java
class Person {
    private boolean isHungry;
    private boolean isDinnerReady;
    synchronized public void eat() {
        while (isDinnerReady == false) {
            // Se la cena non è pronta, aspetto a mangiare
            // finchè non è pronta.
            wait();
        }
        isHungry = false;
    }
    synchronized public void prepareDinner() {
        cook();
        wait(50);
        isDinnerReady = true;
        notifyAll(); // o anche `notify();`
    }
}
```

Conviene aggiungere `throws InterruptedException` ai metodi che chiamano `wait()` al loro interno, per capire se un thread sospeso viene interrotto per qualche ragione all'interno del programma.

## Oggetti immutabili

Si creano senza *setter* (non si rendono gli attributi modificabili), tutti gli attributi sono `final` e `private`.
Non forniscono modi per modificare altri oggetti mutabili, nè i riferimenti ad altri oggetti mutabili (al massimo reference a copiedi essi). Si possono anche impedire *overrides* ai metodi.

## `java.util.concurrent`

È una libreria che offre alternative più efficienti per gestire i thread.

### Lock esplicito

Da [`java.util.concurrent.locks`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/package-summary.html) è possibile utilizzare un lock esplicito, dichiarando esplicitamente un *lock* e poi in un `try` statement provare ad attivare il *lock* e infine rilasciarlo nel `finally` statement.

```java
// Crea un lock
Lock lock = new Lock();

try {
    // Prova ad attivare il lock
    Boolean isLocked = lock.tryLock();
    // ...
} finally {
    // Disattiva il lock
    lock.unlock();
}
```

## Esecutori (*executors*)

Per distinguere tra il compito da eseguire (l'oggetto che implementa l'interfaccia `Runnable`) e il thread stesso (l'oggetto `Thread`), si possono usare gli esecutori, che sfruttano le *thread pools*, utili per evitare pesanti overhead in applicazioni con molti threads.

Anzichè creare un nuovo thread per un oggetto *runnable* `r`

```java
(new Thread(r)).start();
```

si può usare un esecutore `e`

```java
e.execute(r);
```

### Thread pools

Le **thread pools** limitano il tempo in esecuzione di ciascun thread.

Anzichè di creare un nuovo *thread* per ogni *task*, il nuovo task viene messo in una coda e quando c'è un *thread* della *thread pool* inattivo, tale task viene assegnato ad esso.

### Collezioni concorrenti

Molte collezioni o strutture dati in Java non sono `synchronized`, pertanto è necessario utilizzare apposite collezioni o rendere quelle esistenti `synchronized`:

```java
List list = Collections.synchronizedList(new ArrayList());
``` 

Altre collezioni degne di nota sono [BlockingQueue](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) e [ConcurrentHashMap](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html).

## Variabili Atomiche

Le variabili atomiche, dichiarate in [`java.util.atomic`](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html), sono un'implementazione più fine di alcuni tipi di *synchronized statements*, come per esempio un *counter*. Si specificano le singole variabili come `Atomic` e si può interagire con esse tramite appositi metodi.

```java
import java.util.concurrent.atomic.AtomicInteger;
class AtomicCounter {
    private AtomicInteger c = new AtomicInteger(0);

    public void increment() {
        // Sommo 1 a `c`
        c.incrementAndGet();
    }

    public void decrement() {
        // Sottraggo 1 a `c`
        c.decrementAndGet();
    }

    public int value() {
        return c.get();
    }
}
```

# Design Patterns

I *design patterns* sono una serie di principi che permettono di scrivere codice in maniera più efficiente grazie a soluzioni testate per i problemi più comuni.

Principi comuni ai design patterns sono:

- **astrazione**, in modo da essere condivisi tra progettisti con punti di vista differenti
- **bassa complessità**, per essere facilmente comprensibili
- **non domain-specific**, per essere utilizzati in ogni tipo di applicazione

I pattern si dividono in *tre* categorie:

- **creazionali** (riguardano il processo di creazioni degli oggetti)
- **strutturali** (riguardano la composizione di classi e oggetti)
- **comportamentali** (regolano le interazioni tra le oggetti e distribuiscono le responsabilità)

## Pattern creazionali

### Singleton

Il *singleton* serve per assicurarsi che esista una e una sola istanza di una classe.

> Usare infatti solo metodi statici non assicura che esista una sola instance di essa.

In un singleton quindi il *costruttore* è *protetto* o *privato*, e si accede all'unica copia dell'oggetto tramite un *metodo statico*.

L'implementazione più comune è la seguente:

```java
public class Singleton {
    // unica istanza
    private static Singleton instance = null;
    // costruttore invisibile
    private Singleton() {
        // ...
    }

    // uso questo metodo per accedere all'unica istanza
    // possibile della classe.
    public static Singleton instance() {
        // crea l'oggetto solo se non esiste
        if (instance == null) instance = new Singleton();
        // altrimenti
        return instance;
    }
    // ...
}
```

Nel caso di multithreading, conviene usare un metodo `synchronized` per creare l'istanza della classe, come `createInstance()` nell'esempio seguente:

```java
public class Singleton {
    // unica istanza
    private static Singleton instance = null;
    // costruttore invisibile
    private Singleton() {
        // ...
    }

    // crea l'oggetto solo se non esiste
    private synchronized static Singleton createInstance() { 
        if (instance == null) instance = new Singleton();
        // altrimenti
        return instance;
    }

    public static Singleton instance() {
        // chiama metodo synchronized solo se
        // l'oggetto non esiste
        if (instance == null) createInstance();
        // else
        return instance;
    }
    // altri metodi
}
```

Posso infine avere un singleton che si istanzia da solo nel seguente esempio, dove non è possibile accedere al suo costruttore:

```java
public class Singleton {
    // L'unica istanza viene già inizializzata
    final private static Singleton instance = new Singleton();

    // costruttore invisibile
    private Singleton() {
        // ...
    }

    // restituisce l'unica istanza esistente
    public static Singleton instance() {
        return instance
    }
    // ...
}
```

### Adapter

Un'*adapter* è una classe che fa da *tramite* tra un'applicazione e una libreria che deve essere adattata ad essa. 

> Attenzione, quado si parla in questo paragrafo di *interfaccia*, si intende l'insieme di metodi e attributi messi a disposizione da una classe, di solito una libreria di terze parti, non una ***interface*** di java

Ci sono tre attori in questa situazione:

- il **client**, cioè l'*applicazione* che interagisce con un *target* attraverso l'interfaccia messa a disposizione dall'*adapter*
- l'**adapter**, che collega l'interfaccia di una *adaptee* a quella del *client*
- l'**adaptee**, cioè ciò che viene "adattato", di solito una libreria di terze parti

Il vantaggio è che non bisogna modificare il codice del *client* per integrare una nuova libreria, ma basta modificare l'*adapter*.

Un esempio è quello di adattare un programma a diverse GUI (Graphical User Interface) di sistemi operativi diversi (OS): basta utilizzare un adapter per ogni libreria grafica messa a disposizione dai vari OS.

### Pattern Strategy

Una *Strategy* è un approccio utile a rendere un programma estendibile senza dover riscrivere molte classi, oppure quando è necessario scegliere a runtime tra algoritmi diversi, senza che l'utilizzatore sappia quale metodo sia stato scelto: è fondamentale che il tutto sia trasparente.

Un esempio per chiarire le idee è il seguente:

Si prenda un RPG (Role-Playing Game) dove il personaggio (una *sottoclasse* di `Character`) può usare armi (*sottoclassi* di `Weapon`) differenti. Vogliamo che a seconda del tipo di arma, cambi il modo con cui viene calcolato l'esito del combattimento:

```java
public abstract class Character {
    // L'arma è un oggetto di tipo `Weapon`
    Weapon weapon;

    // `fight()` è un azione che viene implementata dai
    // vari personaggi
    abstract void fight();
}
```

```java
public class Paladin extends Character {
    // implementa `fight()` a modo suo
    @Override
    void fight() {
        // ...
    }
}
```

```java
public class Wizard extends Character {
    // implementa `fight()` a modo suo
    @Override
    void fight() {
        // ...
    }
}
```

```java
public class Rogue extends Character {
    // implementa `fight()` a modo suo
    @Override
    void fight() {
        // ...
    }
}
```

Ovviamente utilizzare uno *switch* all'interno di ogni implementazione di *fight* è una pessima idea, perchè se dovessimo cambiarlo, ci toccherebbe cambiarlo per ogni sottoclasse di `Character` che lo implementa, quindi `Knight`, `Wizard` e `Rogue`.

La soluzione più intelligente è definire un interfaccia `Weapon` che viene implementata dai vari tipi di arma (es.: `Sword`, `Dagger`, `Spear`):

```java
interface Weapon {
    void useWeapon();
}
```

```java
class Sword implements {
    @Override
    void useWeapon() {
        // Slash with a sword!
    }
}
```

```java
class Dagger implements {
    @Override
    void useWeapon() {
        // Stab with a dagger!
    }
}
```

```java
class Spear implements {
    @Override
    void useWeapon() {
        // Throw a spear!
    }
}
```

È pratica abbastanza comunque usare un suffisso *Behaviour* o *Strategy* dopo il nome dell'interfaccia e delle classi che la implementano; in questo esempio avremmo potuto utilizzare `WeaponBehaviour` e `SwordBehaviour`, etc.

### Pattern Decorator

Un *Decorator* è un pattern che permette di aggiungere funzionalità a istanze di classi esistenti **senza** usare sottoclassi, particolarmente utile quindi a *runtime* e per evitare di avere un numero enorme di sottoclassi.

Si costruisce una classe (**Decorator**) che ingloba l'oggetto esistente (**Component**) passandolo come *parametro* del *costruttore* del decoratore.

Il *decorator* è dello **stesso** tipo del *component*, in modo da poter liberamente sostituire nel codice le occorrenze.

Un esempio in cui è spesso utilizzato un decorator è negli stream di dati, in cui si vuole aggiungere la possibilità di comprimere, decomprimere, crittografare, etc. uno stream di dati.
Conviene definire un "base" decorator sul quale poi si costruiscono gli altri.

#### Esempio
Analizziamo nel dettaglio un esempio, disponibile online [qui](https://refactoring.guru/design-patterns/decorator/java/example).

Questa è l'interfaccia (astratta) che vogliamo decorare. 
Quello che ci permette di fare è scrivere dei dati o leggerli.

```java
public interface DataSource {
    void writeData(String data);

    String readData();
}
```

Implementiamo l'interfaccia `DataSource` con la classe `FileDataSource`.

```java
public class FileDataSource implements DataSource {
    private String name;

    public FileDataSource(String name) {
        this.name = name;
    }

    @Override
    public void writeData(String data) {
        // scrive i dati in un file
    }

    @Override
    public String readData() {
        // restituisce una stringa dei dati letti
        // da un file
    }
}
```

Creiamo ora un *decoratore* per l'interfaccia `DataSource`: quello che fa è semplicemente identico a quello che faceva l'interfaccia, dobbiamo ancora creare dei decoratori che aggiungono funzionalità; questo ci serve solo come base.

> In Inglese "Wrapper" è "Colui che contiene", mentre "Wrappee" è "colui che è contenuto". Non è un [*typo*](https://www.merriam-webster.com/dictionary/typo).

```java
public class DataSourceDecorator implements DataSource {
    private DataSource wrappee;

    // Copia la reference alla classe originale in `wrappee`
    DataSourceDecorator(DataSource source) {
        this.wrappee = source;
    }

    // Scrive nel file
    @Override
    public void writeData(String data) {
        wrappee.writeData(data);
    }

    // Legge nel file
    @Override
    public String readData() {
        return wrappee.readData();
    }
}
```

Creaiamo ora un decoratore che aggiunga la possibilità di codificare/decodificare il file, grazie ai due metodi `encode()` e `decode()`.

```java
public class EncryptionDecorator extends DataSourceDecorator {
    // Il costruttore fa quello che faceva
    // il decoratore "base"
    public EncryptionDecorator(DataSource source) {
        super(source);
    }

    // Prima CODIFICA, poi SCRIVE i dati nel file
    @Override
    public void writeData(String data) {
        super.writeData(encode(data));
    }

    // Prima LEGGE i dati nel file, poi li DECODIFICA
    @Override
    public String readData() {
        return decode(super.readData());
    }

    private String encode(String data) {
        // Restituisce la versione codificata di `data`
    }

    private String decode(String data) {
        // Restituiisce la versione decodificata di `data`
    }
}
```

Creaiamo ora anche un decoratore per comprimere il nostro filestream, grazie ai metodi `compress()` e `decompress()`:

```java
public class CompressionDecorator extends DataSourceDecorator {

    // Il costruttore fa quello che faceva
    // il decoratore "base"
    public CompressionDecorator(DataSource source) {
        super(source);
    }

    // Prima COMPRIME i dati, poi li scrive nel file.
    @Override
    public void writeData(String data) {
        super.writeData(compress(data));
    }

    // Prima LEGGE i dati dal file, poi li DECOMPRIME
    @Override
    public String readData() {
        return decompress(super.readData());
    }

    private String compress(String stringData) {
        // Restituisce i dati compressi
    }

    private String decompress(String stringData) {
        // Restituisce i dati decompressi
    }
}
```

Alla fine potremo usare i decoratori per creare un nuovo file, codificarlo e comprimerlo senza sforzi:

```java
public class Demo {
    // Main
    public static void main(String[] args) {
        // Dati che devo scrivere
        String superSecretData = "SuperSecretData";
        // Creo il file in cui scriverò i dati
        DataSourceDecorator encoded = 
            new CompressionDecorator(
                new EncryptionDecorator(
                    new FileDataSource("out/OutputDemo.txt")
                )
            );
        // Scrivo i dati
        encoded.writeData(superSecretData);
        // I dati che scrivo sono automaticamente
        // codificati e compressi dal decoratore.
    }
}
```

## Pattern Strutturali

🚧WIP 🚧