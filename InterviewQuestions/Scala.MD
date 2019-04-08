# Interview Questions (SCALA)

## Companion objects
c'est un singleton object qui porte le même nom qu'une classe, il peut accéder aux membres privés de son Companion. <br/>
On l'utilise pour les méthodes et les valeurs qui ne sont pas spécifiques aux instances de la companion class.<br/>
<pre>class Hello {<br/>
    def sayHelloWorld() {<br/>
        println("Hello World");<br/>
    }<br/>
}<br/>
object Hello {<br/>
    def sayHi() {<br/>
        println("Hi!");<br/>
    }<br/>
}<br/>
var hello1 : Hello = new Hello();<br/>
hello1.sayHelloWorld();<br/>
Hello.sayHi();<br/>
</pre>

## Type inference
Le compilateur de Scala peut déduire le type d'une expression, donc on a pas à la déclarer explicitement.<br/>
Mais pour les méthodes récursives, le compilateur ne peut pas inférer le type du retour aussi il n'infère jamais les types de paramètre d'une méthode mais dans certains cas, il peut déduire des types de paramètres de fonction anonymes lorsque la fonction est transmise en tant qu'argument.
<pre>val a=5;<br/>
a: Int = 5<br/>
</pre>
## Currying
Currying permet de transformer une fonction qui attend deux arguments en une fonction qui n'en attend qu'un, et cette fonction renvoie une fonction qui attend le deuxième argument.
<pre>def add(x: Int)(y: Int): Int = {x+y} <br/>
add(1)_<br/>
res1: Int => Int = <function1> <br/>
</pre>
## Gérer les nuls
La solution de Scala pour gérer les nuls consiste à utiliser les classes  Option/some/none, Les classes Some et None sont des  subclasses de Option.
<pre>
def toInt(s: String): Option[Int] = {<br/>
    try {<br/>
        Some(Integer.parseInt(s.trim))<br/>
    } catch {<br/>
        case e: Exception => None<br/>
    }<br/>
}<br/>

toInt(x) match {<br/>
    case Some(i) => println(i)<br/>
    case None => println("That didn't work.")<br/>
}<br/>
</pre>
## Tail recursion
tail-recursive est une méthode dont la toute dernière action est un appel à elle-même.
Lorsque on écrit une fonction récursive, le compilateur Scala peut optimiser le bytecode résultant de la jvm afin que la fonction ne nécessite qu'un seul stack frame, par opposition à un stack frame pour chaque niveau de récursion

## Implémenter les interfaces
Scala trait juste comme une interface Java. on déclare les méthode du trait qu'on souhaite que les classes d'extension l'implémentent.<br/>
Les classes et les objets peuvent étendre les traits, mais les traits ne peuvent pas être instanciés et n'ont donc aucun paramètre.<br/>
## Utilité les implicites dans scala
les implicites aident le compilateur à déterminer le type , à nous aider à élminer la duplicationet et à  écrire du code sûr pour les problèmes qui aboutiraient autrement à des comparaisons de types au moment de l'exécution.<br/>
exemple:implicit parameters
<pre>
def sendText(body: String)(implicit from: String): String = s"$body, from: $from" <br/>
implicit val sender: String = "Alice"<br/>
sendText("hola mundo")<br/>
res3: String = hola mundo, from: Alice <br/>
Cela permet d'éliminer la duplication de code dans les appels à différentes méthodes nécessitant le même paramètre<br/></pre>
Implicit conversions<br/>
<pre>
import scala.language.implicitConversions<br/>
object Playground {<br/>

  implicit def Int2String(number: Int): String = number.toString()<br/>

  def createNumber: Int = scala.util.Random.nextInt<br/>

  val myNumber: String = createNumber<br/>
  val text: String = 123<br/>

}<br/>
On oublie de devoir appliquer n'importe quel type de transformation, elle sera faite automatiquement
</pre>
## Case class vs class
case class's peuvent être pattern matched<br/>-
case class n'a pas besoin de new explicitement, alors que class doit être appelée avec un new<br/>
Par défaut Les paramètres des constructeurs sont private dans class, alors qu'ils sont public dans case class<br/>
case class's se comparent par valeur<br/>
## Case class vs class
Ils sont souvent utilisés pour fournir une alternative aux enums dans java. Comme ils ne peuvent être étendus que dans un même fichier, le compilateur connaît tous les sous-types possibles et don peut raisonner
## FlatMap et Flatten
La méthode flatMap prend une fonction et l'applique à chaque élément de la collection. elle renvoie ensuite une nouvelle collection en utilisant les éléments renvoyés par la fonction. La méthode flatMap est essentiellement une combinaison de la méthode map suivie de la méthode flatten(réduit les éléments d'une collection pour créer une seule collection avec des éléments du même type)
## HIGHER-ORDER FUNCTIONS
HIGHER-ORDER FUNCTIONS prennent d'autres fonctions en tant que paramètres ou renvoient une fonction à la suite.L'un des exemples les plus courants est la fonction map

## FUNCTION vs method
Les fonctions sont des objets, similaire aux méthodes statiques en ce sens qu'elles sont indépendantes d'un objet à invoquer. on les utilise si on a besoin de les transmettre en tant que paramètres ou bien de manipuler leur instance function1.compose(function2)(2).
<pre>
val function1=(x: Int) => x + x<br/>
function1(2)<br/>
res5: Int = 4<br/>
function1<br/>
res6: Int => Int = <function1><br/>
</pre>
Et les methods ne sont pas des objets mais affectés à une instance d'une classe, c'est-à-dire un objet. Exactement la même chose que la méthode en Java, on les utilise si on veut utiliser les valeurs par défaut pour les paramètres ou bien lorsque juste on a besoin de calculer et de retourner.
## FUNCTION vs method
Une fonction dont la valeur de retour dépend de la valeur d'une ou de plusieurs variables déclarées en dehors de cette fonction
<pre>
var factor = 3<br/>
val multiplier = (i:Int) => i * factor<br/>
</pre>
## La différence entre apply et unapply
La méthode apply est comme un constructeur qui prend des arguments et crée un object, unapply prend un objet et essaie de restituer les arguments 
<pre>
object CustomerID {<br/>
     |
     |   def apply(name: String) = s"$name--${Random.nextLong}"<br/>
     |
     |   def unapply(customerID: String): Option[String] = {<br/>
     |     val stringArray: Array[String] = customerID.split("--")<br/>
     |     if (stringArray.tail.nonEmpty) Some(stringArray.head) else None<br/>
     |   }<br/>
     | }<br/>
al customer1ID = CustomerID("tt")<br/>
customer1ID: String = tt---6325513315163355622  <br/>
 customer1ID match {<br/>
     |   case CustomerID(name) => println(name)  <br/>
     |   case _ => println("Could not extract a CustomerID")<br/>
     | }
tt<br/>
</pre>
## Lazy Evaluation
Lazy Evaluation est une stratégie d'évaluation qui retarde l'évaluation d'une expression jusqu'à ce que sa valeur soit nécessaire
<pre>
lazy val lval = 5<br/>
La valeur de lval ne sera pas initialisée avant son appel.
</pre>



