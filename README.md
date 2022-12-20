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

![image](https://user-images.githubusercontent.com/114414329/207859536-06c0b360-9edb-40ab-b658-16022fccb694.png)

Переместил файл Economic.yaml в папку с проектом Unity, запустил Anaconda Prompt (от имени администратора), создал виртуальное пространство и установил нужные пакеты.
Запустил обучение:

![image](https://user-images.githubusercontent.com/114414329/207873672-039e26d1-42e2-4baf-a484-52f18e1cf10c.png)

TensorBoard
Начальные графики:
![image](https://user-images.githubusercontent.com/114414329/208697401-1acb15d6-0ff1-4d68-ab40-b9c7e1dce9ff.png)
![image](https://user-images.githubusercontent.com/114414329/208697430-7090c7b5-b325-4b94-87bf-9f84f6a4da62.png)
![image](https://user-images.githubusercontent.com/114414329/208697460-7d849d08-df65-41f8-9c71-fae37f02a2aa.png)
![image](https://user-images.githubusercontent.com/114414329/208697477-f3ddbfc5-289f-40a2-a069-ee3bdd54fd0d.png)
![image](https://user-images.githubusercontent.com/114414329/208697500-4e7113cb-5ed9-4037-983f-56f5d56a4439.png)


Поменяем epsilon с 0.2 на 0.6, num_epoch с 3 на 8, strength c 1 на 0.9:
![image](https://user-images.githubusercontent.com/114414329/208697251-5f7c2bd0-3d6d-4cbb-a582-24c4b37ef808.png)




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
