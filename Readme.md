### A javascript implementation of L-BFGS

The script `lbfgs.js` contains an implementation of the limited-memory BFGS optimizer.
L-BFGS is commonly used for training in supervised Machine Learning tasks.
To use it, call 

    limitedMemoryBFGS(optimizable, parameters);

where `optimizable` is an object that contains two methods, `getValue(parameters)` and `getGradient(parameters, gradient)`.
The first function returns the value of an objective function, such as a log likelihood, given the specified parameter values. 
The second copies the gradient of that objective function at the specified parameters into the array `gradient`.
I found that limiting memory allocations caused the single biggest gain in performance.

This code is based on the implementation in Mallet.
For a trivial example (the two-variable quadratic equation), these implementations produce identical results down to the last available decimal point.

I've included an example of a Maximum Entropy classifier, in `maxent.html`.
Look at the console output (the actual page is not very interesting!) to see the optimizer working.
The tokenization and MaxEnt value/gradient implementations are not the same as Mallet.
Mallet is about two to three times faster, but I suspect that much of this is due to the fact that javascript is not good with int-int maps, so I'm running through document tokens in sequence, rather than as feature-count vectors.
The sample file contains translations of Danish folktales, used with permission by the translator.

The script depends on numeric.js and d3, but mainly for convenience methods, which could be trivially rewritten.
I initially used more convenience functions from numeric.js, but found that it was often substantially faster to write them as for-loops.
The XRegExp library is useful for parsing Unicode regular expressions, and has nothing particular to do with L-BFGS.