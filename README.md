# home_work_python_11

# Задание:

*Дана функция: f(x) = -12x^4*sin(cos(x)) - 18x^3+5x^2 + 10x - 30

1. Определить корни.
2. Найти интервалы, на которых функция возрастает.
3. Найти интервалы, на которых функция убывает.
4. Построить график.
5. Вычислить вершину.
6. Определить промежутки, на котором f > 0.
7. Определить промежутки, на котором f < 0.

# 1. Найдем и построим график функции.

from sympy import *
from sympy.plotting import plot
from sympy import Interval, symbols, solveset
from sympy.calculus.util import *
from sympy import abc
from numpy import arange
from numpy import cos, sin
from scipy import optimize
from scipy.optimize import differential_evolution
init_printing()

def function(x):
    return -12*sin(cos(x))*x**4 - 18*x**3+5*x**2 + 10*x - 30
    
x = Symbol('x', real=True)
f = -12*sin(cos(x))*x**4 - 18*x**3+5*x**2 + 10*x - 30
plot(f,(x,-100,100))
print(f)
