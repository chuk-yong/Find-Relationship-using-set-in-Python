# Find relationships using set() in Python

To determind if there is a relationship between to entity, we use intersection of 2 sets:

![Intersection of two sets](set.jpg "Intersection of two sets")

in Python, this can be accomplished by:

a = list(A)  
b = list(B)

c = set(a).intersection(b)  
c is a list containing the element in the intersection.


## Building our relationship map by visiting

### We start with A, visit everyone down the list.  Found B.

We can create a relationship map as follows:

A_related = [A,B]  
B_related = [A,B]

### Next, with B, going down the list and found C.

The relationship list should add this new relationship and looks like:

B_related = [A,B, B,C]

To make the list unique and sort we do: sorted(set(B_related))

B_related = [A,B,C]

With this new found list, we should go update everyone in the list so that:

A_related = [A,B,C]  
B_related = [A,B,C]  
C_related = [A,B,C]

### Now, with C, going down the list and found D
The new relationship list should contain [A,B,C,D] for all members in A,B,C and D:  
A_related = [A,B,C,D]  
B_related = [A,B,C,D]  
C_related = [A,B,C,D]  
D_related = [A,B,C,D]

