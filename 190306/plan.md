# ООП в Python "на пальцах" [01:00]
* Неполный взгляд: объект - это переменная, которая не только
  содержит данные, но и возит с собой код для управления ими.
## Базовый синтаксис [00:15]
* self - ещё один параметр
* Конструктор `__init__`
* Всё, что в теле - статика (включая переменные!)
* Перегрузки функций нет
* Есть @staticmethod
* bounded vs unbounded method и его использование в map
* `isinstance` и `type()`

## Примеры: коллекции, итераторы  [00:15]
* Методы `__iter__` и `__next__`
  * "Магические методы" (просто стандартное название)
  * `StopIteration`
* Написание бесконечного списка
* Функции `iter` и `next`
* Использование в `for`
* Написание конечного списка
* Метод `__getitem__`
  * `KeyError`
  * Ссылка на https://docs.python.org/3/reference/datamodel.html
## Генераторы [00:10]
* Ручная итерация по списку, `map`, `filter`
* Generator expression vs list comprehension
  * Сокращённый синтаксис при вызове процедур
* Синтаксический сахар: `yield`
## Перегрузка операторов [00:15]
* `==`, `*`, `+`
* Причины не перегружать:
  * Разное поведение у похожих типов (целочисленное деление в Python 2)
  * `||` похоже на "прямые параллельны", а `vec1 * vec2` может означать разное произведение
  * Скрывает сложные места (к процедурам все привыкли)
* `__add__` и `__radd__`, `NotImplemented`
* `__lt__` против `__gt__`, `total_ordering`
## Хэширование [00:05]
* `__hash__` и `__eq__`, аналог в Java
* Мутабельные объекты и хэширование
* Полиномиальный хэш от строки и длинная арифметика

# Идеология [00:30]
## Отличия от процедур [00:05]
* Методы передаются вместе с данными
* Параметрический полиморфизм (абстракция данных)
  * Код одинаковый, но ведёт себя по-разному
  * Утиная типизация: важны только имена методов, динамически
    ищем нужный
  * Сравнение с C++: наследование и виртуальные функции для полиморфизма
## Реализация в Python [00:10]
* `__dict__` - динамический словарь, `hasattr`
* Сравнение с C++: нет понятия "расположение в памяти" или "виртуальный вызов"
* Кто угодно создаёт любые свойства
* Что угодно - объект со свойствами (`dir`), даже функция, метод (`__call__`) и числа (`.bit_length()`, `.as_integer_ratio()`)

TODO: пример/практика дизайна?
## Контракты и инварианты [00:05]
* У объекта есть контракт: что с ним можно делать и как он себя ведёт
  * Этот контракт синтаксически сосредоточен в одном месте, легче проверять
* Инвариант - условия на внутреннее состояние объекта; как он себя ведёт и почему
  * Можно проверять assert'ами, нарушение - ошибка программиста, а не пользователя
* Интерфейсы для частичного описания контрактов
  * В Python - просто соглашения в документации
  * В C++/Java - реальные интерфейсы/абстрактные базовые классы
## Работа с разными типами [00:10]
* Сложности: 
  * Квадрат/прямоугольник (правильного ответа нет)
  * "Изменяемый список", "список только для чтения", "неизменяемый список"
  * В Python: даже при утиной типизации (что именно мы ожидаем от списка?)
* Принцип подстановки Лисков (LSP) для наследования (в Java)
* Пробле при наследовании данных ("точка" и "точка с номером"):
  * Как сравнивать разные виды точек?
    * Если никак, то нарушаем LSP
    * Если по общим полям, нарушаем транзитивность
    * Если сначала по типам, нарушаем здравый смысыл
* Проблема не в наследовании, а в смешении типов!

# Python ABC (Abstract base Class) [00:15]
* Эмуляция интерфейсов из Java/C++
* Помогает PyCharm понимать код
* https://docs.python.org/3/library/collections.abc.html
  * `Iterable`
  * `Iterator`
  * `Sized`, `Container`, `Collection`
TODO

# Тестирование: принципы FIRST [00:15]
TODO

# Тестирование: mock [00:15]
* `sys.stdin`, `monkeypatch` и `StringIO`
TODO

# Пояснения к домашнему заданию [00:15]
* Абстрактные синтаксические деревья для выражений
* Абстрактные синтаксические деревья для кода
* Язык "ЯТЬ"
  * `Scope`
  * Как писать программы
TODO