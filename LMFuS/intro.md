# Language Models Follow-up Script
## In this introduction we will look at LMFuS syntax, capabilities and built-ins

###  Table of contents:
- What is LMFuS? What is it for and who is it for?
- Syntax & Capabilities
- Built-in functions
- Extending from base files
- Writing libraries

## What is LMFuS? Who and what is it for?
Language Models Follow-up Script(LMFuS for short) is a scripting language that is fully compiled and executed by LMs(Language Models) and LLMs(Large Language Models). It is designed to be simple enough for them to understand while being same of understanding to us humans.

# Syntax & Capabilities
Let's start by looking at this helloworld.fus code:
```cs
$$start
# This is a comment
# There can be comments before/after the start-end scope as well
!# This is a multiline comment
    Tabulations are not required, but nice to include.
!#

out: "Hello, World!" # Do some output

$$end
```
Let's start from the beginning, we see ``` $$start ```, this is a TOKEN (special kind of object in LMFuS that indicates or links to some kind of internal or built-in function) it indicates that the script start at this point, it is of course paired with the ``` $$end ``` token that is same as ``` $$start ``` should ALWAYS be included in script to indicate start and end execution points.

After the token we see the ``` out ``` function. The ```out``` function is, as you can already guess, a function to output some message(text, integers, float, and dtype). We can also configure its datatype output to convert to by defining the default positional argument, like this ```out<dtype: dType>: outputObject```(example: ```out<int>: "The answer is 42. All text will be omitted!"```, output: ```>> 42```), but be aware that the datatype that we define and the one tha we ask the function to output should be convertible(int to float, float to int, int to string, string to ing(ONLY IF STRING HAS ANY int IN IT. If string has int AND string dtypes, string dtype objects will be omitted and only converted int's will remain)).

We think that readability is the most important thing in a programming language, so we made sure that LMFuS is as readable as possible. And as understandable as possible. That's why we made sure that the syntax is as simple to understand as it could be, while being understood the same way by the LMs and LLMs.

# Tokens
## Tokens are special kind of objects in LMFuS that indicates or links to some kind of internal or built-in function.
## There's 6 types of tokens:
- Start token ```$$start```
- End token ```$$end```
- Import token ```$$import``` *
- Debug info. token ```$$debug``` *
- Global variable assignment token ```$$global``` *
- Environmental-global variable assignment token ```$$envglobal``` *
- Code-ignore token ```$$ignore``` *

__More on tokens marked with asterisk in the end of the intro.__

# Comments
## Single line comment
```LMFuS
# This is a single line comment
```
## Multi line comment
```LMFuS
!# This is a multiline comment
    Tabulations are not required, but nice to include.
    Multiline comments can be used to comment out large blocks of code, but it's not recommended to use them for that purpose. Better use ignore token for these kind of purposes.
!#
```
We ALWAYS recommend to include a space after the comment(both single and multiline) character, because it makes the comments more readable. And it's just a good practice.


# Variables
## There are 6 types of variables in LMFuS:
- Integers. DType name: int
- Float. DType name: float
- String. DType name: string
- Boolean. DType name: bool
- List(array). DType name: list
- Dictionary. DType name: dict
- Set. DType name: set
- Tuple. DType name: tuple
- Bytes. DType name: bytes
- Bytearray. DType name: bytearr

LMFuS supports dynamic variable declaration, but you can explicitly define them just like in C-languages.

## Defining variables

You can do it like this(dynamic):
```python
a = 42
b = 42.0
c = "Hello, World!"
d = True
e[5] = {1, 2, 3, 4, 5}
f = {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}
g = (1, 2, 3, 4, 5)
h = toBytes: "Hello, World!"
i = toBytes: "Hello, World!"

sum = a + b
```
Or explicitly:
```python
int a = 42
float b = 42.0
string c = "Hello, World!"
bool d = True
list e[5] = {1, 2, 3, 4, 5}
dict f = {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}
set g = (1, 2, 3, 4, 5)
bytes h = b"Hello, World!"
bytearr i = bytearray(b"Hello, World!")
int sum = a + b
```
If you are defining them explicitly, you can do it in scopes as well:
```cs
int
    a = 42
    b = 42
    sum = a + b

float
    fa = 42.0
    fb = 42.0
    fsum = fa + fb

string
    sa = "Hello, "
    sb = "World!"
    sc = sa + sb

bool
    ba = True
    bb = False
    bsum = ba + bb
 
# And so on...
```

# Built-in functions
## There are ... built-in functions in LMFuS:
- ```out```
- ```in```
- ```return```
- ```break```
- ```continue```
- ```pass```
- ```export```
- ```len```
- ```type```
- ```assert```
- ```exec```
- ```eval```
- ```toString```
- ```toInt```
- ```toFloat```
- ```toBool```
- ```toList```
- ```toDict```
- ```toSet```
- ```toTuple```
- ```toBytes```
- ```append```
- ```extend```
- ```insert```
- ```remove```
- ```pop```
- ```clear```
- ```index```
- ```count```
- ```sort```
- ```reverse```
- ```copy```
- ```deepcopy```
- ```join```
- ```split```
- ```replace```
- ```find```
- ```sum```
- ```max```
- ```min```
- ```rand```
- ```sleep```

# Control structures
## Conditional statements
- If statement
```cpp
if(statement){
    # Do something
}
```
- Elseif statement
```cpp
elseif(statement){
    # Do something
}
```
- Else statement
```cpp
else{
    # Do something
}
```
- Case statement
```cs
case(variable, casesAmount){

    case 1{
        # Do something
    }

    case 2{
        # Do something
    }

    case 3{
        # Do something
    }
}
```

# Loops
## There are 3 types of loops in LMFuS:
- For loop
```cs
for(i = 0; i < 10; i++){
    # Do something
}
```

- While loop
```cs
while(statement){
    # Do something
}
```

- Foreach loop
```cs
foreach(variable, list){
    # Do something
}
```

# Error handling
## There are 2 types of error handling in LMFuS:
- Try-catch-finally
```python
try{
    # Do something
}

catch{
    # Do something
}

finally{
    # Do something
}
```

- Assert
```python
assert(statement){
    # Do something
}
```

# Input and output
### You can do input and output in LMFuS with the ```in``` and ```out``` functions.

- Input
```cs
in: "What's your name?"
```
- Output
```cs
out: "Hello, World!"
```
- Converting to dtypes in ```in``` and ```out``` functions
### You can convert from-to:
- int to float
- float to int
- int to string
- float to string
- string to int
- string to float

# Working with lists and dictionaries
## You can work with lists and dictionaries in LMFuS with the built-in functions.
 
### List functions
- ```append```
- ```extend```
- ```insert```
- ```remove```
- ```pop```
- ```clear```
- ```index```
- ```count```
- ```sort```
- ```reverse```
- ```copy```
- ```deepcopy```
- ```pushback```

Examples of using list functions:
```python
list a<any> = {1, 2, 3, 4, 5}

a.append(6) # Output: {1, 2, 3, 4, 5, 6}

a.extend({7, 8, 9, 10}) # Output: {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

a.insert(0, 0) # Output: {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

a.remove(0) # Output: {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

a.pop(0) # Output: {2, 3, 4, 5, 6, 7, 8, 9, 10}

a.clear() # Output: {}

a.index(1) # Output: 0

a.count(1) # Output: 1

a.sort() # Output: {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

a.reverse() # Output: {10, 9, 8, 7, 6, 5, 4, 3, 2, 1}

a.copy() # Output: {10, 9, 8, 7, 6, 5, 4, 3, 2, 1}

a.deepcopy() # Output: {10, 9, 8, 7, 6, 5, 4, 3, 2, 1}

a.pushback(110010120) # Output: {1, 2, 3, 4, 5, 6, 110010120}
```
## Dictionary functions
### There are 11 built-in functions for dictionaries in LMFuS:
- ```update```
- ```pop```
- ```popitem```
- ```clear```
- ```copy```
- ```deepcopy```
- ```fromkeys```
- ```get```
- ```items```
- ```keys```
- ```values```

### Examples of using dictionary functions:
```python
dict a = {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}

a.update({"f": 6}) # Output: {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5, "f": 6}

a.pop("f") # Output: {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}

a.popitem() # Output: {"a": 1, "b": 2, "c": 3, "d": 4}; Takes last element by default

a.clear() # Output: {}

a.copy() # Output: {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}

a.fromkeys() # Output: {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}

a.get("a") # Output: 1

a.items() # Output: {"a": 1, "b": 2, "c": 3, "d": 4, "e": 5}

a.keys() # Output: {"a", "b", "c", "d", "e"}

a.values() # Output: {1, 2, 3, 4, 5}
```

# File operations
## There are 3 types of file operations in LMFuS:
- Read
- Write
- Append

```python
file = open<"r"> "file.txt"
file = open<"w"> "file.txt"
file = open<"a"> "file.txt"
```

# Classes
## There are 2 types of classes in LMFuS:
- Normal class
- Abstract class

## Normal class
```cs
class className(#optional-parent){
    # Do something
}
```

## Abstract class
```cs
abstract class className(#optional-parent){
    # Do something
}
```
```

# Functions
## There are 2 types of functions in LMFuS:
- Normal function
- Abstract function

## Normal function
```cs
func functionName(#args){
    # Do something
}
```

## Abstract function
```cs
abstract func functionName(#args){
    # Do something
}
```

# Working with text prompts & LLMs memory
## You can work with text prompts and LLMs memory in LMFuS with these built-in functions from the LMTools:
- ```memory(messageIndex<int>)```. messageIndex is a parameter that takes a int. value and returns the message at this index from the LLMs memory

- ```prompt(message<string>)```. This function takes a string value and returns the response from the LLM.

- ```clearMemory()```. This function clears the LLMs memory

- ```clearMemoryAtIndex(index<int>)```. This function clears the LLMs memory at the specified index

- ```configure(role<string> = None; maxTokens<int> = 10**5; temperature<float> = 0.5; topP<float> = 0.5; topK<int> = 0; presencePenalty<float> = 0.5; frequencyPenalty<float> = 0.5; bestOf<int> = 1; logProbs<bool> = False; stop<string> = None; )```. This function takes a string value and returns the response from the LLM.

- ```clearConfig()```. This function clears the LLMs configuration

- ```find(startMessageIndex<int>=-1; seachContent<string>; stopAtFirstFound<bool> = False; returnsInDType<string> = "string")```. This function finds the prompted content starting from the indexed message and returns the message index and the content found

- ```displayConfig(humanFormat<bool> = True; displayHidden<bool> = False; displayDeveloper<bool> = False;)```. This function displays the LLMs configuration

- ```findInMessage(messageIndex<int>; searchContent<string>; stopAtFirstFound<bool> = False; returnsInDType<string> = "string")```. This function finds the prompted content at the indexed message

- ```editMessage(messageIndex<int> = -1; newMessage<string>)```. This function edits the message at the specified index. -1 is the latest message(by default)

- ```displayCached(displayMessages<bool> = True; displaySpecialVariables<bool> = False; displayPointers<bool> = False;)```. This function displays the cached content

- ```clearCached()```. This function clears the cached content

- ```setRules(rules<set>)```. This function sets the rules for the LLM.

- ```displayRules()``` This function displays the rules for the LLM.

- ```setCompilerRules(rules<set>; priorityRules<set>; applyTo<string> = "all")```. This function sets the compiler rules for the LLM.


# Advanced topics(*-marked)
## Tokens marked with asterisk
### Examples
```python
$$import packageName as alias # alias optional
$$import @localPackageName as alias
$$debug # will the tell the LLM(compiler) to print the debug info(variables, hidden and special variables, etc.)
$$global varName# will tell the LLM(compiler) to assign the variable to the global scope
$$envglobal varName # will tell the LLM(compiler) to assign the variable to the environmental-global scope
$$ignore start 
# Will tell the LLM(compiler) to ignore the code between the start and end tokens
$$ignore end
```

# More code examples

Calculator
```cs
$$start
int a = 42
int b = 42
int sum = a + b
$$end
```

Calculator with inputs and outputs
```cs
$$start
int a = in<int>: "Enter the first number: "
int b = in<int>: "Enter the second number: "
int sum = a + b
out<int>: sum
$$end
```

Calculator with user defined amount of inputs
```cs
$$start
int amount = in<int>: "Enter the amount of numbers you want to sum: "
list numbers[amount]
for(i = 0; i < amount; i++){
    int a = in<int>: "Enter the $i$ number: "
    numbers.append(a)
}
int sum = sum: numbers
out<int>: sum
$$end
```

Fully functional normal calculator with user-defined amount of inputs and different operations
```cs
$$start
int amount = in<int>("Enter the amount of numbers you want to operate with: ")
list<int> numbers
for(int i = 0; i < amount; i++){
    int a = in<int>("Enter number " + std::to_string(i+1) + ": ")
    numbers.push_back(a)
}
int sum = sum: numbers
int difference = difference: numbers
int product = product: numbers
int quotient = quotient: numbers

$$end
```

### Functions examples

```cs
func sum(list<int> numbers){
    int sum = 0
    for(int i = 0; i < numbers.size(); i++){
        sum += numbers[i]
    }
    return sum
}
```

```cs
func removeEvenElements(list<int> numbers){
    list<int> oddNumbers
    for(int i = 0; i < numbers.size(); i++){
        if(numbers[i] % 2 != 0){
            oddNumbers.pushback(numbers[i])
        }
    }
    return oddNumbers
}
```

### Class examples
```cs
class Person{
    string name
    int age
    string gender
    string address
    string phoneNumber
    string email
    string job
    string education
    string hobbies
    string family
    string friends
    string socialMedia
    string bio
}

func getPersonInfo(Person person){
    out<string>: person.name
    out<int>: person.age
    out<string>: person.gender
    out<string>: person.address
    out<string>: person.phoneNumber
    out<string>: person.email
    out<string>: person.job
    out<string>: person.education
    out<string>: person.hobbies
    out<string>: person.family
    out<string>: person.friends
    out<string>: person.socialMedia
    out<string>: person.bio
}
```

Inheritance
```cs
class Person{
    string name
    int age
    string gender
    string address
    string phoneNumber
    string email
    string job
    string education
    string hobbies
    string family
    string friends
    string socialMedia
    string bio
}

class Student(Person){
    string school
    string grade
    string class
    string subjects
    string teachers
    string classmates
    string friends
    string socialMedia
    string bio
}

func getStudentInfo(Student){
    out<string>: student.name
    out<int>: student.age
    out<string>: student.gender
    out<string>: student.address
    out<string>: student.phoneNumber
    out<string>: student.email
    out<string>: student.job
    out<string>: student.education
    out<string>: student.hobbies
    out<string>: student.family
    out<string>: student.friends
    out<string>: student.socialMedia
    out<string>: student.bio
}
```

## Summarizing everything example
```cs
$$start

# Importing a library
$$import "mathLib.fus" as math

# Global variable
$$global appName = "LMFuS Demo"

# Environmental-global variable accessible across all LMFuS environment
$$envglobal version = "1.0"

# Defining a class
class Calculator{
    # Constructor
    func Calculator(){
        out: "Calculator initialized"
    }

    # Method to add numbers
    func add(int a, int b){
        return a + b
    }
}

# Instantiating the Calculator class
Calculator calc = new Calculator()

# Using a built-in function
out: "Welcome to " + appName + ", version " + version

# Input and output
string userName = in: "What's your name? "
out: "Hello, " + userName

# Conditional statement
if(userName == "admin"){
    out: "Welcome, admin!"
}
elseif(userName == "guest"){
    out: "Welcome, guest!"
}
else{
    out: "Welcome, unknown user!"
}

# Loop
for(i = 0; i < 5; i++){
    out<int>: i
}

# Error handling
try{
    # Simulate an error
    int result = calc.add("a", 2)
}
catch{
    out: "An error occurred during calculation."
}
finally{
    out: "Attempted calculation."
}

# Working with lists
list<int> numbers = {1, 2, 3, 4, 5}
numbers.append(6)
foreach(int number, numbers){
    out<int>: number
}

# Working with dictionaries
dict<string, int> ages = {"Alice": 30, "Bob": 25}
ages.update({"Charlie": 22})
out<int>: ages.get("Alice")

# File operations
file myFile = open<"w"> "log.txt"
myFile.write: "Log entry"
myFile.close()

# Ending the script
$$end
```

