# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5 выполнил(а):
- Юнусов Эмир Дамирович
- РИ210943
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Вывести "Hello World!" на Unity и Python.
Python:
![22](https://user-images.githubusercontent.com/114414329/192508581-476b6eb3-378d-4e66-b532-0add792bd8f5.png)
![2](https://user-images.githubusercontent.com/114414329/192508602-28f8cd1c-b5da-433d-be77-c132c583b41f.png)

Unity:
![3](https://user-images.githubusercontent.com/114414329/192510118-e88adacd-addd-4b6c-a5f0-55c13f7ab353.png)
![33](https://user-images.githubusercontent.com/114414329/192510127-c7c45db7-02a8-43e9-a21f-702cbe4925e8.png)


## Задание 2
### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач.
Должна ли величина loss стремиться к нулю при изменении исходных данных?
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

```py

import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

plt.scatter(x,y)

```
![image](https://user-images.githubusercontent.com/114414329/192511834-5d9edc21-84b6-4502-b58c-bfe2d86cb350.png)

- Определить следующие связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

```py

def model(a, b, x):
    return a*x + b

def loss_function(a, b, x, y):
    num = len(x)
    prediction = model(a,b,x)
    return (0.5/num) * (np.square(prediction - y)).sum()

def optimize(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    da = (1.0/num) * ((prediction - y) * x).sum()
    db = (1.0/num) * ((prediction - y).sum())
    a = a - Lr * da
    b = b - Lr * db
    return a, b

def iterate(a, b, x, y, times):
    for i in range(times):
        a, b = optimize(a, b, x, y)
    return a, b
    

```
![image](https://user-images.githubusercontent.com/114414329/192513510-54a757f7-61bb-4b83-b3fa-7a56eacb3873.png)

- Начать итерацию.

Инициализация и модель итеративной оптимизации:
```py
a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

a, b = iterate(a, b, x, y, 1)
prediction = model (a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)

```
![image](https://user-images.githubusercontent.com/114414329/192515255-19338a61-beda-40eb-a51d-886a0f18ade4.png)

## Задание 3
### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.
Да, при увеличении итераций loss уменьшается:

loss = 4283.071164163826 при 1 итерации

![image](https://user-images.githubusercontent.com/114414329/192516907-29944ce1-c520-4c6d-adf2-11d44b5337b8.png)

loss = 1837.1247976234213 при 50 итерациях

![image](https://user-images.githubusercontent.com/114414329/192516729-e678d88b-068c-4ef7-9b24-9ce27b9a5858.png)

loss = 191.84756654388002 при 10000 итерациях

![image](https://user-images.githubusercontent.com/114414329/192517097-9f6d01cf-7149-482d-8fff-428afa7d7168.png)

### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.
От параметра Lr прямо пропорционально зависит угол наклона графика.

lr = 0.000001

![image](https://user-images.githubusercontent.com/114414329/192518075-39121143-1116-4b7c-a3f5-3130344b7082.png)

lr = 0.1

![image](https://user-images.githubusercontent.com/114414329/192518240-658bdf01-72c2-4757-beb1-cf659773e714.png)


## Выводы

Я ознакомиться с основными операторами языка Python на примере реализации линейной регрессии, определил связанные функции(функция модели, функция потерь, функция оптимизации) и выявил основные закономерности и зависимости, а так же написал программы по выводу строки "Hello World!" на Python и Unity.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
