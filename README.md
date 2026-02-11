# C# Cheatsheet

**Copy paste reference. TAFE NSW Cert IV Programming.**

---

## Program Skeleton

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        // all code goes here
    }
}
```

---

## Variables

```csharp
string name = "George";
int age = 29;
double price = 49.99;
bool isActive = true;
char grade = 'A';
```

---

## Constants

```csharp
const int MAX_SIZE = 100;
const double TAX_RATE = 0.10;
const string ADMIN = "root";
```

---

## Output

```csharp
Console.WriteLine("Hello World");                    // prints + newline
Console.Write("Enter name: ");                       // prints, no newline (cursor stays)
Console.WriteLine($"Hello {name}, age {age}");       // string interpolation
Console.WriteLine($"Price: {price:F2}");             // 2 decimal places: 49.99
Console.WriteLine($"{"Port",-10} {"State",-8}");     // left-align columns
Console.WriteLine($"{"Port",10} {"State",8}");       // right-align columns
```

---

## Input

```csharp
string input = Console.ReadLine();                   // always returns a string
int number = Convert.ToInt32(Console.ReadLine());     // convert to int (crashes on bad input)
double dec = Convert.ToDouble(Console.ReadLine());    // convert to double

// Safe conversion — won't crash
int port;
if (int.TryParse(Console.ReadLine(), out port))
    Console.WriteLine($"Port: {port}");
else
    Console.WriteLine("Invalid number.");
```

---

## Operators

```csharp
// Arithmetic
int sum = 5 + 3;          // 8
int diff = 10 - 4;        // 6
int product = 3 * 7;      // 21
int quotient = 10 / 3;    // 3 (integer division, no decimals)
double exact = 10.0 / 3;  // 3.333...
int remainder = 10 % 3;   // 1 (modulo — remainder after division)

// Shorthand
count++;                   // count = count + 1
count--;                   // count = count - 1
total += 5;                // total = total + 5
total -= 3;                // total = total - 3
total *= 2;                // total = total * 2

// Comparison (returns bool)
x == y                     // equals
x != y                     // not equals
x > y                      // greater than
x < y                      // less than
x >= y                     // greater or equal
x <= y                     // less or equal

// Logical
true && true               // AND — both must be true
true || false              // OR — at least one true
!true                      // NOT — flips the value
```

---

## Strings

```csharp
string name = "George Wu";

name.Length                       // 9
name.ToUpper()                   // "GEORGE WU"
name.ToLower()                   // "george wu"
name.Trim()                      // removes leading/trailing whitespace
name.Contains("Wu")              // true
name.StartsWith("George")        // true
name.EndsWith("Wu")              // true
name.IndexOf("Wu")               // 7 (position), -1 if not found
name.Substring(0, 6)             // "George" (start, length)
name.Replace("Wu", "Smith")      // "George Smith"
name.Split(' ')                  // string[] { "George", "Wu" }

// String interpolation
string msg = $"Name: {name}, Length: {name.Length}";

// Concatenation
string full = "Hello " + name;

// Escape characters
"\n"                              // newline
"\t"                              // tab
"\\"                              // backslash
"\""                              // double quote
```

---

## Arrays

```csharp
// Declare + initialize
string[] names = { "Alice", "Bob", "Charlie" };
int[] scores = { 85, 92, 78 };
int[] empty = new int[5];               // 5 elements, all 0

// Access
string first = names[0];                // "Alice"
int last = scores[scores.Length - 1];   // 78

// Modify
names[1] = "Bobby";

// Properties
int size = names.Length;                 // 3

// Parallel arrays — same index = same item
string[] rations = { "Biscuit", "Jerky", "MRE" };
int[] calories =   { 250, 180, 620 };
// rations[0] → calories[0] → Biscuit has 250 cal
```

---

## If / Else

```csharp
if (age >= 18)
{
    Console.WriteLine("Adult");
}
else if (age >= 13)
{
    Console.WriteLine("Teen");
}
else
{
    Console.WriteLine("Child");
}

// One-liner (single statement, no braces needed)
if (isOpen)
    Console.WriteLine("Port is open.");
else
    Console.WriteLine("Port is closed.");
```

---

## Switch

```csharp
// String cases (from Console.ReadLine)
switch (choice)
{
    case "1":
        Console.WriteLine("Option 1");
        break;
    case "2":
        Console.WriteLine("Option 2");
        break;
    case "0":
        Console.WriteLine("Exit");
        break;
    default:
        Console.WriteLine("Invalid");
        break;
}

// Int cases (from int variable)
switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;
    case 7:
        Console.WriteLine("Sunday");
        break;
    default:
        Console.WriteLine("Invalid day");
        break;
}
```

---

## For Loop

```csharp
// Basic — runs 5 times (i = 0,1,2,3,4)
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}

// Loop through array
for (int i = 0; i < names.Length; i++)
{
    Console.WriteLine($"[{i}] {names[i]}");
}

// Loop through parallel arrays
for (int i = 0; i < rations.Length; i++)
{
    Console.WriteLine($"{rations[i]} - {calories[i]} cal");
}
```

---

## Foreach Loop

```csharp
// When you don't need the index
foreach (string name in names)
{
    Console.WriteLine(name);
}

// Accumulator pattern
int total = 0;
foreach (int score in scores)
{
    total += score;
}
```

---

## While Loop

```csharp
// Basic
int count = 0;
while (count < 10)
{
    Console.WriteLine(count);
    count++;
}

// Menu loop pattern
bool running = true;
while (running)
{
    ShowMenu();
    string choice = Console.ReadLine();
    switch (choice)
    {
        case "0":
            running = false;
            break;
    }
}
```

---

## Methods

```csharp
// void — does a job, returns nothing
static void Greet(string name)
{
    Console.WriteLine($"Hello {name}");
}
// Call: Greet("George");

// returns int
static int Add(int a, int b)
{
    return a + b;
}
// Call: int sum = Add(5, 3);

// returns bool
static bool IsEven(int number)
{
    return number % 2 == 0;
}
// Call: if (IsEven(42)) ...

// returns int — search pattern
static int Find(string[] items, string search)
{
    for (int i = 0; i < items.Length; i++)
    {
        if (items[i].ToLower() == search.ToLower())
            return i;
    }
    return -1;    // not found
}
// Call: int idx = Find(names, "alice");

// returns int — accumulator pattern
static int Sum(int[] values)
{
    int total = 0;
    foreach (int v in values)
        total += v;
    return total;
}
// Call: int total = Sum(scores);

// void — display with parallel arrays
static void DisplayAll(string[] names, int[] values)
{
    for (int i = 0; i < names.Length; i++)
        Console.WriteLine($"  [{i}] {names[i]} - {values[i]}");
}
// Call: DisplayAll(rations, calories);
```

---

## Method Structure Rule

```csharp
class Program
{
    static void MethodA() { }     // sibling — same level
    static int MethodB() { }      // sibling — same level
    static void Main() { }        // sibling — calls the others
}

// WRONG — method inside method
static void Main()
{
    static void Nested() { }      // ERROR
}
```

---

## Try / Catch

```csharp
try
{
    // risky code
    int result = Convert.ToInt32(input);
}
catch
{
    // runs if the try block fails
    Console.WriteLine("Error occurred.");
}

// With specific exception
try
{
    client.Connect(target, port);
}
catch (Exception ex)
{
    Console.WriteLine($"Error: {ex.Message}");
}
```

---

## Type Conversion

```csharp
// String to number
int n = Convert.ToInt32("42");
double d = Convert.ToDouble("3.14");
int n2 = int.Parse("42");                // same as Convert, throws on bad input

// Safe conversion
int result;
bool ok = int.TryParse("42", out result);  // ok = true, result = 42
bool bad = int.TryParse("abc", out result); // bad = false, result = 0

// Number to string
string s = 42.ToString();
string s2 = $"{42}";                       // interpolation does it automatically

// Casting
double big = 9.7;
int small = (int)big;                      // 9 (truncates, doesn't round)
```

---

## DateTime

```csharp
DateTime now = DateTime.Now;
int year = DateTime.Now.Year;              // 2026
int month = DateTime.Now.Month;            // 1-12
int day = DateTime.Now.Day;               // 1-31
string formatted = now.ToString("yyyy-MM-dd");   // "2026-02-11"
string time = now.ToString("HH:mm:ss");         // "14:30:00"
```

---

## Math

```csharp
Math.Abs(-5)             // 5
Math.Max(10, 20)         // 20
Math.Min(10, 20)         // 10
Math.Round(3.7)          // 4
Math.Floor(3.9)          // 3
Math.Ceiling(3.1)        // 4
Math.Pow(2, 8)           // 256
Math.Sqrt(144)           // 12
```

---

## Random

```csharp
Random rng = new Random();
int roll = rng.Next(1, 7);         // 1-6 (max is exclusive)
int big = rng.Next(100);           // 0-99
double frac = rng.NextDouble();    // 0.0 to 1.0
```

---

## Networking (System.Net.Sockets)

```csharp
using System.Net.Sockets;

// TCP connect scan — check if port is open
static bool ScanPort(string target, int port)
{
    try
    {
        TcpClient client = new TcpClient();
        client.Connect(target, port);
        client.Close();
        return true;     // port open
    }
    catch
    {
        return false;    // port closed/filtered
    }
}
```

---

## StringBuilder (System.Text)

```csharp
using System.Text;

StringBuilder sb = new StringBuilder();
sb.Append("Hello");                // add text
sb.AppendLine(" World");           // add text + newline
sb.Insert(0, "START: ");           // insert at position
sb.Replace("Hello", "Hi");        // replace text
sb.Remove(0, 7);                   // remove 7 chars from position 0
sb.Clear();                        // empty the buffer
string result = sb.ToString();     // convert to final string
```

---

## Common Patterns

```csharp
// Menu-driven app (all 5 patterns)
bool running = true;
while (running)
{
    ShowMenu();
    string choice = Console.ReadLine();
    switch (choice)
    {
        case "1": DoSomething(); break;
        case "0": running = false; break;
        default: Console.WriteLine("Invalid"); break;
    }
}

// Search + handle not found
int idx = Find(items, search);
if (idx != -1)
    Console.WriteLine($"Found: {items[idx]}");
else
    Console.WriteLine("Not found.");

// Accumulator with condition
int count = 0;
foreach (string s in states)
{
    if (s == "open")
        count++;
}

// Bool with OR
static bool IsRisky(string svc)
{
    return svc == "telnet" || svc == "ftp" || svc == "smb";
}

// Output conventions (pentest tools)
// [*] Info    [+] Success    [-] Failure    [!] Warning
Console.WriteLine("[*] Scanning target...");
Console.WriteLine("[+] Port 22 is open.");
Console.WriteLine("[-] Port 80 is closed.");
Console.WriteLine("[!] Telnet detected — high risk.");
```

---

## The 5 Patterns

| # | Pattern | Code | When |
|---|---------|------|------|
| 1 | Store stuff | `string[] x = { };` | Data exists |
| 2 | Loop through | `for (int i = 0; ...)` | Process each item |
| 3 | Decide | `if / switch` | Choose what to do |
| 4 | Wrap in methods | `static int Find(...)` | Reuse code |
| 5 | Keep running | `while (running)` | Interactive app |

---

Vidimus Omnia.
