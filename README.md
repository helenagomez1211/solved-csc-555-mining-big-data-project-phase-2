Download Link: https://assignmentchef.com/product/solved-csc-555-mining-big-data-project-phase-2
<br>
In this part of the project, you will execute queries using Hive, Pig and Hadoop streaming and develop a custom version of KMeans clustering. The schema is available below, but don’t forget to apply the correct delimiter:

<a href="http://rasinsrv07.cstcis.cti.depaul.edu/CSC555/SSBM1/SSBM_schema_hive.sql">http://rasinsrv07.cstcis.cti.depaul.edu/CSC555/SSBM1/SSBM_schema_hive.sql</a>




The data is available at (this is Scale1, the smallest denomination of this benchmark)

<a href="http://rasinsrv07.cstcis.cti.depaul.edu/CSC555/SSBM1/">http://rasinsrv07.cstcis.cti.depaul.edu/CSC555/SSBM1/</a>




In your submission, please note what cluster you are using. Please be sure to <u>submit all code</u> (pig, python and Hive). You should also submit the <u>command lines you use</u> and a <u>screenshot</u> of a completed run (just the last page, do not worry about capturing the whole output). An answer without code will <u>not receive credit</u>.

<strong>I highly recommend creating a small sample input</strong> (e.g., by running head lineorder.tbl &gt; lineorder.tbl.sample) and testing your code with it. You can run <strong>head -n 500 lineorder.tbl</strong> to get a specific number of lines.

NOTE: the total number of points adds up to 70 because Phase I is worth 30 of the project.

<h1>Part 1: Data Transformation (15 pts)</h1>

Transform part.tbl table into a *-separated (‘*’) file: Use Hive, MapReduce with HadoopStreaming and Pig (i.e. 3 different solutions).

In all solutions you must switch odd and even columns (i.e., switch the positions of columns 1 and 2, columns 3 and 4, etc.). You do not need to transform the columns in any way, just a new data file.

<h1></h1>

<h1>Part 2: Querying (25 pts)</h1>

Implement the following query:

select lo_quantity, c_nation, sum(lo_revenue)from customer, lineorderwhere lo_custkey = c_custkey  and c_region = ‘AMERICA’   and lo_discount BETWEEN 3 and 5 group by lo_quantity, c_nation;




using Hive, MapReduce with HadoopStreaming and Pig (i.e. 3 different solutions). I Hive, this merely requires pasting the query into the Hive prompt and timing it. In Hadoop streaming, this will require a total of 2 passes (one for join and another one for GROUP BY).

<h1>Part 3: Clustering (30 pts)</h1>

Create a new numeric file with 25,000 rows and 3 columns, separated by space – you can generate numeric data as you prefer, but submit whatever code that you have used.

<ol>

 <li>(5 pts) Using Mahout synthetic clustering as you have in a previous assignment on sample data. This entails running the <strong>same</strong> clustering command, but substituting your own input data instead of the sample.</li>

 <li>(25 pts) Using Hadoop streaming perform four iterations manually <strong>using 6 centers</strong> (initially with randomly chosen centers). This would require passing a text file with cluster centers using -file option, opening the centers.txt in the mapper with open(‘centers.txt’, ‘r’) and assigning a key to each point based on which center is the closest to each particular point. Your reducer would then compute the new centers, and at that point the iteration is done and the output of the reducer with new centers can be given to the next pass of the same code.</li>

</ol>

The only difference between first and subsequent iteration is that in first iteration you have to pick the initial centers. Starting from 2<sup>nd</sup> iteration, the centers will be given to you by a previous pass of KMeans.

<strong><u>Extra credit (7 pts)</u></strong>: Create the equivalent of KMeans driver from Mahout. That is, write a python script that will automatically execute the hadoop streaming command, then get the new centers from HDFS and repeat the command. This will be easiest to do if you write your reducer to output just the centers (without the key) to HDFS. This way, all you have to do is to execute the get command to get the new centers (you can hard-code the locations of output in HDFS into your script).


