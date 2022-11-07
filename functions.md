# Práctica 07. Funciones

# Factor de ponderación: 7

### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Sea capaz de resolver problemas sencillos en C++ usando todos los conocimientos adquiridos hasta ahora, 
y en particular haciendo uso de sentencias iterativas
* Comience a utilizar funciones en sus programas y modularice sus programas en diferentes funciones
* Conozca los fundamentos de la documentación de código
* Conozca la herramienta Doxygen, las etiquetas definidas en JSDoc y sepa cómo utilizarlas para documentar su
código

### Rúbrica de evaluacion de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva) que se tendrán en cuenta a la hora de evaluar esta práctica.
Se comprobará que el alumnado:
* Es capaz de escribir programas simples en C++ que resuelvan problemas de
  complejidad similar a los que se han propuesto para esta práctica
* Hace que sus programas se estructuren en torno a diferentes funciones (sean modulares)
* Utiliza en todos sus programas comentarios adecuados en el formato requerido por
[Doxygen](https://www.doxygen.nl/index.html)
* Ha automatizado la compilación de sus programas usando un fichero `Makefile`
  para cada uno de los programas que desarrolle 
* Acredita que todas las prácticas realizadas hasta la fecha se encuentran alojadas en repositorios
  privados de [GitHub](https://github.com/).
* Acredita que es capaz de subir programas a la plataforma 
[Jutge](https://jutge.org/)
para su evaluación
* Ha incluido un comentario prólogo en todos los ficheros (`*.cc`, `*.h`) de sus ejercicios
* Hace que todos los programas de sus prácticas se ajusten a la
[Guía de estilo de Google para C++](https://google.github.io/styleguide/cppguide.html) 
* Acredita que es capaz de editar ficheros remotos en su VM usando vi
* Demuestra que es capaz de ejecutar comandos Linux en su VM

### Documentación de código 

* Escriba todos los programas de modo que estén estructurados en funciones.
* Documente cada función de su programa de modo
que cada una contenga comentarios en las líneas anteriores a su definición en la que se indique
	1. Una breve descripción de la finalidad de la función
	2. Para cada uno de sus parámetros se ha de indicar su significado
	3. Si la función no es void, indicar el significado asimismo de su resultado
Así el 
[bloque de comentarios](https://jsdoc.app/tags-description.html)
que debe preceder a cualquier función (o método) debiera tener una apariencia similar a esta:
```
/**
 * Sum numbers in a vector
 *
 * @param values Container whose values are summed
 * @return sum of `values`, or 0.0 if `values` is empty
 */
double SumValues(const std::vector<double>& values) {
  ...
}
```

### Material de estudio complementario
Estudie todo lo que se indica en el epígrafe 
[Comments](https://google.github.io/styleguide/cppguide.html#Comments) 
de la Guía de Estilo de Google y ponga en práctica todo lo que en ella se propone, usando el formato Doxygen y
etiquetas JSDoc para todos los comentarios de su código fuente.

Estudie del
[tutorial de referencia](https://www.learncpp.com/)
en la asignatura los siguientes apartados:
* [Comments](https://www.learncpp.com/cpp-tutorial/comments/)
* El capítulo 2
[Basics: Functions and Files](https://www.learncpp.com/cpp-tutorial/introduction-to-functions/)
(completo)
* [Command line arguments](https://www.learncpp.com/cpp-tutorial/command-line-arguments/)

### Diseño de los programas
Recuerde las que se han estudiado como *Buenas Prácticas* a la hora de diseñar sus funciones:
* El código deberá organizarse en diferentes funciones 
* Cada función deberá realizar una única tarea y hacerlo correctamente 
* El identificador de una función debe reflejar claramente lo que la función hace 

Tal como se indica en 
[How to design your first programs](https://www.learncpp.com/cpp-tutorial/how-to-design-your-first-programs/)
su código debiera estar organizado en torno a funciones que se invocan desde la función *main()*.
Así la apariencia habitual de la función principal de cualquier programa debiera ser algo similar a:
``` .cpp
int main(int argc, char* argv[]) {
  PrintProgramPurpose();
  if (!CheckCorrectParameters(argc, argv, 3)) {
    return 1;
  }
  GetUserInput();
  GetMathematicalOperation();
  GetUserInput();
  CalculateResult();
  PrintResult();

  return 0;
}
```
en el sentido de que la función *main()* es una mera *orquestadora* de las funciones que componen el programa.
*main()* pasa a esas funciones los parámetros necesarios para su funcionamiento y las diferentes funciones
devuelven a *main()* el valor que calculan (si fuera el caso).

Incluya en todos sus programas sendas funciones cuya declaración sería:
```
void PrintProgramPurpose();
bool CheckCorrectParameters(const int argc, char *argv[], const int kCorrectNumber);
```
La primera de ella se invocará al comienzo de la ejecución para imprimir un mensaje explicativo de
la finalidad del programa en cuestión.
La función *CheckCorrectParameters()* devolverá `true` si al programa se le han pasado el número adecuado de
parámetros por línea de comandos (3 en el ejemplo anterior) y `false` en caso contrario.
Estude el programa 
[check-correct-parameters.cc](https://github.com/IB-2022-2023/IB-class-code-examples/blob/master/Functions/check-correct-parameters.cc)
de los ejemplos de código de las clases de teoría que ilustra el uso de estas dos funciones.

### Ejercicios
* Al realizar los ejercicios cree dentro de su repositorio de esta práctica un directorio diferente
para cada uno de los ejercicios.
Asigne a cada uno de esos directorios nombres significativos. 
* Automatice la compilación del programa correspondiente a cada ejercicio con un fichero `Makefile`
independiente para cada programa e inclúyalo en el correspondiente directorio.

1. Escriba un programa que lea un número natural e imprima como salida la suma de los dígitos del número en cuestión. 
```
Public test cases
Input           Output
2022              6
1492             16
0                 0
```

2. Desarrolle un programa que imprima los N primeros términos de la 
