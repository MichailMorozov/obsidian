
___###### tags: #cs
###### links: [[Cheatnotes CS]]
___

1.Пишем программу для ассемблера, назовем её ***hello.s***
```nasm
global _start
section .text 
_start:
	mov rax, 1         ; write(
	mov rdi, 1         ; STDOUT_FILENO,
	mov rsi, msg       ; "Hello, world!\n",
	mov rdx, msglen    ; sizeof("Hello, world!\n")
	syscall            ; ); 
	mov rax, 60        ; exit( 
	mov rdi, 0         ; EXIT_SUCCESS
	syscall            ; ); 
section .rodata
 msg: db "Hello, world!", 10 
 msglen: equ $ - msg
```
2. Запускаем команды в терминале
```bash
$ nasm -f elf64 -o hello.s(?)
$ nasm -f elf64 -o hello.o hello.s(asm)
$ ld -o hello hello.o
$ ./hello
>>> Hello, world!
```
3. Создаём файл на языке Си и называем его ***hello.c***. В файле вызываем скомпилированный исполняемый файл от ассемблера
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
	system("./hello"); // Здесь "./hello" - путь к исполняемому файлу nasm
	return 0;
}
```
4.
Запускаем компилятор gcc в терминале
```bash
$ gcc -c hello.c -o hello.o
$ gcc hello.o -o hello
$ ./hello
>>>Hello, world!
```
5. Создаём программу на Python, называем её ***hello.py***
```python
#!/usr/bin/env/python3

#модуль, позволяющий работать с языком Си
import subprocess 

#записываем данные из программы на Си в переменную
command = "./hello" 

# Запуск скомпилированного файла Си и получение вывода 
output = subprocess.check_output(command, shell=True)

# Вывод результата
print(output.decode())
```
6. Запускаем файл ***hello.py*** в терминале
```bash
$ python3 hello.py
>>> Hello, world!
```


##### Библиотека Си
```nasm
section .data
    hello db "Hello, im NASM", 0
  
section .text
    GLOBAL asmFunction
  
asmFunction:
    mov rax, 1
    mov rdi, 1
    mov rsi, hello
    mov rdx, 16
    syscall
  
    ret
```

```bash
nasm -f elf64 -o nasm_functions.o nasm_functions.asm
```

```c
#include <stdio.h>

extern void asmFunction();
  
int main() {
    asmFunction();
  
    printf("\nHi, im C\n");
  
    return 0;
}
```

```bash
gcc -m64 -c -o main.o main.c
gcc -m64 -o program main.o nasm_functions.o
>>> Hello, im NASM!
>>> Hello, im C!
```

***Создание библиотеки***
```bash
gcc -c -fPIC main.c -o main.o
gcc -shared -o mainlib.so main.o
```