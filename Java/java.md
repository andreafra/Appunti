Java
====

Java è un linguaggio di programmazione che è compilato in *bytecode* eseguibile su ogni architettura che abbia una propria JVM (Java Virtual Machine).

È un linguaggio orientato agli oggetti, cioè consiste di un insieme di classi che contengono **attributi** (variabili) e **metodi** (funzioni). Lo scopo della struttura a classi è limitare tramite opportuni modificatori la **visibilità** delle componenti di un oggetto, al fine di rendere più agevole e modulare la modifica del codice.

Java è un linguaggio *statico*, cioè ogni elemento deve avere un *tipo* esplicito.

## Tipi Primitivi (*primitives*)

Java ha i seguenti tipi primitivi:

- `byte` (8 bit)
- `short` (16 bit)
- `int` (32 bit)
- `long` (64 bit)
- `float` (32 bit)
- `double` (64 bit)
- `boolean` (*vero* o *falso*)
- `char` (16 bit)

Ulteriori tipi possono essere definiti mediante [classi](#classi-classes) o [enum](#enum).

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

### Getter e Setter

Spesso è poco conveniente accedere ad un attributo direttamente, per esempio mediante

```java
dog.timesPetted; // => 10
```

perchè `timesPetted` potrebbe essere sovrascritto. Conviene quindi usare un metodo per ottenere il valore di un attributo, comunemente chiamato *getter*, cioè che contiene la parola *get* (è puramente una formalità/convenzione):

```java
class Dog {
    int timesPetted = 10;
    // ...
    // GETTER
    int getTimesPetted() {
        return timesPetted; // => 10
    }
}
```

Allo stesso modo, possiamo definire un metodo per modificare i valori di un attributo, chiamato *setter*, cioè che contiene la parola *set*:

```java
class Dog {
    int timesPetted = 10;
    // ...
    // SETTER
    void setTimesPetted(int n) {
        if(n > 0) {
            timesPetted = n;
        }
    }
}
```

In questo modo possiamo anche accertarci che vengano rispettate delle convenzioni, come per esempio che `timesPetted` sia mantenuto sempre maggiore di zero.

## Istanze (*instances*) e Riferimenti (*references*)
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

## Tipo statico e dinamico
In Java il tipo che si vede scritto nel codice è definito *statico*:

```java
int number = 5; // Tipo Statico: `int`
String greeting = "Hi!"; // Tipo Statico: `String`
```

Il tipo dinamico è quello della reference di un oggetto al momento in cui è stato instanziato:

```java
Book book = new Book()
// Tipo Statico: `Book` (da `Book book`)
// Tipo Dinamico: `Book` (da `new Book()`)
```

Per le proprietà delle sottoclassi, posso assegnare a una variabile del tipo di una superclasse (`Book`) un'istanza di una sua sottoclasse (`ComicBook`):

```java
Book book = new ComicBook()
// Tipo Statico: `Book` (da `Book book`)
// Tipo Dinamico: `ComicBook` (da `new ComicBook`)
```

Attenzione: non posso accedere agli eventuali metodi e attributi aggiuntivi di `ComicBook` dalla variabile `Book`, perchè il tipo `Book` non è a conoscenza delle estensioni aggiunte dalle sue sottoclassi.

```java
class Book {
    String title;
}

class ComicBook extends Book {
    int episode;
    Image[] pictures;
}
```

```java
Book book = new ComicBook();
book.title; // => OK
book.episode; // => ERROR
```

**NON** si può invece assegnare a una variabile di tipo sottoclasse un'istanza della sopraclasse:

```java
ComicBook comic = new ComicBook(); // OK
ComicBook book = new Book(); // ERROR
```

## Visibilità (*visibility*)
In Java si può decidere la visibilità (scope) di classi, attributi e metodi mediante i **modificatori di visibilità** `public`, `protected`, `private`, che si inseriscono all'inizio di una dichiarazione.

- `public` Ovunque
- `protected` Stesso [*package*](#costruttori-constructors) e *sottoclassi* della classe in questione
- vuoto (friendly) Stesso [*package*](#costruttori-constructors)
- `private` Stessa [classe](#classi-classes)

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

# Enum

Gli [enum](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html) (da *enumerator*) sono un tipo particolare di dati che assegna a una variabile un insieme di costanti.

Un enum viene istanziato a compile-time una sola volta, in modo simile ad un [singleton](#singleton).

```java
public enum Compass {
    NORTH, SOUTH, EAST, WEST
}
```

Si possono poi usare le costanti di un *enum* per esempio in uno *switch case*:

```java
void setDirection(Compass c) {
    switch(c) {
        case NORTH:
            // go north
            break;
        case SOUTH:
            // go south
            break;
        case EAST:
            // go east
            break;
        case WEST:
            // go west
            break;
        default:
            // stay
            break;
    }
}
```

In Java gli *enum* sono più potenti che in altri linguaggi: si possono infatti dichiarare metodi e attributi, proprio come in una classe, ma **solo dopo** aver definito le costanti.

Il compilatore aggiunge inoltre dei metodi come `values()` che restituisce un [array](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html) con tutte le costanti dell'*enum*.

Un *enum* può avere un *costruttore*, ma **deve** essere *privato* o *non accessibile* al di fuori del package.

```java
public enum Planet {
    // Costanti
    // a compile time, il compiler crea attraverso
    // il costruttore le costanti a cui viene 
    // associata la rispettiva massa e raggio.
    // NomeCostante (mass, radius)
    MERCURY (3.303e+23, 2.4397e6),
    VENUS   (4.869e+24, 6.0518e6),
    EARTH   (5.976e+24, 6.37814e6),
    MARS    (6.421e+23, 3.3972e6),
    JUPITER (1.9e+27,   7.1492e7),
    SATURN  (5.688e+26, 6.0268e7),
    URANUS  (8.686e+25, 2.5559e7),
    NEPTUNE (1.024e+26, 2.4746e7);

    // Attributi (costanti)
    private final double mass;   // in kilograms
    private final double radius; // in meters

    // costante (di gravitazione universale)
    public static final double G = 6.67300E-11;

    // Metodi
    // Construttore
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    // Getters per massa e raggio
    private double mass() { return mass; }
    private double radius() { return radius; }
    
    // Altri metodi
    double surfaceGravity() {
        return G * mass / (radius * radius);
    }
    double surfaceWeight(double otherMass) {
        return otherMass * surfaceGravity();
    }  
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
interface Flying {
    int LEGS = 2; // public, static, final
    void fly(); // public, abstract
}
```

Un'interfaccia può estendere altre interfacce mediante la keyword `extends` come per le classi.

```java
interface Flying extends /* <altre interfacce> */ {
    // ...
}
```

Una classe può implementare un'interfaccia mediante la keyword `implements`.

```java
class Bird extends Animal implements Flying {
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
[`Iterator<E>`](http://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html) è un'interfaccia che permette di scandire e rimuovere oggetti da collezioni. È composta dai metodi:

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

#### Implementare `Iterator<E>`

Per creare un proprio *iteratore*, basta implementare la omonima interfaccia `Iterator<E>` e implementare i tre metodi visti sopra:

```java
class MyIterator implements Iterator<E> {
    public boolean hasNext() {
        // deve restituire `True` se e solo se
        // esiste il prossimo elemento
    }

    public E next() throws NoSuchElementException {
        // restituisce il prossimo elemento, altrimenti lancia l'eccezione
    }

    public void remove() throws UnsupportedOperationException {
        // cancella l'ultimo elemento restituito
        // da `next()`
    }
}

```
### `Iterable<T>`
[`Iterable<T>`](http://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html) è un'interfaccia che permette di implementare il for generalizzato. È composta dal metodo 

```java
Iterator<T> iterator();
```

È possibile usare il for generalizzato (o il metodo `forEach()`) su oggetti che implementano tale interfaccia.

#### Implementare `Iterable<T>`

È possibile creare una propria collezione implementando l'interfaccia `Iterable<T>`

```java
class MyCollectio  implements Iterable<T> {
    public Iterator<T> iterator() {
        // Restituisce l'iteratore per scandire
        // la collezione
    }
}
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

#### Principio di Sostituzione di Liskov (LSP)

> I tipi derivati devono essere *totalmente* sostituibili ai rispettivi tipi base.

Alternativamente

> "Se *q(x)* è una proprietà che si può dimostrare essere valida per oggetti *x* di tipo T, allora *q(y)* deve essere valida per oggetti *y* di tipo *S* dove *S* è un sottotipo di *T*."

Se ho una classe A e una classe B che estende A, devo poter chiamare i metodi di A da un'istanza di B, accettando gli stessi tipi in *input* e producendo un *output* dello stesso tipo e rispettando eventuali condizioni (es.: l'input è un `int` maggiore di 0).

Non deve mai ridurre le proprietà di un oggetto, può invece ampliarlo.

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

### Factory Method

È uno dei pattern più usati, che disaccoppia la il codice di una classe da quello che la crea.

Per ogni tipo di *oggetto da produrre* (`ConcreteProduct`) si definisce una classe (`ConcreteFactory`) che contiene il metodo statico `factory()` che produce oggetti di quel tipo. Ogni `ConcreteProduct` estende una classe *astratta* `Product`.

```java
// Definisco le classi
class Pizza {
    // ...
}
class PizzaMarinara extends Pizza {
    // ...
}

// Definisco i Factory che contengono
// i factory method
class PizzaFactory {
    public Pizza factory();
}

public class MarinaraFactory implements PizzaFactory {
    public Pizza factory() {
        return new PizzaMarinara();
    }
}

public class PizzaOrder {
    private PizzaFactory pizzaFactory;
    // Il metodo che userò per creare una pizza, 
    // a cui passo la classe che contiene il
    // factory method
    public void PizzaOrder(PizzaFactory c) {
        pizzaFactory = c;
    }
    public Pizza cook() {
        Pizza pizza = pizzaFactory.factory();
        // Fai altre operazioni con `pizza`
        return pizza;
    }
    // ...
}
```

Posso poi chiamare

```java
// Creo l'instanza di PizzaOrder per avere una
// marinara, passando l'opportuno `Factory`
PizzaOrder marinaraOrder = new PizzaOrder(new MarinaraFactory());
// Faccio operazioni sulla nuova istanza di pizza.
Pizza myFreshPizza = marinaraOrder.cook();
```

### Abstract Factory

Una *abstract factory* è una variante in cui la  factory è un'interfaccia astratta (`AbstractFactory`) e definisce i metodi che devono essere implementati dalle classi `ConcreteFactory`. Inoltre l'abstract factory può creare famiglie di prodotti anziché un solo prodotto. I prodotti dello stesso tipo possono anch'essi implementare un'interfaccia astratta.

Le singole `ConcreteFactory` implementano quindi più metodi factory:

```java
// Definisco un'interfaccia che specifica attributi
// e metodi per le auto che la implementano
interface Car {
    // ...
}
class CityCar implements Car {
    // Avrà delle proprie caratteristiche
    // particolari
}
class SUV implements Car {
    // Avrà caratteristiche diverse
    // da una city car
}

// Definisco una classe ASTRATTA che contiene
// i metodi per i tipi di auto da produrre
interface CarFactory {
    public abstract CityCar makeCityCar();
    public abstract SUV makeSUV();
}

// Creo delle classi CONCRETE che implementano
// la costruzione dei vari modelli di auto dalla
// classe ASTRATTA
class BMWFactory implements CarFactory {
    @Override
    public CityCar makeCityCar() {
        // ...
    };
    @Override
    public SUV makeSUV() {
        // ...
    };
}
class VolkswagenFactory implements CarFactory {
    @Override
    public CityCar makeCityCar() {
        // ...
    };
    @Override
    public SUV makeSUV() {
        // ...
    };
}

class CarDealer {
    CarFactory factory;
    Car car;
    public CarDealer(factory) {
        this.factory = factory;
        this.car = car;
    }

    // Mi restituisce una
    public Car buyCar(boolean isCityCar) {
        if (isCityCar) {
            return new factory.makeCityCar();
        } else {
            return new factory.makeSUV();
        }
    }
}
```

Posso quindi chiamare

```java
CarDealer cd1 = new CarDealer(VolkswagenFactory);
Car myNewCar = cd1.buyCar(true); // => VW CityCar
Car myNewCar = cd1.buyCar(false); // => VW SUV

CarDealer cd2 = new CarDealer(VolkswagenFactory);
Car myNewCar = cd2.buyCar(true); // => BMW CityCar
Car myNewCar = cd2.buyCar(false); // => BMW SUV
```

## Pattern Strutturali

### Adapter

Un'*adapter* è una classe che fa da *tramite* tra un'applicazione e una libreria che deve essere adattata ad essa. 

> Attenzione, quado si parla in questi paragrafi di *interfaccia*, si intende l'insieme di metodi e attributi messi a disposizione da una classe, di solito una libreria di terze parti, non una ***interface*** di java

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

### Facade

Una *facade* ("facciata", di un edificio) è un pattern utile a nascondere la complessità di un insieme di classi molto legate fra loro presentando un'interfaccia semplificata all'utilizzatore.

### Proxy

Un *proxy* è un pattern che si interpone tra un oggetto particolarmente grande o lento, per esempio su un server remoto, di cui copia l'interfaccia (cioè metodi e attributi).

Un proxy può quindi snellire il carico all'oggetto per esempio facendo *pre-processing*, usando una *cache*, stabilendo priorità e code, etc.

### Pattern State

Il *pattern state* permette di estendere facilmente il comportamento di una classe (*context*) in base al suo stato (*state*). È particolarmente conveniente al posto di uno switch (che è limitato) e, similmente al *pattern strategy*, ricorre a un'**interfaccia** che viene implementata da classi che rappresentano i vari stati.

Di solito, lo stato è salvato in un parametro dello stesso tipo dell'interfaccia.

```java
public class Writer {
    WriteState state;

    void writeBook() {
        state.write()
    }

    void sendBookToPublisher() {
        state.send()
    }
}

interface State {
    void write();
    void send();
}

class HandwriteState implements State {
    void write() {
        // Scrivi libro a mano
    }
    void send() {
        // Manda il libro tramite posta
    }
}

class TypewriteState implements State {
    void write() {
        // Scrivi libro con macchina per scrivere
    }
    void send() {
        // Manda il libro tramite fax
    }
}

class DigitalTypewriteState implements State {
    void write() {
        // Scrivi libro al pc
    }
    void send() {
        // Manda il libro via email
    }
}
```
Nell'esempio, se lo stato fosse un'istanza di `DigitalTypewriteState` e usassi il metodo della classe `Writer` `writeBook()`, scriverei il libro al PC. Non devo fare nessuna scelta in `Writer` su quale implementazione di `State` utilizzare,  se non settare correttamente la variabile `state`.


Rispetto al *pattern strategy*, in cui ho un insieme di singoli algoritmi intercambiabili, ma che non dipendono da uno stato, nel *pattern state* ho un insieme di comportamenti che dipendono dallo stato corrente.

### Observer/Observable (Publish/Subscribe)

Molto usati da librerie grafiche e in ambienti distribuiti, gli *observer* permettono ad alcuni oggetti di essere "notificati" quando accade un particolare evento, per esempio quando si fa click su un bottone.

Si definiscono di solito due ruoli, *Subject* ([`Observable`](http://docs.oracle.com/javase/8/docs/api/java/util/Observable.html)) e *Observer* ([`Observer`](http://docs.oracle.com/javase/8/docs/api/java/util/Observer.html)):

- `Subject` è la classe astratta che registra o rimuove gli *observer*, mediante i seguenti metodi:
    - `attach(Observer obs)` aggiunge un nuovo osservatore `obs`
    - `detach(Observer obs)` rimuove l'osservatore obs
    - `notify()` manda una notifica a tutti gli osservatori che il *subject* ha cambiato stato
- `Observer` è un'interfaccia con il seguente metodo:
    - `update()` viene chiamato ogni volta che il *subject* cambia stato, cioè quando riceve una notifica.

### Flyweight Pattern

Quando si potrebbe utilizzare molti oggetti identici e immutabili, può convenire creare un oggetto immutabile (*flyweight*), che rappresenta tutti gli oggetti identici.

Anzichè creare una copia di un oggetto quando serve, si assegna semplicemente una reference al flyweight, che viene salvata in una tabella, e rimossa quando non serve più (solitamente una [WeakHashMap](http://docs.oracle.com/javase/8/docs/api/java/util/WeakHashMap.html), che rimuove la entry quando la chiave non sono è più in uso).

[Questo pattern](https://en.wikipedia.org/wiki/Flyweight_pattern) è conveniente quando il numero di oggetti identici è **molto** elevato.

Il vantaggio è il risparmio di memoria, e che non si perde tempo ad inizializzare oggetti duplicati.

Un esempio potrebbe essere un sistema per gestire le ordinazioni in un bar enorme:
- Ad ogni cliente si assegna la rispettiva ordinazione (inserendo l'ordine nella tabella)
- Si aggiunge a una coda (queue) l'ordinazione.
- Ogni ordinazione è una reference ad un oggetto immutabile (il nostro *flyweight*) che contiene le informazioni necessarie: il nome, la dimensione, gli ingredienti...
- Quando l'ordinazione è servita, si rimuove dalla coda e la si serve al cliente.

I flyweight sono per esempio usati anche nei word processor (come Office Word) per evitare di creare un oggetto per lettera: lettere (o meglio, glifi) uguali sono in realtà reference a un *flyweight*.

## Pattern Architetturali

### Client-Server

Il [modello Client-Server](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) è molto utilizzato dalle applicazioni web come i siti Internet. Si basa su una struttura centrale (*server*) che gestisce la maggior parte della logica e dei dati, e gestisce le interazioni che riceve dagli utenti (*clients*).

![Client-Server](https://upload.wikimedia.org/wikipedia/commons/f/fb/Server-based-network.svg)

### Peer-to-Peer (P2P)

Il [modello Peer-to-Peer](https://en.wikipedia.org/wiki/Peer-to-peer) è molto usato per la condivisione di file tra più macchine, come per i client Torrent.

![P2P](https://upload.wikimedia.org/wikipedia/commons/3/3f/P2P-network.svg)

### Model-View-Controller MVC

MVC è un pattern molto utilizzato per la progettazione di *interfacce utente grafiche* (GUI), in cui si divide la struttura del programma in tre classi di componenti:

- **Model** fornisce i metodi per l'accesso ai dati

- **View** crea e gestisce l'interfaccia utente a partire dai dati accessibili dal *Model*

- **Controller** contiene la logica per gestire le interazioni dell'utente, generalmente riceve notifiche dalla *View* e poi modifica quest'ultima o il *Model*

![MVC](https://upload.wikimedia.org/wikipedia/commons/a/a0/MVC-Process.svg)

# Progettazione

## Principi di Progettazione

### Principio Open-Closed

Vogliamo sfruttare l'ereditarietà per poter cambiare il comportamento di una classe senza modificarla: possiamo però *estendere* la classe solo se possiamo *sostituire* le componenti della *sopraclasse* con delle nuove che rispettino le regole esistenti (*tipo*, *vincoli* su parametri e return).

Deve quindi valere il [principio di sostituizione di Liskov](#Principio-di-Sostituzione-di-Liskov-LSP).

In molte situazioni, è meglio **comporre** (usare la [composizione di UML](https://en.wikipedia.org/wiki/Object_composition#UML_notation)), perché anziché modificare un metodo violando il LSP, è meglio aggiungere nuovi metodi.

### Principio dell'Inversione della Dipendenza

Il **DIP** (Depency Inversion Principle) è un principio in cui una classe deve dipendere da altre classi/interfacce *astratte*, anziché da altre classi concrete.

Ogni volta che ho una *classe* `C` che potrebbe venire estesa in futuro, conviene definirla come sottoclasse di un'*interfaccia astratta* `A`.

Se possibile, anziché riferirsi ad oggetti di tipo `C` (classe concreta), è meglio riferirsi ad oggetti di tipo *statico* `A` (classe/interfaccia astratta). Il vantaggio è una maggiore flessibilità del codice, in cui posso sostituire ad esempio la classe concreta `C` con altre sottoclassi/implementazioni di `A`.

## Valutazione della qualità di un progetto

Un progetto si può valutare secondo diversi indici:

- **correttezza funzionale**, cioè se il progetto *funziona*
- **efficienza**
- **requisiti strutturali**, cioè quanto è facile da *modificare*

Per valutare i *requisiti strutturali*, si possono osservare:

- accoppiamento
- coesione
- [principio open-closed](#Principio-Open-Closed)

### Accoppiamento (*Coupling*)

L'*accoppiamento* è il grado di interconnessione fra classi. Se è molto elevato, vuol dire che è difficile modificare le singole classi, perchè c'è un'alta dipendenza fra esse.

Bisognerebbe cercare di avere un accoppiamento *minimo*.

#### Interaction Coupling
Si ha quando un metodo di una classe ne chiama altri di altre classi.

**Da evitare:** *modificare direttamente* attributi di altre classi.

**Accettabile:** i metodi comunicano direttamente tramite i propri parametri, cioè non accedo agli attributi dell'altra classe.

#### Component Coupling

Una classe `A` è accoppiata ad un'altra classe `B` se ha:

- attributi di tipo `B`
- parametri di tipo `B`
- metodi con variabili locali di tipo `B`

Quando `A` è accoppiata a `C`, è accoppiata automaticamente anche alle sue sottoclassi.
Se c'è Component Coupling, c'è anche Interaction Coupling di solito.

#### Inheritance Coupling

Si ha quando una classe `A` è sottoclasse di `B`.

**Da evitare:** quando una sottoclasse cambia la segnatura (ordine/quantità dei parametri) di un metodo ereditato. (*Impossibile in Java*)

È accettabile se la segnatura di un metodo di cui viene fatto override non cambia.

È consigliabile avere una sottoclasse che aggiunge solo metodi e attributi, ma non fa override dei metodi ereditati.

### Coesione (*Cohesion*)

La *coesione* riguarda gli elementi all'interno di uno stesso modulo, a differenza dell'accoppiamento, che riguarda le connessioni tra le classi.

Una alta coesione (cioè elementi che sono fortemente correlati) porta ad un basso accoppiamento (il che è positivo).

#### Method Coesion

Quando il metodo implementa una funzione singola e ben definita si ha la massima coesione.

Come regola generale, se si riesce a spiegare cosa fa il metodo con una sola frase, si è ottenuta una buona coesione.

#### Class Coesion

Una classe dovrebbe rappresentare un solo concetto e tutte le proprietà dovrebbero contribuire alla sua rappresentazione.

Conviene evitare di inserire concetti diversi nella stessa classe.

Se ci sono metodi che accedono rispettivamente ad attributi disgiunti, è probabile che ci sia una bassa coesione: si potrebbero estrarre delle classi che contengono gruppi di metodi e attributi che interagiscono fra loro.

#### Inheritance Coesion

La coesione è maggiore se si sfrutta la gerarchia delle classi per gestire la generalizzazione (o la specializzazione) dei componenti (cioè se c'è una struttura ragionata dell'ereditarietà delle classi).


## Metriche del Software

È possibile definire delle metriche per valutare un software:

- **Weighted Methods per Class** (WMC)
    - è il numero dei metodi pesati per la loro complessità
    - conviene che sia basso per la maggior parte delle classi
- **Depth of Inheritance Tree** (DIT)
    - di solito è vicino alla radice (0), il massimo è 10
    - si preferisce quindi la comprensibilità alla riusabilità
- **Number of Children** (NOC)
    - è il numero di sottoclassi
    - di solito è basso, spesso è 0, cioè viene sfruttata poco l'ereditarietà
- **Coupling Between Classes** (CBC)
    - di solito è 0, cioè le classi non sono accoppiate
    - gli oggetti di interfaccia hanno un CBC maggiore
- **Response For a Class** (RFC)
    - è il numero totale dei metodi che possono essere invocati da un oggetto della classe
    - di solito è basso
    - gli oggetti di interfaccia hanno un RFC più alto
- **Lack of Cohesion Methods** (LCOM)
    - misura la vicinanza tra i metodi di una classe
    - non è particolarmente utile per predire difetti del codice

Di solito queste metriche vengono calcolate da strumenti appositi.

## Sintomi di un cattivo progetto

Un progetto fatto male è solitamente:

- **Rigido:** è difficile da modificare
- **Fragile:** si *rompe* dopo una modifica
- **Immobile:** è difficile riutilizzare il codice
- **Viscoso:** è più facile prendere scorciatoie (o *hack*) piuttosto che fare uso dei metodi esistenti

## Buone pratiche

### Metodi
- Preferire una dichiarazione di un metodo/attributo *privata* (o *friendly*/*protected*) a una pubblica se non c'è un motivo particolare.

- Meglio definire solo il [*getter*](#getter-e-setter), e il *setter* solo quando serve.

- Non è un obbligo fornire *getter* o *setter* per ogni attributo della classe. Conviene implementare solo quelli che servono.

- Conviene mantenere i metodi con un numero di parametri basso.

- Convine evitare una serie di parametri dello stesso tipo, per esempio

    ```java
    void drawCircle(int x, int y, int w, int h);
    ```
    
    e invece *raccogliere* in delle classi ausiliarie i valori:

    ```java
    // Definite due classi Point e Size...
    Point p1 = new Point(x, y);
    Size s1 = new Size(w, h);
    
    // ...e la seguente funzione...
    // void drawCircle(Point p, Size s);

    // ...posso disegnare un cerchio!
    drawCircle(p1, s1);
    ```
### Anti-pattern

Un *anti-pattern* è una soluzione usata spesso ma riconosciuta come una pratica da evitare.

#### Classe Blob

Una classe enorme che contiene tutta la logica (tipico della programmazione in **C**).

#### Codice duplicato

Il principio **D.R.Y.** (Don't Repeat Yourself) è efficace per evitare di ripetere lo stesso codice per esempio all'interno di più metodi: conviene creare quindi un metodo ausiliario che incapsula il codice ripetuto.

#### Metodi lunghi

Conviene spezzare il codice di un metodo troppo lungo in più metodi per avere una maggiore leggibilità e modularità. Di solito un metodo è sulle 20 righe, nella maggior parte dei casi inferiore ai 40.

#### Mischiare livelli di astrazione

Per esempio, avere una sequenza di una subroutine in un metodo che chiama solo altri metodi di livello d'astrazione superiore.

Per esempio, il seguente metodo specifica inutilmente i passaggi della colazione:

```java
void morningRoutine() {
    wakeUp();
    shower();
    getBread(); // livello d'astrazione inferiore:
    toastBread(); // si potrebbe inglobare in un
    getJam(); // metodo `haveBreakfast()`
    // ...
    dressUp();
}
```

È meglio riscriverlo come:

```java
void morningRoutine() {
    wakeUp();
    shower();
    haveBreakfast();
    // ...
    dressUp();
}
```

#### Mischiare contesti diversi

È da evitare che un metodo faccia operazioni diverse che riguardano ambiti diversi:

```java
boolean isHouseClean() {
    if (bathroom.isClean())
        if (kitchen.sink.isClean())
            if (dirtyClothes.hasBeenWashed())
                return true;
            else
                washClothes(dirtyClothes);
    return false
}
```

È più conveniente riassumere le operazioni in dei metodi ausiliari, in modo da poter eventualmente modificare meglio il codice in futuro:

```java
boolean isHouseClean() {
    return bathroom.isClean() &&
           kitchen.isClean() &&
           laundry.isDone()
}
```

#### Dati e metodi

Se un metodo in una classe `A` usa i dati di una classe `B`, conviene spostare il metodo nella classe `B`.

#### Switch case e pattern

Usare uno swift in certe situazioni rende il codice più difficile da modificare, conviene invece usare un pattern [strategy](#pattern-strategy) o [state](#pattern-state) enum o l'ereditarietà.

#### Blocchi di dati

Conviene raggruppare gruppi di dati affini con delle classi.

## Pattern Stilistici

I *pattern stilistici* sono delle convenzioni per rendere il codice più gradevole da leggere.

### Commenti

I commenti in Java (riga singola: `// ...`, righe multiple: `/* ... */`) sono utili per chiarire i passaggi più oscuri del codice. Sono da evitare i commenti che *ripetono* o *contraddicono* il codice.

Un commento dovrebbe indicare cosa fa il codice in un certo *contesto*, non sottolineare l'ovvio.
Ovviamente, se il codice si capisce senza commenti è ancora meglio.

```java
// Commento inutile:
i = i + 1; // somma 1

// Commento utile:
i = i + 1; // incrementa `cardCounter`

// Miglior implementazione:
cardCounter++;
```

Generalmente, conviene commentare ogni dichiarazione di un metodo spiegando brevemente cosa fa (se è già auto-esplicativo è meglio) o se ha dei requisiti particolari.

### Convenzioni sui nomi

| Entità | Stile | Commento | 
|:-------|:-|:-|
| Classi | `UpperCamelCase` | La prima lettera è sempre *maiuscola*, ogni parola che segue ha la *prima* lettera maiuscola. |
| Interfacce | `UpperCamelCase` | |
| Attributi | `lowerCamelCase` | La prima lettera è sempre *minuscola*, ogni parola che segue ha la *prima* lettera maiuscola. |
| Metodi | `lowerCamelCase` | |
| Costanti | `UPPERCASE` | Le costanti sono sempre in maiuscolo. |

Inoltre:

- le classi hanno sempre nomi singolari, es.: `Stack`, non `Stacks`
- i metodi `void` dovrebbero avere come nome il verbo di ciò che fanno.

    Es.: `openFile()`, `sendNotification()`
- i metodi `boolean` dovrebbero avere `is` + il participio passato (present perfect) di ciò che rappresentano.

    Es.: `isOpen()`, `hasFinished()`

    Fanno eccezione alcuni metodi come `contains()`. Generalmente se letti dovrebbero suonare come delle domande a cui si può rispondere con "sì" o "no".
- i metodi non-`void`, cioè che restituiscono qualcosa, dovrebbero avere il nome di ciò che restituiscono.

    Es.: `sizeOfScreen()`, `getStudent()`

# Programmazione funzionale

È uno stile di programmazione che si basa sul determinare un *output* a partire da degli *input* che vengono passati ad una catena di **funzioni** determinate.

Concetti nuovi sono:

- **First-Class Functions:** le funzioni sono valori che si possono assegnare a variabili, restituire (*return*) o passare come *parametro*.

- **Funzioni Anonime:** le funzioni sono usate come parametro senza dover specificarne il nome.

Java non è un linguaggio funzionale puro ([Haskell](https://www.haskell.org/), Lisp, Erlang, Clojure...), quindi possiede solo alcune caratteristiche di questi linguaggi.

## Espressioni Lambda

### Esempio: `forEach()`

Il metodo `forEach` di un oggetto che implementa l'interfaccia `Iterable` supporta la programmazione funzione, in particolare accetta come parametro una funzione anonima:

```java
List<String> fruits = Arrays.asList("Apple", "Banana", "Coconut");
fruits.forEach(String fruit -> {
    fruit.slice();
    // ...
})
```

Quello che accade è che ogni elemento della lista `fruits` viene passato come parametro `fruit` alla funzione anonima `(parametri) -> {blocco di codice}`, e poi viene eseguito il blocco di codice che segue nel cui *scope* vale la variabile `fruit`.

Nel caso di un singolo comando dopo la freccia `->`, si possono omettere le parentesi graffe `{ }`, mentre nel caso di un singolo parametro si possono omettere quelle tonde `()`.

L'esempio sopra senza utilizzare la programmazione funzionale potrebbe essere:

```java
List<String> fruits = Arrays.asList("Apple", "Banana", "Coconut");
// Uso il for-in di Java
for(String fruit : fruits) {
    fruit.slice();
    // ...
}
```

### Sintassi

```java
myVar.myMethod((param1, param2) -> {
    // ...
})
```

In Java, nelle *lambda functions*, il **tipo** dei parametri può essere [inferito](http://www.treccani.it/enciclopedia/tag/inferire/) dal compilatore. Attenzione: o si specifica il tipo per ogni parametro, o non lo si specifica per nessuno.

È importante che le funzioni passate come parametro siano:

- *non-interfering*, cioè che non modifichino l'input. Si può volendo specificare il tipo del parametro come `final` a questo scopo.
- *stateless*, cioè l'output **non** deve dipendere da fattori al di fuori della funzione, per esempio una variabile globale

### Interfacce funzionali

In Java le funzioni *lambda* rappresentano l'istanza di un'interfaccia *funzionale*, cioè un interfaccia che ha un solo `abstract` method. Ci sono dei tipi già pronti di *interfacce funzionali* sulla [documentazione di Java](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html).

### Method reference

Se si vuole essere più concisi, si può usare una sintassi alternativa per *metodi pre-esistenti* o *named*. Prendiamo come esempio

```java
// converto la mia lista `fruits` in un tipo
// speciale, Stream che permette operazioni
// in parallelo
Stream slicedFruits = fruits.stream()
// L'istruzione non termina fino al `;`.
// .stream() restituisce uno Stream
// .map() lavora su uno stream e restituisce
// un nuovo stream sui cui elementi è applicata
// la funzione .slice()
    .map(fruit -> fruit.slice());
```

Possiamo riscriverlo come

```java
Stream slicedFruits = fruits.stream()
    .map(Fruit::slice())
```

in questo modo si risparmia l'uso del parametro `fruit`.

Ovviamente questa sintassi è totalmente opzionale.

### Quando usare le *funzioni lambda*

Le *lambda functions* sono particolarmente utili quando si ha a che fare con:

- manipolazione di *Collections*
- manipolazione di *Stringhe*
- multi-threading (le funzioni possono essere applicate in parallelo agli elementi di uno stream)
- gestione delle risorse (files, sockets...)

### Iterators vs Stream

Gli [iteratori](#IteratorE) prevedono una visita ordinata di una *collection*, quindi in modo sequenziale e impedendo di usare *multi-threading*.

Uno [stream](http://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html) può essere generato a partire da *collections*, *arrays*, *generatori* e *iteratori*, e permette di sfruttare il *multi-threading* per compiere operazioni su di esso.

Alcuni suoi metodi utili sono:

- `filter(<lambda function>)` restituisce uno stream contenente solo gli elementi per i quali la funzione lambda restituisce `true`.

    ```java
    Stream tallPeople = people.filter(p -> p > 180)
    ```
- `map(<lambda function>)` restituisce un nuovo stream di elementi ai quali viene applicata la funzione lambda passata come parametro. Un esempio è quello sopra.

### Function references

È possibile anche assegnare una funzione lambda ad una variabile di tipo `Predicate` (se restituisce un `Boolean`) o `Function` (altrimenti). Definita così una condizione

```java
final Predicate<Fruit> checkIfhasSeedsAndIsGreen =
    fruit -> fruit.hasSeeds() &&
             fruit.isColor("Green");
```

posso riutilizzarla dopo come

```java
fruits.stream()
      .filter(checkIfHasSeedsAndIsGreen)
      .map(fruit -> System.out.println(fruit));
```

### *Lexical Scoping* e *Clojure*

Si può anche definire un **metodo** che restituisce una *funzione lambda*:

```java
public static Predicate<Fruit> checkColor(final String color) { // parametro
    return fruit -> isColor(color);
}
```

#### Lexical Scoping

Nella riga `return fruit -> isColor(color);` il termine `color` non è un parametro: è una variabile locale al di fuori dello scope della lambda che il compilatore grazie al **lexical scoping** capisce essere legata al *parametro* del metodo che la contiene.

#### Clojure

```java
checkColor("Green");
```

L'espressione sopra è una *clojure* o un'*espressione chiusa*, cioè il cui valore `"Green"` è memorizzato insieme all'ambiente della funzione lambda .

### Optional<T>

[`Optional<T>`](http://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) è un contenitore di un singolo oggetto T, e si usa **solo** quando una funzione **potrebbe non ritornare** un valore. Evita quindi di restituire un null o un'eccezione da gestire.

# JML

## Astrazioni

> **Astrazione**: ignorare dettagli non essenziali per lo scopo che si vuole raggiungere.

### Astrazione per parametrizzazione

Un tipo di astrazione lo abbiamo già visto quando possiamo riassumere una sequenza di istruzioni identiche con una *funzione*, cioè l'*astrazione per parametrizzazione*.

Per esempio, l'operazione per trovare il valore assoluto di un numero, anzichè usare un `if` statement può essere essere sintetizzata da una funzione `abs()` (che esiste già nella libreria `Math`).

```java
// Senza astrazione

if (a < 0) a = -a;
if (b < 0) b = -b;
// ...

// Con astrazione per parametrizzazione
// (abstraction by parametrization)
public static int abs(int p) {
    if (p < 0) return -p;
    else return p;
}

a = abs(a);
b = abs(b);
// ...
```

### Astrazione per specifica

Riprendendo l'esempio sopra, possiamo effettuare invece un  altro tipo di astrazione, quella per specifica.

Nell'*astrazione per specifica* non ci interessa il *come* ma il *che cosa* di un'operazione.

Riprendendo l'esempio di prima, l'astrazione per specifica è *"una funzione che restituisce il valore assoluto del parametro che riceve in input"*.

Potremmo poi implementare come preferiamo la specifica della funzione, l'importante è che essa venga rispettata. Dovesse restituire un numero negativo, c'è sicuramente un errore da qualche parte.

Il vantaggio di quest'astrazione è il fatto che lascia molta libertà nello scrivere il codice e nel fare manutenzione in futuro, l'importante è che venga rispettata la specifica.

### Astrazione procedurale

L'*astrazione procedurale* definisce con una *specifica* un'*operazione complessa* su dati generici o parametri.
Di solito può avere diverse implementazioni.

Si può vedere come la classe d'equivalenza di tutte le funzioni che implementano la stessa specifica.

## Specifica in JML

JML (Java Modelling Language) permette di definire specifiche in [*linguaggio naturale*](https://en.wikipedia.org/wiki/Natural_language_processing) o in *notazione matematica*.

### Pre e post condizioni

In JML si scrive la specifica sopra il metodo in questione in dei commenti speciali che cominciano con `//@` o `/*@ */`. Ogni nuova riga deve contenere un `@` per dire che si tratta di una specifica JML.

Si usano le seguenti *clausole* per specificare le varie condizioni.

È convenienete cercare di avere il minor numero possibile di vincoli ed essere il più generale possibile nella specifica: se si è troppo specifici si limita l'implementazione, se si è troppo generici la specifica è poco utile.

#### `assignable`
`assignable` indica su quali variabili è possibile fare un assegnamento, separate da una "`,`". Se non ci devono essere variabili assegnabili, si aggiunge `\nothing`. Per gli array, si aggiunge `[*]` dopo il nome della variabile.

```java
int a = 0;
int[] b = 1;
//@ assignable \nothing
public static void doNothing() {
    // ...
}

//@ assignable a, b[*]
public static void assignSomething() {
    a = 10;
    b = 27;
}
```

Se si omette `assignables` si può assegnare un valore a qualsiasi variabile.

#### `requires`
`requires` specifica le condizioni sui parametri sotto le quali la specifica è definita, cioè che possiamo chiamare il metodo solo se la condizione è vera. È la *precondizione*.

```java
//@ requires n > 0
public static float squareRoot(int n) {
    // ...
}
```

Se omettiamo la clausola *requires*, il metodo non ha nessuna precondizione da soddisfare.

#### `ensures`
`ensures` specifica il risultato garantito, cioè che cosa deve essere vero, al termine dell'esecuzione del metodo, **solo se** il `requires` è verificato, e non si verificano *eccezioni*. È la *postcondizione normale*.

```java
//@ ensures \result > 0
public static float squareRoot(int n) {
    float root;
    // ...
    return root;
}
```

**Nota:** `\result` è il valore di ciò che viene restituito dal `return`.

Se omettiamo la clausola *ensures*, il metodo non ha nessuna postcondizione da soddisfare (può quindi dare qualsiasi risultato).

#### `signals`
`signals` indica che cosa è vero quando il metodo lancia un'*eccezione*.

```java
// Deve lanciare l'eccezione specificata se il parametro
// `n` è minore di 0.
//@ signals (IllegalArgumentException e) n < 0;
public static float squareRoot(int n) {
    // ...
}
```

#### Commenti/Linguaggio naturale

Per inserire commenti o espressioni in linguaggio naturale, si usano i delimitatori `* ... *`. Tutto ciò che è compreso tra i due "`*`" è un espressione che ha sempre valore `true`.

#### Congiunzioni

Per legare più espressioni simili fra loro si può usare `&&` (AND), `||` (OR), `!` (NOT), e anche `==>` (implicazione) e `<==>` (doppia implicazione).

### Quantificatori

JML fornisce anche dei quantificatori simili a quelli della *logica del primo ordine*, come *per ogni* (for all) e *esiste* (exists).

#### `\old`

**Sintassi:** `\old(x)`

Restituisce il valore della variabile `x` che aveva quando la funzione è stata invocata, cioè il valore iniziale.

#### `\forall`

**Sintassi:**
`(\forall variable (inizializza), condizione ciclo (boolean), condizione (boolen))`

Restituisce `true` se la *condizione* è verificata *per ogni* interazione.

Per esempio, quest'espressione si assicura che gli elementi di un array `a` siano ordinati in modo crescente:

```java
//@ ensures (\forall int i; 0<=i && i< a.length-1; a[i]<=a[i+1])
```

Nella prima parte definisco `int i`, che sarà il contatore.
Nella seconda parte specifico il range per cui effettuo il controllo sulla condizione, cioè per `i` compreso tra `0` e `a.length-1`, cioè la lunghezza dell'array.
Nella terza parte, controllo che ogni elemento di `a`, cioè `a[i]`, sia minore o uguale al successivo `a[i+1]`. Se tale condizione è vera *per ogni* iterazione, la clausola sarà verificata.

#### `\exists`

**Sintassi:** `(\exists variabile; cond. ciclo (boolean); condizione (bool))`

Restituisce `true` se la *condizione* è verificata *almeno una volta*.

```java
//@ ensures
//@ (\exists int i; 0<=i && i<a.length; a[i] == x)
//@ ? x == a[\result]
//@ : \result == -1;
public static int indexOf(int x, int [] a)
```

Come in `\forall`, si itera finchè la condizione del ciclo è *vera*. In quest'esempio, controlliamo se un valore `a[i]` di `a` è uguale al parametro `x` di `indexOf(...)`. Se almeno una volta tale condizione è `true`, l'[operatore ternario](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/op2.html) `? :` (praticamente è un if-else: `<expression> ? < if true> : <if false>`) impone che `x = i`, altrimenti restituisce `-1`.

#### `\num_of`

**Sintassi:** `(\num_of variabile; cond. ciclo (boolean); condizione (bool))`

Restituisce il numero di volte che la condizione è verificate durante il ciclo (cioè il numero di volte che *cond. ciclo* e *condizione* sono verificate).

#### `\sum`

**Sintassi:** `(\sum var; cond. ciclo (boolean); espressione)`

Restituisce la somma dei valori delle espressioni.

#### `\product`

**Sintassi:** `(\product var; cond. ciclo (boolean); espressione)`

Restituisce il prodotto dei valori delle espressioni.

#### `\min`

**Sintassi:** `(\min var; cond. ciclo (boolean); espressione)`

Restituisce il minimo valore di tutte le espressioni computate durante il ciclo.


#### `\max`

**Sintassi:** `(\max var; cond. ciclo (boolean); espressione)`

Restituisce il massimo valore di tutte le espressioni computate durante il ciclo.

### Procedure parziali

Una procedura è *parziale* se ha *requires* (precondizione) non vuoto: ha un comportamento specificato solo per un sottoinsieme del dominio degli argomenti.

```java
//@ requires n > 0
//@ ensures (*condzione sul risultato*)
public void myFunction(int n) {
    // ...
}
```

L'operazione che effettua `myFunction(int n)` è poco sicura: non sappiamo cosa succede se dovesse ricevere in input un numero negativo!

Le procedure parziali sono infatti *poco sicure* da questo punto di vista, conviene avere quindi procedure *totali*.

### Procedure totali

Spesso, nelle procedure *totali* conviene *eliminare* la clausola requires e specificare ogni output possibile mediante *ensures* e *signals*.

Per esempio, una funzione `indexOf(String x, String[] a)` che restituisce la posizione di un elemento `x` all'interno di un array `a`:

```java
//@ requires x != null;
//@ ensures a[\result].equals(x);
//@ signals (NotFoundException e) (*x non e in a *);
public static int indexOf(String x, String[] a) throws NotFoundException
```

può essere migliorata rimuovendo `//@ requires ...`

```java
//@ ensures x != null && a[\result].equals(x);
//@ signals (NotFoundException e) (*x non e
//@ signals (NullPointerException e) x == null;
public static int indexOf(String x, String[] a) throws NullPointerException, NotFoundException
```

Non è conveniente lanciare eccezioni quando la *verifica* richiede più tempo dell'*esecuzione*, fatta eccezione per la fase di testing.

## Astrazione per specifica

Una volta che abbiamo specificato i valori e le operazioni possibili di un *tipo di dato*, abbiamo ottenuto un *ADT* (detto anche *data abstraction*, o semplicemente **tipo**).

Se facciamo astrazione sulla rappresentazione dei valori e su come implementare i metodi, ci rimane solo la *specifica* dell'ADT.

L'ADT divide la *specifica* dall'*implementazione*. Java per conto suo *non è* sufficiente a separare efficientemente specifica da implementazione (fattibile fino ad un certo punto mediante le classi/interfacce).

In JML, nello specificare un *metodo pubblico non statico* devono solo comparire gli elementi **pubblici** del metodo e della classe: \result, i parametri del metodo, [metodi puri](#metodo-puro-pure-method) e attributi pubblici.

### Metodo puro (*pure method*)

Un metodo puro è un metodo non statico che viene dichiarato con la *keyword* `/*@ pure @*/` e:

- non ha effetti collaterali
- `//@ assignables \nothing` si può omettere in quanto ci pensa già la keyword *pure* a imporre la condizione.
- si possono chiamare solo altri metodi puri

Anche i costruttori possono essere dichiarati *pure*, il che vuol dire che possono solo inizializzare gli attributi della classe e nient'altro.