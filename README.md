## Laboratory work III

Представьте, что вы стажер в компании "Formatter Inc.".
### Задание 1
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.
```
git clone https://github.com/tp-labs/lab03
cd /home/alexandra/lab03/formatter_lib
vim CMakeLists.txt

```
```
cmake_minimum_required(VERSION 3.4)
project (formatter_lib)
 
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON) 
add_library(formatter_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter.cpp)
```

```
cmake -H. -B_build && cmake --build _build
```

```-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is GNU 9.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/alexandra/lab03/formatter_lib/_build
Scanning dependencies of target formatter_lib
[ 50%] Building CXX object CMakeFiles/formatter_lib.dir/formatter.cpp.o
[100%] Linking CXX static library libformatter_lib.a
[100%] Built target formatter_lib
```

### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.
```cd ./formatter_ex_lib
  vim CMakeLists.txt
```
```
cmake_minimum_required(VERSION 3.4)
project(formatter_ex_lib)
 
set(CMAKE_CXX_STANDART 11)
set(CMAKE_CXX_STANDART_REQUIRED ON)
 
include_directories("../formatter_lib")

add_library(formatter_ex_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex.cpp)

```

```
-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is GNU 9.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/alexandra/lab03/formatter_ex_lib/_build
Scanning dependencies of target formatter_ex_lib
[ 50%] Building CXX object CMakeFiles/formatter_ex_lib.dir/formatter_ex.cpp.o
[100%] Linking CXX static library libformatter_ex_lib.a
[100%] Built target formatter_ex_lib
```
### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.
```
cd ./hello_world_application
vim CMakeLists.txt
```
```
cmake_minimum_required(VERSION 3.4)
project(hello_world_application)
set(CMAKE_CXX_STANDART 11)
set(CMAKE_CXX_STANDART_REQUIRED ON)
include_directories("../formatter_lib")
include_directories("../formatter_ex_lib")
add_library(formatter_lib STATIC "../formatter_lib/formatter.cpp")
add_library(formatter_ex_lib STATIC "../formatter_ex_lib/formatter_ex.cpp")
add_executable (hello_world_application "hello_world.cpp")
target_link_libraries(hello_world_application formatter_ex_lib formatter_lib)
```
```
-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is GNU 9.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/alexandra/lab03/hello_world_application/_build
Scanning dependencies of target formatter_lib
[ 16%] Building CXX object CMakeFiles/formatter_lib.dir/home/alexandra/lab03/formatter_lib/formatter.cpp.o
[ 33%] Linking CXX static library libformatter_lib.a
[ 33%] Built target formatter_lib
Scanning dependencies of target formatter_ex_lib
[ 50%] Building CXX object CMakeFiles/formatter_ex_lib.dir/home/alexandra/lab03/formatter_ex_lib/formatter_ex.cpp.o
[ 66%] Linking CXX static library libformatter_ex_lib.a
[ 66%] Built target formatter_ex_lib
Scanning dependencies of target hello_world_application
[ 83%] Building CXX object CMakeFiles/hello_world_application.dir/hello_world.cpp.o
[100%] Linking CXX executable hello_world_application
[100%] Built target hello_world_application
```
```
cd ./solver_application
vim CMakeLists.txt
```
```
cmake_minimum_required(VERSION 3.4)
project(hello_world_application)
set(CMAKE_CXX_STANDART 11)
set(CMAKE_CXX_STANDART_REQUIRED ON)
include_directories("../formatter_lib")
include_directories("../formatter_ex_lib")
add_library(formatter_lib STATIC "../formatter_lib/formatter.cpp")
add_library(formatter_ex_lib STATIC "../formatter_ex_lib/formatter_ex.cpp")
add_executable (hello_world_application "hello_world.cpp")
target_link_libraries(hello_world_application formatter_ex_lib formatter_lib)
```
```
- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is GNU 9.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/alexandra/lab03/solver_lib/_build
Scanning dependencies of target formatter
[ 50%] Building CXX object CMakeFiles/formatter.dir/solver.cpp.o
[100%] Linking CXX static library libformatter.a
[100%] Built target formatter
```
```
-- The C compiler identification is GNU 9.4.0
-- The CXX compiler identification is GNU 9.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/alexandra/lab03/solver_application/_build
Scanning dependencies of target formatter_lib
[ 12%] Building CXX object CMakeFiles/formatter_lib.dir/home/alexandra/lab03/formatter_lib/formatter.cpp.o
[ 25%] Linking CXX static library libformatter_lib.a
[ 25%] Built target formatter_lib
Scanning dependencies of target solver_lib
[ 37%] Building CXX object CMakeFiles/solver_lib.dir/home/alexandra/lab03/solver_lib/solver.cpp.o
[ 50%] Linking CXX static library libsolver_lib.a
[ 50%] Built target solver_lib
Scanning dependencies of target formatter_ex_lib
[ 62%] Building CXX object CMakeFiles/formatter_ex_lib.dir/home/alexandra/lab03/formatter_ex_lib/formatter_ex.cpp.o
[ 75%] Linking CXX static library libformatter_ex_lib.a
[ 75%] Built target formatter_ex_lib
Scanning dependencies of target solver_application
[ 87%] Building CXX object CMakeFiles/solver_application.dir/equation.cpp.o
[100%] Linking CXX executable solver_application
[100%] Built target solver_application
```
**Удачной стажировки!**


