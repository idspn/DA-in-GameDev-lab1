# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
Реализовать перцептрон,который умеет производить вычисления, и рассмотреть основные принципы его работы.

## Задание 1
### В проекте Unity реализовать перцептрон,который умеет производить вычисления
Создвем пустой объект и присоединяем к нему файл Perceptron.cs
![image](https://user-images.githubusercontent.com/114414329/205939500-d12991bc-7e31-4f9c-98ca-7e6260085ab4.png)

Создаем логический элемент, который отрабатывает операцию OR:

![image](https://user-images.githubusercontent.com/114414329/205945254-5c8d29a9-4831-4e09-8b03-cce54f15748b.png)

1 эпоха:
![image](https://user-images.githubusercontent.com/114414329/205943332-27072820-e1dc-44de-b09f-5113dc292ba5.png)

2 эпохи:
![image](https://user-images.githubusercontent.com/114414329/205943468-6f11eeba-9e78-4474-bce9-abee90c2bba6.png)

4 эпохи(1 попытка):
![image](https://user-images.githubusercontent.com/114414329/205944180-c2bda489-4c7c-4bde-b102-f96d4ed2781b.png)

4 эпохи(2 попытка):
![image](https://user-images.githubusercontent.com/114414329/205963030-8c956c97-50c7-4f12-a98b-ca16763d8004.png)

Во время 4 эпохи значение не всегдаTotal Error было 0.

Создаем логический элемент, который отрабатывает операцию AND:

![image](https://user-images.githubusercontent.com/114414329/205957943-d208cfdd-726d-45a2-a7f3-fc98b039c5c7.png)

1 эпоха:
![image](https://user-images.githubusercontent.com/114414329/205959599-d7f48efd-1a6c-4c53-9f2a-877209563c2c.png)

4 эпохи:
![image](https://user-images.githubusercontent.com/114414329/205959788-7233dc86-bd79-4926-8734-4da566987ed0.png)

Уже во время 4 эпохи значение Total Error было 0.

Создаем логический элемент, который отрабатывает операцию NAND:

![image](https://user-images.githubusercontent.com/114414329/205962773-84dc354a-13b9-4282-87ca-3f3d0b4b8a36.png)


1 эпоха:
![image](https://user-images.githubusercontent.com/114414329/205960207-d3aa523f-9eef-4a5c-9177-c810299d9962.png)

4 эпохи:
![image](https://user-images.githubusercontent.com/114414329/205960396-c0a72270-f1a4-4080-9343-c31bea331369.png)

6 эпох:
![image](https://user-images.githubusercontent.com/114414329/205960560-bfbf2441-f62f-4e3a-a3b8-179e87734c42.png)

Уже во время 6 эпохи значение Total Error было 0.

Создаем логический элемент, который отрабатывает операцию XOR:

![image](https://user-images.githubusercontent.com/114414329/205960782-01421e2a-b5f1-439a-8d5e-8cea6b495bb3.png)

1 эпоха:
![image](https://user-images.githubusercontent.com/114414329/205961299-c689ac3b-2a40-4a08-828f-20bec4f66e42.png)

4 эпохи:
![image](https://user-images.githubusercontent.com/114414329/205961416-ea57738e-c11b-49fb-b82f-7d6f5dad5137.png)

6 эпох:
![image](https://user-images.githubusercontent.com/114414329/205961639-58019e6f-7495-480f-b5e7-0c59aa11287b.png)

C 4 эпохи значение Total Error всегда  равно 4, делаем вывод, что перцептрон не может обучиться этой операции. Он может решать линейные задачи(OR, AND, NAND).

## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.
На графиках указано среднее значение Total Error за определенное количество попыток для каждой операции.

OR:

![image](https://user-images.githubusercontent.com/114414329/205964648-1ed0fe43-fe90-4dc5-8cb5-e3c3cfbf8be0.png)


AND:

![image](https://user-images.githubusercontent.com/114414329/205965495-30f88bba-9fea-46b4-8cac-2f40b621c891.png)


NAND:

![image](https://user-images.githubusercontent.com/114414329/205965893-a9358a22-ae30-4f7c-9340-02d0f0a3a0c6.png)


XOR:

![image](https://user-images.githubusercontent.com/114414329/205967453-c75a5034-8605-4ce5-a400-2a3b36869963.png)


Количество необходимых эпох  зависит от сложности решаемой операции.

## Задание 3
### Псотроить визуальную модель работы перцептронв на сцене Unity.


## Выводы

Я онакомился с моделью устройством перцептрона. Смог реализовать такие логические операции как OR, AND, NAND. Сделал вывод: однослойный перцептрон можен решать только линейные задачи. Построил графики для оценки работы для каждой операции.

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
