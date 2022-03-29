# Тестовое задание на позицию Junior programmer (Python, C++)

- [X] Задание 1

```
На языке Python или С/С++, написать алгоритм (функцию) определения четности целого числа, 
который будет аналогичен нижеприведенному по функциональности, но отличен по своей сути. 
Объяснить плюсы и минусы обеих реализаций.
```

Функция `Python` из задания:
```python
    def isEven(value):return value%2==0
```
Функция `Python` моя:
```python
    def isEven(value):return bin(value)[-1] == "0"
```

## Разница реализации

Замысел, реализуемый в функции из задания, первым приходит на ум: мы сравниваем остаток от деления на двойку.
В моей же функции происходит сравнение последнего символа битовой записи числа. 



### Сравним скорость выполнения кода, обрабатывающего числа от 0 до 10000 с помощью наших функций:

```python
import timeit


code_to_test = """
def isEven(value):return value%2==0
for i in range(1000):print(i, isEven(i))
"""


elapsed_time = timeit.timeit(code_to_test, number=100)/100
print(elapsed_time)
```

*Получаем время, равное 0.014099473999999999 секундам*




```python
import timeit


code_to_test = """
def isEven(value): return bin(value)[-1] == "0"
for i in range(1000):print(i, isEven(i))
"""


elapsed_time = timeit.timeit(code_to_test, number=100)/100
print(elapsed_time)
```

*Получаем время, равное 0.013724908000000001 секундам*

#### Вывод:
Функции реализованы по-разному: в первом случае мы сравниваем число(остаток от деления) с другим числом, во втором - последний символ строки с необходимым.
Имеем небольшой разрыв по времени выполнения, чем положительно выделяется моя реализация функции.

---
- [X] Задание 2

```
На языках Python(2.7) и/или С++, написать минимум по 2 класса реализовывающих циклический буфер. 
Объяснить плюсы и минусы каждой реализации.
```

На момент выполнения этих заданий, я не обладаю практическим опытом создания циклических буферов. Надеюсь, что в будушем я смогу увидеть места, где применяется нечто подобное.

Итак, получилось такая очередь:

```python
class queue(object):
    def __init__(self, numbers):
        self.numbers = numbers

    def add(self, number):
        self.numbers += [number]

    def take(self):
        taking_number = self.numbers[0]
        self.numbers = self.numbers[1:]
        return taking_number
```

В получившемся классе мы можем создать перечень чисел с возможностью добавления новых элементов с его конца и отбором первого элемента перечня.

#### Что хорошо:
Это работает
#### Что плохо:
Размер перечня не статичный

Было принято решение сделать очередь кольцевой, получилось следующее:

```python
class queue(object):
    def __init__(self, numbers):
        self.numbers = numbers

    def take(self):
        taking_number = self.numbers[0]
        self.numbers = self.numbers[1:]
        self.numbers += [taking_number]
        return taking_number
```

#### Что хорошо:
Это работает
Размер перечня статичный
#### Что плохо:
Нельзя добавить новые данные

---
