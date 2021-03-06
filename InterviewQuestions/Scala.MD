# Interview Questions (SCALA)

## Companion objects
c'est un singleton object qui porte le m�me nom qu'une classe, il peut acc�der aux membres priv�s de son Companion. <br/>
On l'utilise pour les m�thodes et les valeurs qui ne sont pas sp�cifiques aux instances de la companion class.<br/>
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
Le compilateur de Scala peut d�duire le type d'une expression, donc on a pas � la d�clarer explicitement.<br/>
Mais pour les m�thodes r�cursives, le compilateur ne peut pas inf�rer le type du retour aussi il n'inf�re jamais les types de param�tre d'une m�thode mais dans certains cas, il peut d�duire des types de param�tres de fonction anonymes lorsque la fonction est transmise en tant qu'argument.
<pre>val a=5;<br/>
a: Int = 5<br/>
</pre>
## Currying
Currying permet de transformer une fonction qui attend deux arguments en une fonction qui n'en attend qu'un, et cette fonction renvoie une fonction qui attend le deuxi�me argument.
<pre>def add(x: Int)(y: Int): Int = {x+y} <br/>
add(1)_<br/>
res1: Int => Int = <function1> <br/>
</pre>
## G�rer les nuls
La solution de Scala pour g�rer les nuls consiste � utiliser les classes  Option/some/none, Les classes Some et None sont des  subclasses de Option.
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
tail-recursive est une m�thode dont la toute derni�re action est un appel � elle-m�me.
Lorsque on �crit une fonction r�cursive, le compilateur Scala peut optimiser le bytecode r�sultant de la jvm afin que la fonction ne n�cessite qu'un seul stack frame, par opposition � un stack frame pour chaque niveau de r�cursion

## Impl�menter les interfaces
Scala trait juste comme une interface Java. on d�clare les m�thode du trait qu'on souhaite que les classes d'extension l'impl�mentent.<br/>
Les classes et les objets peuvent �tendre les traits, mais les traits ne peuvent pas �tre instanci�s et n'ont donc aucun param�tre.<br/>
## Utilit� les implicites dans scala
les implicites aident le compilateur � d�terminer le type , � nous aider � �lminer la duplicationet et �  �crire du code s�r pour les probl�mes qui aboutiraient autrement � des comparaisons de types au moment de l'ex�cution.<br/>
exemple:implicit parameters
<pre>
def sendText(body: String)(implicit from: String): String = s"$body, from: $from" <br/>
implicit val sender: String = "Alice"<br/>
sendText("hola mundo")<br/>
res3: String = hola mundo, from: Alice <br/>
Cela permet d'�liminer la duplication de code dans les appels � diff�rentes m�thodes n�cessitant le m�me param�tre<br/></pre>
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
case class's peuvent �tre pattern matched<br/>-
case class n'a pas besoin de new explicitement, alors que class doit �tre appel�e avec un new<br/>
Par d�faut Les param�tres des constructeurs sont private dans class, alors qu'ils sont public dans case class<br/>
case class's se comparent par valeur<br/>
## Case class vs class
Ils sont souvent utilis�s pour fournir une alternative aux enums dans java. Comme ils ne peuvent �tre �tendus que dans un m�me fichier, le compilateur conna�t tous les sous-types possibles et don peut raisonner
## FlatMap et Flatten
La m�thode flatMap prend une fonction et l'applique � chaque �l�ment de la collection. elle renvoie ensuite une nouvelle collection en utilisant les �l�ments renvoy�s par la fonction. La m�thode flatMap est essentiellement une combinaison de la m�thode map suivie de la m�thode flatten(r�duit les �l�ments d'une collection pour cr�er une seule collection avec des �l�ments du m�me type)
## HIGHER-ORDER FUNCTIONS
HIGHER-ORDER FUNCTIONS prennent d'autres fonctions en tant que param�tres ou renvoient une fonction � la suite.L'un des exemples les plus courants est la fonction map

## FUNCTION vs method
Les fonctions sont des objets, similaire aux m�thodes statiques en ce sens qu'elles sont ind�pendantes d'un objet � invoquer. on les utilise si on a besoin de les transmettre en tant que param�tres ou bien de manipuler leur instance function1.compose(function2)(2).
<pre>
val function1=(x: Int) => x + x<br/>
function1(2)<br/>
res5: Int = 4<br/>
function1<br/>
res6: Int => Int = <function1><br/>
</pre>
Et les methods ne sont pas des objets mais affect�s � une instance d'une classe, c'est-�-dire un objet. Exactement la m�me chose que la m�thode en Java, on les utilise si on veut utiliser les valeurs par d�faut pour les param�tres ou bien lorsque juste on a besoin de calculer et de retourner.
## FUNCTION vs method
Une fonction dont la valeur de retour d�pend de la valeur d'une ou de plusieurs variables d�clar�es en dehors de cette fonction
<pre>
var factor = 3<br/>
val multiplier = (i:Int) => i * factor<br/>
</pre>
## La diff�rence entre apply et unapply
La m�thode apply est comme un constructeur qui prend des arguments et cr�e un object, unapply prend un objet et essaie de restituer les arguments 
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
Lazy Evaluation est une strat�gie d'�valuation qui retarde l'�valuation d'une expression jusqu'� ce que sa valeur soit n�cessaire
<pre>
lazy val lval = 5<br/>
La valeur de lval ne sera pas initialis�e avant son appel.
</pre>



