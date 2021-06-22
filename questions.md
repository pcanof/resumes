[return to index](index.md)

**How does creating a topic in Kafka work?**

Kafka is a Java library that allows you to perform per-event processing of records in real time. You can process each record as soon as it’s available and gives you the low-latency processing you require. One or more nodes will have as source Kafka topics and you can add additional nodes, which are considered child nodes.  
A topic is similar to a folder in a filesystem, and the events are the files in that folder. Topics in Kafka are always multi-producer and multi-subscriber: a topic can have zero, one, or many producers that write events to it, as well as zero, one, or many consumers that subscribe to these events. Events in a topic can be read as often as needed. 

There are 5 API’s in Kafka. 
- The Admin API to manage and inspect topics, brokers, and other Kafka objects. 
- The Producer API to publish (write) a stream of events to one or more Kafka topics. 
- The Consumer API to subscribe to (read) one or more topics and to process the stream of events produced to them. 
- The Kafka Streams API to implement stream processing applications and microservices. 
- The Kafka Connect API to build and run reusable data import/export connectors that consume (read) or produce (write) streams of events from and to external systems and applications so they can integrate with Kafka. 

We focused on Admin API, where you can to manage and inspect topics and the broker. Once you configure the broker in the PC with the following scripts. 

```
# Start the Kafka zookeeper service 
$ bin/zookeeper-server-start.sh config/zookeeper.properties 
# Start the Kafka broker service 
$ bin/kafka-server-start.sh config/server.properties 
``` 

Then you can create a topic with this script. 

```
$ bin/kafka-topics.sh --create –topic my-topic --bootstrap-server localhost:9092 
```

That script calls for createTopic method from TopicService class method to create the topic “my-topic”. Also, this method checks that the topic name is the expected large, the name doesn’t have invalid characters and assign an Hash ID. The code is in the next link. 
https://github.com/pcanof/kafka/blob/trunk/core/src/main/scala/kafka/admin/TopicCommand.scala 
 
 
**How a pipeline of scikit-learn work?**

Scikit-learn is a Python library specially designed for Machine Learning (ML) algorithms, some of them are classification, regression and clustering. The project was started in 2007 by David Cournapeau as a Google Summer of Code project, then for years this project has been growing tanks to all developers that contribute in the project.  

Pipeline class allows sticking multiple processes into a single scikit-learn estimator. Pipeline class has fit, predict and score method just like any other estimator. In a pipeline object you can add transform methods that is used for fit the machine learning algorithm and then you can use a prediction method with the data you want to use. Using a pipeline will also prevent you from data leakage, disclosing some testing data in your training data. 

All the class is defined in this file that you can see in this link 
https://github.com/scikit-learn/scikit-learn/blob/main/sklearn/pipeline.py 

This is an example for use this class 

```
>>> from sklearn.svm import SVC
>>> from sklearn.preprocessing import StandardScaler
>>> from sklearn.datasets import make_classification
>>> from sklearn.model_selection import train_test_split
>>> from sklearn.pipeline import Pipeline
>>> X, y = make_classification(random_state=0)
>>> X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)
>>> pipe = Pipeline([('scaler', StandardScaler()), ('svc', SVC())])
>>> # The pipeline can be used as any other estimator
>>> # and avoids leaking the test set into the train set
>>> pipe.fit(X_train, y_train)
Pipeline(steps=[('scaler', StandardScaler()), ('svc', SVC())])
>>> pipe.score(X_test, y_test)
0.88
```

And you can see in line 8 we define a pipeline object withe a list of tuples that contained the functions you want to use for transform the data. Then in the line 11 we use fit method to train our ML model with some data thaht we import from the dataset of scikit-learn. When the training is done we can use the score method for see what is the probability if we send the data to our model, it wiil send a expected result.; In this case was 0.88, that is, if we send a data to this model there is a 88% of probability that the model returns a correct result.

**How Numpy convert a list in an Array?**

NumPy is the fundamental package for scientific computing in Python. It is a Python library that provides a multidimensional array object. At the core of the NumPy package, is the ndarray object. This encapsulates n-dimensional arrays of homogeneous data types, with many operations being performed in compiled code for performance.

To convert a list to a ```numpy.array``` object we use a method ```numpy.asarray(a)``` and for that ```a``` most be a list,lists of tuples, tuples, tuples of tuples, tuples of lists and ndarrays. There is another optional parameters like dytpe and order but we focussed only in parameter ```a```.
In the next link you will find the code that is disgned to convert a list object to an Array object. 

https://github.com/numpy/numpy/blob/001c1ca1c507ca18aa22742a5ca0b426a3b877e2/numpy/core/_asarray.py

and then when we can create a ```numpy.ndarray``` object from it and this object can have some methods like choose, clip, resize, etc. For more information about the mehtods you can use you can go to this [link](https://numpy.org/doc/stable/reference/generated/numpy.ndarray.html)

[return to index](index.md)