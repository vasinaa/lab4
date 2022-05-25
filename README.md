## Laboratory work 4 Васина Александра ИУ8-22
[![CI](https://github.com/vasinaa/lab4/actions/workflows/main.yml/badge.svg?branch=master)](https://github.com/vasinaa/lab4/actions/workflows/main.yml)
Вы продолжаете проходить стажировку в "Formatter Inc.".
В прошлый раз ваше задание заключалось в настройке автоматизированной системы CMake.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз. Настройте сборочные процедуры на различных платформах:
используйте GitHub Actions для сборки на операционной системе Linux.

  1.   Создаём директорию [.github/workflows](.github/workflows) и добавляем в неё файл actions.yml:
  
   ```
   
    name: cmake_build
    on:
	  #push:
	  #  branches: [ master ]
	  workflow_dispatch:
	
	jobs:
	  build:
	    runs-on: ubuntu-latest
	    
	    steps:
	    - name: checkout
	      uses: actions/checkout@v3
	    
	    - name: Build a *formatter* library
	      run: |
	        cmake -H. -B_build
	        cmake --build _build
	      shell: bash
	      working-directory: lab_4/formatter_lib
	      
	    - name: Build a *formatter_ex* library
	      run: |
	        cmake -H. -B_build
	        cmake --build _build
	      shell: bash
	      working-directory: lab4/formatter_ex_lib
	      
	    - name: Build a *hello_world* application
	      run: |
	        cmake -H. -B_build
	        cmake --build _build
	      shell: bash
	      working-directory: lab4/hello_world_application
	      
	      
	    - name: Build a *solver* application
	      run: |
	        cmake -H. -B_build
	        cmake --build _build
	      shell: bash
	      working-directory: lab4/solver_application
          ```
          2. [![CI](https://github.com/vasinaa/lab4/actions/workflows/main.yml/badge.svg?branch=master)](https://github.com/vasinaa/lab4/actions/workflows/main.yml)








