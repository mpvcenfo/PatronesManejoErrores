# Excepciones

> Son eventos que ocurren durante la ejecucion de un programa, que interrumpen el flujo normal de las instrucciones del programa.


Al ocurrir errores en los metodos, estos crean un objeto, conocido como Exception object, que contiene la informacion pertinente al error, y este es enviado al sistema en tiempo de ejecucion (runtime system) para que este lo maneje. Este a su vez, busca en la pila de llamadas a metodos, donde se registran los metodos que han sido llamados durante la ejecucion del programa, en busca de un "exception handler" que pueda manejar esta excepcion y continuar con el flujo del programa.
En caso de no encontrar uno, el sistema en tiempo de ejecucion, y por lo tanto el programa, son terminados.

### En Java se reconocen tres distintos tipos de excepciones:

- Las "Checked exceptions", las excepciones que pueden ser previstas, y por lo tanto atrapadas por el programador
- Los "Error", condiciones excepcionales externas a la aplicacion, que no pueden ser previstas, y el sistema no puede recuperarse de ellas.
- Excepciones en tiempo de ejecucion (Runtime Exceptions), que son condiciones internas a la aplicacion y el sistema no puede recuperarse luego de ellas. 
  Normalmente indican errores de programacion, bugs, errores de logica o  poca experiencia con la API.


### El requerimiento "Atrapar o Especificar" (Catch or Specify Requirement) 

En java, honrar este requerimiento significa que el codigo que pueda 'tirar' una excepcion debe estar rodeado por lo siguinte:
- Una declaracion "try", que atrape la excepcion.
- Un metodo que especifique que puede 'tirar' la excepcion. Este debe proveer la clausula "throws".

¿Por que es una buena practica utilizar excepciones?
- Permite separar el codigo de manejo de excepciones del código regular.
- Propagar excepciones a la pila de métodos nos permite crear metodos que se encarguen exclusivamente de esas excepciones, sin tener que preparar cada metodo para este proposito.
- Nos permite separar las excepciones por tipo, dependiendo de las razones por las que estas ocurran, y asi poder especificar y especializar estos objetos para manejar problemas especificos.



## Uso de excepciones.

>Cuando son bien utilizadas pueden mejorar la legibilidad, confiabilidad y mantenibilidad de un programa; cuando no, tienen el efecto opuesto.

### Usar Excepciones unicamente para condiciones excepcionales.
Como su nombre implica, las excepciones son usadas únicamente para casos de excepcionales condiciones, nunca deberían ser usadas para el flujo ordinario de control.

### Usar Excepciones Marcadas para condiciones recuperables y Excepciones de tiempo de ejecución para errores de programación.
Las excepciones marcadas (Checked Exceptions) deben ser manejadas en el catch o propagadas al exterior para ser para ser manipuladas, no es recomendable ignorarlas. Estas excepciones tienen la intención de recuperar en un estado válido en el flujo de control. Debido a que la naturaleza de estas excepciones indica condiciones recuperables, es importante proveer métodos que proporcionen información que puedan ayudar al cliente para regresar dicho estado válido. 	
En el caso de las excepciones no marcadas (Unchecked Exceptions) se trata de excepciones en tiempo de ejecución o errores, estas posiblemente precedan a un comportamiento en el cual sea irrecuperable el estado o flujo de control, por lo que el comportamiento normal sería detener el hilo actual y mostrar un mensaje apropiado de error. La gran mayoría de estos errores tienen que ver con violaciones a las precondiciones (fallas en lo establecido según la especificación de lo que la interfaz(API) espera del cliente) del codigo ejecutando.

> La situación no siempre es blanco o negro.
       
### Evitar el uso innecesario de Excepciones Marcadas.
- Las excepciones marcadas son un excelente feature de Java como lenguaje de programación, obligan al programador a manejar las condiciones excepcionales con la oportunidad de mantener la estabilidad lo cual fomenta la confiabilidad. Son una solución apropiada, pero la prioridad es prevenir su uso con un apropiado manejo del estado de la aplicación.

### Preferir el uso de excepciones comunes.
- La reutilización de código es uno de los atributos que distinguen a los programadores con mayor grado de experticia, las excepciones no se escapan de esta práctica. 
- Reutilizar las excepciones pre-existentes tiene muchos beneficios que hacen que nuestro software sea más fácil de aprender/usar/entender porque tiene establecidas convenciones que les son familiares a los programadores. 
- En el caso de Java las excepciones más utilizadas son: IllegalArgumentException, IllegalStateException, NullPointerException, IndexOutOfBoundsException, ConcurrentModificationException, UnsupportedOperationException.

### Lanzar excepciones apropiadas según la abstracción.
- Un método no debería lanzar una excepción que no tenga una aparente conexión con la tarea que realiza.

### Incluir información de la captura de fallo en el mensaje de detalle.
- Cuando un programa falla debido a una excepción no capturada, el sistema automáticamente imprime el stack trace de la excepción. Este contiene la representación en String de la excepción, el resultado de invocar el método toString. Frecuentemente esta es la única información que tenemos los programadores cuando tenemos que investigar una falla en el sistema, esto quiere decir que si la falla es dificil de replicar será más dificil o imposible tener mayor información. Por esto, dicho mensaje debería contener los valores de todos los parámetros que contribuyeron a la excepción.

### No ignorar las excepciones.
- Parece obvio, pero muy frecuentemente los diseñadores de software declaran un método, lanzan una excepción y la ignoran dejando la sentencia try con el catch vacío. En analogía con ignorar una alarma de incendios, ignorar un bloque catch mata la intención de las excepciones.


#### Referencias
- https://docs.oracle.com/javase/tutorial/essential/exceptions/definition.html
- Joshua Bloch, Effective Java Second Edition.
