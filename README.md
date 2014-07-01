Hands on introduction to Erlang
===============================

 Peer to Peer to peer computing
            (1DT047)

           Summer 2014

       Uppsala university

          Karl Marklund



The Unix/Linux shell
====================

The shell provides a command line
interface (CLI) an operating
system's services.

You only need to know a few basic
shell commands.

* pwd
* ls
* ls -F
* cd

In these notes the Unix/Linux
shell prompt will be represented
by:

    $>

The Erlang shell
================

The Erlang shell is CLI for
entering expression sequences.

From the Unix/Linux shell you
start the Erlang shell by:

    $> erl

In these notes the Erlang shell
prompt will be represented by:

    >

Erlang as a calculator
======================

Try a few arithmetic expression
in the Erlang shell, for example:

    > 1 + 1.

Note: an expression must end with
a period `.`.


Erlang variables
================

You can remember the value of an
expression by *binding* the
result to a name.

Such names are called
*variables*.

Variables must start with an
upper case letter. Examples of
valid variable names:

    A
    B
    Alex
    Alex22

The equal sign `=` is used to
bind values to variables.

    > A = 1 + 1.

You can use any bound variables
to form new expression, for
example:

    > A + 77.

    > B = 2*A.

A variable can only be bound
once.

What happens if we do:

    > A = A + 1.

Atoms
=====

An atom is a literal, *a constant
with name*.

An atoms must be enclosed in
single quotes (') if it does not
begin with a lower-case letter or
if it contains other characters
than alphanumeric characters,
underscore (_), or @.

Examples of atoms:

                a
               ab
               aBC
              a_b_c
            user@host
             'Atom'
       'Atom with spaces!'

Tuples
======

A tuple is a *compound data type* with a *fixed number of terms*.

Examples of tuples:

               {}
               {1}
               {a}
              {1,2}
           {a,33,xyz}
      {88,12,99,{a,b, 77}}

Tuples are used to group together
a static number of "things".

Lists
=====

A list is a *compound data type*
with a *variable number of
terms*.

Examples of lists:

               []
               [1]
               [a]
         [1,b,{11,3},77]
      [88,12, [1,2,3],99,1]

Lists are used to group together
a variable number of "things".

Head and tail
-------------

The first element of a list is called the *head* of the list.

The head of `[1,2,3]` is `1`.

If we cut the head off a list we get a new list called the *tail*.

The tail of `[1,2,3]` is `[2,3]`.

What is the head of the empty
list `[]`?

Adding a new head
-----------------

Adding a new element at the head
of a list to construct a *new*
list:

Try this:

    > L1 = [1,2,3].

    > L2 = [0|L1].

    > La = [b,c,d]
    > X = a.
    > Lb = [X|La] .

What is the result of:

    > [X,La].


Pattern matching
================

Variables are bound to values
through the pattern matching
mechanism.

If the matching succeeds, any
*unbound variables* in the
pattern *become bound*.

If the matching fails, a run-time
error occurs.

We have already seen the match
operator = in action.

In this example:

    > A = 1 + 1.

, the left hand side pattern `A`
is used to match the result of
the right hand side
expression.

If `A` is unbound `A`
will be bound to the value `2`.

Pattern matching also occurs when
evaluating a function call or a
case, receive, or try exression.

List all bounded variables
--------------------------

List all bounded variables in the
shell:

    > b().

Free bounded variables
----------------------

To free all bounded variables in
the Erlang shell:

    > f().

To free a single variable in the
Erlang shell, for example `A`:

    > f(A).


Matching numbers
----------------

Pattern matching on arithmetic
expressions.

Assume `A`, `B` and `C`are
unbound.

    > A = 1.
    > B = A + 1.
    > C = 2.

What happens if try this?

    > C = 2*A.
    > 2 = 2*A.
    > 3 = 2*A.
    > 1 + 1 = 2.
    > 1 + 1 = 3.

Matching tuples
---------------

Pattern matching can be used to
deconstruct a tuples.

Assume `A`, `B` and `C`are
unbound.

    > {A,B,C} = {1,2,3}

After the match `A` is bound to
`1`, `B` to `2`and `C`to `3`.

Pattern matching is also used to
check if a tuple have a certain
"shape".

    > ValidDate = {year, 2014}.
    > RandomTuple = {99, 7}.

What happens if try this?

    > {year, Year} = Date.
    > {year, Year} = RandomTuple.


Matching lists
--------------

Pattern matching can be used to
deconstruct lists.

Extract the *head* and *tail*:

    > [H|T] = [1,2,3].

Now `H` becomes bound to `1` and
`T` to `[2,3]`.

The don't care variable
-----------------------

The special variable `_` is used
when a variable is needed in a
pattern but we don't care about
it.

To only match the head of a list:

    > [H|_] = [a, b, c].

Now `H` is bound to `a`.

To only match the tail:

    > [_|T] = [a, b, c].

Now `T` is bound to `[b,c]`.

Similarly _ can be used when
matching tuples:

    > {A,_,C} = {1,2,3}.

List comprehensions
===================

A compact way to construct
lists.

Try this out:

    > [ 2*A || A <- [1,2,3] ].



    [2,4,6]
    >

Now try this

    > [ A*B || A <- [1,2,3],
               B <- [10, 100] ].



    [10,100,20,200,30,300]
    >


Functions
=========

A functions takes zero or more
*arguments* and returns a
*result*.

Function names must be *atoms*.

Examples of functions:

     init_list() -> [1,2,3].

       double(A) -> 2*A.

      sum(A,B)   -> A + B.

Modules
=======

Functions must be *declared* in
*modules*.

Let’s create our first module
`tut` in a file named `tut.erl`.

Module attributes
-----------------

* module()
* export()
* compile()

Comments (%%)
-------------

Compile and load
----------------

Modules can be compiled and
loaded from the Erlang shell:

    > c(tut).

On success the compile function
`c` returns:

    {ok, tut}

The `tut` module is now loaded
and we can call functions
declared in the module:

    > tut:abc().
    [a,b,c]
    >

Expression sequences (,)
------------------------
Multiple function clauses (;)
-----------------------------

Guarded function clauses (when)
-------------------------------

Case of expressions
-------------------

Anonymous functions (funs)
==========================

We don't need to declare named
functions in modules.

Anonymous functions, a function
without a name are called funs
and are declared written with the
syntax:

F = fun (Arg1, Arg2, ... ArgN) ->
        ...
    end


Note the keywords `fun` and
`end`.

This creates an anonymous
function of `N` arguments and
binds it to the variable `F`.

Printing to standard output
===========================

* io:format/1
* io:format/2

Processes and concepts of concurrency
=====================================

Erlang is designed for *massive
concurrency*.

Erlang processes are
*light-weight*:

 * grow and shrink dynamically.
 * small memory footprint.
 * fast to create and terminate.
 * low scheduling overhead.

A new process have a unique process identifier (PID).

self()
------

The Erlang shell is a process!

    > self().

spawn/1 and spawn/3
-------------------

Examples from `tut2.erl`

Message passing
===============

Examples from `tut3.erl`

Bang - the send message operator!
---------------------------------

Flush note to self()
--------------------

* the process mailbox.
* flush().

Receive and pattern matching
----------------------------

* Very similar to the case of
  expression.
* Guards can be used.
