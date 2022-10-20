# Mental Health Classification of Short Text RNN
 Mental Health tweet dataset - Classification of short texts with Label Correlated Recurrent Neural Network 

# How to Use  
1. Install requirements.txt
2. Download the glove.6B.100d.txt and put it in the same folder 
3. Run clean_data.py to clean data
4. Run original.py to get the baseline result
5. Run the edge.py to get the predict result for each edge
6. Run the enumeration.py to get the predicted result and the accuracy. Our method improves the baseline result by adding the edge info to it, so before running the enumeration.py, make sure you have ran the edge.py and original.py

# Clean_data.py 
Put the train.csv file at the same folder with get_tree.py and clean_data.py. Then run "python clean_data.py "train" 4 1" where sample is the data file name, 4 is the number of top frequent labels we need to keep, and 1 is the number of minimum labels per instance should have. The generated tree structure is stored in the "data/tree_img" folder. There are two imgs in the tree_img folder. Each label of the img with postfix ".digit" is a int number representing the index of the lable.

# Original.py
Original.py is a One-vs-All multi-label model. It consists of the training and prediction processes. There are 4 parameters you need to change according to your data:

"lstm_num", "max_length", and "batchsize" have the same definitions with that of the edge.py.

"dense_num" is the dimensionality of the output of the multi-label classifier which equals to the number of the labels.

"save_data" is a command line argument. In the process of finding the point to stopping the training, you don't need to set the value. Once you find the appropriate number of epochs. You can set the "save_data" to 1 and run the file again to save the predicted results.

run "python original.py _(epoch_num)_ _(save_data)_ _(optimizer_name)_"
- epoch_num: any integer value i.e. 10 
- save_data: 0 or 1 (default = 0)
- Optimizer_name: Neural network optimzer (default = adam)   

# Edge.py
edge.py is a binary classifier for edges. It consists of the training and prediction processes. There are three parameter need to be filled according to the training data info printed by the clean_data.py:

"lstm_num" is the length of the output vector of the LSTM, normally shorter than the "max_length" but bigger than 1.

"max_length" is the max length of the input text we keep. For this parameter I always choose the value bigger than the average length of the training text printed by the clean_data.py.

"batchsize" I always set 32 if the dataset is not very big. 64 or 128 is Ok if the dataset is very big.

"save_data" is a command line argument. In the process of finding the point to stopping the training, you don't need to set the value. Once you find the appropriate number of epochs. You can set the "save_data" to 1 and run the file again to save the predicted results.

run "python edge.py _(epoch_num)_ _(begin_node)_ _(end_node)_ _(save_data)_ _(optimizer_name)_ _(iter_num)_"
- epoch_num: any integer value i.e. 10 
- begin_node: beginning node i.e. edge 
- end_node: edning node i.e. edge 
- save_data: 0 or 1 (default = 0)
- Optimizer_name: Neural network optimzer (default = adam) 
- iter_num: the code will run n times and select the best one as final result (default = 1)

# Enumeration.py
enumeration.py does the inference. There are two parameters you need to change according to the data:

"edge_list" is a list of the edges which are listed in your "data/store" folder. If your "data/store" folder has a list of edges: l0_l1, l0_l2, l0_l3, then you can fill the edge_list with [(0, 1), (0, 2), (0, 3)].

"total_num" is the number of the test instances.

run "python enumeration.py _(upper_bound)_
- upper_bound: 0: use the predicted edge info, 1: use the true edge info to calculate the upper bound

