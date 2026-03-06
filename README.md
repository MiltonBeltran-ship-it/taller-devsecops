# ***Taller 1***

DevSecOps es una forma de trabajar donde el desarrollo, las operaciones y la seguridad colaboran desde el inicio del proyecto. Su idea principal es integrar la seguridad en cada etapa para detectar problemas a tiempo y construir software más seguro sin retrasar el proceso.

**Trazabilidad:** ¿Por qué es un riesgo de seguridad dejar la configuración de user.name y user.email vacía o utilizar datos genéricos en un entorno empresarial?

Usar un nombre o correo genérico afecta la trazabilidad porque impide identificar quién realizó cada cambio en el código. En un ambiente empresarial esto es un riesgo, ya que dificulta investigar errores, auditar actividades o detectar acciones malintencionadas. Cuando los commits no están vinculados a una persona real, se pierde responsabilidad individual y es más fácil que alguien oculte actividades indebidas dentro del repositorio.

**Cifrado Asimétrico:** En el caso de usar SSH, ¿cuál es la diferencia funcional entre la llave privada y la pública? ¿Qué pasaría si un tercero obtiene acceso a tu llave privada?


En un sistema de cifrado asimétrico, la llave pública se comparte y sirve para que los servidores (como GitHub) puedan validar tu identidad.
La llave privada nunca debe salir de tu equipo: es la que te identifica como el propietario legítimo de esa identidad digital.
Si un tercero obtiene tu llave privada, puede hacerse pasar por ti y acceder a tus repositorios como si fueras tú. En el peor de los casos podría modificar o borrar proyectos enteros. Por eso la llave privada debe mantenerse protegida y jamás compartirse.

**Principio de Mínimo Privilegio:** Si decides usar un Token de Acceso Personal (PAT), ¿qué riesgos conlleva asignarle permisos de "Administrador" (Full Control) en lugar de solo permisos de "Lectura/Escritura"?

Asignar permisos de “Administrador” a un PAT le da mucho más poder del que realmente necesita. Un token con privilegios elevados puede crear o borrar repositorios, administrar llaves SSH, modificar configuraciones críticas e incluso eliminar información. Desde el punto de vista de seguridad, esto viola el principio de mínimo privilegio y aumenta el impacto de un posible robo o filtración del token.

**Higiene del Repositorio:** ¿Para qué sirve el archivo .gitignore desde una perspectiva de seguridad? (Menciona al menos dos tipos de archivos que nunca deberían subirse al repositorio remoto).

El archivo .gitignore ayuda a evitar que archivos sensibles o innecesarios terminen en el repositorio. Desde una perspectiva de seguridad, evita que se suban credenciales, configuraciones internas o archivos generados por el sistema.
Dos tipos de archivos que nunca deben subirse son:

Llaves privadas, tokens o contraseñas (por ejemplo: .pem, .key, .env).
Archivos temporales o de sistema, como .DS_Store, thumbs.db o carpetas de compilación (node_modules, bin, obj).

**Exposición de Secretos:** Si accidentalmente subes una llave de API o una contraseña al repositorio en GitHub, ¿es suficiente con borrarla y hacer un nuevo commit? Justifica tu respuesta.

No, no es suficiente.
Aunque borres el archivo en un commit posterior, la información queda guardada en el historial del repositorio, por lo que cualquiera con acceso podría recuperarla. La medida correcta es:

Revocar la llave expuesta (invalidarla).
Quitarla del historial mediante herramientas como git filter-branch o git filter-repo.
Generar una nueva llave o contraseña y reemplazarla en los sistemas que la usen.

Solo así se asegura que el secreto comprometido ya no pueda ser utilizado
