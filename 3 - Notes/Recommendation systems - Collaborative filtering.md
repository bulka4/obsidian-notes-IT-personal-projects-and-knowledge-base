Tags: [[__Machine_Learning]]

# Introduction
Collaborative Filtering is a method for creating a recommendation system ([[Recommendation systems|link]]). 

In this method, we are not looking at items' features, but at items' ratings granted by users. We use here a rating matrix where rows correspond to users, columns corresponds to items and values are rates granted items by users.

We are looking for:
- Similar users - Users which gives similar ratings to items
- Similar items - Which receives similar ratings from all the users

If we find two similar users, then we can recommend to one user items which other user enjoyed.

If we find two similar items, then we can recommend to user items similar to those, which they enjoyed so far.

#MachineLearning 