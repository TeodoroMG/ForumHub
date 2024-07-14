
<img src="https://img.shields.io/badge/STATUS-FINALIZADO-green" display="inline" >


# Forum Hub

Forum Hub es una aplicación web de foro desarrollada con Spring Boot, diseñada para gestionar tópicos de discusión. Esta aplicación incluye funcionalidades CRUD (Crear, Leer, Actualizar, Eliminar) y utiliza JWT (JSON Web Token) para autenticación y autorización, asegurando así un acceso seguro a los recursos.

## Características

- **CRUD de Tópicos**: Permite crear nuevos tópicos, leer los existentes, actualizarlos y eliminarlos.
- **Autenticación y Autorización**: La seguridad está garantizada mediante el uso de tokens JWT, que verifican la identidad del usuario y autorizan el acceso a los recursos.
- **Validaciones**: Los datos de entrada son validados utilizando Jakarta Bean Validation para asegurar que cumplen con los requisitos necesarios antes de ser procesados.
- **Swagger**: La documentación de la API es generada automáticamente, facilitando la visualización y prueba de los endpoints disponibles.

## Dependencias Utilizadas

- **Swagger**: Para la generación de documentación de la API.
- **Lombok**: Simplifica el código eliminando el boilerplate como getters, setters y constructores.
- **Spring Web**: Proporciona las herramientas necesarias para construir aplicaciones web.
- **Spring Boot DevTools**: Ofrece herramientas de desarrollo que mejoran la productividad.
- **Spring Data JPA**: Facilita la interacción con la base de datos mediante JPA (Java Persistence API).
- **Flyway Migration**: Gestiona las migraciones de la base de datos.
- **MySQL Driver**: Controlador necesario para la conexión con bases de datos MySQL.
- **Validation**: Biblioteca para realizar validaciones de datos.
- **Spring Security**: Proporciona funcionalidades de autenticación y autorización.

## Requisitos Previos

- **JDK 17 o superior**: Entorno de desarrollo de Java.
- **Maven 3.8.1 o superior**: Herramienta de automatización de proyectos basada en Java.
- **MySQL 8.0 o superior**: Sistema de gestión de bases de datos.

## Configuración del Proyecto

1. **Clona el repositorio**:

    ```bash
    git clone https://github.com/tu-usuario/tu-proyecto.git
    cd tu-proyecto
    ```

2. **Configura la base de datos MySQL**:

   Ejecuta los siguientes comandos en tu consola de MySQL para crear la base de datos y el usuario necesarios:

    ```sql
    CREATE DATABASE forum_hub;
    CREATE USER 'forum_user'@'localhost' IDENTIFIED BY 'forum_password';
    GRANT ALL PRIVILEGES ON forum_hub.* TO 'forum_user'@'localhost';
    FLUSH PRIVILEGES;
    ```

3. **Configura las propiedades de la aplicación** en `src/main/resources/application.properties`:

    ```properties
    spring.datasource.url=jdbc:mysql://localhost:3306/forum_hub
    spring.datasource.username=forum_user
    spring.datasource.password=forum_password
    spring.jpa.hibernate.ddl-auto=update

    api.security.secret=tu_secreto_de_jwt
    ```

## Ejecución del Proyecto

1. **Compila y ejecuta la aplicación con Maven**:

    ```bash
    mvn clean install
    mvn spring-boot:run
    ```

2. **Accede a la aplicación**:

   La aplicación estará disponible en `http://localhost:8080`.

## Uso de la API

### Autenticación

Para autenticarte, envía una solicitud POST a `/login` con las credenciales del usuario (nombre de usuario y contraseña). La respuesta incluirá un token JWT que debe incluirse en el encabezado de autorización (`Authorization: Bearer <token>`) para todas las solicitudes posteriores.

### Endpoints Principales

- **POST /topicos**: Crea un nuevo tópico.
- **GET /topicos**: Obtiene la lista de tópicos.
- **PUT /topicos/{id}**: Actualiza un tópico existente.
- **DELETE /topicos/{id}**: Elimina un tópico de la base de datos.

## Documentación de la API

La documentación generada por Swagger está disponible en `http://localhost:8080/swagger-ui.html`, permitiendo la visualización y prueba interactiva de los endpoints.


# La autenticación stateless
Es un tipo de autenticación donde el servidor no guarda ninguna información sobre el estado del usuario entre las solicitudes. En lugar de mantener sesiones en el servidor, la autenticación stateless se basa en el uso de tokens para validar la identidad del usuario en cada solicitud.

## Breve Descripción del Proceso
- **Inicio de Sesión:**
  El usuario envía sus credenciales (usuario y contraseña) al servidor.
- **Generación de Token:**
  Si las credenciales son correctas, el servidor genera un token (generalmente un JWT - JSON Web Token) que incluye información sobre el usuario y una firma que garantiza su integridad.
- **Envío del Token:**
  El token se envía al usuario, generalmente en la respuesta HTTP.
- **Uso del Token:**
  El usuario almacena este token en el lado del cliente, típicamente en el almacenamiento local o en cookies.
- **Solicitudes Autenticadas:**
  Para cada solicitud posterior, el usuario envía el token en el encabezado de la solicitud HTTP (por ejemplo, Authorization: Bearer <token>).
- **Validación del Token:**
  El servidor valida el token en cada solicitud sin necesidad de mantener una sesión activa. La validación se realiza comprobando la firma del token y su fecha de expiración.
  Acceso a Recursos: Si el token es válido, el servidor permite el acceso a los recursos solicitados.
  Ventajas
### Escalabilidad:
Dado que no se almacenan sesiones en el servidor, es más fácil escalar horizontalmente la aplicación.
Simplificación del servidor: No es necesario manejar estados de sesión, lo que simplifica la lógica del servidor.
### Seguridad:
Los tokens pueden expirar automáticamente y pueden ser revocados si es necesario.
Desventajas
Complejidad en el cliente: El cliente debe manejar el almacenamiento y la transmisión del token.
Limitaciones de token: Si un token es comprometido, puede ser utilizado hasta que expire o sea revocado.
Para más información sobre la autenticación stateless, puedes consultar fuentes adicionales como Auth0 o JWT.io.

 ![Autenticacion](img/autenticacion%20stateless.jpg)
 #### Autenticación: Es el proceso de verificar la identidad de un usuario o entidad. Por ejemplo, ingresar un nombre de usuario y contraseña para acceder a una aplicación.

 ![Autorizacion ](img/autorizacion%20stateless.jpg)
 #### Autorización: Es el proceso de determinar si un usuario autenticado tiene permisos para acceder a un recurso específico o realizar una acción. Por ejemplo, verificar si un usuario tiene permiso para ver o modificar un documento.


![Security Filter](img/security%20filter%20para%20app%20tipo%20stateless.jpg)
#### Security Filter: Es un componente que intercepta las solicitudes HTTP en una aplicación web para aplicar controles de seguridad como autenticación y autorización. Por ejemplo, un filtro de seguridad puede validar tokens JWT antes de permitir el acceso a las rutas protegidas de una aplicación.

## Sobre mí

¡Hola! Mi nombre es Teodoro Matarrita y soy un desarrollador Java junior de Costa Rica.

- ✨ **Creando bugs desde**: No es mi primer,ni segundo proyecto de programación, donde aprendí más de mis errores que de mis aciertos.
- 📚 **Actualmente aprendiendo**: Arquitectura de microservicios y DevOps para mejorar la eficiencia y escalabilidad de las aplicaciones.
- 🎯 **Objetivos**: Convertirme en un desarrollador full-stack, contribuir a proyectos de código abierto y seguir aprendiendo nuevas tecnologías.
- 🎲 **Dato curioso**: Cuando no estoy programando, me encanta jugar al ajedrez y explorar la biodiversidad de Costa Rica.
- 👨‍💻 **Lenguaje favorito**: Programo principalmente con Java.
- 💻 **Otros lenguajes**:HTML, CSS3, javascript (Front end) & Java (Back end)[Fullstack]


## ¡Conéctate conmigo & Gracias por visitar mi proyecto! 👋

Puedes encontrarme en LinkedIn: [Teodoro Matarrita](https://www.linkedin.com/in/teodoro-matarrita/)

¡Si tienes alguna pregunta o sugerencia, no dudes en contactarme!

## Derechos de Autor
© 2024 JavaDeveloper Inc. Teodoro Matarrita. Todos los derechos reservados.
