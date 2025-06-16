SDK (Software Development Kit) – это ==набор инструментов и ресурсов, необходимых для разработки программного обеспечения==. Он содержит библиотеки, компиляторы, отладчики, документацию и другие компоненты, которые облегчают работу разработчиков.

.Net work with Visual basic, F#. C# and C++
.Net Framework only windows
.Net Core 1 - 3.2 (cross platform)
.Net 5 - delete Core name
.Net Standard - limited, work with low level (Alduin)

API (Application Programming Interface) is ==a set of rules and specifications that allows different software systems to communicate and interact with each other==. Like incapsulation

CTS - common type system. Типы доступные в одном язык доступны и в другом.  это ==часть .NET Framework, которая определяет, как типы данных (классы, интерфейсы, структуры и встроенные типы) объявляются, используются и управляются==. Эта система обеспечивает основу для межъязыковой интеграции и безопасности типов, позволяя программам, написанным на разных языках, взаимодействовать между собой. CTS также определяет принципы наследования и структуру типов, обеспечивая объектно-ориентированную модель, поддерживающую реализацию различных языков программирования. Все типы в CTS, включая встроенные числовые типы, в конечном итоге наследуются от одного базового типа – `System.Object`

CLS - common language specification. это ==набор правил, которые должны соблюдать компиляторы языков программирования, работающие с .NET Framework, чтобы их компоненты могли взаимодействовать друг с другом и с компонентами, написанными на других CLS-совместимых языках==. Он определяет минимальный набор возможностей, которые должны быть реализованы во всех языках, чтобы они могли быть успешно использованы в общей среде исполнения (CLR).
BCL - base class library библиотека, которая нас не ограничивает
FCL - Framewok Class library более жесткая библиотека со своим правилами

Middleware (или промежуточное программное обеспечение, программное обеспечение среднего слоя) - это ==тип программного обеспечения, который выступает как связующее звено между различными приложениями, системами или компонентами, облегчая их взаимодействие и обеспечивая обмен данными между ними== 
Middleware позволяет приложениям, которые могут быть написаны на разных языках и работать на разных платформах, "общаться" друг с другом

класс должны писаться в стиле PascalCase
переменные должны писаться в camelCase

___

типы данных: 
bool - 1b
byte (0-255)
sbyte (-128  -127)
char - 2b (нельзя число писать)
short - 2b Int16
ushort (unsigned short)
int | uint - 4b int32
float - 4b 0.1f  Single
long | ulong - 8b 0.2L Int64
double - 8b
decimal - 16b 0.1m без литерала не сработает

Console.Writeline() - cout
Console.Readline() - cin

if(1) - так делать запрещено

____

switch (expression)
{
	case "Alex":
		break
}

принимает стринги, брейк нужно обязательно использовать. 

goto case позволяет переходить к нужному case. В этом случае break не нужно

можно простенькие выражения использовать в switch case > 10 and < 100

___
/// Loops

for (var i = 0; i < 10; i++)
{

}

while(1) нельзя
while(true) можно

do
{

} while (i < 100)

____
Source code ->
Rosyln компилятор ->
MSIL/IL промежуточный язык для операционок | кроссплатформенность ->
CLR (Common Language Runtime):
	JIT (Just in time) ->
ByteCode (процессор)
___

Console.WriteLine(value1 + value2)
int.Parse() - превращает в инт

___

str.ToUpper() - возвращает увеличенный стринг
str.Length - размер строки
str.Insert - подставляет с индекса
str.Contains -  проверяет, есть ли символ внутри строки
str.Remove(6, 5) - удаляет 5 символов с 6 индекса
str.Replace("Nail", "Tural") - заменить одно на другое
str+= ",," - можно сложить строки
str.Format("{a} + {b}", a, b) или $"{a} + {b} = {a+b}"

все типы данных кроме стринга структуры
объекты класса всегда в хипе, а структуры в стеке.

не деструктор, а финализатор

___
///arrays

int[] arr = new int[3]; 
int[] arr = new int[3] {10, 20, 40};
int[] arr = new int[] {10, 20, 40};
int[] arr = {10, 20, 40};

int[,] arr = new int [2,3]
{
	{10, 20, 30},
	{42, 9, 16}
}

arr[0, 1] = 7;
arr.getLength 
arr.getUpperBound

int[][] [] jagged = new int[3][]
{
	new int[3],
	new int[10]
}
or
jagged[0] = new int[3]

jagged[i][j]

Length вернет 3ку

удалять уже не нужно

==Двумерный массив — это массив элементов, организованных в виде таблицы со строками и столбцами.== ==Каждая строка в двумерном массиве имеет одинаковое количество столбцов.== ==Зубчатый массив, или массив массивов, имеет элементы, которые сами являются массивами, и каждый из этих внутренних массивов может иметь разную длину==
___

у структур  и классов по умолчанию в C#  модификатор доступа private . Модификатор доступа нужно применять к каждому полю

создание объекта:
```csharp
var person = new Person();
Person person = new Person();

//or
Person person = new Person
{
	Age = 25;
	Name = "Alex";
}

person.Name = "Alex";

//свойство:
class Person
{
	public Person() //если дефолт конструктор мы определяем сами, то должын проинициализировать свойства
	{
		Name = string.Empty;
	}

//or

	public Person() : this(0, string.Empty){}

	public Person(int age, string name)
	{
		Age = age;
		Name = name;
	}
	
	public string Name {get; set;} //auto property
	private int _age; //backing field
	public int Age //full property
	{
		get
		{
			return _age;
		}
		set
		{
			if (value > 0)
			{
				_age = value;
			}
		}
	}
}
```

если полю написать readonly (динамическое) он не сможет принимать сетер, но это правило не работает для конструкторов

const работает как constexpr в С++ и мы не сможем передавать такой переменной/полю, если он определяется рантайме

static class -  мы не можем создавать динамические поля и инициализировать этот класс, но мы сможем вызывать его методы у других объектов

**В C#, статический класс -** это тип, который не может быть инстанцирован, то есть его нельзя создавать экземпляры с помощью `new`. Он содержит только статические члены (методы, поля, свойства и т.д.), которые доступны и применяются непосредственно к классу, а не к конкретному экземпляру. 

Основные особенности:

- **Нельзя создать экземпляр:**
    
    Статический класс не может быть инстанцирован, как обычный класс. 
    
- **Только статические члены:**
    
    Все члены статического класса должны быть статическими. 
    
- **Нельзя наследовать:**
    
    От статического класса нельзя наследовать, и сам он не может наследоваться от другого класса (кроме `object`). 
    
- **Упрощенный доступ:**
    
    К статическим членам можно обращаться напрямую по имени класса, например `ClassName.StaticMethod()`. 
    
- **Использование:**
    
    Статические классы часто используются для организации служебных методов, функциональности, не связанной с конкретными объектами, или для представления неизменяемых данных.

```csharp
static class PersonHelper
{
	static PersonHelper()
	{
		//вызывает только 1 раз, когда его где-то вызывают. Нужен для инициализации статических полей
	}
	
	public static bool isAgeValid(int age)
	{
		if(age > 0 && age < 200)
		{
			return true;
		}
		return false;
	}
}
```

=>  тоже самое, что return  в классах

public int Size {get; } -  нет сеттера
public int Size {get; private set} - делает сеттер приватным

readonly = const * 
const = constexpr

___
///Исключения

Exception - класс для всех исключений
Directory - класс, который позволяет управлять папками

try catch - C# не требует в catch ловить ошибку, но лучше так не делать

```csharp
try
{
	Directory.Delete(path);
}
catch (DirectoryNotFoundException ex)
{
	Console.WriteLine($"Message {ex}")
}
catch (Exception ex) //всегда писать последним
{

}
```

создаем свои исключения:

```csharp
class Calculator
{
	public double Divide(double num1, double num2)
	{
		if (num1 == 0)
		{
			throw new ZeroDivisionException("Divided by zero!")
		}
	}
}

class ZeroDivisionException : Exception
{
	public ZeroDivisionException(string message) : base(message)
	{
	}
}
```

___
///namespace

только в одном файле может быть top level statement

где-то с 5й версии сделали неймспейс на уровне файла

пишем так namespace TestNamespace;

using TestNamespace; - использовать неймспейс

можно и так:

var user = new TestNamespace.User();

namespace работает только в том файле, где создан. global using позволяет его использовать везде без объявления

///Enum

 у любого enum есть свой переопределенный ToString()
по умолчанию использует :int но мы можем поменять тип например на byte

///struct vs class

ref -  тоже самое, что &  в с++. Не нужно писать, если мы будем обращаться к полю класса, так как будет разминовка

структура будет копироваться, поэтому лучше, чтобы она не весила более 16 байтов

класс не копируется, а передается по поинтеру

DateTime -  для времени

если какой-то объект находится в классе, то тоже попадает в хип. Например, структура в классе

структура не должна быть изменяемой

init можно использовать вместо set, чтобы инициализировать только 1 раз

___
//Nullable type
null - ссылка на ничего
int val = null !так нельзя делать

с 5й версии ввели ?

string? - значит, что мы можем передать туда null.  Это в основном только для нас нужно. Иначе мы получим ворнинг

```csharp
int? a = null тоже самое  Nullable<int> a = null

string str = Console.Readline()! //null forgiving operator
```

____
/// перегрузка операторов

```csharp
class Number
{
	private int _value;

	public Number(int value)
	{
	
	}

	public static Number operator+(Nuber left, Number right)
	{
		var result = new Number();
		result._value = left.value +s right.value
		return result;
	}
}
```

хотя бы один тип в перегрузке должен быть объектом класса

если мы перегружаем одну сторону, обратная тоже перегружается.

В случае со сравнением, если мы перегружаем одно, то должны и другое. То есть \==,  значит и !=

если без перегрузки сравнивать два объекта класса, то мы сравниваем адреса.

чтобы сохранить эту возможность мы перегружаем public override bool Equals(object? obj)

___

params -  позволяет передавать любое количество значений

//StringBuilder

var builder = new StringBuilder()

нельзя модифицировать обычный string. 
StringBuilder - динамичная строка.  

//Polymorphism

```csharp

abstract class Weapon
{
	private string? _name;
	public Weapon(string name)
	{
		_name = name;
	}
	public string GetName()
	
	public int Damage {get; set;}
	public abstract void Fire();
}

class Shotgun : Weapon
{
	public Shotgun() : base("Shotgun")
	{
		Damage = 10;
	}
	public override void Fire() // мы обязательно должны перегружать метод
	{
	
	}
}
```

___
В С# `??` - это оператор объединения с null, а `!?` - оператор null-определения. Оба они используются для работы с переменными, которые могут быть null.

1. Оператор объединения с null (??)

- **Что делает:** Если левый операнд не null, то возвращает его значение. Если левый операнд null, то возвращает значение правого операнда.
- **Пример:**

Код

```
    string str1 = null;    string str2 = "Привет";
    string result = str1 ?? str2; // result будет "Привет"
```


2. Оператор null-определения (?.)

- **Что делает:** Предоставляет безопасный способ доступа к свойствам или методам переменной, которая может быть null, не вызывая исключение `NullReferenceException`. Если переменная null, возвращает null.
- **Пример:**

Код

```csharp
    string str3 = null;    // Без !?:
    // string length = str3.Length;  //  будет исключение NullReferenceException
    // С !?:
    string length = str3?.Length; // length будет null
```

___
///Interface

определяет методы для реализации
имплементировать интерфесы.

Интерфейс работает как контракт.

Класс описывает характеристики, Интерфейс функционал

```csharp
Interface IMoveable
{
	void Move();
	int Type {get; set;}

	object this[int index]{get; set;}

	//поддержка делегатов и статических абстрактных методов
}
```

 MyClass obk = new MyClass();
 obj.Foo() - реализация метода класса

 IA obk = new MyClass();
 obj.Foo() - реализация метода интерфейса IA
 - с var не получится использовать
 
 у интерфейсов по умолчанию public

//type casting & type conversion

casting - полиморфное изменение
conversion - полное изменение

```csharp 
void WhoIsIt(IMoveable moveableObject)
{
	if (moveableObject is Dog)
	{
		//dynamic cast
		Dog dog = (moveableObject as Dog)!;
		//static cast
		Dog dog = (Dog)moveableObject;
		Console.Writeline("This is a dog")
	}
}

try
{
	Cat cat = (Cat)moveableObject;
}
catch (InvalidCastException ex)
{
	Console.Writeline(ex.Message);
}
```

___

`out` - это ==модификатор параметра, который указывает, что переменная, передаваемая в метод, может быть изменена этим методом, и затем ее измененное значение будет доступно в вызывающей части кода==. В отличие от `ref`, где переменная должна быть уже инициализирована, при использовании `out` переменная может быть неинициализированной. Метод, использующий `out`, обязан присвоить значение этой переменной, и это значение будет доступно после завершения работы метода

out var
out
out int

in (const &) - модификатор требует, чтобы заранее была переменная проинициализирована 

___
///Архитектура

Models - классы, которые содержат только поля и свойства. Хранят в отдельной папке.

свойство ссылочного типа по умолчанию хранит null

Services - классы, которые работают с классами моделей
___
///Делегаты - ссылочный тип
анонимный класс == лямбда выражение
```csharp
Operation op = (a, b) => a - b;
Init _init = (value) => {};
Init _init = value => value = 42;
NoParamDelegate del = () => Console.Writeline("User log in");
```

через "=" мы можем привязать объекту делегата ссылку на любой метод, но этот метод должен соответствовать условиям делегатам

```csharp
delegate int Operation(int a, int b)
```

var result = operation?.Invoke(a, b);
это более безопасный вызов

///Multicast delegates
через += можно добавлять несколько методов или лямбд делегатам и при вызову делегата вызовутся все. Но return возвращается только у последнего

//Sealed class
Изолированные классы **используются для ограничения пользователей от наследования класса**. Класс можно изолировать с помощью ключевого слова sealed . Ключевое слово сообщает компилятору, что класс изолирован и, следовательно, не может быть расширен.

если суммировать делегаты, то их методы приплюснутся

___
//встроенные делегаты

- `Action` — представляет метод, который не возвращает значение и может принимать параметры. - или можно var del 
- `Func` — представляет метод, который возвращает значение и может принимать параметры.
- `Predicate` — представляет метод, который возвращает логическое значение и принимает один параметр.

Делегаты позволяют передавать методы другим методам, как обычные данные. Это полезно, когда нужно сделать код более гибким и универсальным, например, при реализации алгоритмов, которые могут использовать разные методы для сравнения или обработки данных

___
///Event

```csharp

class Chat
{
	private readonly List<string> _message;
	
	public Chat()
	{
		_message = [];
	}
	
	public void SendMessage(string message)
	{
		if(string.IsNullOrWhiteSpace(message))
		{
			return;
		}
	}
	
	message = message.Trim();
	
	_messages.Add(message);
}
```

public event Action/<int/> - отличается от делегата только тем, что его невозможны вызвать за пределом класса.

Также  можно управлять add и remove event

___

//встроенные интерфейсы

 🔹 `IEnumerable<T>` — только перебор (чтение)

`IEnumerable<T>` — это базовый интерфейс, который позволяет **перебирать** (итерировать) элементы коллекции.

- Позволяет использовать `foreach`.
- Только чтение (нет методов добавления, удаления и т.д.).
- Определяет метод `GetEnumerator()`.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

public class MyEnumerable<T> : IEnumerable<T>
{
    private T[] _items;

    public MyEnumerable(T[] items)
    {
        _items = items;
    }

    public IEnumerator<T> GetEnumerator()
    {
        foreach (T item in _items)
        {
            yield return item;
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
}

// Пример использования
class Program
{
    static void Main()
    {
        var myData = new MyEnumerable<int>(new int[] { 1, 2, 3, 4 });

        foreach (var item in myData)
        {
            Console.WriteLine(item);
        }
    }
}

```

🔹 `ICollection<T>` — управление коллекцией

`ICollection<T>` расширяет `IEnumerable<T>` и добавляет **методы управления коллекцией**:

- `Add`, `Remove`, `Clear` — можно изменять коллекцию.
- `Count` — количество элементов.
- Реализуется многими коллекциями: `List<T>`, `HashSet<T>`, `Dictionary<TKey, TValue>.Values` и т.д.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

public class MyCollection<T> : ICollection<T>
{
    private List<T> _items = new List<T>();

    public int Count => _items.Count;

    public bool IsReadOnly => false;

    public void Add(T item)
    {
        _items.Add(item);
    }

    public void Clear()
    {
        _items.Clear();
    }

    public bool Contains(T item)
    {
        return _items.Contains(item);
    }

    public void CopyTo(T[] array, int arrayIndex)
    {
        _items.CopyTo(array, arrayIndex);
    }

    public IEnumerator<T> GetEnumerator()
    {
        return _items.GetEnumerator();
    }

    public bool Remove(T item)
    {
        return _items.Remove(item);
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
}

// Пример использования
class Program
{
    static void Main()
    {
        var collection = new MyCollection<string>();
        collection.Add("Apple");
        collection.Add("Banana");
        collection.Add("Cherry");

        Console.WriteLine($"Count: {collection.Count}");

        foreach (var fruit in collection)
        {
            Console.WriteLine(fruit);
        }

        collection.Remove("Banana");

        Console.WriteLine("After removing 'Banana':");
        foreach (var fruit in collection)
        {
            Console.WriteLine(fruit);
        }
    }
}

```

🔹 `IComparable<T>` — сравнение объектов для сортировки

**Цель:** позволяет объектам **сравнивать себя с другими объектами** того же типа.

Сигнатура: `int CompareTo(T other);`

```csharp
using System;
using System.Collections.Generic;

public class Person : IComparable<Person>
{
    public string Name { get; set; }
    public int Age { get; set; }

    public int CompareTo(Person other)
    {
        if (other == null) return 1;

        // Сортировка по возрасту (от младшего к старшему)
        return this.Age.CompareTo(other.Age);
    }

    public override string ToString() => $"{Name}, {Age} лет";
}

class Program
{
    static void Main()
    {
        List<Person> people = new List<Person>
        {
            new Person { Name = "Alice", Age = 30 },
            new Person { Name = "Bob", Age = 20 },
            new Person { Name = "Charlie", Age = 25 }
        };

        people.Sort(); // Использует CompareTo

        foreach (var person in people)
        {
            Console.WriteLine(person);
        }
    }
}

```

🔹 `IEqualityComparer<T>` — сравнение на **равенство** + **хэш**

**Цель:** позволяет создавать **настраиваемое сравнение** объектов — особенно важно в коллекциях вроде `Dictionary`, `HashSet`.

🔸 Сигнатура:

`bool Equals(T x, T y); int GetHashCode(T obj);`

```csharp
using System;
using System.Collections.Generic;

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

// Кастомный компаратор по имени
public class PersonNameComparer : IEqualityComparer<Person>
{
    public bool Equals(Person x, Person y)
    {
        if (ReferenceEquals(x, y)) return true;
        if (x is null || y is null) return false;

        return x.Name == y.Name;
    }

    public int GetHashCode(Person obj)
    {
        return obj.Name?.GetHashCode() ?? 0;
    }
}

class Program
{
    static void Main()
    {
        var people = new HashSet<Person>(new PersonNameComparer())
        {
            new Person { Name = "Alice", Age = 30 },
            new Person { Name = "Alice", Age = 40 }, // не добавится, т.к. имя совпадает
            new Person { Name = "Bob", Age = 20 }
        };

        foreach (var p in people)
        {
            Console.WriteLine($"{p.Name} ({p.Age})");
        }
    }
}

```

____
///Generics

ключевое слово required требует проинициализировать

класс Path для путей экстеншенов

where T : class - ключевое слово where  ограничивает тип

where T : class, new() - разрешает дефолтный конструктор, т.е. создавать объекты типа T

если where T : NameOfClass -  можно передавать класс и его наследников

//boxin => stack -> heap

void BoxMe(object value) {}

(int)list\[i] - unboxing
___

//File

```csharp
var stream = File.Create("file.cs")

Encoding. - шифрование

var text = "Hello"

var bytes = Encodind.UTF8.GetBytes(text);

stream.Write(bytes); - записывает в буфер
stream.Flush(); - записывает на диск

strean.Close() или using FileStream stream = File.Create("file.cs"); // автоматически дает Dispose(), который освобождает память
```

IDisposable - позволяет использовать using, чтобы вызвать Dispose() для очистки памяти

Flush()  нам тоже при using FileStream stream писать не нужно

Path.Combine("User", "Alex") - сам добавляет слэш

@ - verbatim - строка читается также как пишется

___
/// Streams

var fileStream = new FileStream("file.txt", FileMode.Create, FilleAcess.)

FileMode - Enum, определяющий режим открытия
FilleAcess - Enum, определяющий режим работы с файлом

var streamWrite = new StreamWriter(fileStream) - позволяет записать всё в поток. Но обязательно нужно вызывать Flush()

можно также без FileStream:

new StreamWriter("file.txt", append: true)

StreamReader - для чтения. У него есть разные методы. Каждый раз при вызове читает дальше

StringBuilder вместо string  для нормального чтения

///Serialize and Deserialize JSON

var json = JsonSerializer.Serialize(books, new JsonSerializerOption)
{
	WriteIndented = true; //нормальное отображение
});

File.WriteAllText("books.json", json)

///Read JSON

File.ReadAllText("books.json")

JsonSerializer.Deserialize\<List\<Book>>(text);

можно передавать сырую строку

___

//Binary

BinaryWriter and BinaryReader

\[JsonIgnore] - для запрета сериализации
\[JsonNameProperty] - для переименования параметров

MemoryStream() - для временной записи в буфер. Создает поток, резервный хранилище которого является памятью.

MemoryStream.WriteTo() - запись из мемори в стрим

//record

для сравнения по значениям, можно записывать в одну строчку, можно наследовать только от рекордов, через with можно создать рекорд с измененным параметром

___
//LINQ - lanquage integrated queries

использует extension methods

```csharp

static class Test
{
	public static string Capitalize(this string source)
}
```

ключевое слово для создания экстеншена, дальше можно передавать обычные параметры

в классе может быть много методов, но они должны быть статичными

 на самом деле выглядит как
 var cap = Test.Capitalize(cap);

Select
Where -  пробегается по всем элементам коллекции, отсеивает тех, кто не соответствует условию. Первый раз ничего не даст, потому что ждет второго вызова через фор ич
Min
Max
First - IEnumerable, возвращает первое совпадение
FirstOrDefault - если не нашел, то  вернет значение по умолчанию
Lart - IEnumerable, возвращает последнее совпадение
Skip - пропустить сколько-то
Take - взять сколько-то
SkipWhile - пока соответствует условиям или через

yield - позволяет сохранять состояние и вызывать разный return. А yield break обрывает вызовы этапов yield. Под капотом private bool MoveNext(). 

 