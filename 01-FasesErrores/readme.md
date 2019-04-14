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
