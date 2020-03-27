# Classification and Regression Trees.
CART is represented by binary tree.
#### A node represents a single input variable (X) and a split point on that variable, assuming the variable is numeric. 
#### The leaf nodes (also called terminal nodes) of the tree contain an output variable (y) which is used to make a prediction.
#### Creating a binary decision tree is actually a process of dividing up the input space. A greedy approach is used to divide the space called recursive binary splitting. 
####  Different split points are tried and tested using a cost function. The split with the best cost (lowest cost because we minimize cost) is selected.
#### Regression: cost function is sum of squared errors.
#### Classification: Gini cost function is used. It provides an indication of how pure the nodes are. Node purity mean how mixed the training data assigned to each node is.
#### Splitting continues until nodes contain a minimum number of training examples or a maximum tree depth is reached.

### 1 - Gini Index
#### A Gini score gives an idea of how good a split is by how mixed the classes are in the two groups created by the split. A perfect separation results in a Gini score of 0, whereas the worst case split that results in 50/50 classes in each group result in a Gini score of 0.5 (for a 2 class problem).
#### proportion = count(class_value) / count(rows)
#### Gini is calculated for each child node as follows:

#### gini_index = 1.0 - sum(proportion * proportion)

#### The Gini index for each group must then be weighted by the size of the group, relative to all of the samples in the parent.
#### gini_index = (1.0 - sum(proportion * proportion)) * (group_size/total_samples)

#### The scores are then added across each child node at the split point to give a final Gini score for the split point that can be compared to other candidate split points.

### 2- Create Split
#### 2.1 Split the dataset


#### Splitting a dataset means separating a dataset into two lists of rows given the index of an attribute and a split value for that attribute. Once we have the two groups, we can then use our Gini score above to evaluate the cost of the split.
#### Splitting a dataset involves iterating over each row, checking if the attribute value is below or above the split value and assigning it to the left or right group respectively.
#### 2.2 Evaluate all splits

#### Given a dataset, we must check every value on each attribute as a candidate split, evaluate the cost of the split and find the best possible split we could make. Once the best split is found, we can use it as a node in our decision tree. This is an exhaustive and greedy algorithm.
#### When selecting the best split and using it as a new node for the tree we will store the index of the chosen attribute, the value of that attribute by which to split and the two groups of data split by the chosen split point.
#### Below is a function named get_split() that implements this procedure. You can see that it iterates over each attribute (except the class value) and then each value for that attribute, splitting and evaluating splits as it goes.
### 3 - Built a tree
#### Terminal Nodes
#### Recursive Splitting
#### Building a Tree

#### 3.1 Terminal nodes: we need to decide when to stop growing the tree.
     Max tree depth
     Min node record
     
#### Now we have some ideas of when to stop growing the tree. When we do stop growing at a given point, that node is called a terminal node and is used to make a final prediction. This is done by taking the group of rows assigned to that node and selecting the most common class value in the group. This will be used to make predictions.
#### 3.2 Recursive splitting
#### We know how and when to create terminal nodes, now we can build our tree.
#### New nodes added to an existing node are called child nodes. A node may have zero children (a terminal node), one child (one side makes a prediction directly) or two child nodes. 
#### Once a node is created, we can create child nodes recursively on each group of data from the split by calling the same function again.

##### 1 - Firstly, the two groups of data split by the node are extracted for use and deleted from the node. As we work on these groups the node no longer requires access to these data.
##### 2 - Next, we check if either left or right group of rows is empty and if so we create a terminal node using what records we do have.
##### 3 -We then check if we have reached our maximum depth and if so we create a terminal node.
##### 4 -We then process the left child, creating a terminal node if the group of rows is too small, otherwise creating and adding the left node in a depth first fashion until the bottom of the tree is reached on this branch.
##### 5 - The right side is then processed in the same manner, as we rise back up the constructed tree to the root.
#### 3.3 Building a tree
#### Building the tree involves creating the root node and calling the split() function that then calls itself recursively to build out the whole tree.
### 4-Make a Prediction

### References

#### https://machinelearningmastery.com/implement-decision-tree-algorithm-scratch-python/
#### https://towardsdatascience.com/decision-tree-from-scratch-in-python-46e99dfea775
#### https://towardsdatascience.com/random-forests-and-decision-trees-from-scratch-in-python-3e4fa5ae4249
#### Data Science from Scratch
