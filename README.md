# R-DOSNES
DOSNES is a new method to visualize your data.

This is an R implementation of the method.

## Original DOSNES Project Page
http://yaolubrain.github.io/dosnes/

## Original DOSNES Paper
[Doubly Stochastic Neighbor Embedding on Spheres] (http://arxiv.org/abs/1609.01977) <br>
Yao Lu\*, Zhirong Yang\*, Jukka Corander <br>
(*equal contribution)

## How to use?
Here is a simple example. 
``` 
% Generate data and its similarity matrix
X = matrix(runif(10000),100)
D = dist(X)
P = exp(-D)
P = as.matrix(P)

% Normalize the similarity matrix to be doubly stochastic by Sinkhorn-Knopp method
for(i in 1:100) {
    P = P/rowSums(P)
    P = P %*% diag(1/colSums(P))
}


% Run t-SNE with the spherical constraint
Y = tsne_spher(P);

% Normalize Y to have unity radius for visualization
Z = Y/sqrt(rowSums(Y^2))

#visualize on a sphere
library(rgl)
rgl.spheres(c(0,0,0),col="blue",lit=F)
rgl.points(Z)

``` 


