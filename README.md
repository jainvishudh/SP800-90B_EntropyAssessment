# SP800-90B_EntropyAssessment

Cryptographic random bit generators (RBGs), also known as random number generators (RNGs), require a noise source that produces numerical outputs with some level unpredictability, measured by min-entropy. 
The SP800-90B_EntropyAssessment python package implements the min-entropy assessment methods included in the 2012 draft of Special Publication SP 800-90B.

##Basic Usage

There are two main files in this code package: iid_main.py and noniid_main.py. 

##Using iid_main.py
The file iid_main.py calls all of the tests that determine whether or not the input file appears to contain independent and identically distributed (IID) samples, and if so, gives an entropy assessment. 
The program takes three arguments: 
1. datafile: a binary file containing the samples to be tested.
2. bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.
3. number_of_shuffles: number of shuffles for the shuffling tests to determine whether data appears to be IID. Note that too few shuffles will cause IID to fail the tests.
If the program outputs `IID = False`, try increasing number_of_shuffles, or proceed to noniid_main.py.

###Examples
*	An example that fails due to too few shuffles:
	`>python python iid_main.py truerand_4bit.bin 4 1`

	`IID = False`


* The same data passing when more shuffles are added:

	` >python python iid_main.py truerand_4bit.bin 4 10`

	`IID = True
	
	min-entropy = 3.97271
	
	sanity check = PASS`

##Using noniid_main.py
The file noniid_main.py calls all of the min-entropy estimation methods. The program requires two arguments:
1. datafile: a binary file containing the samples to be tested.
2. bits_per_symbol: the number of bits required to represent the largest output symbol from the noise source. E.g., if the largest value is 12, this would be 4.

###Example
*	Non-IID estimators applied to same data as above:

	`> python noniid_main.py truerand_4bit.bin 4`

	`min-entropy = 3.66238
	
	sanity check = PASS`


##More Information
For more information on using this code, such as optional arguments, see the user guide in this repository.
For more information on the estimation methods, see draft SP at (http://csrc.nist.gov/publications/drafts/800-90/draft-sp800-90b.pdf). 
 
## IG for validation testing.
1.	Collect samples from entropy source.  If possible, samples should be consecutive with none skipped or dropped.  If you cannot collect consecutive samples, document what was collected and why.  Samples must be stored in a binary file.  If source outputs 1 ? 8 bit samples, each sample must be in its own byte, if 9 ? 16 bits per sample, use two consecutive bytes, higher-order byte first, etc.