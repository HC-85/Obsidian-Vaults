#VideoSeries https://www.youtube.com/playlist?list=PLo4jXE-LdDTQo4UUWnDzvZAWKwiH5gjYm
# Class 1
# Numerical ODEs
Suppose we have the scalar case: 
$$
\frac{dy}{dx} = f(y(x), x)
$$We look to discretize.
Using Taylor expansions and truncating to a polynomial:
$$
Y(x_{n+1})=Y(x_n)+\Delta x Y^\prime(x_n) + \mathcal{O}(\Delta x^2)
$$
where $Y$ is the exact ODE solution. 
We can denote $Y^\prime (x_n) = f(Y_n, x_n)$
And $\mathcal{O}(\Delta x^2) = \frac{1}{2}Y{\prime\prime}(\xi_n)(\Delta x)^2$, where $\xi_n$ is an unknown value that makes the error exact.

Our difference equation is then explicit Euler:
$$
y_{n+1} = y_n + \Delta x f(y_n, x_n)
$$
Note that $Y_{n+1}$ is a function white $y_{n+1}$ is a vector.

Implicit Euler is then:
$$
y_{n+1} = y_n + \Delta x f(y_{n+1}, x_{n+1})
$$
The trapezoidal is the average of these:
$$
y_{n+1} = y_n + \frac{\Delta x}{2} (f_{n+1} +  f_n)
$$
Usually when local error is $\mathcal{O}(\Delta x^m)$, global error is $\mathcal{O}(\Delta x^{m-1})$ 

## Absolute stability and the test problem
Let $\frac{dy}{dx} = \lambda y$ and $y(x_0) = y_0$, then we know the solution is $Y(x) = y_0 e^{\lambda x}$.
If $\text{Re}(\lambda)<0$, the solution should decay. 

For explicit Euler we have:
$$
y_{n+1} = y_n + h \lambda y_n  = (1 + \lambda h)y_n
$$
with $h = \Delta x$. Generalizing we get the recurrence relation:
$$
y_n = (1 + \lambda h)^ny_0
$$
For a stable solution, we want the absolute value amplification factor to be less than 1:
$$
|1 + \lambda h|<1
$$
Thus our region of convergence in $\mathbb{C}$ is a unitary disk centered at -1.

For implicit Euler we have:
$$
y_{n+1} = y_n + h \lambda y_{n+1} = \left(\frac{1}{1-\lambda h}\right)y_n
$$For the absolute value of the amplification factor to be less than 1, we must have:
$$
|1-\lambda h|>1
$$
This time, our region of absolute stability in $\mathbb{C}$ is the complement of a unitary disk centered at +1. 

For the trapezoidal, we get something reminiscent of the Mobius transformation:
$$
\left|\frac{1 + \lambda h}{1 - \lambda h}\right|< 1
$$
And its region of absolute stability is the left hand plane. 

Suppose we have an oscillating system and we want to choose between these three methods.
This implies $\lambda$ will be purely imaginary. 
1. Euler explicit would be a bad choice because the imaginary line falls outside the region of absolute stability.
2. Euler implicit would also be bad because since $\text{Re}(\lambda) = 0$, it would induce an spurious damping.
3. For the trapezoidal, we must remember than the border of our region of stability is equal to a value of 1, thus for a purely imaginary $\lambda$, the value will neither decay nor diverge, making it the best choice.
# Class 2
Euler implicit and trapezoidal use two distinct ($1/(1 - h\lambda)$ and $(1 + h\lambda)/(1 - h\lambda)$ respectively) [[Padé Approximants|Padé approximations]] of $\exp(h\lambda)$.

#Pending 
###### Tags
#PartialDifferentialEquations  #NumericalMethods #OrdinaryDifferentialEquations  #Analysis