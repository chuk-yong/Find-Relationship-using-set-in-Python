# Find relationships using set() in Python
Shoppee Challenge Code Challenge 2021 - Multichannel Contacts

To determind if there is a relationship between to entity, we use intersection of 2 sets:

![Intersection of two sets](set.jpg "Intersection of two sets")

in Python, this can be accomplished by:

a = list(A)  
b = list(B)

c = set(a).intersection(b)  
c is a list containing the element in the intersection.

Note: In the code, check for '' as it means empty and should not be interpreted as a match.

There are many caveats in dealing with Pandas dataframe that I found out (I am a R user), some of them would sound trivial to regular Pandas users but these don't make sense:

1. Using .at[] to allocate a list to a cell.  data.iloc[] = [...] does not work.
2. df.data[].copy to make a copy of a datframe you subset or Pandas will consider it a slice of the dataframe.  df=data.['a','b'] is a slice of data.

## Building our relationship map

Do refer to the pdf from the code challenge for details.

### We start with A and found B.  
Build a relationship map (using a list). In the code, a column was created to contain this list.
A_related means Id=A and column = "related".  In our dataframe, Id and rows are the same.

A_related = [A,B]  
B_related = [A,B]

### Next, with B, going down the list and found C.  
The relationship list should add this new relationship and looks like:
B_related = [A,B, B,C]  
To make the list unique and sort we do: sorted(set(B_related))

B_related = [A,B,C]

This may not be optimised, but I went with updating all the members (A,B and C) with the newly created list and updated the relationship status. So now:
A_related = [A,B,C]  
B_related = [A,B,C]  
C_related = [A,B,C]

### Now, with C, going down the list and found D
The new relationship list should contain [A,B,C,D] for all (A,B,C,D):
A_related = [A,B,C,D]  
B_related = [A,B,C,D]  
C_related = [A,B,C,D]  
D_related = [A,B,C,D]

## Caveat in running the code
It is not optimised!  So running it will take a long time.  
Set the nrow value and subset the data accordingly.  e.g.  nrow =1000 and then subset the data to get rows 0-999 will run the code over first 1000 rows to see what the output looks like.  It should contains only paired relationships.  It is possible to find multiple relationship if nrow ~ 10,000

