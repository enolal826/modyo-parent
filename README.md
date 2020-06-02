### SOBRE EL BACK
He seguido un enfoque DDD para la distribución del código. Así mismo, he utilizado un concepto de arquitectura hexagonal, los "use cases", creando
una clase para cada una de las acciones de la aplicaciones (este este caso, únicamente "listar Pokemon").

- application: lo relativo a los use cases, teniendo una "request" y una "response" para cada uno de ellos
- domain: el "core" de nuestra aplicación. Únicamente definimos una entidad para nuestro modelo, "Pokemon" y unos interfaces
que nos permitirán comunicarnos con sus implementaciones en la capa de infrastructura.
- infrastructure: todo lo relativo a lo externo de nuestra aplicación (peticiones entrantes y salientes HTTP)

Aclaraciones:

- Los repositorios son abstracciones para la obtención de nuestras entidades. Nos proveen de las entidades construidas 
- Por falta de tiempo, he hecho muy pocos tests unitarios (también estaría bien hacer alguno de integración falseando la respuesta de la API).
- En los test unitarios, estoy creando los objetos de la factory directamente desde el JSON que la API devuelve por simplicidad
- Estoy utilizando la abstracción de Spring para caché. En este caso, se está cacheando el método "list" del repositorio utilizando
una tabla hash (mapa en Java) en memoria (por defecto)


### SOBRE EL FRONT
Una aplicación muy básica utilizando React y Redux que hace una petición para obtener la lista de Pokemon

### DEPLOYMENT
Utilizando Google Cloud, una forma de proceder bastante simple, accediendo a la máquina y subiendo los siguientes archivos mediante
la CLI de Google:
- aplicación React: tras obtener la versión de "producción" (JavaScript pre-compilado por cuestiones de rendimiento), simplemente servimos los archivos
estáticos. NPM tiene un paquete "serve" bastante útil para esto (es simplemente un servidor Node utilizando Express).
- aplicación Java: generamos el archivo JAR y previa instalación de la JVM, lo ejecutamos.
