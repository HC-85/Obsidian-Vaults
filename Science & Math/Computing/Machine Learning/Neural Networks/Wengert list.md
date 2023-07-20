Defines a function $f$ as a list of statements with single calls to primitive functions (operators) of a sublanguage $G$ on either the inputs or previous statements.

For example, let 
$$f(x_1, x_2) = (2x_1 + x_2)^2 $$
And $G = \{\texttt{add}, \texttt{multiply}\}$.
Then, we can write a Wengert list:
$$
\begin{align}
z_1 &= \texttt{add}(x_1, x_1)\\
z_2 &= \texttt{add}(z_1, x_2)\\
f &= \texttt{multiply}(z_2, z_2)
\end{align}
$$
In Python, this can be simply a list:
```python
[("z1", "add", ("x1, x2")),
 ("z2", "add", ("z1", "z2")),
 ("f", "multiply", ("z2", "z2"))]
```
Along with a dictionary of the sublanguage $G$:
```python
G = {"add": lambda a, b: a + b, "multiply": lambda a, b: a*b}
```
And another with the initial values (parameters):
```python
vals = {"x1": 1, "x2": 2}
```
We use these to iterate through the list, saving each intermediate step in the dictionary `vals`. 

Now, we iterate backwards through the list, calculating `delta`($z_i$) for every $z_i$ in `vals`.
For this we need another dictionary, `DG`:
```python
DG = {"add": [(lambda a,b: 1), (lambda a,b: 1)],
	 "multiply": [(lambda a,b: b), (lambda a,b: a)]}
```
And initialize `delta["f"] = 1`.
