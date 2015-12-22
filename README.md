## Definitions
Taken from Eric Elliott's [Curry or Partial Application?](https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8):
>
- **Application**: The process of applying a function to its arguments in order to produce a return value.
- **Partial Application**: The process of applying a function to some of its arguments. The partially applied function gets returned for later use. In other words, a function that **takes a function with multiple parameters and returns a function with fewer parameters**. Partial application ***fixes*** (partially applies the function to) one or more arguments inside the returned function, and the returned function takes the remaining parameters as arguments in order to complete the function application.
- **Curry**: A function that **takes a function with multiple parameters** as input and **returns a function with exactly one parameter**.

## Examples
*If you want to try executing below examples, consider:
```python
pip install toolz
from toolz import partial, curry
```

Lets start, I will use `Python` for code demonstration. Say we have a small function:
```python
add = lambda x, y, z: x + y + z
```
#### Partial Application:
```python
>>> p_add = partial(add, 1)
>>> p_add(2, 3)
6
```
#### Curry:
```python
>>> c_add = curry(add)
>>> c_add_1 = c_add(1)
>>> c_add_1(2, 3)
6
```
At this point, both `curry` and `partial` *seem* to have the same behavior, **but**, lets go further from above examples:

```python
>>> p_add = partial(add, 1)
>>> p_add(2, 3)
6
>>> p_add(2)
TypeError: <lambda>() takes exactly 3 arguments (2 given)
```
You might have an idea why we got this error. Yes, because Partial application ***fixes*** arguments inside the returned function. In our example, `p_add` has the `1` argument fixed inside, so it will **only accept exactly 2 more arguments** (since our `add` function takes 3 argument).

Now lets try the same with `curry`:
```python
>>> c_add = curry(add)
>>> c_add_1 = c_add(1)
>>> c_add_1(2)
<function <lambda> at 0x00000000031E8F98>
```
`curry`, on the other hand, **returns a function** which we can further assign missing arguments into it.
```python
>>> c_add_1_and_2 = c_add_1(2)
>>> c_add_1_and_2(3)
6
```
or with shorter syntax:
```python
>>> c_add_1(2)(3)
6
```
as well as:
```python
>>> c_add(1)(2)(3)
6
```
In other words, `currying` and `partial application` are two totally different things.


#### References:
- https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8
- http://stackoverflow.com/a/23438430/4328963

#### Thanks for reading!
