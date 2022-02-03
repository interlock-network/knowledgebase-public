# Multi-method dispatch

In typical object-oriented programming languages you will find
yourself defining something like the following pseudocode:

```
class wheel:
  var position = 0;

  method rotate:
    this.position += 1;
```

then, with an instance of `wheel`, we are able to invoke
`rotate`. This is great when we are trying to tie some specific
behavior to a single type of object.

Here is an example of us creating said object, and invoking said
behavior:

```
var x = new wheel();
x.rotate();
```

This is called `single-dispatch`. We are dispatching the method rotate
and passing it `x`. To illustrate, imagine the equivalent could also
be written like this:

```
def rotate(x)
  x.position += 1;

var x = new wheel();
rotate(x);
```

However, what happens when we add a new class (tomato)? We would now have:

```
class wheel
int position = 0;

method rotate
  this.position += 1

------------------------------------------------------------------------

class tomato
int position = 0;

method rotate
  this.position += 2

```

Now if we do:

```
def rotate(x)
  x.position += 1;

var x = new wheel();
rotate(x);
```

rotate must be cognizant of what `x` is! It can't just add 1 to the
position! What if `x` were a tomato? Then `rotate` would set the wrong
value! Here is an example of what `rotate` _could_ look like:

```
def rotate(y):
  switch:
    case y.type == wheel:
       y.position += 1;
    case y.type == tomato:
       y.position += 2;
```

This is what we mean when we say single dispatch. Why? Because we are
only specializing against one thing `y`! There is only *one* typed argument
to the rotate function. Imagine if we could do something like the
following:

```
def rotate(x y):
   switch y.type == wheel && x.type == road:
     // do something
   switch y.type == wheel && x.type == carpet:
     // do something
   switch y.type == tomato && x.type == table:
     // do something
   switch y.type == tomato && x.type == floor:
     // do something
```

as you can see above the behavior of rotate depends on `x` _and_ `y`!
There are now four declared method combinations, however, there could
be an infinite amount. This would get very tiresome to write out, and
be very error prone. For the same reason we don't manually write out:

```
def rotate(y):
  switch:
    case y.type == wheel:
       y.position += 1;
    case y.type == tomato:
       y.position += 2;
```

in single dispatch languages, we don't want to also write out complex
multi-dispatches. Well, the good news is, we don't have to! Some
languages/compilers support multi-dispatch!

In a multi-dispatch language we could write:

```
method rotate (wheel x, floor y):
  wheel.position += 10;

method rotate (wheel x, asphalt y):
  wheel.position += 12;
```

In the above pseudocode, `wheel` is the type, and `x`, is the
reference/placeholder. Given the above definitions, when we invoke
`rotate(q, z)` where `q` is a `wheel` and `z` is a `floor` object, the
language will call the correct method- thereby incrementing the
wheel.position by a value of 10.

To see examples in action, please check out the [Wikipedia article](https://en.wikipedia.org/wiki/Multiple_dispatch).
