# Dirichlet Distribution and its Processes

This project counts on all the code for generating and plotting Dirichlet distributions and their related processes.
All the code is in: [Python 3](https://www.python.org/download/releases/3.0/) and [GNU Octave](https://www.gnu.org/software/octave/) programming language for scientific computing.

## Getting Started

In order to obtain the code of the project in your local machine,
type git clone, and then paste the URL you copied from this repository.

$ git clone https://github.com/dariodematties/Dirichlet.git

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

Since the code in this repository is written in [GNU Octave](https://www.gnu.org/software/octave/)
which is an interpreted language, you won't need to compile the soft in order to run it.
To run this soft you need to have [GNU Octave](https://www.gnu.org/software/octave/) installed
in your machine and [statistics package](https://octave.sourceforge.io/statistics/index.html).
You also need to have [python3](https://www.python.org/download/releases/3.0/) and the following packages:
numpy, scipy.io, matplotlib.pyplot and from scipy, spatial. 
In order to perform classification tests with Support Vector Machine, you will need to install a package called
[libsvm](https://www.csie.ntu.edu.tw/~cjlin/libsvm/) in your machine.
That's all.

## Running the tests

This repository has a function called Dirichlet\_plots which
produces plots of Beta and Dirichlet distribution with parameter
\alpha.
```
Dirichlet_plots([1 1 1])
Dirichlet_plots([10 10 10])
Dirichlet_plots([10 10 10])
Dirichlet_plots([2 5 25])
Dirichlet_plots([0.2 0.2 0.2])
```

![alt text](./images/dist1.jpg)
![alt text](./images/dist2.jpg)
![alt text](./images/dist3.jpg)
![alt text](./images/dist4.jpg)


The Beta distribution takes the two first
components from \alpha

In order to generate plots from Dirichlet samples generated from the soft
we can use Polya's method in the following way:

```
octave:14> tic(); Plot_Dir_dist_points([10 10 10]',"polya",50,10); toc()
Elapsed time is 1.09946 seconds.
octave:15> figure; tic(); Plot_Dir_dist_points([10 10 10]',"polya",50,100); toc()
Elapsed time is 10.6354 seconds.
octave:16> figure; tic(); Plot_Dir_dist_points([10 10 10]',"polya",50,1000); toc()
Elapsed time is 90.3149 seconds.
octave:17> close all
octave:18>
```
![alt text](./images/polya1.jpg)

If you want to plot samples generated by stick-breaking and Gamma methods
you can run the following script lines.

```
octave:45> tic(); Plot_Dir_dist_points([10 10 10]',"stick",500); toc()
Elapsed time is 1.30562 seconds.
octave:46> tic(); Plot_Dir_dist_points([10 10 10]',"gamm",500); toc()
Elapsed time is 0.860974 seconds.
octave:47>
```
![alt text](./images/stickgamm.jpg)

If you want to plot the statistics generated from a realization from
the Dirichlet process by means of the Chinese restaurant process
you can run the following lines.

```
octave:64> tic(), Plot_Dir_proc_points(1,"chinese",10000); toc()
Elapsed time is 8.75048 seconds.
octave:65> tic(), Plot_Dir_proc_points(10,"chinese",10000); toc()
Elapsed time is 11.2502 seconds.
octave:66> tic(), Plot_Dir_proc_points(100,"chinese",10000); toc()
Elapsed time is 11.8098 seconds.
octave:67> tic(), Plot_Dir_proc_points(1000,"chinese",10000); toc()
Elapsed time is 11.072 seconds.
```

![alt text](./images/chinese1.jpg)
![alt text](./images/chinese2.jpg)
![alt text](./images/chinese3.jpg)
![alt text](./images/chinese4.jpg)

If you want to plot the statistics generated from a realization from
the Dirichlet process by means of the Polya's urn process
you can run the following lines.

First of all, you have to define a lambda function in Octave
in order to specify a distribution over partitions.

```
random_color = @() stdnormal_rnd(1);
```
This lambda function specify a standard normal distribution
over partitions.
Then you can run the following commands in Octave.


```
octave:70> tic(); Plot_Dir_proc_points(1,"polya",10000,random_color); toc()
Elapsed time is 8.88695 seconds.
octave:73> tic(); Plot_Dir_proc_points(10,"polya",10000,random_color); toc()
Elapsed time is 11.351 seconds.
octave:74> tic(); Plot_Dir_proc_points(100,"polya",10000,random_color); toc()
Elapsed time is 11.9943 seconds.
octave:75> tic(); Plot_Dir_proc_points(1000,"polya",10000,random_color); toc()
Elapsed time is 12.299 seconds.

```

![alt text](./images/polyaurn1.jpg)
![alt text](./images/polyaurn2.jpg)
![alt text](./images/polyaurn3.jpg)
![alt text](./images/polyaurn4.jpg)


In order to generate plots of realizations from the Dirichlet process from
the stick-breaking method you have to type the following lines of script code.

```
octave:125> subplot(2,2,1)
octave:126> tic(); Plot_Dir_proc_points(1,"stick",50); toc()
Elapsed time is 0.133269 seconds.
octave:127> subplot(2,2,2)
octave:128> tic(); Plot_Dir_proc_points(5,"stick",50); toc()
Elapsed time is 0.125743 seconds.
octave:129> subplot(2,2,3)
octave:130> tic(); Plot_Dir_proc_points(10,"stick",50); toc()
Elapsed time is 0.395299 seconds.
octave:131> subplot(2,2,4)
octave:132> tic(); Plot_Dir_proc_points(12,"stick",50); toc()
Elapsed time is 0.217011 seconds.
octave:133>
```

![alt text](./images/stickbreaking.jpg)


## Running Clustering Experiments

In the file Test.py make:

```
numberOfTests = 1
numberOfSamples = 1000
addingNoise = True
plotSamples = True
sparsity = 0.99

numberOfProcesses = 1
numberOfDimensions = 2
alpha = 1000.0

randomness = True
``` 

and let everything else as it is.

Then run the following command:

```
python3 Test.py
```

and you will see the following plots:

![alt text](./images/TrainingData.png)
![alt text](./images/InferenceData.png)
![alt text](./images/TestingData.png)
![alt text](./images/NoisySamples.png)
![alt text](./images/DP_Clustering.png)


In order to run the clustering processes by means of
[Self Organizing Maps](https://en.wikipedia.org/wiki/Self-organizing_map),
run the following command.

```
python3 SelfOrganizingMapTest.py
```

Then you can plot the lattice map by means of:

```
octave --no-gui
```
and then,
```
PlotSelfOrganizingMap
```
This program is very bad coded. It is not correctly vectorized, as a result
it could take a long period of time to plot the map.

The plot you should obtain is:

![alt text](./images/SOM_Clustering.png)


When you want to perform classification tests, be sure to delete all .mat remainder files before
and then run the codes Test.py or SelfOrganizingMapTest.py with
the variable numberOfTests equal to the number of files you want to analyze.
Then run:

```
octave --no-gui
```
then


```
libsvm_train(0)
```
for linear kernels or

```
libsvm_train(2)
```
for a non-linear special kind of kernel (see [libsvm documentations](https://www.csie.ntu.edu.tw/~cjlin/papers/guide/guide.pdf)).

Finally run

```
libsvm_test()
```

Such tests will average the accuracy through the number of tests (sample files).

## Other Clustering Method you may try is the Growing Neural Gas.

Run
```
python3 GrowingNeuralGasTest.py
```
and you will obtain the following plots.

This is the initial configuration of the network.

![alt text](./images/GNG_Clustering0.png)

After training we have.

![alt text](./images/GNG_Clustering1.png)

Zooming in...

![alt text](./images/GNG_Clustering2.png)

Zooming in again...

![alt text](./images/GNG_Clustering3.png)



