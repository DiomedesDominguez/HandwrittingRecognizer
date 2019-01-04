# HandwrittingRecognizer

A C# Machine Learning application that can recognize handwritten digits like these:

![alt text][handwritting]

This ML application is based in the MNIST database of handwritten digits. Has a training set of 60,000 examples, and a test set of 10,000 examples.

## Algorithm used
The trainer uses the RMSProp algorithm. RMSprop is notorious for not being introduced as a publication, while still being well-known and implemented in deep learning libraries. The first google search result I see when I search for it is the slides from an undergraduate course led by Geoff Hinton, which actually get citations when people refer to it in the literature. These slides go a long way in providing intuition for the idea, and I won't be able to explain it better myself, but I can compress much of the idea into a paragraph

Rather than having just a global, scalar learning rate, we have a vector of learning rates for each trainable parameter. It is iteratively updated with a running average of magnitudes of squares of previous gradients. Changes to the weights during training are now not purely in the direction of the gradient, but rather in the direction of the elementwise division of the gradient by this vector you are maintaining. This may seem weird, but remember that the gradient descent family is a robust group of algorithms, and that the first order gradient is imperfect anyway because we usually don't use higher-order curvature (for high-capacity architectures it is infeasible). There may be more sophisticated justifications for RMSprop, but what I can tell you from my experience is trying to do new or weird things with neural network architectures can lead to gradients whose elemen span many orders of magnitude and “blow up”. Gradient clipping is a well-known way of handling this problem, but RMSprop feels at least a bit more principled.

My best results:
![alt text][results]

[handwritting]: https://raw.githubusercontent.com/DiomedesDominguez/HandwrittingRecognizer/master/handwritting.PNG
[results]: https://raw.githubusercontent.com/DiomedesDominguez/HandwrittingRecognizer/master/Results.PNG

## Machine used for training

I used an Azure Virtual Machine with this configuration:

CPU

	Intel(R) Xeon(R) CPU E5-2673 v4 @ 2.30GHz

	Maximum speed:	2.29 GHz
	Sockets:	1
	Cores:	4
	Logical processors:	8
	Virtualization:	Enabled
	L1 cache:	256 KB
	L2 cache:	1.0 MB
	L3 cache:	200 MB

Memory

	64.0 GB
