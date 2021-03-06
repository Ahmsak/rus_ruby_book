## Numeric

**Добавленные модули: Comparable**

Абстрактный класс для работы с числами.

Если в результате выполнения какого-либо выражения интерпретатор возвращает число, то оно автоматически переводится в десятичную систему счисления.

### Приведение типов

#### Неявное приведение

Подклассы чисел за внешней схожестью имеют различную внутреннюю реализацию. Поэтому перед вызовом метода, интерпретатор приводит переданные аргументы к одному классу. Делается это в соответствии с приведенным ниже списком:

1. Если одно из чисел - комплексное, то и другие числа будут преобразованы в комплексные;

2. Если одно из чисел - десятичная дробь, то и другие числа будут преобразованы в десятичные дроби;

3. Если одно из чисел - рациональная дробь, то и другие числа будут преобразованы в рациональные дроби.

Результат будет экземпляром того же класса, к которому приводятся аргументы.

#### Явное приведение

`.coerce(number) # -> array`

Используется для преобразования двух чисел к одному типу.

1. Если числа принадлежат к разным классам, то они преобразуются в десятичные дроби с помощью метода `.Float`;

2. Текст преобразуется, если он содержит только цифры (поддерживаются двоичная и шестнадцатеричная системы счисления).

~~~~~ ruby
  1.coerce 2.1 # -> [2.1, 1.0]
  1.coerce "2.1" # -> [2.1, 1.0]
  1.coerce "0xAF" # -> [175.0, 1.0]
  1.coerce "q123" # -> error!
~~~~~

`.i # -> complex`

Преобразование числа в комплексное. Метод удален из класса Complex.  
`1.i # -> (0+1i)`

`.to_c # -> complex`

Преобразование числа в комплексное.  
`1.to_c # -> (1+0i)`

`.to_int # -> integer`

Преобразование числа в целое с помощью метода `number.to_i`.  
`2.1.to_int # -> 2`

### Операторы

`.%(number)`  
Синонимы: `modulo`

Используется для вычисления остатка от деления.

`.+(number)` Унарный плюс.

`.-(number)` Унарный минус.

`.<=>(number)` Сравнение.

### Округление

`.ceil # -> integer`

Используется для нахождения наименьшего целого числа, которое будет больше или равно текущего (округление в большую сторону).  
`2.1.ceil # -> 3`

`.floor # -> integer`

Используется для нахождения наибольшего целого числа, которое будет больше или равно текущего (округление в меньшую сторону).  
`2.1.floor # -> 2`

`.round( precise = 0 ) # -> number`  

Используется для округления с заданной точностью. Точность определяет разряд, до которого будет выполнено округление.

~~~~~ ruby
  2.11355.round 4 # -> 2.1136
  2.round 4 # -> 2.0
~~~~~

`.truncate # -> integer`

Целая часть числа.  
`2.1.truncate # -> 2`

### Математические функции

`.abs2 # -> number`

Квадрат числа.  
`-2.1.abs2 # -> 4.41`

`.numerator # -> integer`

Числитель рациональной дроби, полученной с помощью метода `number.to_r`.  
`2.1.numerator # -> 4728779608739021`

`.denominator # -> integer`

Знаменатель рациональной дроби, полученной с помощью метода `number.to_r`.  
`2.1.denominator # -> 2251799813685248`

`.divmod(number) # -> array`

Частное и остаток от деления.  
`1.divmod 3 # -> [0, 1]`

`.div(number) # -> integer`

Округленное частное (округление выполняется с помощью метода `number.to_i`).  
`1.div 3 # -> 0`

`.fdiv(number) # -> float`

Частное в виде десятичной дроби.  
`1.fdiv 3 # -> 0.3333333333333333`

`.quo(number) # -> quotient`

Частное двух чисел. Для двух целых чисел результатом будет рациональная дробь.  
`1.quo 3 # -> (1/3)`

`.remainder(number) # -> integer`

Остаток от деления, вычисляемый как  
`self – number * ( self / number ).truncate`.  
`1.remainder 3 # -> 1`

`.abs # -> number`

Модуль числа.  
`-2.1.abs # -> 2.1`

`.arg # -> number`  
Синонимы: `angle, phase`

Угловое значение для полярной системы координат.

Для действительных чисел возвращает ноль, если число не отрицательно. В другом случае возвращается ссылка на константу `Math::PI`.

~~~~~ ruby
  1.arg # -> 0
  -1.arg # -> 3.141592653589793
~~~~~

`.polar # -> array`

Число в полярной системе координат (`[ self.abs, self.arg ]`).  
`1.polar # -> [1, 0]`

`.real # -> number`

Вещественная часть числа.  
`1.real # -> 1`

`.imag # -> 0`  
Синонимы: `imaginary`

Мнимая часть числа.

`.rect # -> array`

Число в прямоугольной системе координат (`[ self, 0 ]`).  
`1.rect # -> [ 1, 0 ]`

`.conj # -> self`  
Синонимы: `conjugate`

Сопряженное число (используется для комплексных чисел).

### Предикаты

`.integer? # -> bool`

Проверка относится ли число к целым.

~~~~~ ruby
  1.integer? # -> true
  2.1.integer? # -> false
~~~~~

`.real? # -> bool`

Проверка относится ли число к действительным (отрицательный результат возвращается только для комплексных чисел).  
`1.real? # -> true`

`.nonzero? # -> bool`

Сравнение с нулем. Возвращает число, если оно не равно нулю.

~~~~~ ruby
  1.nonzero? # -> 1
  0.0.nonzero? # -> nil
~~~~~

`.zero? # -> bool`

Сравнение с нулем.

~~~~~ ruby
  1.zero? # -> false
  0.0.zero? # -> true
~~~~~

### Итераторы

`.step( limit, step = 1) { |number| } # -> self`

Перебор чисел.

Если одно из чисел не относится к целым, то все числа преобразуются в десятичные дроби. При этом число итераций соответствует  
`n + n * Flt::EPSILON`, где `n == limit – self / step`.

### Остальное

`.singleton_method_added(*object)`

Попытка определить собственный метод числа считается исключением.