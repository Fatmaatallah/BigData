# Interview Questions (spark)

## Transformation vs Action
Les transformations créent un nouveau RDD à partir d'un RDD existant et elles sont exécutées à la demande (Lazy Evaluation)<br/>
Ex: filter (), union ().
<br/>
Les Actions déclenchent l'exécution des transfomrations à l'aide du DAG et retournent un résultat au Driver program après l'exécution des calculs sur l'ensemble de données<br/>
Ex: count(), first()
<pre>
val f = sc.textFile("/user/raj_ops/spark-labs/data/twinkle/sample.txt")<br/>
val filtered = f.filter(line => line.contains("twinkle"))<br/>
filtered: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[75] at filter at <console>:29<br/>
filtered.count()<br/>
res122: Long = 2<br/>
</pre>
## Driver en spark
Spark Driver est le processus qui crée et possède une instance de SparkContext. C'est le program qui contient la méthode main dans laquelle l'instance de SparkContext est créée.Il divise une spark application en tasks et les planifie et répartie les tasks sur les executors.Il coordonne les workers et l'execution globale des tasks.

## Spark streaming 
Spark streaming  est le module de spark qu'on utilise pour traiter les données en diffusion en Real Time.Il rassemble des streaming data provenant de différentes ressources,telles que log files, social media data, stock market data ou Hadoop ecosystems comme Flume et Kafka.Il décompose l'input Data en batchs.

## RDD
Resilient Distributed datasets: est le concept central spark, c'est un jeu de donnéses qui se parcourt comme une collection,il est découpé en partition et distribué sur plusieurs noeuds d'un cluster, il est resilient  car Si l'un des nouds hébergeant la partition échoue, un autre noud récupère ses données.

## RDD vs DStream
DStream est représenté par une série continue de RDD et chaque RDD contient des données provenant avec un certain intervalle. Toute opération appliquée sur un DStream se traduit par des opérations sur les RDD sous-jacents

## Création d'un RDD
on peut créer un RDD avec:
Charger les data files à partir du local ou bien d'un DFS
<pre>
val f = sc.textFile("/user/raj_ops/spark-labs/data/twinkle/sample.txt")</pre>
aralléliser une collection
<pre>
val u1 = sc.parallelize(List("m1", "m2", "m3"))</pre>
A partir d'un rdd existant
<pre>
val u2 = u1.filter(x => x.like("m1"))</pre>
A partir d'une DataFrame ou DataSet existante
<pre>
val u3 = u2.toDF().rdd</pre>

## Composant de spark
Spark Core: moteur de base pour le traitement de données parallèle et distribué à grande échelle
Spark Streaming: utilisé pour le traitement de données en streaming en temps réel
Spark SQL: intègre le traitement relationnel à l'API de Spark
GraphX: Graphes et calcul parallèle graphique
MLlib: utiliser les algos de machine learning dans Apache Spark

## Accumulator
Ils sont des variables en write-only initialiser une fois et envoyer aux workers en paralléle (seul le driver qui peut les lire), elles sont utilisés pour implémenter des compteurs ou des sommes.
 <pre>
val accum = sc.accumulator(0, "My Accumulator")<br/>
sc.parallelize(Array(1, 2, 3, 4)).foreach(x => accum += x)<br/>
accum.value<br/>
res5: Int = 10</pre>

## Serialization







