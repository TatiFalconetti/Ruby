### Задания к занятию 2

* Типы данных Ruby
* Управляющие конструкции
* Циклы и итераторы



#### 1. Методы Ruby Core API

Найдите в документации Ruby по адресу http://ruby-doc.org/core/ методы для объектов разных классов. Поэкспериментируйте с ними в интерактивной оболочке `irb`

Для класса `Fixnum`:

* Метод, возвращающий вещественный результат от деления     `fdiv(numeric)`
* Метод проверяющий, является ли число нечётным             `odd?`
 
Для класса `Integer`:

* Метод, возвращающий Наибольший Общий Делитель 2-х чисел       `gcd(int2)`
* Метод, позволяющий итерировать от одного числа до другого     `downto(limit)`  `upto(limit)`
* Метод приведения целого числа к рациональному                 `rationalize([eps])`

Для класса `Numeric`:

* Метод, позволяющий итерировать от данного целого числа с указанием шага итерации и числа верхнего предела итерации `step(by: step, to: limit)`
* Метод, приводящий данное число к комплексному (мнимому)  `i`

Для класса `Float`:

* Метод, приводящий вещественное число к строке  `to_s`

Для класса `Array`:

* Метод, возвращающий последний элемент из массива (с его извлечением из массива)  `pop`
* Метод, добавляющий элемент в конец массива `push(obj, ... )`

Для класса `Hash`:

* Метод, возвращающий массив ключей хэша        `keys`
* Метод, возвращающий массив значений хэша      `values`

Для класса `Range`:

* Метод, проверяющий, включено ли последнее значение в диапазон `exclude_end?`



#### 2. Условное выражение `if-else-end`

Представьте, что у вас есть объект класса `Hash`:

```ruby
player = { name: 'johnny', color: :red }
```

и переменная `colors`:

```ruby
colors = [:blue, :white, :green, :red, :orange]
```

Напишите код, который будет выбирать случайный цвет из массива `colors` и сравнивать его с цветом в хэше `player`.

**Если цвета совпадают** — выводите сообщение «Джонни, ты прав!». **Если цвета не совпадают, но количество символов из которых они состоят одинаково** — выводите: «Джонни, букв столько же, но значение иное!». **В остальных случаях** — выводите любое другое сообщение.

Постарайтесь сделать так, чтобы сообщения в выводе не включали явно заданное имя, а брали его из хэша с помощью интерполяции.

Оберните код в метод, можно в несколько.



```ruby
def check_color randColor
	player = { name: 'johnny', color: :green }
    if randColor == player[:color]
        puts "#{player[:name]}, ты прав!"
    elsif  randColor.length == player[:color].length
        puts "#{player[:name]}, букв столько же, но значение иное!"
    else
        puts "Любое другое сообщение!"
    end
end

colors = [:blue, :white, :green, :red, :orange]
randColor = colors[rand(5)]
puts "#{randColor}"
check_color randColor
```


#### 3. Итерация с условиями

У вас есть массив имён, например:

```ruby
names = %w[ambientsketchbook Erik\ Wollo Brian\ Eno Evangelos\ Papathanassiou Shulman]
```

Пробегитесь по ним и выведите только те, **длина которых меньше 10 символов** и **первая буква заглавная**. При реализации условий постарайтесь каждое из них обернуть в отдельный метод.


```ruby
 def checkLength name
 	name.length < 10
 end
 
 def checkCaps name
 	name.chr == name.chr.capitalize
 end
 
names = %w[ambientsketchbook Erik\ Wollo Brian\ Eno Evangelos\ Papathanassiou Shulman]

names.each do |name|
   puts "#{name}" if checkLength(name) && checkCaps(name)
 end
```

#### 4. Количество символов в элементе массива

Посчитайте количество символов в каждом элементе массива:

```ruby
[“Ruby”, “Python”, “JavaScript”, “Java”, “.NET”, “HTML”, “Clojure”]
```

Подсказка:

Используйте метод `inject`

Результат выведите на экран в виде хэша:

```ruby
{"Ruby"=>4, "Python"=>6, "JavaScript"=>10, "Java"=>4, ".NET"=>4, "HTML"=>4, "Clojure"=>7, "Go"=>2}
```



```ruby
hashLang = {}
result = langs.inject(0) do |sum, lang|
   hashLang.store(lang, lang.length)
end
```


#### 5. Самая удивительная последовательность

Напишите метод вычисления [последовательности Фибоначчи](https://ru.wikipedia.org/wiki/Числа_Фибоначчи). Попробуйте реализовать алгоритм с помощью цикла и с помощью рекурсии. На следующем занятии мы сравним что работает быстрее.

```ruby
def Fib n
	f1 = 0
	f2 = 1
	i = 0
for i in (i..n)
		print " #{f1}"
		fib = f1 + f2
		f1 = f2
		f2 = fib
	end
end

Fib 20
```


```ruby
def Fib n
	if n == 0 
       0
    elsif n == 1
    	1
    else 
       Fib(n-1) + Fib(n-2)
      end
end

(0..10).each {|n| print "#{Fib(n)} "}
```

#### 6. Продвинутый шифр Цезаря

Напишите алгоритм [rot13](), позволяющий кодировать и декодировать текст на английском языке. Например:

```ruby
cypher = 'Lbh unpxrq n irel frperg zrffntr!'
rot13(cypher) # => ?
```


```ruby    
def rot13 cypher
	cypher.each_codepoint do |c|
		if ("a".."z").include?(c.chr) 
			c += c < "a".ord+13 ? 13 : -13
		elsif ("A".."Z").include?(c.chr) 
			c += c < "A".ord+13 ? 13 : -13
		end
		print c.chr
	end
end

cypher = 'Lbh unpxrq n irel frperg zrffntr!'
rot13(cypher)  # You hacked a very secret message!
```