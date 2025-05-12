# Домашнее задание 3

## Подготовка
```
git clone https://github.com/tp-labs/lab03
git remote remove origin
git remote add origin https://github.com/ammobaggage/lab03
git branch -m main 
```

## Задание 1
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
---
```
cmake -H. -B_build
```

**Вывод:**
```
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.3.0
-- The CXX compiler identification is GNU 13.3.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (1.3s)
-- Generating done (0.0s)
-- Build files have been written to: /home/opiates/ammobaggage/workspace/projects/lab03/formatter_lib/_build
```
---
``` 
cmake --build _build
```

**Вывод:**
```
[ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
[100%] Linking CXX static library libformatter.a
[100%] Built target formatter
```
---
```
git add .
git commit -m "Добавлена сборка formatter_lib"
git push origin main
```

## Задание 2
```
cd formatter_ex_lib
touch CMakeLists.txt
cat > CMakeLists.txt << EOF
	>cmake_minimum_required(VERSION 3.5)
	project(formatter_ex)
	
	add_subdirectory(../formatter_lib formatter)
	
	set(CMAKE_CXX_STANDARD 11)
	set(CMAKE_CXX_STANDARD_REQUIRED ON)
	
	add_library(formatter_ex STATIC formatter_ex.cpp)
	
	target_include_directories(
	    formatter_ex
	    PRIVATE
	    ../formatter_lib
	)
	
	target_link_libraries(formatter_ex PRIVATE formatter)
	>EOF
```
---
```
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
```
**Вывод:**
```
-- The C compiler identification is GNU 13.3.0
-- The CXX compiler identification is GNU 13.3.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
CMake Deprecation Warning at /home/opiates/ammobaggage/workspace/projects/lab03/formatter_lib/CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (1.1s)
-- Generating done (0.0s)
-- Build files have been written to: /home/opiates/ammobaggage/workspace/projects/lab03/formatter_ex_lib/build
```
---
```
cmake --build .
```
**Вывод:**

```
[ 25%] Building CXX object formatter/CMakeFiles/formatter.dir/formatter.cpp.o
[ 50%] Linking CXX static library libformatter.a
[ 50%] Built target formatter
[ 75%] Building CXX object CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
[100%] Linking CXX static library libformatter_ex.a
[100%] Built target formatter_ex
```
---
```
git add .
git commit -m "Добавлена сборка formatter_ex_lib"
git push origin main
```

## Задание 3
```
cd hello_world_application
touch CMakeLists.txt
cat > CMakeLists.txt << EOF
	> cmake_minimum_required(VERSION 3.5)
	project(hello_world)
	add_executable(hello_world hello_world.cpp)
	target_link_libraries(hello_world PRIVATE formatter_ex)
	target_include_directories(hello_world PRIVATE
	    ${CMAKE_SOURCE_DIR}/formatter_ex_lib
	    ${CMAKE_SOURCE_DIR}/formatter_lib
	)
	> EOF
```
---
```
cd ..
cd solver_application
touch CMakeLists.txt
cat > CMakeLists.txt << EOF
	> cmake_minimum_required(VERSION 3.5)
	project(solver)
	add_executable(solver equation.cpp)
	target_link_libraries(solver PRIVATE formatter_ex solver_lib)
	target_include_directories(solver PRIVATE
	    ${CMAKE_SOURCE_DIR}/formatter_ex_lib
	    ${CMAKE_SOURCE_DIR}/formatter_lib
	    ${CMAKE_SOURCE_DIR}/solver_lib
	)
	> EOF
```
---
```
cd ..
touch CMakeLists.txt
cat > CMakeLists.txt << EOF
	> cmake_minimum_required(VERSION 3.5)
	project(lab03)
	
	add_subdirectory(formatter_lib)
	add_subdirectory(formatter_ex_lib)
	add_subdirectory(solver_lib)
	add_subdirectory(hello_world_application)
	add_subdirectory(solver_application)
	> EOF
```
---
```
cd solver_lib
touch CMakeLists.txt
cat > CMakeLists.txt << EOF
	> cmake_minimum_required(VERSION 3.5)
	project(solver_lib)
	add_library(solver_lib STATIC solver.cpp)
	target_link_libraries(solver_lib PRIVATE formatter_ex)
	target_include_directories(solver_lib PUBLIC
	    ${CMAKE_CURRENT_SOURCE_DIR}
	    ${CMAKE_SOURCE_DIR}/formatter_ex_lib
	    ${CMAKE_SOURCE_DIR}/formatter_lib
	)
	> EOF
```
---

>Тут я забыл выйти из директории, поэтому этот коммит отправит только часть изменений.

```
git add .
git commit -m "Добавлена основная сборка (3 задание)"
git push origin main
```

>Сейчас отправятся оставшиеся файлы.

```
cd ..
git add .
git commit -m "Добавлена основная сборка (3 задангие)"
git push origin main
```

**Карев Георгий | ИУ8-21**
