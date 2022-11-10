# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Юнусов Эмир Дамирович
- РИ210943
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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
### Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере.

```
behaviors: #cоздание списка для разных агентов
  RollerAgent: #имя агента
    trainer_type: ppo #тип 
    hyperparameters:
      batch_size: 10 #количество шагов для каждой итерации
      buffer_size: 100 #количество шагов до изменения схемы движения
      learning_rate: 3.0e-4 #рейтинг обучения
      beta: 5.0e-4 #случайность выбора движения
      epsilon: 0.2 скорость обновления обучения
      lambd: 0.99 #
      num_epoch: 3 #количество шагов для обновления схемы движения
      learning_rate_schedule: linear # скорость обучения от времени
    network_settings: #сетевые настройки
      normalize: false #параметр для нормалицации входных данных
      hidden_units: 128 #количество скрытых единиц неронной сети
      num_layers: 2 #определяет количество скрытых слоев нейронной сети
    reward_signals: #параметр влияющий на систему вознаграждения в процессе обучения
      extrinsic: #коэффициент для внешних вознаграждений
        gamma: 0.99 #коэффициент для будущих вознаграждений
        strength: 1.0 #коэффициент вознаграждения
    max_steps: 500000 #максимальное число экспериментов 
    time_horizon: 64 #Количество число ML агента, хранящихся в буфере до ввода в модель
    summary_freq: 10000 #количество шагов до опубликования текущей статистики
    
 ```
 Decision Requester: запрашивает решение через каждые временные промежутки.
 Behavior Parameters: определяет то, каким образом объектом принимаются решения.
    
    

## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и в первом задании, случайно изменять координаты на плоскости

## Выводы

Что такое игровой баланс и как системы машинного обучения могут быть использованы для того, чтобы его скорректировать? Игровой баланс представляет собой равновесие между числами,описывающие разные игровые характеристики. Сиситемы машинного обучения совершенствуют игру, корректируя уровень сложности и сохраняя баланс между сложностью и легкостью.



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
