# Desarrollo-de-Software
En este repositorio voy a plasmar todo lo aprendido en la materia Desarrollo de Software de la Universidad Tecnológica Nacional.

Repaso JS
Se trata de un lenguaje común, que se ejecuta en dos entornos diferentes (en el servidor, mediante node, y el cliente, mediante cualquiera de los motores provistos por tu navegador preferido) y ofrece varias herramientas que hacen de puente entre estos.
Mencionamos algunas de sus herramientas (node, npm / yarn) y hacemos una brevísima demo de node vs el navegador. Es que JavaScript soporta múltiples entornos de ejecución (runtime environment):

servidor: node (intérprete) + npm (gestor de paquetes / dependencias) + otras cosas
cliente: navegadores (browsers)
- opera
- brave
- chrome: v8
- firefox: spidermonkey

Arquitectura Web
En la arquitectura Web, programar en el servidor es obligatorio, hacerlo en el cliente no. De hecho, hay diferentes estilos de clientes:

cliente liviano: solo tienen programación (significativa) en el servidor. En DDSi se trabajará esta arquitectura.
cliente pesado: tienen (y ejecutan) cantidades de código significativas tanto en el cliente (tipicamente navegador) como en el servidor. En DDSo utilizaremos esta arquitectura.
Tecnologías típicas: Angular, React, Vue

Además, los clientes pesados darán origen a una división (técnica, tecnológica, de equipos de trabajo) frecuente en el mundo Web: Front-end y Back-end (no es el mismo sentido que en otras materias): la primera es el nombre que se le da a la programación del lado del cliente, mientras que el segundo se le da a la programación del lado del servidor.

**¿Toda aplicación Web requiere JavaScript?**

El servidor se puede programar en CUALQUIER lenguaje.
El cliente sí requiere JS, porque es el único lenguaje soportado en la práctica en los navegadores.
Peeeeero, no toda aplicación requiere programar en el cliente (puede ser cliente liviano!)
Igual, aún en aplicaciones cliente liviano podría haber alguna porción pequeña de JS


**¿Qué diferencias habrá en el estilo de programación / las tecnologías / lo que se programa?**

Lenguaje: en el Front sí o sí tenemos que usar JS. En el servidor, no es necesario
Versiones: puede haber diferencias en las versiones y tabla de compatibilidad del entorno de JS entre navegadores. Por lo tanto en el Front, tenemos que considerar que nuestro código podría no funcionar igual en todos los navegadores.
Capacidad de cómputo/memoria: la programación del lado del cliente podría ejecutarse en entornos con menor capacidad de cómputo que el servidor (ejemplo, un celular)
Seguridad: lo que se ejecuta en el servidor ocurre dentro de un entorno controlado, bajo nuestra supervisión, pero lo que se ejecuta en el cliente no: el cliente podría estar ejecutando un código modificado que NO sea el que diseñamos
Conexión: el cliente podría tener un nivel de conectividad limitado (por ejemplo 3g)
El servidor está bajo presión de cómputo: tiene que ser capaz de escalar su capacidad de cómputo a medida que tiene mas clientes.
El código del servidor suele girar en torno al dominio, mientras que el código del cliente gira en torno a los elementos visuales y sus eventos e interacciones con quien usa la aplicación.


**MODELADO DE CAPAS**
En particular, en el contexto de la programación del lado del servidor (ya sea porque estamos en una arquitectura web de cliente liviano o porque estamos trabajando en backend de una arquitectura web cliente pesado), hay varias formas de responder a esto:

- Modelo de capas !!!
- Modelo MVC Web
- Modelo VIP (Interactor)
- Modelos orientados a objetos sin una arquitectura particular
- Modelos orientados a objetos organizados únicamente en torno a incumbencias de presentación, dominio y persistencia. Muchas veces esta idea y el modelo de capas convergen, pero acá la organización entre componentes no es tan rígida.

1. Capa de enrutamiento (nivel superior), en la que encontraremos rutas
2. Capa de controladores, en la que encontraremos controladores
3. Capa de servicios, en la que encontraremos servicios
4. Capa de persistencia (nivel inferior), en la que encontraremos modelos y repositorios (también llamados managers o DAOs)


**Biblioteca vs. Framework**
**La necesidad de reutilizar**
Para entender un poco de qué estamos hablando, remontémonos a los orígenes del desarrollo de software: 

Originalmente, toda funcionalidad que fuera necesaria para una aplicación, había de ser implementada a mano por el equipo encargado de la construcción del producto en cuestión. Por ejemplo, si se necesitaba conocer la longitud de un string, podía implementarse una función del estilo:

```javascript
int string_length(char* unString){
	int i = 0, longitud = 0;
	while(unString[i] != '\0'){
		longitud++, i++;
	}
	return longitud;
}
```
Y luego utilizarla:

 ```javascript
    char* palabra = “Una palabra”;
    printf("La palabra es %s y tiene %d caracteres", palabra,string_length(palabra));
 ```


Y reutilizarse múltiples veces dentro del proyecto, evitando así la necesidad de desarrollar funcionalidad ya existente, evitando repetir lógica y generando una abstracción nueva.

Sin embargo, eventualmente el proyecto finalizaría, uno nuevo arrancaría y las probabilidades indican que seguramente la función string_length sería necesaria nuevamente y debería ser desarrollada una vez más, prácticamente replicando el código de otro proyecto anterior.

Fue entonces que surgieron las bibliotecas, como forma de compartir funciones y estructuras ya desarrolladas entre varios proyectos.

**Las bibliotecas resuelven un problema de reutilización de lógica asociada a abstracciones, representada e implementada a través de código.**

Los frameworks condicionan fuertemente el diseño de un componente de software. Éstos suelen manejar el flujo de ejecución del programa e invertir el control, siendo ellos quienes deciden cuándo llamar al código cliente. (Quien programa jamás define el método main, sino que es el framework el que lo define y eventualmente llama al código cliente, como ejecutarPrograma)

Es común que los frameworks definan aspectos tales como el orden de ejecución de ciertas tareas, la forma en la que se van a escribir ciertas operaciones (DSLs) o incluso las estructuras de directorios que se van a utilizar para guardar el código fuente.

También suele ser común que definan clases abstractas que el código cliente extenderá y métodos abstractos que son los que quien programa ha de implementar con el comportamiento propio de la aplicación.  (El framework define la clase abstracta AplicaciónConTests que el código cliente extiende completando definiciones de métodos como limpiarTodo y prepararTest)


Una biblioteca y un framework tienen en común que:

Ambos definen abstracciones y lógica propias
Ambos implementan dichas abstracciones y lógica en código reutilizable.


Sin embargo, se diferencian en que:


Es responsabilidad de quien programa decidir cómo y cuándo utilizar los componentes - Bibliotecas
Este define la forma en la que se estructurará el código y quien programa se ve obligado a seguir esa forma - Frameworks
Las decisiones de diseño que se toman suelen tener bajo impacto en el diseño del código que la utiliza - Bibliotecas
Las decisiones de diseño que se toman pueden condicionar fuertemente el diseño del código cliente - Frameworks
Utilizan control directo: El código cliente  llama funciones de la biblioteca e instancia las estructuras que la biblioteca pueda definir. - Bibliotecas
Utilizan control inverso: Es el framework el que llama funciones abstractas que el código cliente define en concreto. - Frameworks


**Introducción a MVC Web con Express**
**1.1 MVC**
Es un acrónimo de Model-View-Controller (Modelo, Vista, Controlador en inglés), es el nombre con el que se conoce a una familia de arquitecturas de presentación. Éstas se caracterizan por una separación clara entre los componentes encargados de implementar la lógica de negocio (modelo) y los de interacción y presentación de información (vista), mediados por un conjunto de componentes intermedios (controlador).

Sin embargo, dependiendo de la tecnología de presentación y comunicación subyacente (escritorio, Web, consolas, etc) y el actor con quien interactúa el sistema (personas, navegadores, otros sistemas, etc) las responsabilidades y canales de comunicación entre dichos componentes varían ligeramente. Por ejemplo, en el mundo Web nos encontramos con las limitaciones de la arquitectura cliente-servidor, en la que:
- la lógica de presentación se encuentra distribuida entre el cliente y el servidor;
- la lógica de modelo se encuentra en el servidor;
- y el cliente no puede recibir mensajes desde el servidor sin que haya una petición previa. 

Por ese motivo, en la estructura de un MVC Web tradicional, las comunicaciones vista-controlador y vista-modelo cambian: 

**1.3 Tecnologías del lado del servidor y del lado del cliente**
Las tecnologías del lado del servidor (server-side, en inglés) son aquellas que, en el contexto de una arquitectura Web, se ejecutan en el servidor. Contrastan con las tecnologías del lado del cliente (client-side), que se ejecutan casi exclusivamente en navegadores. Por consiguiente, las tecnologías del lado del servidor presentan mayores grados de libertad, dado que no están sometidas al (necesario) alto nivel de estandarización que los navegadores y los comités como W3C imponen. 

Así, es frecuente encontrar una gran dama de opciones de lenguajes, bibliotecas, herramientas y frameworks, mientras que sus contrapartidas del lado del cliente necesitan, a la corta o a la larga, traducirse a las tecnologías mencionadas en el apartado anterior. 

**1.4 Express**
Y ahora sí, ¡llegamos a Express! Se trata de un framework liviano para node.js el cual permite la programación Web del lado del servidor en general, y la comunicación HTTP. Puede ser utilizado tanto para construir APIs HTTP/REST cómo para generar vistas HTML dinámicas, por lo que vamos a encontrarlo por igual en:
arquitecturas de cliente liviano: aquellas en que la mayor parte de nuestra lógica de presentación se encontrará en el servidor) 
arquitecturas de cliente pesado: aquellas en que la lógica de presentación se encontrará fundamentalmente en el cliente y utilizaremos una mayor cantidad de tecnologías de ese lado.
Express se caracteriza por ser minimalista, es decir, requerir para su uso una cantidad mínima de conceptos comparado contra otras tecnologías. 
Express por sí mismo no fuerza conceptos de MVC, pero si organizamos adecuadamente nuestro código, podremos implementar, finalmente, una arquitectura MVC Web con Express.




**ORQUESTACIÓN DE CASOS DE USO**
class Huesped
crearReserva()
buscarAlojamientos()
MAL

Buscamos lo siguiente
class Huesped
class Reserva
class Alojamiento{
	estaDisponibkeEntre(rango)
	agregarReserva(reserva)
}

Tendremos otra clase que orqueste

**ARQUITECTURA POR CAPAS**
Controller -> Service -> Repository
Cada capa tiene un rol único


(Ejemplo de take away)

Capa de controladores(recepcionista)
Recibe las solicitudes externas (web, API, etc), las traduce al lenguaje de dominio, las delega en las capas inferiores para que las resuelvan, y devuelve la respuesta esperada..
Esta capa expone los endpoints.
Recibe los inputs al lenguaje de dominio, y luego delega a la capa de Services.
Es responsable de manejar excepciones, códigos HTTP, validaciones superficiales (que los tipos de datos que recibe el endpoint sean correctos)
No debe haber lógica de negocio.
Un buen controlador es delegador y explícito.

Capa de Servicios (barista)
Orquesta ejecución de una operación de negocio.
LLama a los objetos de dominio, repositorios y otros objetos de utilidad.
Separa el "como se hace algo"(dominio) del "cuando y en qué orden" se hace (servicio)

Capa de Repositorios
Encapsula el acceso al medio persistente, que puede ser: memoria, archivos, bases de datos, etc.
Traduce las entidades del dominio a un formato persistible y viceversa.

Capa de dominio
Lógica de negocio pura. Reglas, validaciones, entidades y objetos de valor.
Existe una separación clara de responsabilidades entre las distintas clases.
Las clases son autocontenidad y validadas.

Vamos a la práctica.

**Paginación**
Que pasa si una API tiene miles de registros?
No se puede mandar todos en una sola consulta
Es lento
Ocupa mucho ancho de banda
Cuesta renderizar
Mala experiencia de usuario

La paginación es una técnica para dividir una gran cantidad de datos en una catidad limitada.
Genera mejor rendimiento (menos datos por request)
Menor consumo de red
Navegación más cómoda para el usuario

Request
GET /productos ? page = 2 & limit = 10;

Cáclulo en el servidor
const offset = (page - 1) * limit
const paginado = lista.slice(offset, pffset + limit)

Respuesta
{
	"page" : 2,
	"per_page": 10,
	"total" : 50,
	...
}

**Cualidades**
Separar en capas reduce la complejidad
Acoplamiento bajo -> cada capa depende de la capa adyacente
Cohesión alta -> cada capa tiene un propósito claro
Simplicidad (KISS/YAGNI/DRY) -> responsabilidades claras evitan duplicación y sobre ingeniería
KISS: Keep it simple, stupid
YAGNI: You arent gonna need it
DRY: Dont repeat yourself

Robustez -> entidades y reglas aisladas, protegias del mal uso
Flexibilidad:
-> cambiar BD, servicio externo o UI sin tocar el núcleo del negocio
-> modificar características con poco esfuerzo
-> agregar nuevas características con poco impacto
