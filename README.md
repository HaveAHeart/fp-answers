# 1. Сравнение императивного и декларативного подходов к программированию. Примеры языков.

Вкратце: 

- императивная программа отвечает на вопрос "как"
- декларативная программа отвечает на вопрос "что"

## Императивное программирование

Программа - набор инструкций, изменяющих состояние системы. Всё остальное - абстракции.

Выполнение программы - переход между состояниями.

Примеры:

- Fortran
- Java
- C#
- ...

## Декларативное программирование

Программа задается в виде формальной спецификации (описывается ожидаемый результат).

Примеры:

- XML
- SQL
- Prolog
- Haskell
- ...

# 2. Функциональное программирование. Основные особенности.

Функциональное программирование - частный случай декларативного программирования.

Программа - выражение (функция в математическом смысле), которое можно вычислить.

Выполнение программы - вычисление этого выражения.

Примеры:

- LISP
- Haskell
- F#
- ...

Особенности:

- Используются только чистые функции
- Функции — это данные, а данные — это функции
- Захват переменных из контекста (closures)
- Полнота через рекурсию
- Каррирование (currying)

# 3. История ФП. Возникновение. Семейства языков.

Лямбда-исчисление было придумано Алонзо Чёрчем в 1930-х

LISP - первый функциональный язык программирования (1958)

- позволяет использовать 
  - лямбда-функции 
  - рекурсию
  - условные выражения,
- имеет динамическую типизацию
- имеет garbage collector
- все является линейным списком, в т.ч. сама программа

Другие функциональные языки программирования:

- ML (197x)
  - вывод типов
  - алгебраические типы данных
- Miranda (1985)
  - lazy evaluation
- Erlang (1986)
  - совмещал особенности функционального и логического программирования
  - сверхпараллельность (поддержка процессов)
  - модель акторов
  - устойчивость к сбоям
- Haskell (1990)
  - чисто функциональное программирование
  - строгая статическая типизация
  - вывод типов
  - lazy evaluation
- Scala
  - Java + Haskell
- F#
  - OCaml + C#
- Swift
- Kotlin
- Rust
- Dart
- ...

# 4. Лямбда-исчисление. Основные понятия и механизмы. Вычисление в лямбда-исчислении

Лямбда-исчисление - формальная система для формализации и анализа вычислимости.

- все - это функция от одного аргумента.
- значения можно заворачивать в новые функции
- к аргументам внутри функции можно применять другие функции

Типы выражений:

- Лямбда-выражения
- Применения одних выражений к другим
- Переменные

В основе системы лежат 2 операции:

- абстракция - построение лямбда-функции от аргумента (`𝜆x.<выражение над x>`)
- аппликация - вызов функции к заданному аргументу (`f a`, где `f` - функция, `a` - аргумент)

Вычисление - переписывание термов (`(𝜆x.y) a`, в выражении `y` заменить все `x` на `a`). Достигается это при помощи:

- 𝛼-конверсия - переименовывание переменных в лямбдах
  - 𝛼-эквивалентность - отношение выражений, при котором они являются одинаковыми с точностью до 𝛼-конверсии
- 𝛽-редукция - заменяет все вхождения аргумента на входящее значение
  - 𝛽-нормальная форма - выражение после применения 𝛽-редукции, если она завершается за конечное число шагов
  - 𝛽-эквивалентность - отношение выражений, при котором их 𝛽-нормальные формы одинаковы

# 5. Лямбда-исчисление. Представление данных. Булеаны Чёрча и пары Чёрча

Булеаны Чёрча:

```
true ∶= 𝜆 x y . x
false ∶= 𝜆 x y . y
if ∶= 𝜆 c t f . c t f

not ∶= 𝜆 b x y . b y x  
```

Пары Чёрча:

```
pair ∶= 𝜆 a b f . f a b
first ∶= 𝜆 p . p (𝜆 a b . a)
second ∶= 𝜆 p . p (𝜆 a b . b)
```

Принцип замыкания (closure): Все символы, которые были видны в функции на момент её создания, доступны внутри этой 
функции даже после её создания, т.е. каждая функция может потенциально хранить в себе кучу данных.

# 6. Лямбда-исчисление. Представление данных. Числа Чёрча.

Натуральные числа можно выразить через числа Пеано (есть только 0 и операция +1):

```
0 ∶= 𝜆 f y . y
1 ∶= 𝜆 f y . f y
2 ∶= 𝜆 f y . f (f y)
3 ∶= 𝜆 f y . f (f (f y))
...

inc ∶= 𝜆 n f y . f (n f y)
dec ∶= 𝜆 n f y . n (𝜆 g h . h (g f)) (𝜆 q . y) (𝜆 u . u)

+ ∶= 𝜆 a b f y . a f (b f y)
- ∶= 𝜆 m n . n dec m
* ∶= 𝜆 m n . n (+ m) 0

isZero ∶= 𝜆 n . n (𝜆 x . false) true
```

# 7. Лямбда-исчисление. Рекурсия

```
m ∶= 𝜆 x . x x
𝜔 ∶= m m
```

𝜔-комбинатор - дивергентный комбинатор, способный переписываться сам в себя.

Y-комбинатор (комбинатор неподвижной точки):

```
y ∶= 𝜆 f . (𝜆 x . f (x x)) (𝜆 x . f (x x))
```

# 8. Чистые функции. Особенности программирования на чистых функциях. Функции высших порядков. Каррирование.

Чистая функция - функция в программном и математическом смысле; функция, которая не производит побочных эффектов:

- IO-операции
- изменение глобальных и локальных переменных (отсутствует изменяемое состояние)

Особенности функционального подхода:

- все является функциями
- функции могут принимать и возвращать функции
- функции идемпотентны
- функции не производят побочных изменений
- можно создавать на лету (лямбда-выражения) и возвращать как значения
- можно передавать как аргументы другим функциям

Функции высших порядков — функции, оперирующие функциями (`map`, `filter`).

Каррирование дает возможность представить функцию от N аргументов в виде функции от 1 аргумента, возвращающей функцию от
N - 1 аргумента.

# 9. Ленивая и энергичная (строгая) стратегии исполнения. Разновидности и примеры.

## Ленивая стратегия исполнения

Ленивая стратегия исполнения - стратегия, при которой вычисление выражения откладывается до тех пор, пока не понадобится 
результат вычисления этого выражения. Таким образом аргументы функции могут быть вычислены уже непосредственно во 
время выполнения функции.

Виды:

- call-by-name - вычисляем аргумент по мере надобности каждый раз, когда он нужен
- call-by-need - вычисляем аргумент в какой-то момент времени до того, как он понадобится, и запоминаем его

## Энергичная стратегия исполнения

Энергичная стратегия исполнения - стратегия, при которой вычисление результатов выражений происходит до применения 
функций к ним.  

Виды:

- call-by-value - вычисляем аргумент до вызова функции и передаём туда его значение
- call-by-reference - вычисляем аргумент до вызова функции и передаём в функцию ссылку на него
- ...

### Примеры ленивого выполнения

Haskell является языком с ленивым исполнением.

В ООП языках (Java, C++, ...) `if` является ленивым, т.к. вычисление обеих веток и выбор нужной из них не эффективно.

Логические операции `&&` и `||` также являются ленивыми.

# 20. Классы типов в Haskell. Аппликативные функторы, монады

### Чуть больше про монады

Любая монада - аппликативный функтор, и при помощи функций, реализованных в типе аппликативного функтора, реализуются некоторые функции монады:

- `pure` (functor) = `return` (monad)

- `fmap` (functor) = `fmap` (monad)

Есть более короткий набор для реализации монады:

- `return :: a -> m a`

- `bind aka >>= :: m a -> (a -> m b) -> m b`


По сути, `bind` - это `flatten` на `fmap` со следующими законами:

```
(>>=) :: m a -> (a -> m b) -> m b
x >>= f = flatten (fmap f x)

Где:
return x >>= f === f x
m >>= return === m
(m >>= f) >>= g === m >>= (\x -> f x >>= g)
```

Аппликативный функтор можно выразить через монаду, но не наоборот (`bind` невыразим в обратном случае).

### Do-синтаксис

Do-синтаксис в монадах позволяет задавать контекст при вычислениях - получается очень похоже на использование переменных, поэтому часто используется. Пример:

```
xplusytimez =
    x >>= \ x' ->
        y >>= \ y' ->
            (f y') >>= \ z' ->
                return $ x' + y' * z'

xplusytimez =
    do
        x' <- x
        y' <- y
        z' <- f y'
        return $ x' + y' * z'
```

Использование монадных инструментов упрощает работу с, например, Maybe и Error, избавляя от необходимости руками писать проверки на корректность используемых данных.

### Примеры монад из ООП:

- Асинхронное программирование (`future`/`promise`)

- Реактивное программирование (`observable`)

# 21. Монады: Reader, Writer, State.

### Reader

Задаёт контекст для вычислений, который может быть получен "извне", и задаётся при вызове `runReader`:

```
xplusenv x = do
    x' <- x
    env <- ask
    return $ x' + env
fortyTwoPlusEnv = xplusenv (return 42)
runReader fortyTwoPlusEnv 3 === 45
runReader fortyTwoPlusEnv 8 === 50

```

### Writer

Задаёт контекст для вычислений, в который может быть что-либо записано "изнутри", и прочитано впоследствии при вызове `runWriter`:

```
logFirst x y = do
    x' <- x
    y' <- y
    if (x' > y') then tell [x']
        else return ()
    return $ x + y
foo = logFirst (return 5) (return 4)
fee = logFirst (return 13) (return 12)
bar = logFirst foo fee
runWriter foo === (9, [5])
runWriter fee === (25, [13])
runWriter bar === (34, [5,13,9])
```

### State

Объединение `Reader` и `Writer`: контекст, в который можно писать (`put`) и из которого можно читать (`get`).

Стоит отметить, что подобное псевдо-изменяемое состояние всё ещё функционально-чистое:

- Контекст невозможно создать без использования внешних функций;

- Сам контекс изолирован в монадных операциях, чтобы получить оттуда значения также нужны внешние функции.

Если представить, что всё окружающее состояние программы - это состояние, которое можно поместить в `State`, и изменить `runState` на `main` - получится монада `IO`.

# 22. Монады-трансформеры.

Иногда возникает необходимость использовать несколько разных контекстов отновременно:

- `Error` + `State`

- `State` + `IO`

- ...

Для подобных случаев существуют монады-трансформеры: в них все операции реализованы так, чтобы они передавались "внутренней" монаде.


```
type GetCtx a = State (Input, Position) a
type Parser a = ErrorT GetCtx a
```

# 23. Хвостовая рекурсия.

В процедурных программах глубина стека ограничена - превысили глубину, получили StackOverflow.

В ФП - слишком много через рекурсию - что делать? 

Оптимизация хвостовых вызовов (TCO - tail call optimisation). Общая идея:

- В каждом кадре стека хранятся переменные/аргументы, адрес возврата и результат

- Если подобных хранимых частей кадра нет/они не нужны, то кадр можно перезаписать

- Для такого нужно, чтобы рекурсивный вызов был последним вызовом в теле функции - например, можно рекуррентно передавать локальную переменную

```
fact 0 = 1
fact 1 = 1
fact n = n * fact $ n - 1

tc_fact 0 k = k
tc_fact 1 k = k
tc_fact n k = tc_fact (n - 1) (k * n)
fact n = tc_fact n 1
```

TCO:

- Есть в большинстве функциональных ЯП

- Отсутствует во многих "гибридных" ЯП (Java, Python) - ФП на таких языках будет грустным

- В Haskell TCO не особо полезна из-за ленивости языка


# 24. Амортизированная сложность алгоритмов. Метод банкира. Примеры.

В ФП вместо быстрых массивов - медленные связанные структуры данных. Кажется, что это значит, что на ФП нельзя написать что-либо быстрое, однако необходимо  просто использовать другой вид оценки:

- Наихудшая - привычная нам по структурному программированию/ООП, не подходит;

- Средняя

- Амортизированная - именно она будет интересна

Один из примеров поиска амортизированной сложности "в лоб" - метод агрегатов: доказать, что для любой последовательности операций из заданного набора средняя сложность на операцию равна заданной.

Метод агрегатов сложный, поэтому ему на замену придуманы методы банкира и физика.

Метод банкира:

- Считаем, что за каждую операцию платят фиксированную зарплату (e.g. 3$)

- За каждую примитивную операцию нужно заплатить 1$

- Амортизированная сложность операции - максимально возможные убытки

Пример с `ArrayList`/`Vector`/etc.:

- Добавление в конец: +3$
  
  - При этом -1$ на копирование элемента

- Удаление с конца: -1$ (из тех, что мы заработали при добавлении элемента)

- Таким образом, на векторе из N элементов всегда получим минимум N$

- Эти же N$ уйдут на операцию перевыделения памяти при необходимости - т.е. мы всегда выйдем как минимум в ноль, скорее всего, даже останемся в плюсе

- -> Операции добавления и удаления в векторе амортизированно константные

# 25. Амортизированная сложность алгоритмов. Метод физика. Примеры.

Для метода физика нужны:

- Начальное состояние системы: потенциал равен нолю

- В качестве функции потенциала берётся функция по внутреннему состоянию системы

Пример с `ArrayList`/`Vector`/etc.:

- Начальный потенциал: ноль

- Потенциал вектора: `|N - (M - N)|`, где N - число активных элементов, M - размер массива

- Добавление в конец - операция `O(1)`, по формуле увеличивает потенциал на 2

- Перевыделение - операция `O(N)`, уменьшает потенциал с N до 0

- Удаление с конца - операция `O(1)`, которая:
  
  - В верхней "половине" вектора уменьшает потенциал на 2
  
  - В нижней "половине" вектора увеличивает потенциал на 2

# 26. Изменяемые/неизменяемые структуры данных. Персистентное/эфемерное применение СД.

### Изменяемые структуры данных

- Скрытое изменяемое состояние

- Обычно просты

- Простые алгоритмы

### Неизменяемые структуры данных

- Нет внутренних изменений

- каждое изменение - новый экземпляр

- Легче искать ошибки

- Легче параллелить

- Сложнее реализовать

В ФП - все структуры данных являются неизменяемыми - сейчас нас интересуют только они.

### Примерение структур данных

- Эфемерное - изменение на месте, передача в функции

- Персистентное - существующее в нескольких состояниях одновременно
  
  - Персистентность - способность пережить "создателя"
  
  - иногда персистентное использование = 1-2 копии структуры, иногда - тысячи

# 27. Функциональные структуры данных: очередь и zipper.

### Очередь

Очередь aka Queue реализована через два однонаправленных списка:

- Список добавляемых элементов

- Список удаляемых элементов

- Инвариант - список удаляемых элементов не может быть пустым, если список добавляемых не пуст

- Реализация инварианта - если удаляемый пуст, а добавляемый - не пуст, то переворачиваем список добавляемых и меняем списки местами

### Zipper

Иногда при работе с листами возникает необходимость вставить/удалить много элементов в какую-то точку в середине листа. Для таких операций хорошо подходит zipper, реализуемый через два однонаправленных списка:

- Первый список - левая часть (до указателя)

- Второй список - правая часть (после указателя)

Zipper персистентен и может быть расширен на другие структуры данных.

# 28. Функциональные структуры данных: деревья поиска. Красно-чёрное дерево.

Красно-чёрное дерево - одно из самых известных бинарных деревьев поиска:

- Каждая вершина имеет цвет - красный или чёрный

- Листья дерева всегда чёрные

- У красной вершины не может быть красных детей

- Все пути от корня до листа должны содержать одинаковое количество чёрных вершин

При балансировке различных деревьев меняются только вершины, ведущие к балансируемому узлу - остальные делят память с новой версией.

Зачастую нет смысла в идеальной балансировке дерева - большое число операций балансировки негативно сказывается на производительности, а достигаемого в, например, красно-чёрном дереве, logN хватает - это в любом случае намного меньше, чем N.

# 29. Функциональные структуры данных: кучи.

Бинарное дерево, в котором корень - наименьший элемент.

Обычно куча реализована в виде дерева, которое иногда может быть упаковано в массив.

Heap property - дети всегда больше родителей.

Пример: левосторонняя куча (leftist heap):

- бинарное дерево

- ранг - длина правой хорды вершины

- ранг левого ребёнка больше или равен рангу правого ребёнка

- обычно ранг хранят прямо в дереве (чтобы не пересчитывать)

Ещё пример: двоичная куча:

- Состоит из биномиальных деревьев

- Деревья реализуют Heap property

- Дерево ранга N - это два дерева ранга (N - 1), где левое дерево подвешено к вершине правого

- Количество элементов - число, двоичным представлением которого является куча
  
  - Где дерево есть - 1, где нет - 0
  
  - Объединение куч = сложение двоичных чисел

- Сложности операций:
  
  - Поиск + удаление минимума  - `O(K) | K <= log (N + 1)`
  
  - Можно хранить минимальный элемент - тогда операция константная
  
  - Вставка элемента - `O(K) | K <= log (N + 1)` (на самом деле амортизированно константна)

# 30. Функциональные структуры данных: случайные структуры данных. Treap.

Treap = Tree + Heap, реализуется следующим образом:

- В каждой ячейке два значения:
  
  - По первому - бинарное дерево поиска
  
  - По второму - куча

- Куча хорошо самобалансируется - значит, не надо тратиться на операции перебалансировки

- Значение для кучи берётся из генератора случайных чисел
  
  - Вероятность выйти по высоте за `4 log N` крайне мала

Помимо операций с деревом, есть две дополнительные операции:

- `split` - делим дерево на два поддерева
  
  - Игнорируем heap property, но следим за балансом дерева поиска

- `merge` - сливаем два дерева в одно
  
  - Игнорируем сортированность, но следим за heap property

# 31. Функциональные структуры данных: случайные структуры данных. Skip list.

Вместо дерева поиска можно использовать отсортированный массив (бинарный поиск по нему). Однако в ФП нет массивов, только однонаправленные списки. Значит, можно вставить ссылки больше, чем на один элемент вперёд:

- Идём по самому первому списку (начало - конец), сравниваем текущий элемент с искомым

- "Перепрыгнули" - возвращаемся к предыдущему элементу и спускаемся на уровень ниже

- Повторяем до нахождения элемента

- `O(log N)` если ссылки оптимальны и количество уровней тоже `O(log N)`

- Организация ссылок - броском монетки:
  
  - Да - вставляем в текущий список и все нижележащие
  
  - Нет - спускаемся ниже и повторяем цикл

- Хороший генератор - хорошая оптимальность ссылок

# 32. Функциональные структуры данных: индексные деревья и хеш-деревья.

### Индексное дерево

- Бинарное дерево с большим количеством детей - 32/64

- Небольшие массивы "бесплатно" копируются 

- Индексирование - по битам внутри значений

- Рядом с каждым элементом - маска: число, в котором битами указано, где в массиве есть элементы

Получаем:

- Дешёвое копирование (маленькие массивы)

- Остальные операции - персистентны (как в обычном дереве)

- Меняем размер дерева - регулируем персистентность/высоту

### Хэш-дерево

Индексное дерево, где вместо индекса - хэш. Чисто в теории, везде константы - доступ константный, как у хэш-таблицы, но на практике хуже.

# 33. Метод расписаний (Scheduling) и его применение к функциональным структурам данных. Очередь с константными операциями.

### Sheduling

У большинства структур данных в ФП - хорошая амортизированная сложность, но их сложно использовать в персистентном режиме. В общем случае, можно попробовать свести операцию с амортизированной сложностью к операции с наихудшей сложностью. Для такого сведения используется, например, метод расписаний:

- Применяется при:
  
  - Амортизированно константной сложности операции
  
  - Возможности разбить операцию на много маленьких константных операций

- Использует ленивые техники

- В общем случае невозможно

Общая идея:

- В структуру данных добавляется ленивый список работ, которые нужно выполнить в момент выплаты долга

- Например, очередь (queue) при реализации через два списка с необходимостью переворачивать один из них, при этом `reverse` - монолитная операция

- Значит, при каждой операции над очередью лениво делается часть `reverse`, а результат сохраняется в промежуточном списке

- Для этого в конец выходного списка добавляется обещание перевернуть входной список

- Работает, только когда длины списков равны

- Промежуточный список - "список-счётчик", содержащий ещё ленивые элементы

```
-- Добавить в конец выходного списка обещание входного
rotate [] (y:_) a = y:a
rotate (x:xs) (y:ys) a =
x : rotate (Queue xs ys (y:a))

-- Зафорсить ровно 1 элемент из расписания
exec (Queue f r (x:s)) = (Queue f r s)
exec (Queue f r []) = let f' = rotate f r [] in Queue f' [] f'


push (Queue f r s) x = exec (Queue f (x:r) s)
top (Queue [] r s) = error "empty queue"            
    (Queue (x:f) r s) = x
pop (Queue [] r s) = error "empty queue"
    (Queue (x:f) r s) = exec (Queue f r s)

```

# 34. Ленивое выполнение. Особенности ленивых алгоритмов.

Haskell - язык с ленивым выполнением, если точнее - `call-by-need`: значение считается один раз, затем просто подставляется. 

Некоторые привычные операторы даже в привычных энергичных языках являются ленивыми: `if` (иначе просчитывает результаты из обеих веток), `&&`, `||`.

Однако у ленивых алгоритмов есть ряд недостатков:

- Тяжелее дать оценку сложности

- Возможны тормоза приложения в неожиданные моменты времени

- Ошибки могут быть отложены до неизвестного заранее момента

Избавиться от ленивости в необходимых местах возможно одним из следующих способов:

- `seq` , считает всего на 1 уровень

- `deepseq`, считает до конца

- `!(h:t) / $!` - BangPatterns

- `'` - строгие версии функций на основе `seq`, например, `foldl` - `foldl'` 

# 35. Ленивое выполнение. Работа со списками в ленивом языке.

Haskell - ленивый, структуры данных в нём - тоже:

```
list = [0, 1, 2, 3, error "Slap!", 5]
...
show $ take 3 list -- [0, 1, 2]
show $ take 5 list -- Slap!
```

Списки могут быть рекуррентно-бесконечными:

```
list = 1 : list
```

Фактически, выше получили бесконечный список единиц.

Комбинаторы, которым не нужен весь список, будут работать на бесконечных списках:

- `map`

- `filter`

- `zip`/`zipWith`

Функции, которым нужен весь список. могу не работать:

- `show`

- `length`

- `reverse`

- `last`

- ...

Пример использования ленивости списков - найти N-ую ЦИФРУ в списке квадратов натуральных чисел:

```
square x = x * x
allSquares = square <$> [1..]
result n = (concatMap show allSquares) !! n
```

# 36. Ленивое выполнение. Потоки.

Потоки - гарантированно бесконечная структура данных.

Поток - функтор:

```
instance Functor Stream where fmap f (Cons h t) = Cons (f h) (fmap f t)

sreturn x = srepeat x

diag (Cons h t) = Cons (shead h) $ diag (stail <$> t)
sflatten :: Stream (Stream x) -> Stream x
sflatten = diag
```

`return` возвращает первые N элементов, `flatten` берёт диагональ от значений всех "сжимаемых" потоков.
