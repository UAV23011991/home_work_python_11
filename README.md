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

-12*x**4*sin(cos(x)) - 18*x**3 + 5*x**2 + 10*x - 30

Судя по графику - функция немонотонная и имеет большое количество корней, поэтому выведем график при х ∈ [—10, 10].

Похоже, что данная функция имеет минимум 4 корня.

    plot(f,(x,-10,10))
    print(f)
    
![1 2](https://user-images.githubusercontent.com/110101307/204028983-f0778264-8322-4dbd-99a0-8cf08d56040f.png)

Найдем точное кол-во корней:

    qtyXres = 0
    tempXres = function(-10)
    for i in arange (-10, 10, 0.001):
        if tempXres * function(i) < 0: qtyXres += 1
    tempXres = function(i)
    print(f"Общее кол-во корней = {qtyXres}")

Итого корней: 6.

# 2. Определим корни.

И так, ранее мы вычислили, что данная функция имеет 6 корней.

Находим каждый корень (перебором), до тех пор пока функция не преодолеет "0", после чего уточним значение с помощью функции nsolve().

    def funcRootResult(minX, maxX, step):
        tempDifferense = 0
        if function(minX) - function(minX + step) < 0:
            for i in arange (minX, maxX, step):
                if function(i) > tempDifferense: 
                    nearestX = i
                    message = f"Функция возрастает!\nx = {i} => f(x) = {function(i)}\nf(x) = 0 при x = {nsolve(f, nearestX)}"
                    return message
        if function(minX) - function(minX + step) > 0:
            for i in arange (minX, maxX, step):
                if function(i) < tempDifferense: 
                    nearestX = i
                    message = f"Функция убывает!\nx = {i} => f(x) = {function(i)}\nf(x) = 0 при x = {nsolve(f, nearestX)}"
                    return message
                    
**Корень 1:**

Ответ: f(x) = 0 при x = -7.65062228513275

    plot(f,(x,-8,-7))
    print(f)
    print(funcRootResult(-7.7, -7.6, 0.00001))
    
![1 3](https://user-images.githubusercontent.com/110101307/204030551-dc139c52-d33b-4249-aabf-c2144d364e48.png)

Данная функция убывает.
x = -7.65062000000187 => f(x) = -0.0876621130482391
f(x) = 0 при x = -7.65062228513275

***

**Корень 2:**

Ответ: f(x) = 0 при x = -5.02686592820621

    plot(f,(x,-5.5,-4.5))
    print(f)
    print(funcRootResult(-5.1, -4.9, 0.00001))
    
![1 4](https://user-images.githubusercontent.com/110101307/204031249-0bda3c80-7103-4eb5-baf7-40786dedfa97.png)

Данная функция возрастает.
x = -5.026860000002769 => f(x) = 0.0438220023861220
f(x) = 0 при x = -5.02686592820621

***

**Корень 3:**

Ответ: f(x) = 0 при x = -1.33896663927711

plot(f,(x,-2,2))
print(f)
print(funcRootResult(-1.5, -1.3, 0.00001))

![1 5](https://user-images.githubusercontent.com/110101307/204031718-f06b36f9-cde0-4771-b19f-cf2d8ae08a51.png)

Данная функция убывает.
x = -1.338959999998945 => f(x) = -0.000733721380150598
f(x) = 0 при x = -1.33896663927711

***

**Корень 4:**

Ответ: f(x) = 0 при x = 2.27305684575625

    plot(f,(x,1.5,3))
    print(f)
    print(funcRootResult(2.2, 2.3, 0.00001))
    
![1 6](https://user-images.githubusercontent.com/110101307/204032086-65a247a1-38f5-409f-bf09-d9458662a4da.png)

Данная функция возрастает.
x = 2.273060000000479 => f(x) = 0.000909509824197130
f(x) = 0 при x = 2.27305684575625

***

**Корень 5:**

Ответ: f(x) = 0 при x = 4.38352369796896

    plot(f,(x,3,5))
    print(f)
    print(funcRootResult(4.35, 4.4, 0.00001))

![1 7](https://user-images.githubusercontent.com/110101307/204032624-fa5fd91b-819a-4e84-a54f-5e69ec37f560.png)

Данная функция убывает.
x = 4.38352999999873 => f(x) = -0.0231731259884640
f(x) = 0 при x = 4.38352369796896

***

**Корень 6:**

Ответ: f(x) = 0 при x = 8.03516413341352

    plot(f,(x,7.5,8.5))
    print(f)
    print(funcRootResult(8, 8.1, 0.00001))

![1 8](https://user-images.githubusercontent.com/110101307/204033028-59aa6cf5-fdf8-4444-aa4d-2d073f506c67.png)

Данная функция возрастает.
x = 8.035169999998669 => f(x) = 0.290239321712306
f(x) = 0 при x = 8.03516413341352

***

 **Всего корней 6 при f(0) на отрезке х ∈ [—10, 10]:**
 
 1. -7.65062228513275
 2. -5.02686592820621
 3. -1.33896663927711
 4. 2.27305684575625
 5. 4.38352369796896
 6. 8.03516413341352

# Вычисляем вершину.

И так, мы выяснили, что данная функция имеет 6 корней и известны их значения.

Зная график и кол-во корней, можно предположить, что количество вершин равно 5.

Для точного подсчета вершин умножим все ее коэффициенты на 5.
 
    ftemp = 5*12*sin(cos(5*x))*x**4 - 5*18*x**3+5*5*x**2 + 5*10*x - 30
    plot(ftemp,(x,-2.5,2.5))
    print(ftemp)
    
![1 9](https://user-images.githubusercontent.com/110101307/204034803-4eb318a1-d164-48ed-9d7e-37ed1ba85b9f.png)

60*x**4*sin(cos(5*x)) - 90*x**3 + 25*x**2 + 50*x - 30

**Уточняем кол-во вершин:**

    def functionTemp(x):
        return 60*x**4*sin(cos(5*x)) - 90*x**3 + 25*x**2 + 50*x - 30

    qtyExtr = 0
    check = true
    ## Кусок кода ниже фактически считает сколько раз функция поменяла свое направление.
    for i in arange (-2.5, 2.5, 0.025):
        tempRes = functionTemp(i + 0.025)
        tempY = functionTemp(i)
        if check == true:
            if tempY - tempRes > 0: 
                continue
            else: 
                check == false
                ## print(f"{tempY} < {tempRes}")
                qtyExtr += 1 
                continue
        if check == false:
            if tempY - tempRes < 0: 
            continue
            else:
                check == true
                ## print(f"{tempY} > {tempRes}")
                qtyExtr += 1
                continue
    
    print(f"Общее кол-во вершин = {qtyExtr}")
    
Итого общее кол-во вершин: 89.

Найдем все вершины на отрезке отрезке х ∈ [—10, 10]:

    def extrFuncValue (func, bMin, bMax):
        bounds = [(bMin, bMax)]
        extrFuncValue = differential_evolution(func, bounds)
        return (extrFuncValue.x,extrFuncValue.fun)

    print("Найдены следующие вершины:")
    res = extrFuncValue(function, -7, -5) ##границы между x1 и x2 (примерно)
    print(f"A ({res[0][0]}, {res[1]})")
    res = extrFuncValue(lambda x:-function(x), -5,-1) ##границы между x2 и x3 (примерно)
    print(f"B ({res[0][0]}, {res[1] * -1})")
    res = extrFuncValue(function, -1, 2) ##границы между x3 и x4 (примерно)
    print(f"С ({res[0][0]}, {res[1]})")
    res = extrFuncValue(lambda x:-function(x), 2,4) ##границы между x4 и x5 (примерно)
    print(f"D ({res[0][0]}, {res[1] * -1})")
    res = extrFuncValue(function, 4, 8) ##границы между x5 и x6 (примерно)
    print(f"E ({res[0][0]}, {res[1]})")
 
**Найдено 5 вершин на отрезке х ∈ [—10, 10]:**
 
A (-6.8313694021473355, -13820.534926467413)

B (-4.167783530421969, 3111.363238735963)

С (1.7006072713193556, -74.1062930861087)

D (3.8193108255086323, 872.2557702910614)

E (7.001031659787006, -25610.50968103302)


 
