# Семинар №1 - Въведение
## Що е то *алгоритъм*?
Ще започнем с един цитат от научната литература:
```
What is an algorithm? An algorithm is a procedure to accomplish a specific task. 
An algorithm is the idea behind any reasonable computer program. 
To be interesting, an algorithm must solve a general, well-specified problem.
```
Общоприета формална дефиниция за понятието алгоритъм няма. Често обаче се среща следното описание, което и ние ще използваме в рамките на курса:
> **Алгоритъм** наричаме *крайна* последователност от стъпки, които водят до решаването на дадена задача.
---
[ **EXTRA** ] Някои ключови свойства на алгоритмите са:
* Финитност - алгоритъмът прикючва за краен брой стъпки независимо от входните данни.
* Дефинитност - всяка стъпка е прецизно и недвусмислено дефинирана.
* Детерминираност - изходът (резултатът) зависи изцяло от входните данни и от нищо друго.
* И други...

## Що е то *структура от данни*?
Първо нека разгледаме понятието **данни**. Те представляват значима за нас **информация** под формата на числови стойности. С цел лесното им съхранение, трансфер и обработка, данните трябва да бъдат **структурирани**.

> **Структура от данни** можем да дефинираме като начин да подредим (*структурираме*) данните в подходящ формат спрямо конкретната задача.

Формално можем и да използваме следният цитат:
```
Структура от данни е организирана информация, която може да се опише, създаде и обработи с помощта на програма.
```

**Няма перфектна структура от данни** - всяка една има своите предимства и недостатъци. С течение на курса ще се запознаем с някои от най-често срещаните структури и ще видим приликите и разликите между тях, както и в какви ситуации трябва да бъдат използвани.

---
[ **EXTRA** ] Една структура от данни се състои от:
* Логическо описание - декомпозиция на структурата до по-простите й съставни елементи, както и възможните операции над нея. Това е абстрактна концепция, която не зависи по никакъв начин от имплементация или използван изчислителен модел.
* Физическо описание - представяне на структурата в паметта спрямо конкретна имплементация.

## Анализ на сложността
Сложността на един алгоритъм е ключова негова характеристика, която ни позволява да *съпоставяме неговата ефикасност* с тази на други алгоритми. Тя е мярка за това колко **ресурси** (най-често *време* и *памет*) са необходими при изпълнение върху вход с **конкретна големина**.

### Сложност по време
Бихме могли да определим сложността по време като функция, която ни дава информация за това колко на брой стъпки ще извърши алгоритъма при вход с конкретна големина (която често ще бележим с `n`).

Ясно се вижда, че това е доста непълно определение. Например, задачата сортиране на масив може да отнеме много по-малко стъпки за вече сортиран масив, отколкото за несортиран такъв със същата големина. Затова разглеждаме няколко "сценарии" за сложността по време:

* **Сложност в най-лошия случай** (Worst-Case) - песимистична оценка за сложността на алгоритъма. Тя ни показва колко най-много стъпки можем да очакваме той да извърши.
  
* **Сложност в най-добрия случай** (Best-Case) - оптимистична оценка за сложността на алгоритъма. Тя ни показва колко най-малко стъпки можем да очакваме той да извърши.
  
* **Сложност в средния случай** (Average-Case) - показва осреднено колко стъпки очакваме алгоритъмът да извърши, като вземем предвид всеки един възможен вход с конкретната подадена големина.
  
* **Амортизирана сложност** - сложност при многократно изпълнение на алгоритъма. Тази оценка е полезна при операции, които много често са "евтини" за изпълнение, но в някои крайни случаи могат да бъдат "скъпи".

#### Примери за сложност по време
* О(1) - константна сложност
```c++
int average(int first, int second)
{
	return (first + second) / 2;
}
```

* О(log n) - логаритмична сложност
```c++
int binarySearch(const int* arr, int target, int left, int right) 
{
    if (left > right) 
    {
        return -1;
    }

    int mid = left + (right - left) / 2;

    if (arr[mid] == target) 
    {
        return mid;
    } 
    else if (arr[mid] < target) 
    {
        return recursiveBinarySearch(arr, target, mid + 1, right);
    } 
    else 
    {
        return recursiveBinarySearch(arr, target, left, mid - 1);
    }
}
```

* О(n) - линейна сложност
```c++
int factorial(unsigned n) 
{
    unsigned res = 1;
    for(unsigned i = 1; i <= n; i++)
    {
        res *= i;
    }
    return res;
}
```

* О(n*log n) - линейно-логаритмична сложност
```c++
void printIndexes(const int* arr, size_t size) 
{
    for (int i = 0; i < size; i++) 
    {
        std::cout << binarySearch(arr, size, arr[i], 0, size - 1);
    }
}
```

* О(n^2) - квадратична сложност
```c++
void printPairs(const int* arr, size_t size) {
    for (int i = 0; i < size; i++) 
    {       
        for (int j = 0; j < size; j++) 
        {   
            std::cout << arr[i] << " " << arr[j] << std::endl;
        }
    }
}
```

* O(1.618^n) - експоненциална сложност с основа phi
```c++
int fibonacci(int n) 
{ 
    if (n <= 0) 
    { 
        return 0; 
    } 
    else if (n == 1) 
    { 
        return 1; 
    } 
    else 
    { 
        return fibonacci(n - 1) + fibonacci(n - 2); 
    } 
}
```

* О(2^n) - експоненциална сложност с основа 2
```c++
void towersOfHanoi(int n, char src, char aux, char dest) 
{ 
    if (n == 1) 
    { 
        cout << "Move disk 1 from " << src << " to " << dest << endl; 
        return; 
    } 

    towersOfHanoi(n - 1, src, dest, aux);
    cout << "Move disk " << n << " from " << src << " to " << dest << endl; 
    towersOfHanoi(n - 1, aux, src, dest); 
}
```

* Въпрос - този алгоритъм с каква сложност е?
```c++
void example(const int* arr, size_t n) 
{ 
    int s = 0;
    for (int i = 1; i <= n; i++)
    {
        for (int j = n + i - 5; j <= n; j++)
        {
            s += 2;
        } 
        s++;
    }
}
```

### Сложност по памет
Сложността по памет на даден алгоритъм е количеството памет, който той използва в процеса си на изпълнение, като съответно не броим тази, заделена за входа му. Най-просто казано - **работната памет** на алгоритъма.

Аналогично на сложността по време може да се разглежда сложност по памет в най-добрия, в средния и в най-лошия случай.

Алгоритъм, който използва константно количество памет (с други думи O(1) сложност по памет) се нарича **in-place**.

---
[ **EXTRA** ] Сложността по памет е ограничена отгоре от сложността по време. Това е така, тъй като стъпките по заделянето и обработката на работната памет се включва към общия брой стъпки, което съответно прави сложността по време (броят стъпки) по-голям или равен от размера на допълнителната памет.

## Изчисляване на сложност
### Сложност на итеративни алгоритми
Итеративни алгоритми са тези, които използват в рамките на своето изпълнение така наречените конструкции за цикъл - for, while, do-while.

[ **EXTRA** ] Най-разпространеният и прост метод за изчисляване на сложността им е подходът със **суми по изпълнението на циклите**.

**Примери:**

```c++
void sumFirstFive(vector<int>& arr) 
{
    int sum = 0;
    for (int i = 0; i < 5; i++) 
    {
        sum += arr[0];
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(1)
</details>
<br/>

```c++
void sum(vector<int>& arr) 
{
    int sum = 0;
    size_t n = arr.size();
    for (int i = 0; i < n; i++) 
    {
        sum += arr[0];
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n)
</details>
<br/>

```c++
void sum(vector<int>& arr) 
{
    int sum = 0;
    for (int i = 0; i < arr.size(); i++) 
    {
        sum += arr[0];
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n)
</details>
<br/>

```c++
bool isPrime(int n) 
{
    if(n <= 1)
    {
    	return false;
    }

    bool isPrime = true;
    for (int i = 2; i <= sqrt(n); i++)
    {
    	if (n % i == 0)
    	{
    		isPrime = false; 
    		break;
    	}
    }

    return isPrime;
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(log(n) * n^(1/2))

  (Функцията sqrt има сложност Theta(log(n)))
</details>
<br/>

```c++
bool isPrime(int n) 
{
    if(n <= 1)
    {
    	return false;
    }

    bool isPrime = true;
    double sqrtFromNumberToCheck = sqrt(n);
    for (int i = 2; i <= sqrtFromNumberToCheck; i++)
    {
    	if (n % i == 0)
    	{
    		isPrime = false; 
    		break;
    	}
    }

    return isPrime;
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n^(1/2))
</details>
<br/>

```c++
void doStuff(vector<int>& arr) 
{
    int n = arr.size();
    for (int i = 1; i <= n; i *= 2) 
    {
        // Theta(1)
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(log(n))
</details>
<br/>


```c++
void doStuff(vector<int>& arr) 
{
    int n = arr.size();
    for (int i = 1; i <= n; i++) 
    {
        for(int j = i; j <= n; j++)
        {
            // Theta(1)
        }
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n^2)
</details>
<br/>

```c++
void doStuff(vector<int>& arr) 
{
    int n = arr.size();
    for (int i = 1; i <= n; i++) 
    {
        for(int j = 1; j <= n; j+=i)
        {
            // Theta(1)
        }
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n*log(n))
</details>
<br/>

```c++
void doStuff(vector<int>& arr) 
{
    int n = arr.size();
    for (int i = 2; i <= n; i *= 2) 
    {
        for(int j = 1; j <= i; j++)
        {
            // Theta(1)
        }
    }
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n)
</details>
<br/>

### Сложност на рекурсивни алгоритми
Рекурсивни алгоритми са тези, които в рамките на своето изпълнение извикват себе си директно или индиректно, като входните данни на всяко следващо извикване трябва да бъдат различни.

[ **EXTRA** ] Има множество подходи за пресмятане на сложността на рекурсивен алгоритъм. Някои от тях са:
* Анализ на дървото на изпълнение
* Индукция по размера на входа
* Чрез рекурентни уравнения
* Други...

**Примери:**
```c++
int sum(int n) 
{
    if (n <= 0)
    {
        return 0;
    }
    return 1 + sum(n - 1);
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(n)
</details>
<br/>

```c++
int divSum(int n) 
{
    if (n <= 0)
    {
        return 0;
    }
    return 1 + sum(n/2);
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(log(n))
</details>
<br/>

```c++
unsigned fibb(unsigned n) 
{
    if (n < 2)
    {
        return 1;
    }
    return fibb(n-1) + fibb(n-2);
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(1.618^n)
</details>
<br/>

```c++
int tree(int n) 
{
    if (n <= 0)
    {
        return 0;
    }
    return tree(n - 1)+ tree(n - 1);
}
```
<details>
  <summary>Отговор</summary>
  Сложност по време: Theta(2^n)
</details>
<br/>

## Допълнителни материали
За задачите в HackerRank ще е добре да разгледате документациите на следните структури, разглеждани в курса по ООП:

* [**std::string**](https://en.cppreference.com/w/cpp/string/basic_string) - динамичен масив с char елементи (низ)
* [**std::pair**](https://en.cppreference.com/w/cpp/utility/pair) - наредена двойка от типове Т1 и Т2
* [**std::vector**](https://en.cppreference.com/w/cpp/container/vector) - динамичен масив с елементи от тип Т

Две полезни команди, които ще "забързат" кода ви в HackerRank също така са:
```c++
ios_base::sync_with_stdio(false);
cin.tie(NULL);
```

## Решаване на задачи:

[Link към задачи, решавани на семинара (2SUM, Move Zeros, Plus One)](https://www.hackerrank.com/contests/seminar-01)

### Допълнителни задачи
[01. Encode Password](https://www.hackerrank.com/contests/practice-1-sda/challenges/encoding-password)

[02. Majority Element](https://leetcode.com/problems/majority-element/description/)

[03. Water Volumes](https://leetcode.com/problems/container-with-most-water/description/)

[04. Single Number](https://leetcode.com/problems/single-number/description/)

[05. First Missing Positive](https://leetcode.com/problems/first-missing-positive/description/)
