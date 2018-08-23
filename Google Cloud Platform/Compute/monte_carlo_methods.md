* Based on this tutorial https://cloud.google.com/solutions/monte-carlo-methods-with-hadoop-spark


* Create a cloud dataproc cluster
    * This means that you currently have 3 or more connected VMs 
        * connected together to perform operations in parallel
        * have preinstalled libraries like pyspark
* SSH the master VM
    * Run a Monte Carlo simulation using Python that estimates the growth of a stock portfolio over time 
        * Initiate by `pyspark`
    * Run a Monte Carlo simulation using Scala that simulates how a casino makes money
        * Initiate by `spark-shell`
  
* Notes
    * Use `sc.parallelize` in both pyspark(python) and sparkshell(scala) to parallelize the map reduce operation on all instances
  