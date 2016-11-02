
# Programming with Python

Python is a versatile programming language. Programming languages can be divided along many lines, but in particular, Python is considered a high-level programming software. This is opposed to low-level languages like Machine code or assembly. The difference is readability or what the user input commands look like for the computer to process. Machine-code is usually decimal, octal or hexidecimal sets which get converted to binary. Python uses language that is much more human-readable.

Python is a valuable tool for researchers as well because it provides methods to create tools that you might use over and over as well as evaluate and visualize data sets.

We will run through a lot of information and techniques today, but by the end we don't expect you to be experts or remember everything, we only want to give you a firm grasp of the basics and some experience using the programs.

## Analyzing Patient Data

In this lesson we are going to work with a set of files that contain the record of patients' daily level of inflammation.

Python also incoporates tools that are designed to make our lives easier, called _libraries_.

One way to think about libraries is as a bookshelf full of books. In a real world library, books are grouped together by a common theme. Python libraries are similar in that they are collections of tools based around a common theme.

Lets import a library now

Type:
>import numpy

and press Shift + Enter


```python

```

Numpy is a python library that contains lots of tools that deal with manipulating numbers. Now that we have our library imported, lets take a look at our data.

_(While typing)First we call on our library numpy, then we call on the loadtxt function in that library. Loadtxt requires some input, so we're going to give it a filename using the fname parameter. Inflammation-01.csv is a comma seperated value file, which means that it is a series of data seperated by commas. The loadtxt function also needs to know how our data is seperated so we're going to feed it the delimiter parameter as well._

Type:
>numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

and press Shift + Enter


```python

```

So we can now see our dataset. However, we still cannot really begin to work with this data. Entering the command like we did let us see the data, but the computer has not stored it for us to manipulate yet. To do that we need to load the file into a variable. Before that lets go over variables and how they can be used and manipulated. 

Variables are simply a placeholder or name that can be used to store data. Python’s variables must begin with a letter and are case sensitive. Lets create a variable weight_kg and assign it 55 for a value.

Type:
>weight_kg=55

and press Shift + Enter


```python

```

Similar to what you've seen in bash, sometimes running a command returns no output, but that doesn't mean it didn't work, and actually it usually means it did work.

Lets print the value of our variable to check:

Type:
>print(weight_kg)

and press Shift + Enter


```python

```

Now we have a variable and it has a value, lets work with it.

Assume that you want to know the weight of an object in pounds instead of kilograms. Lets convert it using arithmatic.

Type:
>print('weight in pounds:', 2.2 * weight_kg)

and press Shift + Enter


```python

```

You can type multiple lines in a single cell by pressing Enter without holding shift. Remeber multiple lines only use Enter, to run a cell use Shift + Enter. Now lets change our variable's value. 

Type:
>weight_kg = 57.5

>print('weight in kilograms is now:', weight_kg)

and press Shift + Enter


```python

```

Variables only remember their value. Even if that value is generated with a mathematical equation, only the end result is retained. To demonstrate this, lets creat a variable called weight_lb and assign it's value using an equation.

Type:
>weight_lb = (2.2 * weight_kg)

>print('weight in kilograms:', weight_kg, ' and in pounds:' weight_lb)


```python

```

Now according to our output, weight_kg is 57.5 and weight_lb is 126.5. The key take away is that the value for weight_lb is 126.5, not (2.2 * weight_kg). Weight_lb doesn't care where it's information came from, it only cares about its final value of 126.5. Lets test this by changing the value of weight_kg again.

Type:
>weight_kg = 100.0

>print('weight in kilograms is now:', weight_kg, ' and in weight in pounds is still:' weight_lb)


```python

```

Lets store our data set from the file into a variable so we can begin to work with it.

Type:
>data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')


```python

```

Lets verify that our data has been loaded by printing the variable value.

Type:
>print(data)


```python

```

Now we can work with this data in earnest, lets determine the class of data stored in our variable.

Type:
>print(type(data))


```python

```

The data in our variable 'data' is classified as an N-dimensional array, or an array composed of rows and columns.

We can also determine the shape of our array.

Type:
>print(data.shape)


```python

```

This tells us that the data has sixty rows and forty columns. We can also pull out a single point of data from the array. 

We're going to pull the first value, but lets discuss a quick caveat. Humans typically count starting with the number 1, so you might assume the first value's coordinates are [1,1], but it's actually [0,0]. Python uses zero-origin for it's arrays. Why you may ponder? Because history. Feel free to ask me after the session, because I too asked. To clarify, if we have a single axis array 'A' with 8 peices of information then the first element is A[0] and the last is A[7]. So an array of this format, with 'N' pieces of data, follows the formula: 0 to N-1

Lets pull the first value from our array.

Type:
>print('first value in data:', data[0,0])


```python

```

Now lets choose a value from the middle.

Type:
>print('middle value in data:', data[30,20])


```python

```

What if we wanted to select a section of data? Lets select the ten colums and first four rows.

Type:
>print(data[0:4, 0:10])


```python

```

We can also select sections without starting from zero.

Type:
>print(data[5:10, 0:10])


```python

```

If you know you're starting from the beginning of a slice, or wish to include the end you can leave out the upper or lower bounds. lets save a small slice into a variable and print it.

Type:
>small = data[:3, 36:]

>print('small is:')

>print(small)


```python

```

We can perform mathematical operations on our data set. Lets create a new data set with the values multiplied times two.

Type:
>doubledata = data * 2.0


```python

```

Lets check this to make sure it did what we wanted.

Type:
>print('original:')

>print(data[:3, 36:])

>print('doubledata:')

>print(doubledata[:3, 36:])


```python

```

We can also perform mathematical operations on more than one array. 

Type:
>tripledata = doubledata + data


```python

```

lets check this as well.

Type:
>print('tripledata:')

>print(tripledata[:3, 36:])


```python

```

Numpy also has more complex operations, forinstance lets find the average value of the dataset.

Type:
>print(numpy.mean(data))


```python

```

Numpy also has other functions that can use an array as an input. You can also set more than one variable or perform several functions on the same line. For example lets get the maximum, minimum and the standard deviation.

Type:
>maxval, minval, stdval = numpy.max(data), numpy.min(data), numpy.std(data)

>print('maximum inflammation:', maxval)

>print('minimum inflammation:', minval)

>print('standard deviation:', stdval)


```python

```

Perhaps we want to look at the values for the first row. Remember Python arrays start with zero, so the first patient is actually: patient 0.

We also want to put in a comment that explains what this code does to remind us later, or perhaps even other researchers, programmers, and others who might review or use this code later. Comments start with the # (pound or hashtag) and are ignored by the computer.

_(While typing) First lets create a variable for patient 0 that contains only the first row and all columns, and then our comment. Finally we will print the maximum inflammation for patient 0._

Type:
>patient_0 = data[0, :] # 0 on the first axis, everything on the second

>print('maximum inflammation for patient 0:', patient_0.max())


```python

```

It might be tedious to create variables for each patient, so lets create a statement that combines the print statement and our function call

Type:
>print('maximum inflammation for patient 2:', numpy.max(data[2, :]))


```python

```

Perhaps we need the maximum for all patients, or the average imflammation by day. Python also allows us to work along a single axis. Lets get the average for each day.

Type:
>print(numpy.mean(data, axis=0))


```python

```

We can even visualize our data directly in our Jupyter notebook by importing another library call 'matplotlib'. By default matplotlib creates images in new windows, but we want them to apper directly in our notebook. Lets make a heatmap of our data set inside the notebook.

_(while typing) First lets import our new library, matplotlib. Then we'll put in a command that makes sure our images appear in the notebook. Finally we instruct the to create the image and tell it to display the image._

Type:
>import matplotlib

>% matplotlib inline

>image = matplotlib.pyplot.imshow(data)

>matplotlib.pyplot.show()


```python

```

Now lets make some line graphs that show some different aspects of our data. First, we'll start with the average inflammation.

_(while typing) Create a variable called ave_inflammation with the value that calls on numpy and then the mean function then we provide the variable data and we want average over time so we're working along the 0 axis. Then we create the linegraph image with our new variable and finally tell it to display the image._

Type:
>ave_inflammation = numpy.mean(data, axis=0)

>ave_plot = matplotlib.pyplot.plot(ave_inflammation)

>matplotlib.pyplot.show()


```python

```

Lets make a linegraph of the maximum inflammation as well, but this time without creating a variable.

_(while typing) This time we want to put the image name in and call on numpy and the max function and then just feed in the data set information directly. Then we tell it to display the graph._

Type:
>max_plot = matplotlib.pyplot.plot(numpy.max(data, axis=0))

>matplotlib.pyplot.show()


```python

```

And lets  get the minimum in the same way.

Type:
>min_plot = matplotlib.pyplot.plot(numpy.min(data, axis=0))

>matplotlib.pyplot.show()


```python

```

Now we're going to take what we've learned and put it all together to create a function that will show us three graphs. We're only going to add a couple of new things here to increase readability. The first element is matplotlib.pyplot.figure(); this creates a special space for us to put our graphs into. Figsize is an element of .figure that helps dictate how large the images will be. Lastly we're going to group our images using subplots. We're also going to pretend we haven't typed anything above this new cell.

_describe steps while typing_

Type:
>import numpy

>import matplotlib.pyplot

>data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

>fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))

>axes1 = fig.add_subplot(1, 3, 1)

>axes2 = fig.add_subplot(1, 3, 2)

>axes3 = fig.add_subplot(1, 3, 3)

>axes1.set_ylabel('average')

>axes1.plot(numpy.mean(data, axis=0))

>axes2.set_ylabel('max')

>axes2.plot(numpy.max(data, axis=0))

>axes3.set_ylabel('min')

>axes3.plot(numpy.min(data, axis=0))

>fig.tight_layout()

>matplotlib.pyplot.show()


```python

```

A bit of humor, if we hadn't told it to use a tight layout...it would have been squished together even more than it is above.
