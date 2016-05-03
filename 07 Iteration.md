Chapter 7  Iteration
====================

This chapter is about iteration, which is the ability to run a block of statements repeatedly. We saw a kind of iteration, using recursion, in Section 5.8. We saw another kind, using a <code>for</code> loop, in Section 4.2. In this chapter we’ll see yet another kind, using a <code>while</code> statement. But first I want to say a little more about variable assignment.
7.1  Reassignment
-----------------

As you may have discovered, it is legal to make more than one assignment to the same variable. A new assignment makes an existing variable refer to a new value (and stop referring to the old value).

<pre>
>>> x = 5
>>> x
5
>>> x = 7
>>> x
7
</pre>
The first time we display x, its value is 5; the second time, its value is 7.
Figure 7.1 shows what **reassignment** looks like in a state diagram.

![State diagram.](http://greenteapress.com/thinkpython2/html/thinkpython2008.png "Figure 7.1: State diagram.")

At this point I want to address a common source of confusion. Because Python uses the equal sign (=) for assignment, it is tempting to interpret a statement like <code>a = b</code> as a mathematical proposition of equality; that is, the claim that <code>a</code> and <code>b</code> are equal. But this interpretation is wrong.

First, equality is a symmetric relationship and assignment is not. For example, in mathematics, if *a*=7 then 7=*a*. But in Python, the statement <code>a = 7</code> is legal and <code>7 = a</code> is not.

Also, in mathematics, a proposition of equality is either true or false for all time. If *a=b* now, then *a* will always equal *b*. In Python, an assignment statement can make two variables equal, but they don’t have to stay that way:
<pre>
>>> a = 5
>>> b = a    # a and b are now equal
>>> a = 3    # a and b are no longer equal
>>> b
5
</pre>
The third line changes the value of <code>a</code> but does not change the value of <code>b</code>, so they are no longer equal.
Reassigning variables is often useful, but you should use it with caution. If the values of variables change frequently, it can make the code difficult to read and debug.
7.2  Updating variables
-----------------------
A common kind of reassignment is an update, where the new value of the variable depends on the old.
<pre>
>>> x = x + 1
</pre>
This means “get the current value of <code>x</code>, add one, and then update <code>x</code> with the new value.”
If you try to update a variable that doesn’t exist, you get an error, because Python evaluates the right side before it assigns a value to x:
<pre>
>>> x = x + 1
NameError: name 'x' is not defined
</pre>
Before you can update a variable, you have to **initialize** it, usually with a simple assignment:
<pre>
>>> x = 0
>>> x = x + 1
</pre>
Updating a variable by adding 1 is called an **increment**; subtracting 1 is called a **decrement**.
