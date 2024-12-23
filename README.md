## 1.  Что такое соглашение об именовании, зачем оно используется? ##
Соглашение об именовании — это набор правил оформления кода, установленных командой разработчиков или организацией. Оно упрощает взаимодействие в команде, позволяя легко различать элементы кода благодаря единому стилю.
## 2. Какие три этапа проходит написанный при сборке скомпилированной программы? В чем суть этих этапов? ##
+ **Препроцессинг**
Препроцессор обрабатывает директивы, такие как `#include` и `#define`, и объединяет файлы `.cpp` и `.h` с одинаковыми именами.

+ **Компиляция**
Код преобразуется из понятного людям в машинный, проходя токенизацию, синтаксический и семантический анализ. Также выполняется оптимизация кода.

+ **Связывание (линковка)**
Линковщик объединяет скомпилированные единицы трансляции, связывает вызовы функций с их определениями и формирует готовую исполняемую программу.
## 3. Что такое единица трансляции, на каком этапе сборки программы происходит объединение единиц трансляции, в чем заключается суть процесса объединения? ##
Единица трансляции — это максимальный объем кода, который компилятор обрабатывает за один раз. Она включает содержимое одного `.cpp` файла и подключенные через `#include` заголовочные файлы.

Объединение единиц трансляции происходит на этапе связывания (линковки).

Суть процесса объединения заключается в следующем:

+ Линковщик связывает все скомпилированные единицы трансляции в один исполняемый файл.
+ Он сопоставляет вызовы функций, переменных и других элементов между различными единицами, разрешая их зависимости.
+ Объединяются также внешние объекты и библиотеки, если они используются

## 4. На какие этапы подразделяет процесс компиляции одной единицы трансляции? В чем их суть? ##

Процесс компиляции одной единицы трансляции подразделяется на следующие этапы:

#### Токенизация ####
Код разбивается на минимальные значимые элементы (токены), такие как ключевые слова, идентификаторы, операторы, и т.д. Например, строка `int a = 42`; превращается в токены: `int`, `a`, `=`, `42`, `;`. Пробелы и отступы игнорируются.

#### Синтаксический анализ ####
Проверяется корректность структуры кода с точки зрения синтаксиса. Например, проверяется правильность написания типов, переменных, функций, а также их расположение и оформление. Это аналог проверки орфографии в тексте.

#### Семантический анализ #### 
Проверяется смысловая правильность кода. Компилятор анализирует последовательность токенов, чтобы убедиться, что они составляют осмысленные конструкции, например, правильность типов в выражениях и соответствие переданных аргументов функциям.

#### Оптимизация ####
Код преобразуется для повышения эффективности. Компилятор сокращает лишние вычисления, разворачивает циклы, вставляет литералы, убирает ненужные ветвления и применяет другие оптимизации.

#### Генерация промежуточного кода ####
Код на языке высокого уровня преобразуется в промежуточное представление, более близкое к машинному коду (например, условно похожее на C). Это помогает убрать абстракции, такие как классы, не поддерживаемые напрямую оборудованием.

#### Генерация объектного кода ####
Компилятор создает машинный код для данной единицы трансляции, включая адресацию локальных переменных и функций. Неизвестные внешние ссылки оставляются для разрешения на этапе связывания.
## 5. На какие два этапа подразделяется выделение переменной? Могут ли они быть разнесены в программе? Что будет хранится в переменной если не установить ее значение? ##
Процесс выделения переменной подразделяется на два этапа:

#### Декларирование (объявление) ####
Это процесс резервирования имени для переменной. После декларации переменной ее можно использовать в коде для обращения к выделенной области памяти. Пример:

```cpp
int a;
```
Здесь объявляется переменная a типа int, но ей не присваивается значение.

#### Инициализация ####
Это процесс присвоения переменной первого значения. Пример:

```cpp
int a = 0;
```
Здесь переменная a сразу инициализируется значением 0.

Могут ли этапы быть разнесены в программе?
Да, они могут быть разнесены. Например:

```cpp
int a;  // Декларация
a = 5;  // Присвоение значения
```

Однако присвоение значения позже не считается инициализацией, так как инициализация происходит только в момент объявления переменной.

Что будет храниться в переменной, если не установить ее значение?
Если переменной не присвоено значение, она содержит "мусорное значение" — случайное значение, оставшееся в памяти, выделенной для этой переменной. Это значение зависит от содержимого памяти, используемой под переменную, и его поведение непредсказуемо.

## 6. На какие две группы делятся типы? Назовите примеры. ##
Типы делятся на две группы:

#### Встроенные типы ####
Это типы, которые уже имеются в языке программирования:

+ Логический тип: bool (хранит значения true или false).
+ Символьный тип: char, wchar_t, char16_t, char32_t (хранят символы в различных кодировках).
+ Целочисленные типы: int, short, long (для хранения целых чисел).
+ Типы с плавающей запятой: float, double (для хранения дробных чисел).
#### Пользовательские типы ####
Это типы, которые программист создает самостоятельно, комбинируя встроенные типы и задавая правила их взаимодействия. Например:

+ Классы.
+ Структуры.
+ Перечисления (enum).

## 7. Какие бывают виды констант? Чем они отличаются? Какие существуют ограничения? ##
### Виды констант и их отличия: ###
#### Константы времени исполнения (runtime constants) ####

Их значение вычисляется во время выполнения программы.
Могут быть объявлены с использованием ключевого слова const.
Такие константы могут зависеть от переменных, значение которых известно только во время выполнения программы.
Пример:
```cpp
int b = 2;
const int N = 10;
const int M = N / b; // Значение M вычисляется при выполнении программы
```
#### Константы времени компиляции (compile-time constants) ####

Их значение вычисляется во время компиляции.
Для их объявления используется ключевое слово constexpr.
Константы времени компиляции должны быть однозначными и не могут зависеть от переменных, значения которых вычисляются во время выполнения программы.
Пример:

```cpp
constexpr int N = 10;
constexpr int M = N * 2; // Вычисляется во время компиляции
```

Пример ошибки:
```cpp
int b = 2;
constexpr int N = b; // Ошибка: значение `b` не известно во время компиляции
```

#### Основные отличия: #### 
Время вычисления значения:
Константы времени исполнения вычисляются во время выполнения программы, а времени компиляции — на этапе компиляции.
Зависимость от переменных:
Константы времени компиляции не могут зависеть от переменных, чьи значения не известны на этапе компиляции.
#### Ограничения: ####
Для констант времени компиляции:

Должны быть однозначными и определяться только из других констант времени компиляции.
Нельзя использовать значения, зависящие от состояния программы во время выполнения.
Для констант времени исполнения:

Инициализируются только один раз, при создании.
После инициализации их значение нельзя изменить, но они могут быть основаны на переменных.

## 8. Что такое область видимости? Что является единицей области видимости в С++? Привести пример видимости переменных во вложенных и параллельных областях видимости. ##
#### Область видимости в C++ ####
+ Область видимости — это правило, определяющее, где переменная доступна для использования. Единицей области видимости является блок кода {}.

#### Основные правила: ####
+ Родительская область: переменные видны в дочерних блоках.
+ Дочерняя область: переменные видны только внутри блока и его вложенных областях.
+ Параллельная область: переменные видны только в своем блоке и вложенных в него.
+ Замещение: переменная в дочерней области с тем же именем скрывает переменную из родительской области.

## 9. Что такое сигнатура функции? Какие части сигнатуры есть? Чем заканчивается функция которая возвращает значение? Может ли функция не возвращать значения? ##

#### Сигнатура функции ####
Сигнатура функции — это описание функции, включающее:

+ Тип возвращаемого значения: указывает, какой тип данных возвращает функция (например, int, double, void и т. д.).
+ Имя функции: уникальное название, следующее правилам именования.
+ Список параметров: включает типы и имена параметров (обязательные и/или с значением по умолчанию).

Пример сигнатуры:

```cpp
double square(double value);
```
Основные моменты:
+ Функция, которая возвращает значение, должна завершаться оператором return с соответствующим значением:


```cpp
return <значение>;
```

+ Функция может не возвращать значения, если используется тип void:
  
```cpp
void printHello() {
    cout << "Hello!";
}
```

+ Параметры функции могут быть обязательными или иметь значения по умолчанию:

```cpp
int sum(int a, int b = 0); // b имеет значение по умолчанию
```

#### Пример реализации и вызова: ####

```cpp
#include <iostream>
using namespace std;

double square(double value) { // Тип double, имя square, параметр value
    return value * value;
}

void printHello() { // Тип void, функция ничего не возвращает
    cout << "Hello!";
}

int main() {
    double x = 5.0;
    cout << "Square: " << square(x) << endl; // Вызов функции square
    printHello(); // Вызов функции printHello
    return 0;
}
```
## 10. Что такое ссылка и указатель, чем они отличаются, в чем они похожи? Для чего используются ссылки, для чего используются указатели? ##

#### Ссылка и указатель в C++ 
Ссылка и указатель — инструменты для работы с памятью, которые позволяют обращаться к одному и тому же участку памяти, но имеют важные различия.

#### Похожесть:
И ссылка, и указатель предоставляют доступ к данным по адресу.
Оба позволяют изменять значение переменной, к которой они относятся.
#### Различия:
Ссылка — это синоним переменной. Она создаётся для доступа к той же памяти, но не занимает отдельное место в памяти.
#### Пример:

```cpp
int a = 10;
int& ref = a; // Ссылка на a
ref = 20;     // Изменяет значение a через ссылку
cout << a;    // Выведет 20
```
 Указатель — это отдельная переменная, которая хранит адрес памяти другой переменной. Он требует выделения памяти для хранения этого адреса.
Пример:

```cpp
int a = 10;
int* ptr = &a; // Указатель на a
*ptr = 20;     // Разыменование указателя, изменение значения a
cout << a;     // Выведет 20
```
 Инициализация: Ссылка должна быть сразу связана с переменной, указатель можно объявить без указания адреса.

```cpp
int a = 10;
int* ptr;      // Указатель может быть пустым
ptr = &a;      // Инициализация позже
int& ref = a;  // Ссылка обязана указывать на переменную при создании
```

 Изменяемость: Ссылка всегда ссылается на одну и ту же переменную, указатель может менять адрес, на который указывает. 

 Использование:
Ссылки удобны для передачи данных в функции без копирования, особенно для больших объектов.
Указатели необходимы для работы с динамической памятью, создания сложных структур данных (например, связных списков), а также для работы с массивами и адресной арифметикой.
## 11. Какие типы памяти есть в С++? Чем они отличаются? На каком этапе жизненного цикла программы определяется их размер? ## 

Типы памяти в C++ и их особенности
#### 1. Статическая память
Статическая память выделяется программе при её запуске. Это фиксированный объём памяти, который используется для хранения переменных, кода программы, литералов и других компонентов. Размер статической памяти определяется на этапе компиляции и остаётся неизменным в течение выполнения программы.

Особенности:
+  Выделяется автоматически при запуске программы.
Используется для хранения глобальных переменных, статических переменных и данных на стеке. Быстрая работа с памятью, так как она управляется компилятором. Размер памяти ограничен и фиксирован.
Когда определяется размер:
+ На этапе компиляции программы.

Применение:
+ Используется для переменных, чьё количество и размер известны заранее, а также для временных переменных внутри функций, циклов или условий.

#### 2. Динамическая память
Динамическая память, также называемая кучей, выделяется программе по запросу во время выполнения. Она управляется операционной системой, которая выделяет необходимый объём памяти для программы.

Особенности:
+ Размер и объём не фиксированы, их можно задавать и изменять в ходе выполнения программы. Управляется вручную с помощью операторов new и delete. Используется для хранения больших массивов данных, сложных структур, и в случаях, когда объём данных заранее неизвестен. Выделение памяти медленнее, чем для статической, из-за необходимости взаимодействия с операционной системой.

Когда определяется размер: 
+ На этапе выполнения программы.

Применение:
+ Незаменима для работы с большими объёмами данных и сложными структурами, особенно если их размер или количество нельзя предсказать заранее.

Пример выделения динамической памяти, оператор new: 

```cpp
int* new_int = new int;
float* new_float = new float;
void* new_void = new char;
```

```cpp
delete new_int;
delete new_float;
delete new_void;
```

#### Сравнение статической и динамической памяти
Статическая память быстрее и проще в использовании, но ограничена по размеру и возможностям. Динамическая память предоставляет гибкость и позволяет обрабатывать большие объёмы данных, но требует более тщательного управления, чтобы избежать утечек памяти.

#### Вывод:
Статическая память используется для локальных переменных и заранее известных данных. Динамическая память необходима для обработки больших массивов данных или сложных структур, особенно если их объём заранее неизвестен.

## 12. Операция взятия указателя и разыменования указателя, их символьные обозначения и суть? ##

#### Операция взятия указателя и разыменования указателя в C++
Операция взятия адреса
+ Символ: &
Суть:
+ Эта операция используется для получения адреса памяти переменной. Она возвращает указатель на переменную, показывая, где в памяти хранится её значение.
Пример:

```cpp
int n = -1;
cout << &n << endl; // Выводит адрес переменной n в памяти, например, 0x61fe1c
```

Применение:
+ Необходима для инициализации указателей.
  
```cpp
int* pn = &n; // Указатель pn хранит адрес переменной n
```

Операция разыменования указателя
+ Символ: *
Суть:
+ Операция используется для получения значения, хранящегося по адресу, на который указывает указатель. Она "разыменовывает" указатель, позволяя работать с данными, находящимися в памяти.
Пример:

```cpp
int n = -1;
int* pn = &n;
cout << *pn << endl; // Выводит значение переменной n, то есть -1
```
Применение:
+ Позволяет изменять или читать данные по указанному адресу.
Взаимосвязь операций
Операции взятия адреса & и разыменования * являются взаимоисключающими, то есть их совместное использование в выражении, например, *&n, возвращает оригинальное значение переменной n.

```cpp
cout << *&n << endl; // Эквивалентно n
```
Пример с пояснением

```cpp
int n = -1;
int* pn = &n;       // Указатель pn хранит адрес переменной n
cout << pn << endl; // Выводит адрес n
cout << *pn << endl; // Выводит значение переменной n (-1)
```
+ &: Получаем адрес переменной n, который сохраняется в pn.
+ *: Получаем значение по адресу, который хранится в pn, то есть n.

Операции взятия адреса и разыменования позволяют работать с памятью напрямую, что делает указатели важным инструментом для управления динамическими структурами данных, взаимодействия с функциями и аппаратными ресурсами.

## 13. Статические массивы, их представление в памяти, указатели на массивы, арифметика указателей? ##


#### Статические массивы и их представление в памяти
Статический массив в C++ — это структура данных фиксированного размера, которая хранится в непрерывной области памяти. Каждый элемент массива располагается строго последовательно друг за другом.

При создании массива:

```cpp
int array[10];
```
переменная `array` фактически представляет собой указатель на первый элемент массива. Адрес переменной `array` совпадает с адресом первого элемента массива (`&array[0]`).

Пример:
```cpp
int array[10] {0};
cout << array << endl;       // Адрес начала массива
cout << &array[0] << endl;   // Тоже самое
```
Особенность статических массивов — адрес их начала жестко связан с самим массивом и не может быть изменен, в отличие от обычного указателя.

#### Указатели на массивы
Указатели в C++ используются для работы с массивами. Можно присвоить массив указателю:

```cpp
int* parray = array;
```

Теперь `parray` указывает на начало массива, и доступ к элементам массива возможен через разыменование:

```cpp
cout << *(parray + 1) << endl; // Значение второго элемента
```

#### Арифметика указателей
С указателями можно производить арифметические операции для навигации по массиву:

+ Сложение (`+`): Смещение вправо по памяти на количество элементов.
+ Вычитание (`-`): Смещение влево по памяти.
+ Инкремент (`++`): Смещение указателя на один элемент вперед.
+ Декремент (`--`): Смещение указателя на один элемент назад.
Особенности:
Смещение указателя зависит от типа данных, на которые он указывает. Например, для `int*` каждое смещение на единицу передвигает указатель на 4 байта (если `sizeof(int) == 4`).
Пример:

```cpp
int array[4] {3, 5, 13, 1};
int* p = array;

cout << *(p + 1) << endl;  // 5
*(p + 1) = 11;             // Изменение второго элемента массива
cout << array[1] << endl;  // 11
```

#### Работа с массивами через указатели
Операция доступа к элементу массива array[N] эквивалентна:

```cpp
*(array + N)
```

Компилятор выполняет смещение указателя на `N * sizeof(тип элемента)` байт и затем разыменовывает полученный адрес.

Итоги
+ Статические массивы хранятся в непрерывной области памяти.
+ Переменная массива (array) является указателем на первый элемент.
+ Арифметика указателей позволяет манипулировать массивами, например, перемещаться между элементами.
+ Операции с массивами зависят от размера базового типа данных.

## 14. Динамические массивы, их представление в памяти, процесс выделения? ##

Динамические массивы — это массивы, размер которых определяется во время выполнения программы, а не на этапе компиляции. Они хранятся в области памяти, называемой кучей (heap), и управляются программистом вручную.

#### Процесс создания динамических массивов ####
+ Выделение памяти: Для создания динамического массива используется оператор new:

```cpp
int* array = new int[size];
```
+ `size` — количество элементов массива.
+ Возвращается указатель на первый элемент массива.
+ Память выделяется в куче, что позволяет массиву существовать до тех пор, пока не будет освобождена вручную.
#### Инициализация массива: После выделения памяти можно заполнить массив:

```cpp
for (int i = 0; i < size; ++i) {
    array[i] = i * 2;  // Пример инициализации
}
```

#### Освобождение памяти: После использования массива память должна быть освобождена оператором `delete[]`:

```cpp
delete[] array;
array = nullptr;  // Указатель обнуляется для предотвращения ошибок доступа
```

#### Представление в памяти
#### Куча (heap):

+ Динамический массив хранится в куче.
+ Указатель (int* array) хранится в стеке (stack) и указывает на первую ячейку массива в куче.

#### Непрерывная область памяти: 

+ Динамический массив, как и статический, представляет собой непрерывный блок памяти.
+ Доступ к элементам осуществляется так же, как в статических массивах, с помощью арифметики указателей или синтаксиса индексов.
Пример программы с динамическим массивом

```cpp
#include <iostream>
using namespace std;

int main() {
    int size;

    // Запрос размера массива у пользователя
    cout << "Введите размер массива: ";
    cin >> size;

    // Создание динамического массива
    int* array = new int[size];

    // Инициализация массива
    for (int i = 0; i < size; ++i) {
        array[i] = i * 10;
    }

    // Вывод значений массива
    cout << "Элементы массива: ";
    for (int i = 0; i < size; ++i) {
        cout << array[i] << " ";
    }
    cout << endl;

    // Освобождение памяти
    delete[] array;
    array = nullptr;

    return 0;
}
```

#### Особенности динамических массивов
#### Гибкость:

+ Размер задается во время выполнения программы.
+ Удобны, когда заранее неизвестен объем данных.

#### Управление памятью:

+ Программист обязан вручную освобождать память.
+ Невыполнение этого правила приводит к утечкам памяти (memory leaks).

#### Риск ошибок:

+ Доступ за пределы массива (out-of-bounds) может привести к неопределенному поведению.
+ Забытая операция delete[] приводит к утечке памяти.

###
# Расширение динамического массива
Так как размер массива фиксируется при выделении памяти, его расширение требует создания нового массива большего размера:

```cpp
int newSize = size * 2;
int* newArray = new int[newSize];

// Копирование данных из старого массива
for (int i = 0; i < size; ++i) {
    newArray[i] = array[i];
}

// Освобождение памяти старого массива
delete[] array;

// Переназначение указателя
array = newArray;
size = newSize;
```

#### Итоги
+ Динамические массивы создаются с помощью new и освобождаются через delete[].
+ Они хранятся в куче, что обеспечивает гибкость при работе с памятью.
+ Правильное управление памятью — ключ к предотвращению утечек и ошибок.

## 15. Операторы new и delete, их суть, тип рабочей памяти, удаление массивов? 

Оператор `new`: выделение динамической памяти
Оператор `new` используется для выделения памяти в куче (heap) — области памяти, управляемой операционной системой. Он возвращает указатель на выделенную область памяти, позволяя программе работать с ней.

Общая форма

```cpp
<тип данных>* <имя переменной> = new <тип данных>;
```

Примеры

```cpp
int* new_int = new int;      // Выделение памяти для одного целого числа
float* new_float = new float; // Для одного числа с плавающей точкой
void* new_void = new char;    // Выделение памяти для одного символа (тип void*)
```

+ Память выделяется динамически и остается доступной, пока не будет вручную освобождена.
+ Возвращаемый оператором `new` указатель указывает на первую ячейку выделенного блока памяти.
+ Переменная, хранящая адрес памяти, размещается в стеке (stack), но сама память выделяется в куче.

#### Оператор `delete`: освобождение памяти
Оператор `delete` освобождает память, выделенную ранее с помощью оператора new, и уведомляет операционную систему о том, что эта память больше не нужна.

Пример использования

```cpp
delete new_int;   // Освобождение памяти для одного объекта
delete new_float;
delete new_void;
```
Если память не освободить, возникает утечка памяти — память остается зарезервированной, хотя программа её уже не использует. Это особенно критично в долгих циклах, где утечка может привести к значительному росту потребления памяти.

#### Работа с массивами в куче
Создание массивов
Для выделения памяти под массив используется тот же оператор new:

```cpp
int* array = new int[10]; // Выделение памяти под массив из 10 элементов
```

Удаление массивов
При удалении динамических массивов обязательно использовать delete[], чтобы освободить всю выделенную память:

```cpp
delete[] array;  // Освобождение памяти под массив
array = nullptr; // Обнуление указателя для предотвращения ошибок
```
Использование `delete` без `[]` при работе с массивом приводит к неопределённому поведению.

#### Отличия работы с динамической памятью в C++ от других языков
#### Отсутствие сборщика мусора:

+ В C++ нет автоматического механизма освобождения памяти, как в Java или Python.
+ Программист сам управляет выделением и освобождением памяти.

#### Гибкость, но повышенная ответственность:

+ В отличие от языков с автоматической сборкой мусора, C++ позволяет более точно контролировать работу с памятью.
+ Однако ошибки в освобождении памяти (утечки или двойное освобождение) могут привести к краху программы или неопределённому поведению.

#### Необходимость следить за областью видимости:

+ При выходе переменной-указателя за область видимости её значение (адрес) теряется, но сама выделенная память в куче остаётся занятой, если не вызван `delete`.

#### Итоги
+ Оператор new выделяет память в куче и возвращает указатель на неё.
+ Оператор delete освобождает память, выделенную оператором new.
+ Для массивов необходимо использовать delete[] для корректного освобождения всей памяти.
+ Управление динамической памятью требует особого внимания, чтобы избежать утечек и других ошибок.

## 16. Файловая структура программы, модули, стражи компиляции
+ Файловая структура: Разделение кода на `.h` (заголовочные файлы) и `.cpp` (реализация).
+ Модули: Логически связанные части кода, которые можно разделить на файлы.
 +Использование модулей: `#include "module.h"` подключает модуль.
+ Стражи компиляции: Используются для предотвращения повторного включения заголовков:
  
```cpp
#ifndef HEADER_H
#define HEADER_H
// код
#endif
```
## 17. Область имен (namespace), using
+ Область имен: Избегает конфликтов имен:

```cpp
namespace myNamespace { int x = 5; }
```
+ Стандартная область имен: std (например, std::cout).
+ Директива using:
  
```cpp
using namespace std; // Упрощает доступ к std::cout -> cout
```

## 18. Нулевой указатель и указатель на пустоту
+ Нулевой указатель: Указывает на ничто, обозначается nullptr. Используется для проверки наличия адреса:
```cpp
int* ptr = nullptr;
```
+ Указатель на пустоту: Указывает на адрес любого типа, тип `void*`:
```cpp
void* ptr;
ptr = &variable; // Пример
```

## 19. Перечисления
+ Описание: Набор именованных констант.
+ Пример:

```cpp
enum Color { RED, GREEN, BLUE };
Color myColor = RED;
```

## 20. Структура
+ Описание: Пользовательский тип данных, объединяющий поля.
Пример:
```cpp
struct Point { int x, y; };
Point p = {1, 2};
```

## 21. Объединение
+ Описание: Переменная занимает одну область памяти для всех полей.
+ Пример:
```cpp
union Data { int i; float f; };
Data d;
d.i = 10; // d.f теряет значение
```

## 22. Псевдонимы
+ Описание: Новый алиас для существующего типа.
+ Пример:
```cpp
using IntAlias = int;
IntAlias x = 10;
```
## 23. Inline функция, аргументы по умолчанию
+ Inline: Устраняет вызов функции, заменяя на код.
```cpp
inline int add(int a, int b) { return a + b; }
```
+ Аргументы по умолчанию:
```cpp
int func(int x = 10) { return x; }
```
## 24. Перегрузка функций, указатели на функции
+ Перегрузка: Одинаковое имя, разный список аргументов.
Указатель на функцию:
cpp
Copy code
int (*funcPtr)(int, int) = add;
## 25. Абстракция
Описание: Сокрытие деталей реализации, предоставление интерфейса.
## 26. Парадигма программирования
Описание: Подход к написанию кода. Изучали ООП.
## 27. Объектно-ориентированное программирование
Три кита: Наследование, инкапсуляция, полиморфизм.
## 28. Класс и объект
Класс: Шаблон.
Объект: Экземпляр.
Пример:
cpp
Copy code
class MyClass {};
MyClass obj;
## 29. Конструкторы и деструкторы
Конструктор: Специальный метод для инициализации.
Деструктор: Метод, вызываемый при удалении объекта.
Пример:
cpp
Copy code
class MyClass {
  MyClass() {}  // Конструктор
  ~MyClass() {} // Деструктор
};

## 30. Наследование
Описание: Позволяет создавать новые классы на основе существующих, наследуя их поля и методы.
Синтаксис:
cpp
Copy code
class Base {}; // Родительский класс
class Derived : public Base {}; // Наследник
Наследование конструкторов: Позволяет использовать конструкторы базового класса в наследнике:
cpp
Copy code
class Derived : public Base {
    using Base::Base; // Наследует конструкторы
};
## 31. Инкапсуляция и модификаторы доступа
Описание: Инкапсуляция — скрытие реализации и предоставление доступа через интерфейс (методы).
Модификаторы доступа:
public: Доступен всем.
protected: Доступен только наследникам и внутри класса.
private: Доступен только внутри класса.
Пример:
cpp
Copy code
class MyClass {
private:
    int secret;
public:
    void setSecret(int s) { secret = s; }
    int getSecret() { return secret; }
};
## 32. Полиморфизм
Описание: Возможность использования одного интерфейса для работы с разными типами объектов.
Пример:
cpp
Copy code
class Base {
public:
    virtual void show() { cout << "Base"; }
};

class Derived : public Base {
public:
    void show() override { cout << "Derived"; }
};

Base* obj = new Derived();
obj->show(); // Вывод: Derived
## 33. Дружественные функции и перегрузка операторов
Описание:
Дружественные функции имеют доступ к приватным полям класса, но не являются членами класса.
Перегрузка операторов позволяет использовать операторы с пользовательскими типами.
Пример дружественной функции:
cpp
Copy code
class MyClass {
    int x;
public:
    MyClass(int val) : x(val) {}
    friend void print(const MyClass&);
};

void print(const MyClass& obj) { cout << obj.x; }
Пример перегрузки оператора:
cpp
Copy code
MyClass operator+(const MyClass& a, const MyClass& b) {
    return MyClass(a.x + b.x);
}
## 34. Некопируемый и несоздаваемый класс
Описание:
Некопируемый класс: Запрещает копирование объектов.
Несоздаваемый класс: Запрещает создание экземпляров.
Примеры:
cpp
Copy code
class NoCopy {
    NoCopy(const NoCopy&) = delete; // Запрет копирования
};

class NoInstance {
    NoInstance() = delete; // Запрет создания объектов
};
## 35. Виртуальные методы
Описание: Методы, которые могут быть переопределены в наследниках.
Пример:
cpp
Copy code
class Base {
public:
    virtual void func() { cout << "Base"; }
};
Чисто виртуальные методы: Определяются как = 0:
cpp
Copy code
virtual void func() = 0;
## 36. Абстрактный и интерфейсный класс
Абстрактный класс: Имеет хотя бы один чисто виртуальный метод. Используется для создания базовых интерфейсов.
Интерфейсный класс: Это абстрактный класс, все методы которого чисто виртуальные.
## 37. Потоки ввода/вывода
Описание: Стандартные потоки для работы с консолью или файлами.
cin для ввода.
cout для вывода.
Пример перегрузки операций:
cpp
Copy code
friend ostream& operator<<(ostream&, const MyClass&);
## 38. Контейнерные классы: последовательные контейнеры
Описание: Контейнеры, хранящие элементы в порядке их добавления.
Примеры:
vector — динамический массив.
deque — двусторонняя очередь.
list — двусвязный список.
## 39. Контейнерные классы: ассоциативные контейнеры
Описание: Контейнеры, хранящие элементы по ключу.
Примеры:
map — ключ-значение.
set — уникальные элементы.
## 40. Итераторы
Описание: Объекты, позволяющие проходить по элементам контейнера.
Пример цикла с итератором:
cpp
Copy code
for (auto it = vec.begin(); it != vec.end(); ++it) {
    cout << *it;
}
## 41. Вектор
Описание: Динамический массив, размер которого изменяется автоматически.
Пример:
cpp
Copy code
vector<int> vec = {1, 2, 3};
vec.push_back(4);
## 42. Список
Описание: Двусвязный список, обеспечивает эффективное добавление и удаление элементов.
Пример:
cpp
Copy code
list<int> lst = {1, 2, 3};
## 43. Стек и очередь
Описание:
Стек: Реализует принцип LIFO.
Очередь: Реализует принцип FIFO.
Примеры:
cpp
Copy code
stack<int> s;
s.push(1);
queue<int> q;
q.push(1);
## 44. Словарь (map)
Описание: Хранит пары ключ-значение с уникальными ключами.
Пример:
cpp
Copy code
map<string, int> dict;
dict["key"] = 42;
## 45. Множество (set)
Описание: Хранит уникальные элементы в упорядоченном виде.
Пример:
cpp
Copy code
set<int> mySet = {1, 2, 3};
## 46. Метапрограммирование, шаблоны
Описание: Позволяет создавать универсальный код для работы с любыми типами.
Пример шаблона функции:
cpp
Copy code
template <typename T>
T add(T a, T b) { return a + b; }
## 47. Шаблонная функция
Описание: Функция, работающая с любым типом данных.
Пример:
cpp
Copy code
template <typename T>
void func(T arg) { cout << arg; }
## 48. Шаблонный класс
Описание: Класс, работающий с любым типом данных.
Пример:
cpp
Copy code
template <typename T>
class MyClass {
    T data;
};

## 49. Стандартная библиотека C++
Описание: Содержит набор инструментов для упрощения разработки: контейнеры, алгоритмы, функции и т.д.
Примеры составляющих:
Контейнеры: vector, map, set.
Алгоритмы: std::sort, std::find, std::for_each.
Ввод/вывод: iostream, fstream.
Стандартная библиотека алгоритмов:
Что содержит: Алгоритмы сортировки, поиска, обработки коллекций.
Пример использования:
cpp
Copy code
vector<int> vec = {3, 1, 4};
sort(vec.begin(), vec.end()); // Сортировка
## 50. Предикат
Описание: Функция, возвращающая true или false в зависимости от условий.
Зачем нужен: Используется в алгоритмах для фильтрации или проверки условий.
Пример:
cpp
Copy code
bool isEven(int x) { return x % 2 == 0; }
vector<int> vec = {1, 2, 3, 4};
auto it = find_if(vec.begin(), vec.end(), isEven);
## 51. Функтор
Описание: Объект класса, который можно вызывать как функцию.
Зачем нужен: Для более сложных операций, чем у простых функций.
Пример:
cpp
Copy code
class Counter {
    int count = 0;
public:
    int operator()() { return ++count; }
};

Counter c;
cout << c(); // 1
cout << c(); // 2
## 52. Лямбда-функции
Описание: Анонимные функции, создаваемые прямо в месте вызова.
Зачем нужны: Упрощают код, делают его компактным.
Пример:
cpp
Copy code
vector<int> vec = {1, 2, 3};
auto it = find_if(vec.begin(), vec.end(), [](int x) { return x > 2; });
## 53. Структура объявления лямбда-функции
Описание: Лямбда состоит из:
Захвата переменных: [&x, y] (по ссылке, по значению).
Списка параметров: (int a, int b).
Тела функции: { return a + b; }.
Минимальное объявление:
cpp
Copy code
[]() {};
## 54. Исключения
Описание: Механизм обработки ошибок во время выполнения программы.
Пример:
cpp
Copy code
try {
    throw runtime_error("Error");
} catch (const runtime_error& e) {
    cout << e.what();
}
## 55. Порождение исключений
Описание: Исключения могут быть созданы с помощью throw.
Пример собственного класса исключений:
cpp
Copy code
class MyException : public exception {
    const char* what() const noexcept override { return "My error"; }
};

try {
    throw MyException();
} catch (const MyException& e) {
    cout << e.what();
}
## 56. Производительность исключений
Описание: Исключения полезны, но могут снижать производительность из-за накладных расходов.
Рекомендации:
Использовать для обработки редких ошибок.
Для частых случаев использовать проверки (if).
Порядок отлова исключений: От более специфичных к более общим.

## Примеры практических заданий
#### 1. Выделить память под трехмерный массив
Задание: Создайте динамический трехмерный массив, заполните его значениями и освободите память.

Пример решения:

```cpp
int*** create3DArray(int x, int y, int z) {
    int*** arr = new int**[x];
    for (int i = 0; i < x; ++i) {
        arr[i] = new int*[y];
        for (int j = 0; j < y; ++j) {
            arr[i][j] = new int[z];
        }
    }
    return arr;
}

void delete3DArray(int*** arr, int x, int y) {
    for (int i = 0; i < x; ++i) {
        for (int j = 0; j < y; ++j) {
            delete[] arr[i][j];
        }
        delete[] arr[i];
    }
    delete[] arr;
}

int main() {
    int x = 3, y = 3, z = 3;
    int*** array = create3DArray(x, y, z);

    // Заполнение массива
    for (int i = 0; i < x; ++i)
        for (int j = 0; j < y; ++j)
            for (int k = 0; k < z; ++k)
                array[i][j][k] = i + j + k;

    delete3DArray(array, x, y);
    return 0;
}
```
#### 2. Написать класс комплексного числа
Задание: Реализуйте класс, представляющий комплексное число, с возможностью сложения и вывода.

Пример решения:

```cpp
#include <iostream>
using namespace std;

class Complex {
    double real, imag;
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    friend ostream& operator<<(ostream& out, const Complex& c) {
        return out << c.real << " + " << c.imag << "i";
    }
};

int main() {
    Complex a(1, 2), b(3, 4);
    Complex c = a + b;
    cout << c << endl; // 4 + 6i
    return 0;
}
```

#### 3. Для класса `MyInt` переопределить вывод в поток
Задание: Реализуйте класс MyInt и переопределите оператор <<.

Пример решения:

```cpp
class MyInt {
    int value;
public:
    MyInt(int val = 0) : value(val) {}

    friend ostream& operator<<(ostream& out, const MyInt& obj) {
        return out << "MyInt: " << obj.value;
    }
};

int main() {
    MyInt num(42);
    cout << num << endl;
    return 0;
}
```

#### 4. Переопределить оператор суммирования двух MyInt
Задание: Реализуйте оператор + для класса MyInt.

Пример решения:

```cpp
class MyInt {
    int value;
public:
    MyInt(int val = 0) : value(val) {}

    MyInt operator+(const MyInt& other) const {
        return MyInt(value + other.value);
    }

    friend ostream& operator<<(ostream& out, const MyInt& obj) {
        return out << obj.value;
    }
};

int main() {
    MyInt a(10), b(20);
    MyInt c = a + b;
    cout << c << endl; // 30
    return 0;
}
```

#### 5. Написать дружественную функцию копирования хранилища MyArray в std::vector
Задание: Реализуйте дружественную функцию для копирования данных из пользовательского класса в std::vector.

Пример решения:

```cpp
#include <vector>
using namespace std;

class MyArray {
    int* data;
    size_t size;
public:
    MyArray(size_t sz) : size(sz) {
        data = new int[size];
        for (size_t i = 0; i < size; ++i) data[i] = i + 1;
    }

    ~MyArray() { delete[] data; }

    friend void copyToVector(const MyArray& arr, vector<int>& vec);
};

void copyToVector(const MyArray& arr, vector<int>& vec) {
    vec.assign(arr.data, arr.data + arr.size);
}

int main() {
    MyArray arr(5);
    vector<int> vec;
    copyToVector(arr, vec);

    for (int val : vec) cout << val << " "; // 1 2 3 4 5
    return 0;
}
```

6. Написать свой класс исключения
Задание: Создайте пользовательский класс исключения и используйте его.

Пример решения:

```cpp
#include <exception>
#include <iostream>
using namespace std;

class MyException : public exception {
public:
    const char* what() const noexcept override {
        return "Custom exception occurred!";
    }
};

int main() {
    try {
        throw MyException();
    } catch (const MyException& e) {
        cout << e.what() << endl;
    }
    return 0;
}
```

#### 7. Продемонстрировать работу области видимости
Задание: Покажите работу глобальных, локальных и статических переменных.

Пример решения:

```cpp
#include <iostream>
using namespace std;

int globalVar = 10;

void showScopes() {
    static int staticVar = 20;
    int localVar = 30;

    cout << "Global: " << globalVar << ", Static: " << staticVar << ", Local: " << localVar << endl;
    staticVar++;
}

int main() {
    showScopes();
    showScopes();
    return 0;
}
```

#### 8. Продемонстрировать работу наследования конструкторов
Задание: Используйте `using` для наследования конструкторов.

Пример решения:

```cpp
class Base {
protected:
    int value;
public:
    Base(int val) : value(val) {}
};

class Derived : public Base {
public:
    using Base::Base; // Наследуем конструкторы
};

int main() {
    Derived obj(42);
    return 0;
}
```

#### 9. Отнаследоваться от класса и переопределить метод, вызвав родительский
Задание: Переопределите метод в производном классе, вызвав метод базового класса.

Пример решения:

```cpp
class Base {
public:
    virtual void show() { cout << "Base" << endl; }
};

class Derived : public Base {
public:
    void show() override {
        Base::show();
        cout << "Derived" << endl;
    }
};

int main() {
    Derived obj;
    obj.show();
    return 0;
}
```
