7. fejezet Iteráció
===================
Ez a fejezet az iterációról szól, ami egy utasításblokk ismételt végrahajtásának képességét jelenti. Láttunk már példát rekurzióra épülő iterációra a 5.8 fejezetben, és egy másikat, ami a <code>for</code> ciklusra épül, a 4.2 fejezetben. Ebben a fejezetben még egy másfajtával ismerkedünk meg, ami a <code>while</code> utasítást használja. De először szeretnék egy kicsit többet mondani a változó értékadásról.
7.1  Új értékadás
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
7.3  The <code>while</code> statement
------------------------
Computers are often used to automate repetitive tasks. Repeating identical or similar tasks without making errors is something that computers do well and people do poorly. In a computer program, repetition is also called **iteration**.

We have already seen two functions, <code>countdown</code> and <code>print_n</code>, that iterate using recursion. Because iteration is so common, Python provides language features to make it easier. One is the <code>for</code> statement we saw in Section 4.2. We’ll get back to that later.

Another is the <code>while</code> statement. Here is a version of <code>countdown</code> that uses a <code>while</code> statement:
<pre>
def countdown(n):
    while n > 0:
        print(n)
        n = n - 1
    print('Blastoff!')
</pre>
You can almost read the while statement as if it were English. It means, “While n is greater than 0, display the value of n and then decrement n. When you get to 0, display the word Blastoff!”
More formally, here is the flow of execution for a while statement:

Determine whether the condition is true or false.
If false, exit the while statement and continue execution at the next statement.
If the condition is true, run the body and then go back to step 1.
This type of flow is called a loop because the third step loops back around to the top.
The body of the loop should change the value of one or more variables so that the condition becomes false eventually and the loop terminates. Otherwise the loop will repeat forever, which is called an infinite loop. An endless source of amusement for computer scientists is the observation that the directions on shampoo, “Lather, rinse, repeat”, are an infinite loop.

In the case of countdown, we can prove that the loop terminates: if n is zero or negative, the loop never runs. Otherwise, n gets smaller each time through the loop, so eventually we have to get to 0.

For some other loops, it is not so easy to tell. For example:

def sequence(n):
    while n != 1:
        print(n)
        if n % 2 == 0:        # n is even
            n = n / 2
        else:                 # n is odd
            n = n*3 + 1
The condition for this loop is n != 1, so the loop will continue until n is 1, which makes the condition false.
Each time through the loop, the program outputs the value of n and then checks whether it is even or odd. If it is even, n is divided by 2. If it is odd, the value of n is replaced with n*3 + 1. For example, if the argument passed to sequence is 3, the resulting values of n are 3, 10, 5, 16, 8, 4, 2, 1.

Since n sometimes increases and sometimes decreases, there is no obvious proof that n will ever reach 1, or that the program terminates. For some particular values of n, we can prove termination. For example, if the starting value is a power of two, n will be even every time through the loop until it reaches 1. The previous example ends with such a sequence, starting with 16.

The hard question is whether we can prove that this program terminates for all positive values of n. So far, no one has been able to prove it or disprove it! (See http://en.wikipedia.org/wiki/Collatz_conjecture.)

As an exercise, rewrite the function print_n from Section 5.8 using iteration instead of recursion.
