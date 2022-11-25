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
    
![1 1](https://user-images.githubusercontent.com/110101307/204028416-6c8dc639-3a1e-4c9a-ab5a-f922f8fb5039.png)

Судя по графику - функция немонотонная и имеет большое количество корней, поэтому выведем график при х ∈ [—10, 10].
Судя повсему данная функция имеет минимум 4 корня.

    plot(f,(x,-10,10))
    print(f)
    
![1 2](https://user-images.githubusercontent.com/110101307/204028983-f0778264-8322-4dbd-99a0-8cf08d56040f.png)

Точное кол-во корней:

    qtyXres = 0
    tempXres = function(-10)
    for i in arange (-10, 10, 0.001):
        if tempXres * function(i) < 0: qtyXres += 1
    tempXres = function(i)
    print(f"Общее кол-во корней = {qtyXres}")

Итого корней: 6.

# 2. Определяем корни.

И так, ранее мы вычислили, что данная функция имеет 6 корней.
Находим каждый корень (перебором), до тех пор пока функция не преодолеет "0", после чего уточним значение с помощью функции nsolve().
