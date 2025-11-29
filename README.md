# CppBasics

## 0. Setup & Compiling
- Source file: .cpp
- Common includes:
```cpp
    #include <iostream>
    using namespace std; // optional
```

- Compile & run (GCC / g++):
```cpp
    g++ main.cpp -o main
    ./main        // Windows: .\main.exe
```

- Multiple files:
```cpp
    g++ main.cpp utils.cpp -o app
```


## 1. Basic Syntax
- main function:
```cpp
    #include <iostream>
    using namespace std;

    int main() {
        cout << "Hello\n";
        return 0; // 0 = success
    }
```

- Variables & types:
```cpp
    int a = 5;
    double pi = 3.14;
    char c = 'A';
    bool ok = true;
```

- auto:
```cpp
    auto x = 10;      // int
    auto y = 3.5;     // double
```

- Input / Output:
```cpp
    int age;
    cout << "Enter age: ";
    cin >> age;
    cout << "You are " << age << " years old.\n";
```


## 2. Control Flow
- if / else:
```cpp
    if (x > 0) {
        cout << "positive\n";
    } else if (x == 0) {
        cout << "zero\n";
    } else {
        cout << "negative\n";
    }
```

- for loop:
```cpp
    for (int i = 0; i < 10; i++) {
        cout << i << " ";
    }
```

- while:
```cpp
    int n = 5;
    while (n > 0) {
        cout << n << " ";
        n--;
    }
```

- do-while:
```cpp
    int x;
    do {
        cout << "Enter positive: ";
        cin >> x;
    } while (x <= 0);
```

- switch:
```cpp
    int op;
    cin >> op;
    switch (op) {
        case 1: cout << "Option 1\n"; break;
        case 2: cout << "Option 2\n"; break;
        default: cout << "Unknown\n";
    }
```


## 3. Functions
- Define & call:
```cpp
    int add(int a, int b) {
        return a + b;
    }

    int main() {
        int result = add(3, 4);
        cout << result; // 7
    }
```

- Pass by value vs reference:
```cpp
    void incByValue(int x) {
        x++; // local copy only
    }

    void incByRef(int &x) {
        x++; // original changes
    }
```

- Function overloading:
```cpp
    int max(int a, int b) { return (a > b) ? a : b; }
    double max(double a, double b) { return (a > b) ? a : b; }
```

## 4. Arrays & std::vector
- Raw arrays (fixed size):
```cpp
    int arr[5];                 // uninitialized
    int arr2[5] = {1,2,3,4,5};

    int n = 5;
    for (int i = 0; i < n; i++) {
        cout << arr2[i] << " ";
    }
  // size must be known at compile time (stack arrays)
```

- Dynamic array (manual):
```cpp
    int n;
    cin >> n;
    int *a = new int[n];

    // use a[0] ... a[n-1]

    delete[] a;
```

- std::vector (recommended):
```cpp
    #include <vector>

    vector<int> v;      // empty
    v.push_back(10);
    v.push_back(20);

    for (int x : v) {
        cout << x << " ";
    }

    cout << v.size();   // number of elements
    v[0] = 100;         // indexing
```

- Vector with known size:
```cpp
    vector<int> v1(5);       // 5 elements, default 0
    vector<int> v2(5, 7);    // 5 elements, all 7
```

## 5. Strings
- std::string:
```cpp
    #include <string>

    string s = "Hello";
    cout << s << "\n";
    cout << s.size();       // length

    s += " world";          // concatenation

    for (char c : s) {
        cout << c << "-";
    }
```

- Input with spaces:
```cpp
    string name;
    getline(cin, name);     // reads whole line
```

- Common operations:
```cpp
    s[0];                   // first char
    s.substr(0, 5);         // from index 0, length 5
    s.find("lo");           // index or string::npos
```

## 6. Pointers & References
- Pointer basics:
```cpp
    int x = 10;
    int *p = &x;       // p stores address of x

    cout << p;         // address
    cout << *p;        // value at that address (10)

    *p = 20;           // x becomes 20
```

- nullptr:
```cpp
    int *p = nullptr;  // no address
```

- Reference:
```cpp
    int x = 5;
    int &ref = x;      // alias of x
    ref = 10;          // x becomes 10
```

- App-level rule of thumb:
    - Use references in function parameters.
    - Use pointers for dynamic memory or smart pointers.


## 7. Dynamic Memory (Basic)
- Manual allocation:
```cpp
    int *p = new int(5);
    cout << *p;
    delete p;

    int *arr = new int[10];
    // use arr[0..9]
    delete[] arr;
```
`
- Prefer: std::vector, std::string, smart pointers over raw new/delete.


## 8. Structs & Classes
- struct (public by default):
```cpp
    struct Point {
        int x;
        int y;
    };

    int main() {
        Point p;
        p.x = 3;
        p.y = 4;
    }
```

- class (private by default):
```cpp
    class Player {
    private:
        string name;
        int hp;
    public:
        Player(string n, int health) {
            name = n;
            hp = health;
        }

        void takeDamage(int dmg) {
            hp -= dmg;
        }

        int getHp() const { // const = does not modify members
            return hp;
        }
    };
```

- Usage:
```cpp
    int main() {
        Player p("Ben", 100);
        p.takeDamage(30);
        cout << p.getHp(); // 70
    }
```

- Constructor with member initializer list:
```cpp
    class Player {
        string name;
        int hp;
    public:
        Player(string n, int health) : name(n), hp(health) {}
    };
```

- Encapsulation:
    - Keep data private.
    - Expose behavior via public methods.


## 9. Inheritance & Polymorphism
- Basic inheritance:
```cpp
    class Shape {
    public:
        virtual double area() const { return 0.0; }
        virtual ~Shape() {}
    };

    class Circle : public Shape {
        double r;
    public:
        Circle(double radius) : r(radius) {}
        double area() const override { return 3.14159 * r * r; }
    };
```

- Polymorphism with pointers:
```cpp
    Shape *s = new Circle(5.0);
    cout << s->area();  // calls Circle::area
    delete s;
```

- Idea:
    - Use virtual for customizable behavior in subclasses.
    - Access via Base* or Base&.


## 10. Standard Library (STL) Essentials
- Common headers:
    - #include <vector>
    - #include <string>
    - #include <array>
    - #include <map>
    - #include <unordered_map>
    - #include <set>
    - #include <unordered_set>
    - #include <algorithm>
    - #include <numeric>

- std::array:
```cpp
    array<int, 5> arr = {1,2,3,4,5};
```

- std::map / std::unordered_map:
```cpp
    map<string, int> score;
    score["Ben"] = 10;
    cout << score["Ben"];

    unordered_map<string, int> fastScore; // no order, faster average
```

- std::set / std::unordered_set:
```cpp
    set<int> s;
    s.insert(5);
    s.insert(3);
    s.insert(5); // duplicate ignored
```

- Algorithms:
```cpp
    vector<int> v = {5,3,8,1};

    sort(v.begin(), v.end());          // 1 3 5 8
    reverse(v.begin(), v.end());       // 8 5 3 1

    int sum = accumulate(v.begin(), v.end(), 0);
    auto it = find(v.begin(), v.end(), 5); // iterator or v.end()
```

## 11. Error Handling
- Return codes:
```cpp
    int loadConfig() {
        if (/* failed */) return -1;
        return 0;
    }
```

- Exceptions:
```cpp
    #include <stdexcept>

    double divide(double a, double b) {
        if (b == 0) throw runtime_error("Division by zero");
        return a / b;
    }

    int main() {
        try {
            cout << divide(10, 0);
        } catch (const runtime_error &e) {
            cout << "Error: " << e.what();
        }
    }
```

- assert (debug only):
```cpp
    #include <cassert>

    int main() {
        int x = 5;
        assert(x > 0); // if false, abort in debug
    }
```


## 12. File I/O
- Read and write text files:
```cpp
    #include <fstream>
    #include <string>

    int main() {
        // Write
        ofstream out("data.txt");
        if (!out) return 1;
        out << "Hello file\n";
        out.close();

        // Read
        ifstream in("data.txt");
        if (!in) return 1;
        string line;
        while (getline(in, line)) {
            cout << line << "\n";
        }
        in.close();
    }
```


## 13. Splitting Code into Multiple Files
- Player.h:
```cpp
    #pragma once
    #include <string>
    using namespace std;

    class Player {
        string name;
        int hp;
    public:
        Player(string n, int hp);
        void takeDamage(int dmg);
        int getHp() const;
    };
```

- Player.cpp:
```cpp
    #include "Player.h"

    Player::Player(string n, int h) : name(n), hp(h) {}

    void Player::takeDamage(int dmg) {
        hp -= dmg;
    }

    int Player::getHp() const {
        return hp;
    }
```

- main.cpp:
```cpp
    #include <iostream>
    #include "Player.h"
    using namespace std;

    int main() {
        Player p("Ben", 100);
        p.takeDamage(40);
        cout << p.getHp();
    }
```

- Compile:
    g++ main.cpp Player.cpp -o game

## 14. Operators & Boolean Logic

- Arithmetic: `+  -  *  /  %`
- Assignment: `=  +=  -=  *=  /=  %=`
- Comparison: `==  !=  <  >  <=  >=`
- Logical: `&&  ||  !`
- Increment: `++  --`
- Ternary:
    ```cpp
    int minVal = (a < b) ? a : b;
    ```

- Boolean expressions:
    ```cpp
    bool isAdult      = (age >= 18);
    bool isEqualFive  = (x == 5);
    bool notFive      = (x != 5);

    bool adultAndRich  = (age >= 18 && money > 1000);
    bool childOrSenior = (age < 18 || age >= 65);
    bool notAdult      = !(age >= 18);
    ```

---

## 15. More on Loops

- `while` (condition checked before each iteration):
    ```cpp
    int i = 0;
    while (i < 5) {
        cout << i << " ";
        i++;
    }
    ```

- `do-while` (runs at least once):
    ```cpp
    int val;
    do {
        cin >> val;
    } while (val <= 0);
    ```

- Classic `for` (known count):
    ```cpp
    for (int i = 0; i < 5; i++) {
        cout << i << " ";
    }
    ```

- Range-based `for` (for-each style):
    ```cpp
    int arr[] = {1, 2, 3};
    for (int x : arr) {
        cout << x << " ";
    }
    ```

- `break` and `continue`:
    ```cpp
    while (true) {
        int v;
        cin >> v;

        if (v < 0) break;     // exit the loop
        if (v == 0) continue; // skip rest, go to next iteration

        // process v...
    }
    ```

---

## 16. Function Parameters & Prototypes

- Pass by value (copy):
    ```cpp
    void incVal(int x) { 
        x++; // caller not changed
    }
    ```

- Pass by reference:
    ```cpp
    void incRef(int &x) {
        x++; // caller variable changes
    }
    ```

- `const` reference (read-only, avoids copy):
    ```cpp
    void printName(const string& name) {
        cout << name << "\n";
    }
    ```

- Function prototype:
    ```cpp
    int mul(int x, int y);   // declaration (prototype)

    int main() {
        int r = mul(2, 3);
    }

    int mul(int x, int y) {  // definition
        return x * y;
    }
    ```

---

## 17. Scope (Global vs Local)

- Global variable: defined outside all functions
- Local variable: defined inside a function or block

```cpp
int gvar = 10;   // global

void foo() {
    int local = 5;   // only visible inside foo()
}
```
Inner scopes can see outer variables, but not the other way around.

## 18. Pointer Tricks (Array + Pointer)
You already know basic pointers. Common array pattern:

```cpp
int arr[3] = {4, 1, 5};

// Pointer walking through array
for (int *p = arr; p < arr + 3; p++) {
    cout << *p << " ";
}
```

## 19. const Correctness
cpp
Copy code
void foo(const int x);   // x not modified
void bar(int& x);        // x may change
void baz(const int& x);  // reference but read-only
In classes:

```cpp
class Sample {
    int value;
public:
    int get() const { return value; } // does not modify object
    void set(int v) { value = v; }    // may modify object
};
```
Use const wherever something should not be changed (helps avoid bugs).

## 20. Enums
Basic enum:

```cpp
enum Color { RED, GREEN, BLUE };

Color c = RED;
```
Scoped enum (recommended):

```cpp
enum class Direction { Up, Down, Left, Right };

Direction dir = Direction::Up;
```

## 21. Random Numbers (classic C-style)
```cpp
#include <cstdlib> // rand, srand
#include <ctime>   // time

int main() {
    srand(time(nullptr));           // seed once

    int r1to6   = rand() % 6 + 1;   // 1–6
    int r1to100 = rand() % 100 + 1; // 1–100
}
```
(For serious projects, modern C++ prefers <random>, but this is enough early on.)

## 22. Namespaces
```cpp
namespace mathStuff {
    int square(int x) { return x * x; }
}

int main() {
    int s = mathStuff::square(5);  // 25
}
```
Avoid using namespace std; in headers; ok in small .cpp files when learning.

## 23. Templates (Basic)
```cpp
template <typename T>
T myMax(T a, T b) {
    return (a > b) ? a : b;
}

int   m1 = myMax(3, 7);        // T = int
double m2 = myMax(2.5, 1.3);   // T = double
```
Templates let you write one function that works for many types.

## 24. Recursion (Example)
```cpp
int fact(int n) {
    if (n <= 1) return 1;      // base case
    return n * fact(n - 1);    // recursive case
}
```
Rules of thumb:

- Must have a base case that stops.
- Each call should simplify the problem and move toward the base case.
