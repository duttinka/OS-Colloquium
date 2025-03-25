# OS-Colloquium
**Никитёнок Диана Михайловна**   
**9 Группа**  
**Вариант 2**  

## Ответы на вопросы

### Нулевая группа вопросов
#### 1. Win API, необходимое для Лабораторной работы №2
Лабораторная работа требует написания консольного процесса, который создаёт три потока:  
- main — главный поток;
- min_max — поток, вычисляющий минимум и максимум в массиве чисел;
- average — поток, вычисляющий среднее значение.

Для создания потоков и управления ими использовались следующие функции Win API:
- `CreateThread` – для создания потоков.
  
    ```cpp
   HANDLE hThread1, hThread2;
   DWORD ThreadID1, ThreadID2;
   hThread1 = CreateThread(NULL, 0, min_max, &data, 0, &ThreadID1);
   hThread2 = CreateThread(NULL, 0, average, &data, 0, &ThreadID2);

- `WaitForSingleObject` – для ожидания завершения потоков. Если требуется синхронизировать несколько потоков одновременно, можно использовать WaitForMultipleObjects.
  
  ```cpp
    WaitForSingleObject(hThread1, INFINITE); 
    WaitForSingleObject(hThread2, INFINITE); 

- Sleep — приостановка выполнения потока.
Для задержки выполнения программы в лабораторной работе использовались следующие вызовы:

Поток min_max: 7 миллисекунд после каждого сравнения элементов массива.

Поток average: 12 миллисекунд после каждой операции суммирования элементов.

Для защиты общих данных используются критические секции (InitializeCriticalSection, EnterCriticalSection, LeaveCriticalSection), если потребуется расширение функциональности.

Если потоки работают с ограниченными ресурсами, используются семафоры (CreateSemaphore, WaitForSingleObject, ReleaseSemaphore).

#### 2. Что такое процесс в ОС Windows?
Процесс – это экземпляр программы, выполняющийся в операционной системе. Каждый процесс имеет:
- Собственное адресное пространство.
- Набор системных ресурсов (файлы, дескрипторы).
- Один или несколько потоков выполнения.
#### 3. Что такое критическая секция
Критическая секция – это участок кода, доступ к которому должен быть строго синхронизирован, чтобы избежать одновременного выполнения несколькими потоками. Для работы с критическими секциями используются:
-InitializeCriticalSection
-EnterCriticalSection
-LeaveCriticalSection
    ```cpp
CRITICAL_SECTION cs;
InitializeCriticalSection(&cs);
EnterCriticalSection(&cs);
// критический код
LeaveCriticalSection(&cs);


#### 4. Что такое семафор
Семафор – это средство синхронизации, которое ограничивает количество потоков, одновременно получающих доступ к ресурсу. В Win API используется:
-CreateSemaphore
-WaitForSingleObject
-ReleaseSemaphore

#### 5. Сравнительный анализ C++98 и современных стандартов
1). **Потоки:**
   - **C++98**: Нет поддержки потоков (используются WinAPI/pthread).
   - **C++98 с Boost**: Поддержка потоков через **Boost.Thread**.
   - **C++11/17**: Встроенная поддержка потоков через **std::thread**.
   - **C++11/17 с Qt**: Используется **QThread** для потоков.
2). **Умные указатели:**
   - **C++98**: Только сырые указатели.
   - **C++98 с Boost**: **boost::shared_ptr** для управления памятью.
   - **C++11/17**: **std::shared_ptr** и **std::unique_ptr**.
   - **C++11/17 с Qt**: **QSharedPointer** для работы с памятью.
3). **Функциональные объекты:**
   - **C++98**: **std::bind1st**, **std::bind2nd**.
   - **C++98 с Boost**: **boost::bind**.
   - **C++11/17**: **std::bind**, **std::function**.
   - **C++11/17 с Qt**: **std::function**.
4). **Работа с JSON/XML:**
   - **C++98**: Нет стандартных средств, парсинг вручную.
   - **C++98 с Boost**: **boost::property_tree** для работы с XML/JSON.
   - **C++11/17**: Использование сторонних библиотек, например, **nlohmann/json**.
   - **C++11/17 с Qt**: **QJsonDocument**, **QXmlStreamReader** для работы с JSON/XML.
5). **Регулярные выражения:**
   - **C++98**: Нет поддержки.
   - **C++98 с Boost**: **boost::regex** для регулярных выражений.
   - **C++11/17**: **std::regex**.
   - **C++11/17 с Qt**: **QRegularExpression** для работы с регулярными выражениями.
     
### Общие вопросы

#### 1.ООП (Объектно-Ориентированное Программирование)
ООП — парадигма программирования, основанная на концепциях:
1. Инкапсуляция
2. Наследование
3. Полиморфизм
4. Абстракция

#### 2. Магическое число 7 Миллера
Джордж Миллер утверждал, что человек может удерживать в памяти 7±2 элемента информации.  

#### Примеры в IT:
1. 7 фаз компиляции в C++.
2. 7 регистров процессора (x86) – EAX, EBX, ECX, EDX, ESI, EDI, EBP.
3. Количество уровней вложенности в коде (до 7, иначе код трудно понимать)
4. Количество вкладок в браузере, которые может удерживать человек
5. Окно кода в IDE (обычно 7 строк в фокусе)
6. Количество элементов в UI-меню
7. Количество колонок в таблице UI

#### 3. Энтропия ПО
Энтропия в ПО — тенденция системы к усложнению и деградации.

#### Негэнтропийные меры (снижение энтропии)
1. Рефакторинг кода
2. Тестирование (TDD, Unit-тесты)
3. Статический анализ кода
4. Документирование API
5. Фиксированные кодстайлы 

#### 4. 5 признаков сложной системы по Бучу
1. Абстракция (пример: использование структур в С)
2. Инкапсуляция (пример: хранение данных в main.h)
3. Модульность (пример: Makefile + модульная структура)
4. Иерархия (пример: наследование в C++ проектах)
5. Типизация (пример: строгая типизация в C++)

#### 5. Закон иерархических компенсаций Седова
Закон: чем сложнее система, тем больше на нижних уровнях компенсации.
Исторические примеры в IT:
1. MS-DOS → Windows (упрощение UI → усложнение ядра)
2. C → Python (упрощение кода → усложнение интерпретатора)
3. Git → GUI клиенты (GitKraken) (простота для пользователя → сложность под капотом)
4. Скрипты Bash → Docker (упрощение деплоя → сложные контейнеры)
5. Rust как замена C++ для безопасного управления памятью.

# Задачи

## 1) Генерация чисел Фибоначчи
  ```cpp
  #include <gtest/gtest.h>
  #include <vector>

  std::vector<int> fibonacci(int n) {
      if (n <= 0) return {};
      std::vector<int> fib{0};
      if (n > 1) fib.push_back(1);
      for (int i = 2; i < n; ++i) {
          fib.push_back(fib[i - 1] + fib[i - 2]);
      }
      return fib;
  }

  TEST(FibonacciTest, BasicCases) {
      EXPECT_EQ(fibonacci(1), std::vector<int>({0}));
      EXPECT_EQ(fibonacci(2), std::vector<int>({0, 1}));
      EXPECT_EQ(fibonacci(5), std::vector<int>({0, 1, 1, 2, 3}));
  }

  TEST(FibonacciTest, EdgeCases) {
      EXPECT_EQ(fibonacci(0), std::vector<int>());
      EXPECT_EQ(fibonacci(-5), std::vector<int>());
  }
```

## 2) Проверка палиндромов
  ```cpp
#include <gtest/gtest.h>
#include <string>

bool is_palindrome(int num) {
    auto str = std::to_string(num);
    auto reversed = std::string(str.rbegin(), str.rend());
    return str == reversed;
}

TEST(PalindromeTest, PositiveCases) {
    EXPECT_TRUE(is_palindrome(121));
    EXPECT_TRUE(is_palindrome(1221));
    EXPECT_TRUE(is_palindrome(1));
}

TEST(PalindromeTest, NegativeCases) {
    EXPECT_FALSE(is_palindrome(123));
    EXPECT_FALSE(is_palindrome(10));
}
```
## 3) Разворот связного списка
  ```cpp
#include <gtest/gtest.h>
#include <vector>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

Node* reverse_list(Node* head) {
    Node* prev = nullptr;
    while (head) {
        Node* next = head->next;
        head->next = prev;
        prev = head;
        head = next;
    }
    return prev;
}

std::vector<int> list_to_vector(Node* head) {
    std::vector<int> result;
    while (head) {
        result.push_back(head->data);
        head = head->next;
    }
    return result;
}

TEST(LinkedListTest, ReverseList) {
    Node* head = new Node(1);
    head->next = new Node(2);
    head->next->next = new Node(3);

    Node* reversed = reverse_list(head);
    EXPECT_EQ(list_to_vector(reversed), std::vector<int>({3, 2, 1}));
}

