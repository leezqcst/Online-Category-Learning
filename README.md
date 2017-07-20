 # Online Category-learning and Classification 

### Overview

The following is an outline for an unsupervised machine-learning algorithm that classifies and adapts to input patterns in real-time. It uses two main steps to accomplish this: First, a probability density function is approximated according to a collection of samples. Second, a category is assigned to each new sample with respect to its point on the probability space.

More generally, a multidimensional probability space is generated from on a set of previous observations, and used to comprehend and interpret each incoming observation. A sample represents a point, and the specific location of the point determines how it is classified. A gradient ascent algorithm is used to traverse the space from each sample point to a maximum, resulting in a feasible category estimation for the sample.

Online learning provides a method of optimization in real-time, enabling one to adapt to environmental changes, indefinitely. A number of problems are introduced however, particularly the need for a process which disposes of irrelevant data in order to make room for important information. This is not only important when useless information is learned, but also (and perhaps more importantly) when previously-relevant information is not longer useful. In each case, the irrelevant information must be filtered out or forgotten, such that the finite memory accessible to a system at any given time is being used as efficiently as possible.
	
When a sample is received, a Gaussian function is multiplied by a learning rate and added to the space surrounding the sample point. Each non-zero point on the space gradually approaches zero, such that any point is reduced back to zero unless it “grows’ via sampling at a faster rate than it “decays”. The decay rate at any given point has a negative correlation with the absolute value at that point. In other words, a high-density area will decay slower than a low-density area, and is preserved more strongly and for a longer period of time than a low-density area. This causes the system to effectively “forget” the less relevant information, thus resolving the optimization problem stated above.

![Density Estimation](https://github.com/CarsonScott/Online-Category-Learning/blob/master/img/Density%20approximation.PNG)

### Examples

The probability space and its derivatives are used to identify the subspaces that represent features or classes, as well as the boundaries between them. Classees are learned based on the relative frequency of a sample at any given time being an instance of that class. Therefore the goal is to generate a space of simple boundary points our lines.

The sample set was generated by choosing 1000 random values between 0 and 100. Each time a new value is selected, there's a moderate chance that instead of choosing bewteen 0 and 100 and random, we i select an element from a subset of values, which represent 'attractors', or states that the system tends toward. In other words, an attractor has a geeater probability of being chosen at any given time than any one of the non-attractor values.

##### Attractors: {7, 54, 87}

![Probability Space](https://github.com/CarsonScott/Online-Category-Learning/blob/master/img/Probability%20Space.PNG)

This cannot be done efficiently without some intermediate step, and in this case that deals with converting a probability space into a binary space, given a function that takes a subset of the probability space at any given time and returns the local variance passed through a threshold.

![Normed Probability Space](https://github.com/CarsonScott/Online-Category-Learning/blob/master/img/Probability%20Space%20(Normed).PNG)

Finally, the binary space is transformed into a sparse array that reperesents boundary points between classes. The derivative is used to assign a given sample to a class, with respect to  boundaries that seperate it from the rest of the space. Instances of a given class are detected when a sample point is between the boundaries that define said class. 

![Feature Space](https://github.com/CarsonScott/Online-Category-Learning/blob/master/img/Feature%20Space.PNG)
