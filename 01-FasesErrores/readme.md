# 01-FasesErrores

1. Escribir hello2.c, que es una variante de hello.c:

#include <stdio.h>
int/*medio*/main(void){
int i=42;
 prontf("La respuesta es %d\n");
 
2. Preprocesar hello2.c, no compilar, y generar hello2.i. Analizar su
contenido.

3. Escribir hello3.c, una nueva variante:

int printf(const char *s, ...);
int main(void){
int i=42;
 prontf("La respuesta es %d\n");
 
4. Investigar la semántica de la primera línea.

5. Preprocesar hello3.c, no compilar, y generar hello3.i. Buscar diferencias
entre hello3.c y hello3.i.

6. Compilar el resultado y generar hello3.s, no ensamblar.

7. Corregir en el nuevo archivo hello4.c y empezar de nuevo, generar
hello4.s, no ensamblar.

8. Investigar hello4.s.

9. Ensamblar hello4.s en hello4.o, no vincular.

10.Vincular hello4.o con la biblioteca estándar y generar el ejecutable.

11.Corregir en hello5.c y generar el ejecutable.

12.Ejecutar y analizar el resultado.

13.Corregir en hello6.c y empezar de nuevo.

14.Escribir hello7.c, una nueva variante:

int main(void){
int i=42;
 printf("La respuesta es %d\n", i);
}

15.Explicar porqué funciona.

paul99tapia  
1679363  
Tapia Puña  
Paul Sergio  

-----------------------------------------------------------------------------

P.2

gcc -std=c11 -E hello2.c > hello2.i
El comando gcc con la opcion -E genera el codigo preprocesado y lo envia a la salida estandar, por eso debemos redirigir la salida al archivo hello2.i  
Los comentarios fueron remplazados por blancos y se ven todas las declaraciones del header file que se incluyo (stdio.h)  

P.4

La sintaxis de la primera linea indica la declaración una función que puede recibir más argumentos de cualquier tipo.  
En la funcion en la que se lo utiliza debe de haber al menos un parametro definido.

P.5

gcc -std=c11 -E hello3.c > hello3.i

Diferencias:

Se incluyeron las lineas  
`# 1 "hello3.c"`  
`# 1 "<built-in>"`  
`# 1 "<command-line>"`  
`# 1 "hello3.c"`  

Estos son linemarkers. En este caso, el 1 indica el inicio del archivo.

P.6

gcc -std=c11 -S hello3.i

(Da el siguiente error)

hello3.c: In function 'main':  
hello3.c:5:5: warning: implicit declaration of function 'prontf'; did you mean 'printf'? [-Wimplicit-function-declaration]  
     prontf("La respuesta es %d\n");  
     ^~~~~~  
     printf  
hello3.c:5:5: error: expected declaration or statement at end of input  

P.7

gcc -std=c11 -E hello4.c > hello4.i

(Genera el hello4.i)

gcc -std=c11 -S hello4.i

(Da el siguiente warning)

hello4.c: In function 'main':  
hello4.c:5:5: warning: implicit declaration of function 'prontf'; did you mean 'printf'? [-Wimplicit-function-declaration]  
     prontf("La respuesta es %d\n");  
     ^~~~~~  
     printf  

(Genera el hello4.s)

P.8 

El hello4.s contiene codigo en lenguaje Assembler.

P.9

gcc -std=c11 -c hello4.s

(Genera el hello4.o)

P.10

gcc -std=c11 hello4.o -lmsvcrt -o hello4.exe  
c:/mingw/bin/../lib/gcc/mingw32/8.2.0/../../../../mingw32/bin/ld.exe: hello4.o:hello4.c:(.text+0x1e): undefined reference to `prontf'  
collect2.exe: error: ld returned 1 exit status  

P.11

gcc -std=c11 hello5.c -o hello5.exe

(Se genero hello5.exe)

P.12

hello5

(Al ejecutarlo)
 
La respuesta es 4200640

Esto es debido a que no se pasó el argumento correspondiente a printf.

P.13

gcc -std=c11 -E hello6.c > hello6.i  
gcc -std=c11 -S hello6.i  
gcc -std=c11 -c hello6.s  
gcc -std=c11 hello6.c -o hello6.exe  
hello6  

(Al ejecutarlo:)

La respuesta es 42

P.14

gcc -std=c11 hello7.c -o hello7.exe


hello7.c: In function 'main':  
hello7.c:3:5: warning: implicit declaration of function 'printf' [-Wimplicit-function-declaration]  
     printf("La respuesta es %d\n", i);  
     ^~~~~~  
hello7.c:3:5: warning: incompatible implicit declaration of built-in function 'printf'  
hello7.c:3:5: note: include '<stdio.h>' or provide a declaration of 'printf'  
hello7.c:1:1:  
+#include <stdio.h>  
 int main(void){  
hello7.c:3:5:  
     printf("La respuesta es %d\n", i);  
     ^~~~~~  

hello7  
La respuesta es 42  

Esto funciona porque la libreria estandar de C (en la cual printf esta incluida) es likeada por default
