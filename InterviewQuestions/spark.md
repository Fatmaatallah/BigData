# Interview Questions (spark)

## Transformation vs Action
Les transformations cr�ent un nouveau RDD � partir d'un RDD existant et elles sont ex�cut�es � la demande (Lazy Evaluation)<br/>
Ex: filter (), union ().
<br/>
Les Actions d�clenchent l'ex�cution des transfomrations � l'aide du DAG et retournent un r�sultat au Driver program apr�s l'ex�cution des calculs sur l'ensemble de donn�es<br/>
Ex: count(), first()
<pre>
val f = sc.textFile("/user/raj_ops/spark-labs/data/twinkle/sample.txt")<br/>
val filtered = f.filter(line => line.contains("twinkle"))<br/>
filtered: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[75] at filter at <console>:29<br/>
filtered.count()<br/>
res122: Long = 2<br/>
</pre>
## Driver en spark
Spark Driver est le processus qui cr�e et poss�de une instance de SparkContext. C'est le program qui contient la m�thode main dans laquelle l'instance de SparkContext est cr��e.Il divise une spark application en tasks et les planifie et r�partie les tasks sur les executors.Il coordonne les workers et l'execution globale des tasks.

## Spark streaming 
Spark streaming  est le module de spark qu'on utilise pour traiter les donn�es en diffusion en Real Time.Il rassemble des streaming data provenant de diff�rentes ressources,telles que log files, social media data, stock market data ou Hadoop ecosystems comme Flume et Kafka.Il d�compose l'input Data en batchs.

## RDD
Resilient Distributed datasets: est le concept central spark, c'est un jeu de donn�ses qui se parcourt comme une collection,il est d�coup� en partition et distribu� sur plusieurs noeuds d'un cluster, il est resilient  car Si l'un des nouds h�bergeant la partition �choue, un autre noud r�cup�re ses donn�es.

## RDD vs DStream
DStream est repr�sent� par une s�rie continue de RDD et chaque RDD contient des donn�es provenant avec un certain intervalle. Toute op�ration appliqu�e sur un DStream se traduit par des op�rations sur les RDD sous-jacents

## Cr�ation d'un RDD
on peut cr�er un RDD avec:
Charger les data files � partir du local ou bien d'un DFS
<pre>
val f = sc.textFile("/user/raj_ops/spark-labs/data/twinkle/sample.txt")</pre>
arall�liser une collection
<pre>
val u1 = sc.parallelize(List("m1", "m2", "m3"))</pre>
A partir d'un rdd existant
<pre>
val u2 = u1.filter(x => x.like("m1"))</pre>
A partir d'une DataFrame ou DataSet existante
<pre>
val u3 = u2.toDF().rdd</pre>

## Composant de spark
Spark Core: moteur de base pour le traitement de donn�es parall�le et distribu� � grande �chelle
Spark Streaming: utilis� pour le traitement de donn�es en streaming en temps r�el
Spark SQL: int�gre le traitement relationnel � l'API de Spark
GraphX: Graphes et calcul parall�le graphique
MLlib: utiliser les algos de machine learning dans Apache Spark

## Accumulator
Ils sont des variables en write-only initialiser une fois et envoyer aux workers en parall�le (seul le driver qui peut les lire), elles sont utilis�s pour impl�menter des compteurs ou des sommes.
 <pre>
val accum = sc.accumulator(0, "My Accumulator")<br/>
sc.parallelize(Array(1, 2, 3, 4)).foreach(x => accum += x)<br/>
accum.value<br/>
res5: Int = 10</pre>

## Serialization







