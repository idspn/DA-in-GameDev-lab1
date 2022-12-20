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
Обучить ML-Agent'а и проанализировать как обучение зависит от параметров yaml.

## Задание 1
### Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

Открыл проект и ознакомился с его работой:

![image](https://user-images.githubusercontent.com/114414329/208715046-4b3c5af7-32f4-46c4-bf28-48603118320b.png)

Переместил файл Economic.yaml в папку с проектом Unity, запустил Anaconda Prompt (от имени администратора), создал виртуальное пространство и установил нужные пакеты.
Запустил обучение:

TensorBoard
Начальные графики:

![image](https://user-images.githubusercontent.com/114414329/208698924-a85957b2-4e9e-412b-bffa-405ef43d1095.png)
![image](https://user-images.githubusercontent.com/114414329/208698980-8b7541f8-e18f-422a-80a2-84bd2e7a388e.png)
![image](https://user-images.githubusercontent.com/114414329/208704494-8b13298d-11a2-4892-92d0-e92b33c60195.png)
![image](https://user-images.githubusercontent.com/114414329/208704528-7228579c-1d3b-4a6f-a8b2-8c4233817eb0.png)
![image](https://user-images.githubusercontent.com/114414329/208704562-a4983617-6077-4024-9c17-c6c5b66e218e.png)


Поменял epsilon на 0.6:

![image](https://user-images.githubusercontent.com/114414329/208699421-6456dadc-6897-45f7-94a2-9d1b854be9a5.png)
![image](https://user-images.githubusercontent.com/114414329/208699488-273ad253-4407-4fc9-8843-437524604d58.png)

Поменял num_epoch на 5:

![image](https://user-images.githubusercontent.com/114414329/208714685-36b88bb4-31ad-49a5-b18d-10f943c3fced.png)
![image](https://user-images.githubusercontent.com/114414329/208714712-e239400f-86ac-41b1-823e-4dd52a834bc3.png)


Поменял lambd на 0.8:

![image](https://user-images.githubusercontent.com/114414329/208703763-62d8c86b-0ac8-4803-9362-036d6e35a48f.png)
![image](https://user-images.githubusercontent.com/114414329/208703792-7c00824f-e76d-487c-9577-b129f3cc3462.png)

## Задание 2
### Опишите результаты, выведенные в TensorBoard. 

Environment:

Cumulative Rewards - это общее вознаграждение по всем агентам, с течением времени должно постоянно увеличиваться.

Episode Length - это средняя продолжительность обучния агентов.

Losses:

Policy Loss — это потеря политики со временем, при успешной тренировке значения должны уменьшаться.

Value loss - это потеря функции со временем, показывает то, как успешно агент прогнозирует значение своего следующего состояния.

Policy:

Entropy - это значения случайности решений агента.

Epsilon - это скорость изменения политики.

Extrinsic Reward - это среднее вознаграждение, полученное за эпизод.

Extrinsic Value Estimate - это среднее значение для всех положений агента, при успешной тренировке - увеличивается.

## Выводы

Я научился интегрировать экономическую систему в Unity, обучать ML Agent и выводить графики в TensorBoard, выяснил, как изменение параметров влияет на поведение модели.

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
