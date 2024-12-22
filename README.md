# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
- Идрисов Фуад Асип оглы
- РИ230917

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

## Цель работы
Поработать со скриптом перцептрона, поэксперементировать с таблицами истинностями.

## Задание 1: в проекте Unity реализовать перцептрон, который умеет производить вычисления:
### OR | дать комментарии о корректности работы
### AND | дать комментарии о корректности работы
### NAND | дать комментарии о корректности работы
### XOR | дать комментарии о корректности работы
Код Perceptron
```py

using System;
using UnityEngine;

public class Perceptron : MonoBehaviour
{
    private float[] weights;
    private float bias;
    private float learningRate = 0.1f;
    private int epochs = 10000;
    private float error;
    private int maxEpochsToDisplay = 15; // Максимальное количество эпох, для которых выводится информация

    // Метод активации (пороговая функция)
    private int Activate(float sum)
    {
        return sum >= 0 ? 1 : 0;
    }

    public void Train(int[,] inputs, int[] outputs)
    {
        weights = new float[inputs.GetLength(1)];
        bias = 0.0f;

        // Обучение
        for (int epoch = 0; epoch < epochs; epoch++)
        {
            error = 0.0f;

            for (int i = 0; i < inputs.GetLength(0); i++)
            {
                float sum = 0.0f;

                // Рассчитываем сумму произведений входных данных на веса
                for (int j = 0; j < inputs.GetLength(1); j++)
                {
                    sum += inputs[i, j] * weights[j];
                }

                sum += bias;

                // Прогнозируем значение
                int prediction = Activate(sum);

                // Целевое значение
                int target = outputs[i];
                int errorTerm = target - prediction;

                // Корректируем веса
                for (int j = 0; j < weights.Length; j++)
                {
                    weights[j] += learningRate * errorTerm * inputs[i, j];
                }
                bias += learningRate * errorTerm;

                // Считаем ошибку
                error += Math.Abs(errorTerm);
            }

            // Выводим информацию в консоль только если количество эпох меньше или равно 15
            if (epoch <= maxEpochsToDisplay)
            {
                Debug.Log($"Epoch: {epoch}, Error: {error}");
            }

            // Если ошибка стала равна нулю, обучение завершено
            if (error == 0)
            {
                Debug.Log($"Training completed at Epoch {epoch}. Perceptron has learned successfully.");
                break;
            }
        }

        // После 15 эпох не выводим больше ошибок
        if (epochs > maxEpochsToDisplay)
        {
            Debug.Log("Epoch limit reached, stopping further output.");
        }
    }

    // Метод для вычисления результата для новых данных
    public int Compute(int[] input)
    {
        float sum = 0.0f;
        for (int i = 0; i < input.Length; i++)
        {
            sum += input[i] * weights[i];
        }
        sum += bias;
        return Activate(sum);
    }
}
```
OR 

![image](https://github.com/user-attachments/assets/7004f178-ab10-45cb-869c-be2871f72a18)

Комментарий: перцептрон проявляет высокую скорость обучения и эпоха при которой ошибок нет равна 3

AND 

![image](https://github.com/user-attachments/assets/9e7b109a-f4d6-4a78-a767-1f5556e965cd)

Комментарий: количество эпох обучения как и в OR равна 3

NAND 

![image](https://github.com/user-attachments/assets/4d053e1c-30ba-48e5-b30f-209ecd15626f)

Комментарий: Скорость обучения перцептрона снизилась и эпоха при которой ошибок нет равна 5

XOR 

![image](https://github.com/user-attachments/assets/9434e5d4-cd6f-4301-bd0e-3ce748eceaff)

Комментарий: перцептрон не может обучится вне зависимости от количества эпох(ограничение я поставил 15, но поверьте при 10000, он также не хотел обучаться) 

## Задание 2: 
### Построить графики зависимости количества эпох от ошибки  обучения. Указать от чего зависит необходимое количество эпох обучения.
OR

Высокая скорость обучения может быть обусловлена тем, что операция OR имеет относительно простую структуру, что облегчает адаптацию персептрона к этой задаче.

AND 

NAND

Снижение скорости обучения  может свидетельствовать о том, что NAND, хотя и проще, чем XOR, может требовать некоторой дополнительной настройки весов для достижения оптимальных результатов.

XOR

Невозможность обучения персептрона вне зависимости от количества эпох и допущение ошибок во всех случаях может говорить о том, что XOR представляет собой задачу, которую персептрон не может решить в рамках текущей структуры. Вероятно, требуется более сложная архитектура с дополнительными слоями или другие методы обучения.

![image](https://github.com/user-attachments/assets/4bc6f648-d251-4cf3-9a77-6579286b22a2)



## Задание 3:
### Построить визуальную модель работы перцептрона на сцене Unity.


## Выводы

В ходе лабораторной работы успешно реализованы и протестированы операции OR, AND, и NAND с использованием перцептрона в Unity. Проанализирована зависимость количества эпох от ошибки обучения, что позволяет лучше понять требования к обучению для разных операций.

## Powered by
Идрисов Фуад Асип оглы
