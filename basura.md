### Objetivos
Los objetivos de esta práctica son que el alumnado:
* Conozca la herramienta CMake y sepa usarla para construir sus programas ejecutables


### Rúbrica de evaluacion de esta práctica
Todo el código que se presente a evaluación ha de cumplir los estándares definidos en la 
[Guía de Estilo de Google para C++](https://google.github.io/styleguide/cppguide.html).

Se señalan a continuación otros aspectos (la lista no es exhaustiva) que se tendrán en cuenta a la hora de evaluar esta práctica.
El alumnado ha de acreditar que:

* Conoce los conceptos expuestos en el material de referencia de esta práctica.
* Ha realizado todos los ejercicios propuestos, así como que es capaz de desarrollar otros de complejidad similar.
* Es capaz de escribir un fichero CMakeLists.txt para automatizar el proceso de compilación de sus programas.
* Todos sus programas se estructuran en directorios diferentes para cada "proyecto" haciendo que cada uno de
  ellos contenga un fichero `CMakeLists.txt` con la configuración de despliegue del proyecto.
* Todas las prácticas realizadas hasta la fecha se encuentran alojadas en repositorios de
[GitHub](https://github.com/).
* Los programas deben contener comentarios adecuados en el formato requerido por 
  [Doxygen](https://www.doxygen.nl/index.html).
* Sus programas se compilan correctamente utilizando la utilidad `make` y un fichero `Makefile`.
* Todos los identificadores que utilice en su programa (constantes, variables, etc.) deberán ser
  siempre significativos. No utilice nunca identificadores de una única letra, tal vez con la excepción de las variables que utilice para iterar en un bucle.
* Sabe editar y modificar sus programas usando VSC con una conexión remota a la máquina virtual Linux de la asignatura.
* Ha realizado todos sus ejercicios en la máquina virtual Ubuntu de la asignatura.
* Todos los programas que desarrolla, antes de su ejecución imprimen en pantalla un mensaje indicando la finalidad del programa así como la información que precisará del usuario para su correcta ejecución.
* Todos sus programas contienen comentarios adecuados en el formato requerido por Doxygen.
* Todos los ficheros de código del proyecto correspondiente a esta práctica están alojados en un repositorio
  de GitHub
* Conoce las técnicas básicas de depuración usando VSC y su depurador integrado.

### La herramienta `cmake`
[CMake](https://es.wikipedia.org/wiki/CMake)
es lo que se conoce como un sistema de metaconstrucción. 
No se utiliza para construir (generar, *build* en inglés) el programa ejecutable de una aplicación sino
que produce ficheros de proyecto nativos para la plataforma de destino. 
Por ejemplo, CMake en Windows generará una solución para Visual Studio; 
en Linux generará un fichero Makefile; 
en macOS generará un proyecto para XCode y así sucesivamente. 
Eso es lo que la palabra *meta* indica: CMake construye sistemas de construcción 
(*builders*). 
La herramienta `make` es un sistema de construcción, posiblemente el más común.

Un proyecto basado en CMake siempre contiene un fichero `CMakeLists.txt`
que describe cómo se estructura el proyecto, la lista de ficheros 
de código fuente que se ha de compilar, lo que CMake debe generar a partir de él y así sucesivamente. 
Se trata en definitiva de un fichero de configuración para la herramienta CMake.
CMake leerá las instrucciones de ese fichero y producirá el resultado deseado. 

Una característica positiva de CMake es el llamado "out-of-source build". 
Cualquier fichero requerido para la construcción final, incluyendo los ejecutables, 
será almacenado en un directorio de construcción separado (habitualmente llamado `build/`). 
Esto evita que el directorio de origen que contiene el código fuente se llene de 
ficheros no deseados y hace que sea fácil volver a empezar: sólo hay que eliminar 
el directorio destino de la compilación (directorio `build`) y listo.

CMake es una herramienta muy potente que admite multitud de opciones.
En 
[la documentación](https://cmake.org/cmake/help/latest/index.html) 
de la herramienta se pueden estudiar en profundidad estas opciones, pero para la utilización que perseguimos
realizar en esta asignatura bastará con que estudie detenidamente 
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
