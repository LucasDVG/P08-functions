# Práctica 07. Funciones

# Factor de ponderación: 7

### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Sea capaz de resolver problemas sencillos en C++ usando todos los conocimientos adquiridos hasta ahora, 
  y en particular utilizando funciones
* Diseñe, desarrolle y utilice funciones en sus programas haciendo que sus programas sean modulares
* Conozca la herramienta CMake y sepa cómo usarla para construir sus programas ejecutables

### Rúbrica de evaluacion de esta práctica
Se señalan a continuación los aspectos más relevantes (la lista no es exhaustiva) que se tendrán en cuenta a la hora de evaluar esta práctica.
Se comprobará que el alumnado:
* Conoce los conceptos expuestos en el material de referencia de esta práctica.
* Ha realizado todos los ejercicios propuestos
* Es capaz de escribir programas simples en C++ que resuelvan problemas de
  complejidad similar a los que se han propuesto para esta práctica
* Es capaz de escribir un fichero CMakeLists.txt para automatizar el proceso de compilación de sus programas.
* Hace que sus programas se estructuren en torno a diferentes funciones (sean modulares)
* Todos sus programas se estructuran en directorios diferentes para cada "proyecto" haciendo que cada uno de
  ellos contenga un fichero `CMakeLists.txt` con la configuración de despliegue del proyecto.
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
* Que todos los programas que desarrolla, antes de su ejecución imprimen en pantalla un mensaje indicando la 
  finalidad del programa así como la información que precisará del usuario para su correcta ejecución.
* Hace que todos los programas que se presentan para su evaluación cumplan con los estándares definidos en la
[Guía de estilo de Google para C++](https://google.github.io/styleguide/cppguide.html) 
* Utiliza siempre identificadores significativos en su programa (para constantes, variables, etc.) y
  no utiliza nunca identificadores de una única letra, tal vez con la excepción de las variables que utilice para iterar en un bucle.
* Acredita que es capaz de editar ficheros remotos en su VM usando vi
* Ha realizado todos sus ejercicios en la máquina virtual Ubuntu de la asignatura.
* Demuestra que es capaz de ejecutar comandos Linux en su VM

### La herramienta `cmake`
[CMake](https://es.wikipedia.org/wiki/CMake)
es lo que se conoce como un sistema de metaconstrucción. 
No se utiliza para construir (generar, *build* en inglés) el programa ejecutable de una aplicación sino
que produce ficheros de proyecto nativos para la plataforma de destino. 
Por ejemplo, CMake en Linux generará un fichero Makefile; 
en Windows generará una solución para Visual Studio; 
en macOS generará un proyecto para XCode y así sucesivamente. 
Eso es lo que la palabra *meta* indica: CMake construye sistemas de construcción (*builders*). 
La herramienta `make` que ya se ha estudiado, es un sistema de construcción, posiblemente el más común, y así
en *Informática Básica* se utilizará CMake para construir un fichero Makefile con el que se compilará cada uno
de los proyectos (programas) que se desarrollen.

Un proyecto basado en CMake siempre contiene un fichero `CMakeLists.txt`
que describe cómo se estructura el proyecto, la lista de ficheros 
de código fuente que se ha de compilar, lo que CMake debe generar a partir de él y así sucesivamente. 
Se trata en definitiva de un fichero de configuración para la herramienta CMake.
CMake leerá las instrucciones de ese fichero y producirá el resultado deseado. 

Una característica positiva de CMake es el llamado "*out-of-source build*". 
Cualquier fichero requerido para la construcción final, incluyendo los ejecutables, 
será almacenado en un directorio de construcción separado (habitualmente llamado `build/`). 
Esto evita que el directorio de origen que contiene el código fuente se llene de 
ficheros no deseados y hace que sea fácil volver a empezar: sólo hay que eliminar 
el directorio destino de la compilación (directorio `build`) y listo.

CMake es una herramienta muy potente que admite multitud de opciones.
En 
[la documentación](https://cmake.org/cmake/help/latest/index.html) 
de la herramienta se pueden estudiar en profundidad estas opciones, pero para la utilización que perseguimos
realizar en *Informática Básica* bastará con que estudie detenidamente 
[este breve tutorial](https://www.internalpointers.com/post/modern-cmake-beginner-introduction).

En el directorio raíz del repositorio de esta práctica hallará un subdirectorio `fibonacci_sum` con el
siguiente contenido:

```
  fibonacci_sum
  ├── CMakeLists.txt             // Fichero de configuración para CMake
  ├── doc                        // Documentación
  ├── fibonacci.Doxyfile         // Fichero de configuración para Doxygen
  ├── LEE_ME.txt
  └── src                        // Código fuente de la aplicación
      ├── fibonacci_main.cc
      ├── fibonacci_sum.cc
      ├── fibonacci_sum.h
      ├── tools.cc
      └── tools.h
```
Esa estructura de directorios (a la que se añadirán los directorios `build` y -opcionalmente `lib`-)
es habitual en proyectos de desarrollo de software.
En este ejemplo se ha tomado la aplicación `fibonacci_sum` que calcula la suma de términos pares de la serie
de Fibonacci y se ha fragmentado la aplicación en 5 ficheros de código (`*.cc` y `*.h`).
El fichero de configuración `CMakeLists.txt` contiene la configuración que se utiliza para el despliegue de la
aplicación.
Al efecto de ilustrar este proceso, se crea una librería `libtools.a` que se aloja en el directorio `lib`. 
El programa binario (`fibonacci_sum`) se construye enlazando esta librería con el resto del código objeto
producto de la compilación.

Para construir la aplicación, siga los siguientes pasos (que son los habituales):
```
$ cd fibonacci_sum
$ mkdir build
$ cd build
$ cmake ..
$ make
```

El comando `cmake`, usando el fichero de configuración `CMakeLists.txt`, creará en el directorio `build` el fichero `Makefile`
que utiliza el comando `make` para construir la aplicación, cuyo programa binario `fibonacci_sum` se crea
asimismo en el directorio `build`.

Experimente con este fichero de configuración entregado, `CMakeLists.txt` para adaptarlo a cada uno
de sus propios proyectos (ejercicios de la práctica).
No es necesario en principio, que construya librerías propias para sus programas.
La construcción de una librería se ha incluído en este ejemplo con la finalidad de ilustrar ese proceso.
################################################################

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


####################

/**
 * @brief Return true if both parameters are (approximately) equal 
 * @param[in] number1 First number to compare
 * @param[in] number2 Second number to compare
 * @param[in] epsilon Precision for the comparison. It defaults
 * @see https://www.tutorialspoint.com/floating-point-comparison-in-cplusplus
 * @see https://stackoverflow.com/a/17341/12791643
 */
bool AreEqual(const double number1, const double number2, const double epsilon = 1e-7) {
  const bool result = fabs(number1 - number2) <= ((fabs(number1) < fabs(number2) ? fabs(number2) : fabs(number1)) * epsilon);
  // if (result == false) {  // Para depuración
  //   std::cout << std::setprecision(20);
  //   std::cout << "Epsilon:    " << epsilon << std::endl;
  //   std::cout << "Número1:    " << number1 << std::endl;
  //   std::cout << "Número2:    " << number2 << std::endl;
  //   std::cout << "Difference: " << fabs(number1 - number2) << std::endl;
  // }
  return result;
}

####################




1. Escriba un programa que lea un número natural e imprima como salida la suma de los dígitos del número en cuestión. 
```
Public test cases
Input           Output
2022              6
1492             16
0                 0
```

2. Desarrolle un programa que imprima los N primeros términos de la 
