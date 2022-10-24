
# Link Prediction with Pytorch GCN  
In this repository, I use PyG to predict the existence of an edge between every two nodes.   
I use the karate club dataset. It is a small social network dataset. This repository is mainly for teaching the link prediction task with PyG GCN. 
# Data Splitting to test and train set. 
As I explained in node classification for the karate club dataset, we can use a trainable embedding as node features, X.   
I make the data of 34 nodes and a trainable embedding vector of size=5 for each node. I use edge indices in the networkx karate club dataset. 
After preparing the dataset I use the command "RandomLinkSplit" to split data to train and test. I considered no validation for this project. 
# Analysis of train and test data   
I used the networkx draw command to visualize the train and test set of this dataset.   
In fact, link prediction is an edge classification task here. When using the RandomLinkSplit, the present edges are labeled as 1 and some edges are added which are labeled as zero. These zero edges do not exist in the original dataset. Then the collection of two labeled edges is splitted to test and train.  
You can see that edges with 0 labels are pink and edges with label 1 are black. 
![image](https://user-images.githubusercontent.com/67642255/197508731-ecd5bdc5-3c7e-4243-ac45-5ab5b9dd8671.png)

# Model   
The model consists of two parts. 
In the first part, we derive the embedding of all nodes. 
In the second part, we concatenate the derived embedding of the source and target nodes of each edge and then I feed it to a linear layer.  Then the output would be the label of that edge.   
Note that in some projects, we compute the inner product of the source and target node embedding. This is how we calculate the similarity of two nodes to form an edge between them. Then we use this value and a sigmoid function to predict the label of the edge.   
# Train the model.  
For training the model, we should consider an important thing. 
We only use those edges in the train set for deriving the node embeddings which have a label 1. I specified them as pos_edge_index. 
Some people split the data to train and test without considering the edge with label 0 in the train set. After training the z, they add edges with the label 0 by using NegativeSampling command. I am not sure it is the best idea since we may consider an edge with 0 labels in both the train and test sets. 
After training the model I showed the result using an animation. In the following animation, the wrong predictions are shown with red edges, true label 1 edges are black and true label 0 edges are pale turquoise. 


