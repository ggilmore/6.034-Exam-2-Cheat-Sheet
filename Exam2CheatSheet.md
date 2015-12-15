\newenvironment{dummy}{}{}

#6.034 Exam 2 Cheat Sheet


##Identification Trees

Use training data to determine series of tests that determine classification

###How to Build an ID tree - Steps

1. Partition data into groups based on the value of a particular feature

2. Choose test with the lowest disorder

$$
\text{Average Disorder} = \sum_{b \in \text{ branches}} \frac{\text{\# of training points in } b}{\text{total \# of training points}} \times \text{Disorder}(b)
$$

$$
\text{Disorder}(b) = - \sum_{y \in \text{ classifications}} \frac{\text{\# of training points in }y}{\text{\# of training points in }b} \log_2{(\frac{\text{\# of training points in }y}{\text{\# of training points in }b})}
$$

3. Keep doing this until all the training points are correctly classified

###Notes

- more complex trees could be a sign of over fitting
    - or, tests rely too much on outliers to classify data

- within the same subtree, don't use the same test twice

\begin{dummy}
\Tree [.X [.\text{...} ] [.Y [.\text{...} Y ] ] ]
\end{dummy}

$Y$ doesn't give you any new information

- however, the following is perfectly fine

\begin{dummy}
\Tree [.X Y Y ]
\end{dummy}

- (one branch) - this is the same basically as not running a test (should never occur)

\begin{dummy}
\Tree [.\text{...} [.X [.\text{...} ] ]]
\end{dummy}

##$K$ Nearest Neighbors

__Training__ – Store all feature vectors in the training set, along with each class label.

__Prediction__ – Given a query feature vector, find “nearest” stored feature vector and return the associated class.

__1-NN__: Given an unknown point, pick the closest 1 neighbor by some distance measure.
Class of the unknown is the 1-nearest neighbor's label.


__k-NN__: Given an unknown, pick the k closest neighbors by some distance function.
Class of unknown is the mode of the $k$-nearest neighbor's labels.
_$k$ is usually an odd number to facilitate tie breaking_.

__Normalization:__ To separate values clustered close together, divide by the standard deviation


__Relevant features:__ All features are used; to find relevant ones, have to cross-validate, dropping features out.

__What’s the k?:__ Can find best value using cross-validation
Voting for vectors? $k$-Nearest Neighbors votes on class for query feature vector; reduces sensitivity to noise

$k$-NN fixes a set of decision boundaries for whether a point is/is not in a given class.

###Distance Metrics

__Euclidean Distance (common)__

$$
D(\vec{w}, \vec{v}) = \sqrt{\sum_{i}^{n}(w_i -v_i)^2}
$$

__Manhattan Distance (Block distance)__
- Sum of distances in each dimension
$$
D(\vec{w}, \vec{v}) = \sqrt{\sum_{i}^{n}\mid w_i -v_i \mid }
$$

__Hamming Distance (for non-numerical data)__
- Sum of differences in each dimension

$$
D(\vec{w}, \vec{v}) = \sqrt{\sum_{i}^{n} I(w_i, v_i)}
$$

$$
I(x,y) = \begin{cases}
  1 & \mbox{if } \text{different} \\
  0 & \mbox{if } \text{identifical}
\end{cases}
$$

__Cosine Similarity__
- Used in Text classification; words are dimensions;
documents are vectors of words; vector component is
$1$ if word $i$ exists.

$$
D(\vec{w}, \vec{v}) = \frac{\vec{w} \cdot \vec{v}}{\mid \vec{w} \mid \mid \vec{v} \mid} = \cos(\theta)
$$

###Drawing Decision Boundaries

![Decision Boundaries - 1](drawingdecisionboundaries1.pdf)\

![Decision Boundaries - 2](drawingdecisionboundaries2.pdf)\

##Constraint Propagation

![Constraint Propagation - 1](6034-constraint-1.pdf)\

![Constraint Propagation - 2](6034-constraint-2.pdf)\ 

###Various Notes

- backtracking in all 4 domains

- usually it's a decent idea to try to start with the most constrained variable first, or the variable with the smallest domain

- amount of backtracking in Prop-Any $\leq$ amount of backtracking in DFS

- amount of variable assignments in Prop-Any $\leq$ amount of variable assignments in DFS
