## Домашнее задание 3

### Подготовка
Создаю проект.
```
git clone https://github.com/tp-labs/lab03
git remote remove origin
git remote add origin https://github.com/ammobaggage/lab03
git branch -m main 
```

Представьте, что вы стажер в компании "Formatter Inc.".
### Задание 1
```
cd lab03/formatter_lib
touch CMakeLists.txt
cat > CMakeLists.txt << EOF
	> cmake_minimum_required(VERSION 3.4)
	project(formatter)
	set(CMAKE_CXX_STANDARD 11)
	set(CMAKE_CXX_STANDARD_REQUIRED ON)
	add_library(
	    formatter
	    STATIC
	    formatter.cpp
	)
	include_directories(${CMAKE_CURRENT_SOURCE_DIR})
	> EOF
```

```cmake -H. -B_build```
**Вывод:**
>CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
>  Compatibility with CMake < 3.5 will be removed from a future version of
>  CMake.
>
> Update the VERSION argument <min> value or use a ...<max> suffix to tell
>  CMake that the project does not need compatibility with older versions.


>-- The C compiler identification is GNU 13.3.0
>-- The CXX compiler identification is GNU 13.3.0
>-- Detecting C compiler ABI info
>-- Detecting C compiler ABI info - done
>-- Check for working C compiler: /usr/bin/cc - skipped
>-- Detecting C compile features
>-- Detecting C compile features - done
>-- Detecting CXX compiler ABI info
>-- Detecting CXX compiler ABI info - done
>-- Check for working CXX compiler: /usr/bin/c++ - skipped
>-- Detecting CXX compile features
>-- Detecting CXX compile features - done
>-- Configuring done (1.3s)
>-- Generating done (0.0s)
>-- Build files have been written to: /home/opiates/ammobaggage/workspace/projects/lab03/formatter_lib/_build



### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.

### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

**Удачной стажировки!**

## Links
- [Основы сборки проектов на С/C++ при помощи CMake](https://eax.me/cmake/)
- [CMake Tutorial](http://neerc.ifmo.ru/wiki/index.php?title=CMake_Tutorial)
- [C++ Tutorial - make & CMake](https://www.bogotobogo.com/cplusplus/make.php)
- [Autotools](http://www.gnu.org/software/automake/manual/html_node/Autotools-Introduction.html)
- [CMake](https://cgold.readthedocs.io/en/latest/index.html)

```
Copyright (c) 2015-2021 The ISC Authors
```
