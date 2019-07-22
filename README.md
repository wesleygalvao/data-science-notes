# My notes on Data Science


## Frameworks, Tools and libraries

- [Apache Hadoop](https://hadoop.apache.org/)
- [Apache Spark](https://spark.apache.org/)
- [D3](https://d3js.org/)
- [Flink](https://flink.apache.org/)
- [ggplot](http://ggplot.yhathq.com/)
- [Jupyter Docker Images](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html)
- [Jupyter](https://jupyter.org/)
- [Kaggle](https://www.kaggle.com/)
- [Matplotlib](https://matplotlib.org/)
- [Numpy](https://numpy.org/)
- [Pandas Profiling](https://github.com/pandas-profiling/pandas-profiling)
- [Pandas](https://pandas.pydata.org/)
- [r-project](https://www.r-project.org/)
- [Scikit-learn](https://scikit-learn.org/)
- [SciPy](https://www.scipy.org/)
- [Seaborn](https://seaborn.pydata.org/)


## Snippets

##### Jupyter - Pyspark


```shell script

docker run --rm \
-v ~:/home/jovyan/work \
-p 8888:8888 \
-p 4040:4040 \
-p 4041:4041 \
jupyter/pyspark-notebook
```

```python

import pyspark 

sc = pyspark.SparkContext('local[*]')

# do something to prove it works
rdd = sc.parallelize(range(1000))
rdd.takeSample(False, 5)
```


##### D3 on Jupyter

```shell script
!pip install py_d3 -q
```

```shell script
%load_ext py_d3
```

```html
%%d3


<div id="my_dataviz"></div>


<script>
    // set the dimensions and margins of the graph
    var width = 450
        height = 450
        margin = 40
    
    // The radius of the pieplot is half the width or half the height (smallest one). I subtract a bit of margin.
    var radius = Math.min(width, height) / 2 - margin
    
    // append the svg object to the div called 'my_dataviz'
    var svg = d3.select("#my_dataviz")
      .append("svg")
        .attr("width", width)
        .attr("height", height)
      .append("g")
        .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");
    
    // Create dummy data
    var data = {a: 9, b: 20, c:30, d:8, e:12}
    
    // set the color scale
    var color = d3.scaleOrdinal()
      .domain(data)
      .range(d3.schemeSet2);
    
    // Compute the position of each group on the pie:
    var pie = d3.pie()
      .value(function(d) {return d.value; })
    var data_ready = pie(d3.entries(data))
    // Now I know that group A goes from 0 degrees to x degrees and so on.
    
    // shape helper to build arcs:
    var arcGenerator = d3.arc()
      .innerRadius(0)
      .outerRadius(radius)
    
    // Build the pie chart: Basically, each part of the pie is a path that we build using the arc function.
    svg
      .selectAll('mySlices')
      .data(data_ready)
      .enter()
      .append('path')
        .attr('d', arcGenerator)
        .attr('fill', function(d){ return(color(d.data.key)) })
        .attr("stroke", "black")
        .style("stroke-width", "2px")
        .style("opacity", 0.7)
    
    // Now add the annotation. Use the centroid method to get the best coordinates
    svg
      .selectAll('mySlices')
      .data(data_ready)
      .enter()
      .append('text')
      .text(function(d){ return "grp " + d.data.key})
      .attr("transform", function(d) { return "translate(" + arcGenerator.centroid(d) + ")";  })
      .style("text-anchor", "middle")
      .style("font-size", 17)
</script>
```

## Books

## Papers

- [Resilient distributed datasets: A fault-tolerant abstraction for in-memory cluster computing](https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final138.pdf)
- [MapReduce: Simplified Data Processing on Large Clusters](http://research.google.com/archive/mapreduce.html)
- [The PageRank Citation Ranking: Bringing Order to the Web](http://ilpubs.stanford.edu:8090/422)
- [MapReduce: Simplified Data Processing on Large Clusters](http://research.google.com/archive/mapreduce.html)
- [The Google File System](http://research.google.com/archive/gfs.html)
- [Amazon’s Dynamo](http://www.allthingsdistributed.com/2007/10/amazons_dynamo.html)
- [Bigtable: A Distributed Storage System for Structured Data](http://research.google.com/archive/bigtable.html)
- [A Few Useful Things to Know about Machine Learning](http://homes.cs.washington.edu/~pedrod/papers/cacm12.pdf)
- [Random Forests](http://oz.berkeley.edu/~breiman/randomforest2001.pdf)
- [A Relational Model of Data for Large Shared Data Banks](http://www.seas.upenn.edu/~zives/03f/cis550/codd.pdf)
- [Map-Reduce for Machine Learning on Multicore](http://machinelearning.wustl.edu/mlpapers/paper_files/NIPS2006_725.pdf)
- [Pasting Small Votes for Classification in Large Databases and On-Line](http://sci2s.ugr.es/keel/pdf/algorithm/articulo/1999-ML-Breiman-Pasting%20Small%20Votes%20for%20Classification%20in%20Large%20Databases%20and%20On-Line.pdf)
- [Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank](http://nlp.stanford.edu/~socherr/EMNLP2013_RNTN.pdf)
- [Spanner: Google’s Globally-Distributed Database](http://research.google.com/archive/spanner.html)
- [Megastore: Providing Scalable, Highly Available Storage for Interactive Services](http://research.google.com/pubs/pub36971.html)
- [F1: A Distributed SQL Database That Scales](http://research.google.com/pubs/pub41344.html)
- [APACHE DRILL: Interactive Ad-Hoc Analysis at Scale](http://online.liebertpub.com/doi/pdfplus/10.1089/big.2013.0011)
- [A New Approach to Linear Filtering and Prediction Problems](http://www.cs.unc.edu/~welch/kalman/media/pdf/Kalman1960.pdf)
- [Top 10 algorithms on Data mining</a>](http://www.cs.umd.edu/~samir/498/10Algorithms-08.pdf)

## Datasets

- [Kaggle datasets](https://kaggle.com/datasets)
- [Youtube 8M](https://research.google.com/youtube8m/download.html)
- [Stack Exchange](https://data.stackexchange.com/help)

## Ref Cards

 - [**Tensorflow**](https://github.com/sandysnunes/data-science-notes/blob/master/PDFs/Tensorflow.pdf)<br>
  - [**Keras**](https://github.com/sandysnunes/data-science-notes/blob/master/Keras.jpg)<br>
  - [**Neural Networks Zoo**](https://github.com/sandysnunes/data-science-notes/blob/master/Neural%20Networks%20Zoo.png)<br>
  - [**Numpy**](https://github.com/sandysnunes/data-science-notes/blob/master/Numpy.png)<br>
  - [**Scipy**](https://github.com/sandysnunes/data-science-notes/blob/master/Scipy.png)<br>
  - [**Pandas-1**](https://github.com/sandysnunes/data-science-notes/blob/master/Pandas-1.jpg)<br>
  - [**Pandas-2**](https://github.com/sandysnunes/data-science-notes/blob/master/Pandas-2.jpg)<br>
  - [**Pandas-3**](https://github.com/sandysnunes/data-science-notes/blob/master/Pandas-3.png)<br>
  - [**Scikit-learn**](https://github.com/sandysnunes/data-science-notes/blob/master/Scikit%20Learn.png)<br>
  - [**Matplotlib**](https://github.com/sandysnunes/data-science-notes/blob/master/Matplotlib.png)<br>
  - [**ggplot2-1**](https://github.com/sandysnunes/data-science-notes/blob/master/ggplot2-1.jpg)<br>
  - [**ggplot2-2**](https://github.com/sandysnunes/data-science-notes/blob/master/ggplot2-2.jpg)<br>
  - [**PySpark**](https://github.com/sandysnunes/data-science-notes/blob/master/PySpark.jpg)<br>
  - [**PySpark-RDD**](https://github.com/sandysnunes/data-science-notes/blob/master/PySpark-RDD.png)<br>
  - [**PySpark-SQL**](https://github.com/sandysnunes/data-science-notes/blob/master/PySpark-SQL.png)<br>
  - [**R Studio(dplyr & tidyr)-1**](https://github.com/sandysnunes/data-science-notes/blob/master/Data%20Wrangling%20with%20dplyr%20and%20tidyr%20-%20R%20Studio-1.jpg)<br>
  - [**R Studio(dplyr & tidyr)-2**](https://github.com/sandysnunes/data-science-notes/blob/master/Data%20Wrangling%20with%20dplyr%20and%20tidyr%20-%20R%20Studio-2.jpg)<br>
  - [**Neural Network Cells**](https://github.com/sandysnunes/data-science-notes/blob/master/Neural%20Network%20Cells.png)<br>
  - [**Neural Network Graphs**](https://github.com/sandysnunes/data-science-notes/blob/master/Neural%20Network%20Graphs.png)<br>
  - [**Deep Learning Cheat Sheet**](https://github.com/sandysnunes/data-science-notes/blob/master/Deep%20Learning%20Cheat%20Sheet-Hacker%20Noon.pdf)<br>
  - [**Dask1**](https://github.com/sandysnunes/data-science-notes/blob/master/Dask1.png)
  - [**Dask2**](https://github.com/sandysnunes/data-science-notes/blob/master/Dask2.png)
  - [**Dask3**](https://github.com/sandysnunes/data-science-notes/blob/master/Dask3.png)
  - [**Dask4**](https://github.com/sandysnunes/data-science-notes/blob/master/Dask4.png)
  - [**All Cheat Sheets(PDF)**](https://github.com/sandysnunes/data-science-notes/blob/master/All%20Cheat%20Sheets.pdf)<br>

## Notebooks

## GitHub Repos

- [Awesome Public Datasets](https://github.com/awesomedata/awesome-public-datasets)
- [Awesome Data Science](https://github.com/bulutyazilim/awesome-datascience) 
- [Data Science Resources](https://github.com/jonathan-bower/DataScienceResources) 
- [Data science blogs](https://github.com/rushter/data-science-blogs) 
- [Machine Learning for Software Engineers](https://github.com/ZuzooVn/machine-learning-for-software-engineers) 
- [Data Science Specialization resources](https://github.com/DataScienceSpecialization/courses) 
- [Data Science Specialization notes](https://github.com/sux13/DataScienceSpCourseNotes) 
- [Python Data Science Tutorials](https://github.com/ujjwalkarn/DataSciencePython) 
- [R Data Science Tutorials](https://github.com/ujjwalkarn/DataScienceR) 
- [Machine Learning & Deep Learning Tutorials](https://github.com/ujjwalkarn/Machine-Learning-Tutorials) 
- [Learn Data Science open resources](https://github.com/nborwankar/LearnDataScience) 
- [List of Data Science/Big Data Resources](https://github.com/chaconnewu/free-data-science-books) 
- [General Assembly's Data Science course materials](https://github.com/justmarkham/DAT8) 
- [Scikit-learn Tutorial](https://github.com/jakevdp/sklearn_tutorial) 
- [theano-tutorial](https://github.com/craffel/theano-tutorial) 
- [IPython Theano Tutorials](https://github.com/jaberg/IPythonTheanoTutorials) 
- [ISLR-python](https://github.com/JWarmenhoven/ISLR-python) 
- [Awesome R](https://github.com/qinwf/awesome-R) 
- [Evaluation of Deep Learning Frameworks](https://github.com/zer0n/deepframeworks) 
- [Amazon Web Services — a practical guide](https://github.com/open-guides/og-aws)

## Podcasts
- ### Podcasts for Beginners:
    - [Talking Machines](http://www.thetalkingmachines.com/)
    - [Linear Digressions](http://lineardigressions.com/)
    - [Data Skeptic](http://dataskeptic.com/)
    - [This Week in Machine Learning & AI](https://twimlai.com/)
    - [Machine Learning Guide](http://ocdevel.com/podcasts/machine-learning)

- ### "More" advanced podcasts
    - [Partially Derivative](http://partiallyderivative.com/)
    - [O’Reilly Data Show](http://radar.oreilly.com/tag/oreilly-data-show-podcast)
    - [Not So Standard Deviation](https://soundcloud.com/nssd-podcast)

- ### Podcasts to think outside the box:
    - [Data Stories](http://datastori.es/)

## Communities
- Quora
    - [Machine Learning](https://www.quora.com/topic/Machine-Learning)
    - [Statistics](https://www.quora.com/topic/Statistics-academic-discipline)
    - [Data Mining](https://www.quora.com/topic/Data-Mining)

- Reddit
    - [Machine Learning](https://www.reddit.com/r/machinelearning)
    - [Computer Vision](https://www.reddit.com/r/computervision)
    - [Natural Language](https://www.reddit.com/r/languagetechnology)
    - [Data Science](https://www.reddit.com/r/datascience)
    - [Big Data](https://www.reddit.com/r/bigdata)
    - [Statistics](https://www.reddit.com/r/statistics)

- [Data Tau](http://www.datatau.com/)

- [Deep Learning News](http://news.startup.ml/)

- [KDnuggets](http://www.kdnuggets.com/)

## Interview Questions
- [How To Prepare For A Machine Learning Interview](http://blog.udacity.com/2016/05/prepare-machine-learning-interview.html)
- [40 Interview Questions asked at Startups in Machine Learning / Data Science](https://www.analyticsvidhya.com/blog/2016/09/40-interview-questions-asked-at-startups-in-machine-learning-data-science)
- [21 Must-Know Data Science Interview Questions and Answers](http://www.kdnuggets.com/2016/02/21-data-science-interview-questions-answers.html)
- [Top 50 Machine learning Interview questions & Answers](http://career.guru99.com/top-50-interview-questions-on-machine-learning/)
- [Machine Learning Engineer interview questions](https://resources.workable.com/machine-learning-engineer-interview-questions)
- [Popular Machine Learning Interview Questions](http://www.learn4master.com/machine-learning/popular-machine-learning-interview-questions)
- [What are some common Machine Learning interview questions?](https://www.quora.com/What-are-some-common-Machine-Learning-interview-questions)
- [What are the best interview questions to evaluate a machine learning researcher?](https://www.quora.com/What-are-the-best-interview-questions-to-evaluate-a-machine-learning-researcher)
- [Collection of Machine Learning Interview Questions](http://analyticscosm.com/machine-learning-interview-questions-for-data-scientist-interview/)
- [121 Essential Machine Learning Questions & Answers](https://elitedatascience.com/mlqa-reading-list)
- [Top 50 Spark Interview Questions and Answers for 2018](https://www.dezyre.com/article/top-50-spark-interview-questions-and-answers-for-2018/208)
