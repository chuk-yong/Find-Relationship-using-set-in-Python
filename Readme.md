# Find relationships using set() in Python

To determind if there is a relationship between to entity, we use intersection of 2 sets:

![Intersection of two sets](set.jpg "Intersection of two sets")

in Python, this can be accomplished by:

a = list(A)  
b = list(B)

c = set(a).intersection(b)  
c is a list containinglemenst in the intersection.


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

## Implementation and much better ways
My implementation of the method applying to Shoppee Code Challenge 2021: Multi-channel contacts: shoppee_walk.py  

Do not run the code as it is very, very slow.

Information about this challenge can be found at: https://www.kaggle.com/c/scl-2021-da

### A much much better implementation: Using Dictionary!
As submitted yeogaa: https://www.kaggle.com/yeogaa/multi-channel-contacts-0-953-15-sec

By combining set and dictinary, you can skip many of the pitfalls using list to compare and find attributes that make up a relationship.  The code showed an expert use of these properties to complete the task beautifully and swiftly.

So, build a dictionary with Email, Phone and ContactId as the keys and Id as the value.  So now the starting relationship map looks like:

{'Email1': {A,B}, 'Phone123':{B,C}, 'ContactId45678':{C,D}....}

Now, we have relationship maps built based on same email, same phone number and same ContactId.  

Next, iterate over the keys and finding the intersection of the values to extract relatioship map.

rel_map ={}


First key is 'Email1', get the value to cur_map = {A,B} -- iterate over A,B

Is A in the rel_map? No -- add to rel_map
rel_map = {'A':{A,B}}
Is B in the rel_map? No -- add to rel_map
rel_map = {'B':{A,B}}

Second key is 'Phone123', get the value to cur_map = {B,C} -- iterate  
Is B in rel_map?  Yes, update cur_map  
cur_map.update(rel_map['B']) --> cur_map = {B,C,A}
Is C in rel_map? No -- add to rel_map
rel_map = {'A':{A,B}, 'B':{A,B}, 'C':{B,C,A}}
with cur_map update all in the list to produce:
rel_map = {'A':{B,C,A}, 'B':{B,C,A}, 'C':{B,C,A}}

## Other takeaways
Doing this on Python and Pandas is quite different from R.  

R is purpose-built for dealing with data frames/tables.  Python is general purpose computing tool that just happens to have Pandas to deal with Data Frame.  Reading from dataframe very inefficient and also many times, when you extract or subset a row or column, it returns a completely different animals -- np array, pd series.  How to add a list to a cell?  use data.at()?! What is that?

For ML tasks like data cleaning, pre-processing, transformation and statistical analysis, it is probably better to stick with R.  However, Python is so very convenient with online tools like colab, makes it so easy to work on the project from anywhere.    





