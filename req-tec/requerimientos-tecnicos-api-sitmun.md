# Requerimientos técnicos API SITMUN

**Este documento está deprecated**. La versión más actualizada de esta documentación está en <https://sitmun.github.io>.

----


## Arquitectura del Cliente de SITMUN 3

### Contexto del sistema

El diagrama de contexto del sistema muestra el **Cliente de SITMUN 3** y cómo encaja en el mundo en términos de las personas que lo utilizan (los **Usuarios**) y los otros sistemas de software con los que interactúa (**Servicios web de información territorial** y **Bases de datos de información territorial**).

Los **usuarios** utilizan el **cliente de SITMUN 3** para visualizar y modificar información territorial. El **cliente de SITMUN 3** utiliza los **Servicios web de información territorial** y **Bases de datos de información territorial** para acceder a información territorial alfanumérica, vectorial y raster. El código de color en el diagrama indica los sistemas de software que ya existen (las cajas grises) y los que se van a construir (azules).

![Contexto del Cliente de SITMUN 3](img/contexto-sistema-cliente-sitmun-3.svg)

## Contexto en detalle

El diagrama de contenedor del **Cliente de SITMUN 3** muestra los contenedores (aplicaciones JavaScript, proxy, servicios, almacenamiento de datos, microservicios, etc.) que componen este sistema de software. El contenedor del **Cliente de SITMUN 3** (el cuadro punteado) consta de seis contenedores:

- **Visor**: Es aplicación **Angular** de una sola página que se ejecuta en el navegador web del cliente, proporcionado acceso a información territorial a un **Usuario** para un **Territorio** y una **Aplicación** seleccionada. El usuario se autentica en el **Visor** usando la **API de autenticación**. Con la **API de configuración y autorización** accede a la configuración que debe usar para un **Usuario**/**Territorio**/**Aplicación**. La **API de configuración y autorización** también le da acceso a información adicional de configuración como el listado de **Territorios** y el listado de **Aplicaciones**. La configuración puede contener URI que apuntan al **Proxy**.

- **Servidor estático**: Es un sistema Java/Spring Boot que simplemente muestra el contenido estático (HTML, CSS y JavaScript) que constituye el **Visor**.

- **API de autenticación**: Una API JSON/HTTPS proporcionada por una aplicación Java/Spring Boot que permite autenticar a un **Usuario**. Este servicio le devuelve un **token JWT** que identifica al usuario.

- **API de configuración y autorización**: Una API JSON/HTTPS proporcionada por una aplicación Java/Spring Boot que permite obtener una **Configuración** para el visor dado un **Token de usuario**, el identificador de un **Territorio** y el identificador de una **Aplicación**. También da acceso a información adicional de configuración como el listado de **Territorios** y el listado de **Aplicaciones**. Si la petición no tiene **token JWT** se asume que es el usuario público.

- **PROXY Middleware**: Una API HTTPS del lado del servidor que actúa como proxy a **Servicios web de información territorial restringidos** y **Bases de datos de información territorial**. Si las peticiones contienen un **token JWT** este se utiliza para validar la petición y obtener información adicional contra la **API de configuración**. El **Territorio** y la **Aplicación** se pasa por parámetros en la petición.

- **Base de datos**: Una base de datos relacional que contiene información sobre **Usuarios**, **Territorios**, **Aplicaciones** y demás elementos de configuración del modelo de SITMUN 3.

> **NOTA**: La **API de autenticación** y la **API de configuración y autorización** forman parte del componente denominado como **Backend**.

![Contexto del Cliente de SITMUN 3](img/contenedor-cliente-sitmun-3.svg)

## Diagramas de secuencia

TBD.

- [ ] Carga del visor e inicialización
- [ ] Configuración personalizada para un usuario en un territorio y aplicación
- [ ] Uso del proxy middleware
 
