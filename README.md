GRID-SEARCH.JAR
##########################################################

grid-search.jar searches for the best parameters that maximize the performance of a machine learning algorithm. 
The program will output a .txt file with the performances found in each fold for each parameter searched.
The parameters that are found to lead to the best performances are used and a model.bin is returned. This is the best model
learned by the machine learning algorithm.

The grid-search.jar executable performs the following algorithms:

(based on Support Vector Machines)
SVMrank with Linear Kernel - Contains 1 parameter: the c parameter
SVMrank with Non-Linear Kernel - Contains 2 parameters: the c parameter and the g parameter

(based on Neural Networks)
RankNet - Contains 2 parameters: the number of iterations and the number of nodes to be present in the hidden layer

(based on Boosting Theory)
AdaRank - Contains 1 parameter: the number of iterations
RankBoost - Contains 2 parameters: the number of iterations and the threshold for weak candidates

(based on Constraints)
Coordinate Ascent - Contains 2 parameters: the number of random restarts and the number of iterations
 
General example of usage:

java -jar grid-search.jar SVMrankLinear <path> <c_param> <metric> <num_folds>
java -jar grid-search.jar SVMrankNonLinear <path> <c_param> <g_param> <metric> <num_folds>
java -jar grid-search.jar RankNet <path> <epochs_param> <nodes_param> <metric> <num_folds>
java -jar grid-search.jar AdaRank <path> <iterations_param> <metric> <num_folds>
java -jar grid-search.jar RankBoost <path> <iterations_param> <threshold_candidates_param> <metric> <num_folds>
java -jar grid-search.jar Coordinate_Ascent <path> <randomRestarts_param> <iterations_param> <metric> <num_folds>

The metric allowed are:
- MAP
- P@k where k is an integer

To run the examples that I sent you, do the following.

RUN SVMRANK LINEAR KERNEL: train a model that searches for the best parameters until a maximum of 5 in the c parameter
######################################################################

	cd examples
 	java -jar grid-search.jar SVMrankLinear ./example_dataset/SmallRL/SVMLin/ 5 MAP 4 
	

RUN SVMRANK NON LINEAR KERNEL: train a model that searches for the best parameters until a maximum of 2 in the c parameter and 2 in the g parameter
######################################################################

	cd examples
	java -jar grid-search.jar SVMrankNonLinear ./example_dataset/SmallRL/SVMRadial/ 2 2 MAP 4

RUN RANKNET: train a model that searches for the best parameters until a maximum of 10 iterations and at most 2 nodes in the hidden layer
######################################################################

	cd examples
	java -jar grid-search.jar RankNet ./example_dataset/SmallRL/RankNet/ 2 1 MAP 4

RUN ADARANK: train a model that searches for the best parameters until a maximum of 5 iterations
######################################################################

	cd examples
	java -jar grid-search.jar AdaRank ./example_dataset/SmallRL/AdaRank/ 5 MAP 4

RUN RANKBOOST: train a model that searches for the best parameters until a maximum of 5 iterations and at most 2 weak candidates 
######################################################################

	cd examples
	java -jar grid-search.jar RankBoost ./example_dataset/SmallRL/RankBoost/ 2 2 MAP 4

RUN COORDINATE ASCENT: train a model that searches for the best parameters until 5 random restarts and 3 iterations
######################################################################

	cd examples
	java -jar grid-search.jar Coordinate_Ascent ./example_dataset/SmallRL/CoordAsc/ 2 1 MAP 4
	
RUN ADDITIVE GROVES: automatically finds the best parameters
runs a part from the grid search program
Usage: ag_train -t _train_set_ -v _validation_set_ -r _attr_file_ [-a _alpha_value_] [-n _N_value_] [-b _bagging_iterations_] [-s slow|fast|layered] [-i _init_random_] [-c rms|roc]
######################################################################

	./Learning_to_Rank_Algorithms/Additive_Groves/ag_train -t example_dataset/SmallAG/Fold1/trainAG -v example_dataset/SmallAG/Fold1/trainAG -r example_dataset/SmallAG/AGattr_small -s slow
	
	perform this for each fold!
	
