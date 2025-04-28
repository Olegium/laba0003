У МЕНЯ ЛАБА 3 СЛЕТЕЛА ВОТ ЧТО УДАЛОСЬ ВОССТАНОВИТЬ
В ОБЩИХ ЧЕРТАХ
```bash
cd ~/formatter_lib2
mkdir build && cd build
cmake ~/formatter_lib2/CMakeLists.txt
make

cd ~/formatter_ex
mkdir build && cd build
cmake ~/formatter_ex/CMakeLists.txt
make

cd ~/hello_world
mkdir build && cd build
oleg@NotebookLenovo:~/hello_world2$ cmake CMakeLists.txt
make
```
CMakeLists.txt для formatter_lib
```
  GNU nano 7.2                                                          cmake_minimum_required(VERSION 3.10)
project(formatter)

if(POLICY CMP0077)
    cmake_policy(SET CMP0077 NEW)
endif()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SOURCES
    formatter.cpp
)

set(HEADERS
    formatter.h
)

add_library(formatter STATIC ${SOURCES} ${HEADERS})

target_include_directories(formatter
    PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

if(UNIX)
    target_compile_options(formatter PRIVATE -Wall -Wextra -pedantic)
endif()
[CMakeLists.txt](https://github.com/user-attachments/files/19939857/CMakeLists.txt)

install(TARGETS formatter
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(FILES ${HEADERS}
    DESTINATION include/formatter
)
```
CMakeLists.txt общий
```
  GNU nano 7.2                                                                 cmake_minimum_required(VERSION 3.10)
project(FormatterSolverProject)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Подключаем поддиректории с библиотеками и приложениями
add_subdirectory(formatter_ex)
add_subdirectory(solver_lib)
add_subdirectory(hello_world)
add_subdirectory(solver)
```
CMakeLists.txt для formatter_ex
```
cmake_minimum_required(VERSION 3.10)
project(formatter_ex)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(../formatter_lib formatter)

set(SOURCES
    formatter_ex.cpp
)

set(HEADERS
    formatter_ex.h
)

add_library(formatter_ex STATIC ${SOURCES} ${HEADERS})

target_link_libraries(formatter_ex PRIVATE formatter)

target_include_directories(formatter_ex
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

install(TARGETS formatter_ex
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(FILES ${HEADERS}
    DESTINATION include/formatter_ex
)

```
CMakeLists.txt hello world
```
  GNU nano 7.2                                 CMakeLists.txt                                           # Создаем исполняемый файл hello_world
add_executable(hello_world
    ~/hello_world2/hello_world.cpp
)

# Подключаем библиотеку formatter_ex
```
ВЫВОД 
```
oleg@NotebookLenovo:~/hello_world2$ cmake CMakeLists.txt
CMake Warning (dev) in CMakeLists.txt:
  No project() command is present.  The top-level CMakeLists.txt file must
  contain a literal, direct call to the project() command.  Add a line of
  code such as

    project(ProjectName)

  near the top of the file, but after cmake_minimum_required().

  CMake is pretending there is a "project(Project)" command on the first
  line.
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in CMakeLists.txt:
  cmake_minimum_required() should be called prior to this top-level project()
  call.  Please see the cmake-commands(7) manual for usage documentation of
  both commands.
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/hello_world2
```
CMakeLists.txt solver
```
add_executable(solver
    ~solver/solver.cpp
)
target_link_libraries(solver PRIVATE solver_lib formatter_ex)
```
ВЫВОД SOLVER
```
oleg@NotebookLenovo:~/solver$ cmake CMakeLists.txt
```
```
CMake Warning (dev) in CMakeLists.txt:
  No project() command is present.  The top-level CMakeLists.txt file must
  contain a literal, direct call to the project() command.  Add a line of
  code such as

    project(ProjectName)

  near the top of the file, but after cmake_minimum_required().

  CMake is pretending there is a "project(Project)" command on the first
  line.
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in CMakeLists.txt:
  call.  Please see the cmake-commands(7) manual for usage documentation of
  both commands.
This warning is for project developers.  Use -Wno-dev to suppress it.

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
-- Configuring done (1.6s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/solver
oleg@NotebookLenovo:~/solver$

```
ЛАБА ПОЛНОСТЬЮ
```
oleg@NotebookLenovo:~$ mkdir formatter_lib2
oleg@NotebookLenovo:~$ cd formatter_lib2
oleg@NotebookLenovo:~/formatter_lib2$ nano formatter.h
oleg@NotebookLenovo:~/formatter_lib2$ nano formatter.cpp
oleg@NotebookLenovo:~/formatter_lib2$ nano CMakeLists.txt
oleg@NotebookLenovo:~/formatter_lib2$ cd
oleg@NotebookLenovo:~$ mkdir build
mkdir: cannot create directory ‘build’: File exists
oleg@NotebookLenovo:~$ mkdir build2
oleg@NotebookLenovo:~$ cd build2
oleg@NotebookLenovo:~/build2$ cmake
Usage
```
```

  cmake [options] <path-to-source>
  cmake [options] <path-to-existing-build>
  cmake [options] -S <path-to-source> -B <path-to-build>

Specify a source directory to (re-)generate a build system for it in the
current working directory.  Specify an existing build directory to
re-generate its build system.

Run 'cmake --help' for more information.

```
```
oleg@NotebookLenovo:~/build2$ cd
oleg@NotebookLenovo:~$ cd formatter_lib2
oleg@NotebookLenovo:~/formatter_lib2$ cmake ~/formatter_lib2/CMakeLists.txt
```
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
-- Configuring done (4.2s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/formatter_lib2
```
ТУТ У МЕНЯ СЛОМАЛСЯ ВВОД СТРОКИ И ЗАТЕР ПРЕДЫДУЩИЕ КОМАНДЫ
```
oleg@NotebookLenovo:~/formatter_lib2$ cd
oleg@NotebookLenovo:~$ mkdir formatter_ex
oleg@NotebookLenovo:~$ cd formatter_ex
oleg@NotebookLenovo:$
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ s GNU 13.3.0
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ usr/bin/c++ - skipped
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ done
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ GNU 13.3.0
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ one
oleg@NotebookLenovo:~/formatter_ex$ r/bin/cc - skipped
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ ne
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ d_library):
oleg@NotebookLenovo:~/formatter_ex$ ter_ex
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ iles cannot be regenerated correctly.
oleg@NotebookLenovo:~/formatter_ex$ nano CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex$ nano formatter.cpp
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$
oleg@NotebookLenovo:~/formatter_ex$ nano formatter.cpp
oleg@NotebookLenovo:~/formatter_ex$ nano formatter.h
oleg@NotebookLenovo:~/formatter_ex$ cmake ~/formatter_ex/CMakeLists.txt
-- Using local formatter library
-- Configuring done (0.0s)
oleg@NotebookLenovo:~/formatter_ex$ cd
oleg@NotebookLenovo:~$ mkdir hello_world
oleg@NotebookLenovo:~$ cd hello_world
oleg@NotebookLenovo:~/hello_world$ nano CMakeLists.com
oleg@NotebookLenovo:~/hello_world$ nano CMakeLists.txt
oleg@NotebookLenovo:~/hello_world$ nano main.cpp

oleg@NotebookLenovo:~/hello_world$ nano CMakeLists.txt
oleg@NotebookLenovo:~/hello_world$ nano CMakeLists.txt

oleg@NotebookLenovo:~/hello_world$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/hello_world$ cd
oleg@NotebookLenovo:~$ cd formatter_ex
oleg@NotebookLenovo:~/formatter_ex$ mkdir build && cd build

oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex/build$ cd
oleg@NotebookLenovo:~$ cd formatter_ex

oleg@NotebookLenovo:~/formatter_ex$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex$ mkdir build && cd build
mkdir: cannot create directory ‘build’: File exists
oleg@NotebookLenovo:~/formatter_ex$ mkdir build3 && cd build3

oleg@NotebookLenovo:~/formatter_ex/build3$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build3$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build3$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build3$ nano ~/formatter_lib2/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex/build3$ nano ~/formatter_ex/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex/build3$ cd
oleg@NotebookLenovo:~$ cd formatter_lib2
oleg@NotebookLenovo:~/formatter_lib2$ mkdir build && cd build

oleg@NotebookLenovo:~/formatter_lib2/build$ nano ~/formatter_lib2/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_lib2/build$ rm -rf build/
oleg@NotebookLenovo:~/formatter_lib2/build$ cmake .. -DCMAKE_INSTALL_PREFIX=../install
```
```
-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/formatter_lib2
```
```
oleg@NotebookLenovo:~/formatter_lib2/build$ cd
oleg@NotebookLenovo:~$ cd ~/formatter_ex/

oleg@NotebookLenovo:~/formatter_ex$ cd build

oleg@NotebookLenovo:~/formatter_ex/build$ nano ~/formatter_ex/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex/build$ cd ~/formatter_ex/

oleg@NotebookLenovo:~/formatter_ex$ ls CMakeLists.txt
CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.cpp
oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.h

oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.cpp
oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.h

oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.h
oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.cpp
oleg@NotebookLenovo:~/formatter_ex$ nano ~/formatter_lib2/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex$ nano ~/formatter_lib2/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.cpp
oleg@NotebookLenovo:~/formatter_ex$ nano formatter_ex.txt
oleg@NotebookLenovo:~/formatter_ex$ nano CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex$ nano CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex$ nano ~/formatter_lib2/CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex$ nano ~/formatter_lib2/CMakeLists.txt
oleg@NotebookLenovo:~/formatter_ex$ nano CMakeLists.txt

oleg@NotebookLenovo:~/formatter_ex$ cd
oleg@NotebookLenovo:~$ mkdir solver_lib
oleg@NotebookLenovo:~$ cd solver_lib
oleg@NotebookLenovo:~/solver_lib$ nano CMakeLists.txt
oleg@NotebookLenovo:~/solver_lib$ nano solver.cpp
oleg@NotebookLenovo:~/solver_lib$ nano solver.h

oleg@NotebookLenovo:~/solver_lib$ nano CMakeLists.txt
oleg@NotebookLenovo:~/solver_lib$ nano CMakeLists.txt
oleg@NotebookLenovo:~/solver_lib$ cmake CMakeLists.txt
```
```
CMake Warning (dev) in CMakeLists.txt:
  No project() command is present.  The top-level CMakeLists.txt file must
  contain a literal, direct call to the project() command.  Add a line of
  code such as

    project(ProjectName)

  near the top of the file, but after cmake_minimum_required().

  CMake is pretending there is a "project(Project)" command on the first
  line.
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in CMakeLists.txt:
  cmake_minimum_required() should be called prior to this top-level project()
  call.  Please see the cmake-commands(7) manual for usage documentation of
  both commands.
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in CMakeLists.txt:
  No cmake_minimum_required command is present.  A line of code such as

    cmake_minimum_required(VERSION 3.28)

  should be added at the top of the file.  The version specified may be lower
  if you wish to support older CMake versions for this project.  For more
  information run "cmake --help-policy CMP0000".
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/solver_lib
```
```
oleg@NotebookLenovo:~/solver_lib$ cd
oleg@NotebookLenovo:~$ nano hello_world
oleg@NotebookLenovo:~$ mkdir hello_world
mkdir: cannot create directory ‘hello_world’: File exists
oleg@NotebookLenovo:~$ mkdir hello_world2
oleg@NotebookLenovo:~$ cd hello_world2
oleg@NotebookLenovo:~/hello_world2$ nano hello_world.cpp
oleg@NotebookLenovo:~/hello_world2$ nano CMakeLists.txt

oleg@NotebookLenovo:~/hello_world2$ nano CMakeLists.txt
oleg@NotebookLenovo:~/hello_world2$ nano CMakeLists.txt

oleg@NotebookLenovo:~/hello_world2$ nano ~/solver_lib/CMakeLists.txt
oleg@NotebookLenovo:~/hello_world2$ nano ~/solver_lib/CMakeLists.txt
oleg@NotebookLenovo:~/hello_world2$ nano CMakeLists.txt
oleg@NotebookLenovo:~/hello_world2$ cmake CMakeLists.txt
```
```
CMake Warning (dev) in CMakeLists.txt:
  No project() command is present.  The top-level CMakeLists.txt file must
  contain a literal, direct call to the project() command.  Add a line of
  code such as

    project(ProjectName)

  near the top of the file, but after cmake_minimum_required().

  CMake is pretending there is a "project(Project)" command on the first
  line.
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in CMakeLists.txt:
  cmake_minimum_required() should be called prior to this top-level project()
  call.  Please see the cmake-commands(7) manual for usage documentation of
  both commands.
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/hello_world2
```
```
oleg@NotebookLenovo:~/hello_world2$ cd
oleg@NotebookLenovo:~$ mkdir solver
oleg@NotebookLenovo:~$ cd solver
oleg@NotebookLenovo:~/solver$ nano CMakeLists.txt
oleg@NotebookLenovo:~/solver$ nano CMakeLists.txt
oleg@NotebookLenovo:~/solver$ nano solver.cpp
oleg@NotebookLenovo:~/solver$ cmake CMakeLists.txt
```
```
CMake Warning (dev) in CMakeLists.txt:
  No project() command is present.  The top-level CMakeLists.txt file must
  contain a literal, direct call to the project() command.  Add a line of
  code such as

    project(ProjectName)

  near the top of the file, but after cmake_minimum_required().

  CMake is pretending there is a "project(Project)" command on the first
  line.
This warning is for project developers.  Use -Wno-dev to suppress it.

CMake Warning (dev) in CMakeLists.txt:
  call.  Please see the cmake-commands(7) manual for usage documentation of
  both commands.
This warning is for project developers.  Use -Wno-dev to suppress it.

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
-- Configuring done [CMakeCache.txt](https://github.com/user-attachments/files/19939876/CMakeCache.txt)
([Cmake[CMakeLists.txt](https://github.com/user-attachments/files/19939875/CMakeLists.txt)
Lis[CMakeCache.txt](https://github.com/user-attachments/files/19939872/CMakeCache.txt)
t.txt](https://github.com/user-attachments/files/19939859/CmakeList.txt)
1.6s)
-- Generating done (0.0s)
-- Build files have been written to: /home/oleg/solver
oleg@NotebookLenovo:~/solver$
```
