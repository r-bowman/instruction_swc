
# Programming with Python

Python is a versatile programming language. Programming languages can be divided along many lines, but in particular, Python is considered a high-level programming software. This is opposed to low-level languages like Machine code or assembly. The difference is readability or what the user input commands look like for the computer to process. Machine-code is usually decimal, octal or hexidecimal sets which get converted to binary. Python uses language that is much more human-readable.

Python is a valuable tool for researchers as well because it provides methods to create tools that you might use over and over as well as evaluate and visualize data sets.

We will run through a lot of information and techniques today, but by the end we don't expect you to be experts or remember everything, we only want to give you a firm grasp of the basics and some experience using the programs.

## Analyzing Patient Data

Python also incoporates tools that are designed to make our lives easier, called _libraries_.

One way to think about libraries is as a bookshelf full of books. In a real world library, books are grouped together by a common theme. Python libraries are similar in that they are collections of tools based around a common theme.

Lets import a library now

Type:
>import numpy

and press Shift + Enter


```python
import numpy
```

Numpy is a python library that contains lots of tools that deal with manipulating numbers. Now that we have our library imported, lets take a look at our data.

_(While typing)First we call on our library numpy, then we call on the loadtxt function in that library. Loadtxt requires some input, so we're going to give it a filename using the fname parameter. Inflammation-01.csv is a comma seperated value file, which means that it is a series of data seperated by commas. The loadtxt function also needs to know how our data is seperated so we're going to feed it the delimiter parameter as well._

Type:
>numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

and press Shift + Enter


```python
numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
```




    array([[ 0.,  0.,  1., ...,  3.,  0.,  0.],
           [ 0.,  1.,  2., ...,  1.,  0.,  1.],
           [ 0.,  1.,  1., ...,  2.,  1.,  1.],
           ..., 
           [ 0.,  1.,  1., ...,  1.,  1.,  1.],
           [ 0.,  0.,  0., ...,  0.,  2.,  0.],
           [ 0.,  0.,  1., ...,  1.,  1.,  0.]])



So we can now see our dataset. However, we still cannot really begin to work with this data. Entering the command like we did let us see the data, but the computer has not stored it for us to manipulate yet. To do that we need to load the file into a variable. Before that lets go over variables and how they can be used and manipulated. 

Variables are simply a placeholder or name that can be used to store data. Python’s variables must begin with a letter and are case sensitive. Lets create a variable weight_kg and assign it 55 for a value.

Type:
>weight_kg=55

and press Shift + Enter


```python
weight_kg=55.0
```

Similar to what you've seen in bash, sometimes running a command returns no output, but that doesn't mean it didn't work, and actually it usually means it did work.

Lets print the value of our variable to check:

Type:
>print(weight_kg)

and press Shift + Enter


```python
print(weight_kg)
```

    55.0
    

Now we have a variable and it has a value, lets work with it.

Assume that you want to know the weight of an object in pounds instead of kilograms. Lets convert it using arithmatic.

Type:
>print('weight in pounds:', 2.2 * weight_kg)

and press Shift + Enter


```python
print('weight in pounds:', 2.2 * weight_kg)
```

    weight in pounds: 121.00000000000001
    

You can type multiple lines in a single cell by pressing Enter without holding shift. Remeber multiple lines only use Enter, to run a cell use Shift + Enter. Now lets change our variable's value. 

Type:
>weight_kg = 57.5

>print('weight in kilograms is now:', weight_kg)

and press Shift + Enter


```python
weight_kg = 57.5
print('weight in kilograms is now:', weight_kg)
```

    weight in kilograms is now: 57.5
    

Variables only remember their value. Even if that value is generated with a mathematical equation, only the end result is retained. To demonstrate this, lets creat a variable called weight_lb and assign it's value using an equation.

Type:
>weight_lb = (2.2 * weight_kg)

>print('weight in kilograms:', weight_kg, ' and in pounds:' weight_lb)

and press Shift + Enter


```python
weight_lb = (2.2 * weight_kg)
print('weight in kilograms:', weight_kg, 'and in pounds:', weight_lb)
```

    weight in kilograms: 57.5 and in pounds: 126.50000000000001
    

Now according to our output, weight_kg is 57.5 and weight_lb is 126.5. The key take away is that the value for weight_lb is 126.5, not (2.2 * weight_kg). Weight_lb doesn't care where it's information came from, it only cares about its final value of 126.5. Lets test this by changing the value of weight_kg again.

Type:
>weight_kg = 100.0

>print('weight in kilograms is now:', weight_kg, ' and in weight in pounds is still:' weight_lb)

and press Shift + Enter


```python
weight_kg = 100.0
print('weight in kilograms is now:', weight_kg, ' and in weight in pounds is still:', weight_lb)
```

    weight in kilograms is now: 100.0  and in weight in pounds is still: 126.50000000000001
    

## Who's Who in Memory

At this point we've only entered a couple of variables, but in your work you may have a number of variables. If you're unsure or would like to know what variables you have, there is a helpful python command for that.

Type:
>%whos

and press Shift + Enter


```python
%whos
```

    Variable    Type      Data/Info
    -------------------------------
    numpy       module    <module 'numpy' from 'C:\<...>ges\\numpy\\__init__.py'>
    weight_kg   float     100.0
    weight_lb   float     126.50000000000001
    

Variables can hold different types of data from a single value like we used above to an array. Lets store our data set from the file into a variable so we can begin to work with it.

Type:
>data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

and press Shift + Enter


```python
data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
```

Lets verify that our data has been loaded by printing the variable value.

Type:
>print(data)

and press Shift + Enter


```python
print(data)
```

    [[ 0.  0.  1. ...,  3.  0.  0.]
     [ 0.  1.  2. ...,  1.  0.  1.]
     [ 0.  1.  1. ...,  2.  1.  1.]
     ..., 
     [ 0.  1.  1. ...,  1.  1.  1.]
     [ 0.  0.  0. ...,  0.  2.  0.]
     [ 0.  0.  1. ...,  1.  1.  0.]]
    

Now we can work with this data in earnest, lets determine the class of data stored in our variable.

Type:
>print(type(data))

and press Shift + Enter


```python
print(type(data))
```

    <class 'numpy.ndarray'>
    

The data in our variable 'data' is classified as an N-dimensional array, or an array composed of rows and columns.

## Data Type

There are a number of other attributes we can learn about our data. Lets see what the type of data is in our data set.

Type:
>print(data.dtype)

and press Shift + Enter


```python
print(data.dtype)
```

    float64
    

What this tells us is that the values in our files are floats, or approximate real numbers. We can also determine the shape of our array.

Type:
>print(data.shape)

and press Shift + Enter


```python
print(data.shape)
```

    (60, 40)
    

This tells us that the data has sixty rows and forty columns. We can also pull out a single point of data from the array.


