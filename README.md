# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
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
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity. При выполнении задания можно использовать видео-материалы и исходные данные, предоставленные преподавателями курса.
Создал новый пустой 3D проект на Unity. Скачал папку с ML агентом. В созданный проект добавил ML Agent, выбрав Window - Package Manager - Add Package from disk. Последовательно добавьте .json – файлы: ml-agents-release_19 / com,unity.ml-agents / package.json, ml-agents-release_19 / com,unity.ml-agents.extensions / package.json. Далее запустил Anaconda Prompt для возможности запуска команд через консоль. Далее пишу серию команд для создания и активации нового ML-агента, а также для скачивания необходимых библиотек: mlagents 0.28.0; torch 1.7.1;
Создаем на сцене плоскость, куб и сферу: 

![image](https://user-images.githubusercontent.com/114414329/201128679-5f8d264f-fd07-43df-bcc0-bede582184b3.png)

Создаем простой C# скрипт-файл и подключаем его к сфере:
```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if(distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}

```

Объекту «сфера» добавляем компоненты Rigidbody, Decision Requester, Behavior Parameters и настройте их так, как показано на рисунке ниже:

![image](https://user-images.githubusercontent.com/114414329/201130288-4fa7770d-8441-4268-ad84-be0902e45dd0.png)

В корень проекта добавляем файл конфигурации нейронной сети, доступный в папке с файлами проекта по ссылке:

```py

behaviors:
  RollerBall:
    trainer_type: ppo
    hyperparameters:                 
      batch_size: 10
      buffer_size: 100
      learning_rate: 3.0e-4
      beta: 5.0e-4
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: linear
    network_settings: 
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    max_steps: 500000
    time_horizon: 64
    summary_freq: 10000

```
Запускаем работу ml-агента:

![image](https://user-images.githubusercontent.com/114414329/201131853-a32ecdee-64bf-41dd-8a04-2ba7ba54784a.png)

Возвращаемся в проект Unity, запускаем сцену, проверяем работу ML-Agent’a. Сделаем 3, 9, 27 копий модели «Плоскость-Сфера-Куб», запускаем симуляцию сцены и наблюдаем за результатом обучения модели:

![image](https://user-images.githubusercontent.com/114414329/201132301-13c4d822-6bbc-438e-8b0b-a0dbab25b0c2.png)

![image](https://user-images.githubusercontent.com/114414329/201132422-89143650-35e0-44be-a90f-07823d89a1c0.png)

После обучения шарик не падает с платформы и сам двигается к новому кубу.


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
