# Mental Health Classification of Short Text RNN
 Mental Health tweet dataset - Classification of short texts with Label Correlated Recurrent Neural Network 

# How to Use  
1. Download the glove.6B.100d.txt and put it in the same folder 
2. Run clean_data.py to clean data
3. Run original.py to get the baseline result
4. Run the edge.py to get the predict result for each edge
5. Run the enumeration.py to get the predicted result and the accuracy. Our method improves the baseline result by adding the edge info to it, so before running the enumeration.py, make sure you have ran the edge.py and original.py

# Clean_data.py 
Put the train.csv file at the same folder with get_tree.py and clean_data.py. Then run "python clean_data.py "train" 4 1" where sample is the data file name, 4 is the number of top frequent labels we need to keep, and 1 is the number of minimum labels per instance should have. The generated tree structure is stored in the "data/tree_img" folder. There are two imgs in the tree_img folder. Each label of the img with postfix ".digit" is a int number representing the index of the lable.

# Original.py
Original.py is a One-vs-All multi-label model. It consists of the training and prediction processes. There are 4 parameters you need to change according to your data:

"lstm_num", "max_length", and "batchsize" have the same definitions with that of the edge.py.

"dense_num" is the dimensionality of the output of the multi-label classifier which equals to the number of the labels.

"save_data" is a command line argument. In the process of finding the point to stopping the training, you don't need to set the value. Once you find the appropriate number of epochs. You can set the "save_data" to 1 and run the file again to save the predicted results.

run "python original.py _(epoch_num)_ _(save_data)_ _(optimizer_name)_
- epoch_num: any integer value i.e. 10 
- save_data: 0 or 1 (default = 0)
- Optimizer_name: Neural network optimzer (default = adam)   
