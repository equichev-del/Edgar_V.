# Mi primera base de datos en PostgresSQL usando docker y datagrip
Este respositorio contiene la documentacion y especificaciones tecnicas para la instalacion, configuracion y despliegue de una base de datos relacional postgresSQL utilizando contenedores Docker, y su posterior administracion mediante el entorno de desarrollo integrado (IDE) datagrip.
---
## 1. comando para ejecutar docker con postgresSQL
para iniciar un contenedor de Docker con la imagen oficial de PostgreSQL en segundo plano, epone el puerto estandar y asigna una contraseña de administrador, ejecuta el siguiente comando en tu terminal o PowerShell:

'''bash
docker run --name pg-server -e POSTGRES_PASSWORD=tu_contraseña_aqui -p 5432:5432 -d postgres
'''

### explicacion de los parametros:
*  '--name pg-server': Asigna el nombre descriptivo 'pg-server' al contenedor para identificarlo facilmente.
*  'e- POSTGRES_PASSWORD=...': define la variable de entorno obligatoria para establecer la contraseña del superusuario por defecto ('postgres`).
*  -p 5432:5432': Mapea el puerto '5432' de tu maquina local al puerto interno'5432' del contenedor de Docker.
*  '-d': ejecuta el contenedor en modo "detacged" (en segundo plano), liberando la terminal.
*  'postgres': Especifica que se descargue y se use la ultima imagen oficial de PostgreSQL desde Docker hub.

  --

## 2. Pasos para configurar DataGrip

Para vincular el entorno de desarrollo integrado (IDE) DataGrip con el servidor PostgreSQL que acabas de desplegar en Docker, sigue esta secuencia de pasos:

1. **Iniciar DataGrip:** Abre la aplicación en tu sistema operativo.
2. **Crear una nueva fuente de datos:**
   * Localiza el panel lateral izquierdo llamado **Database**.
   * Haz clic en el ícono **`+` (New)** de la esquina superior izquierda de ese panel.
   * Navega por el menú desplegable: **Data Source** -> **PostgreSQL**.
3. **Instalación de controladores (Drivers):**
   * En la parte inferior de la ventana de configuración, busca una advertencia en amarillo que indica la falta de controladores (*Driver files are not downloaded*).
   * Haz clic en el enlace **Download** para que DataGrip descargue e instale automáticamente los conectores oficiales de PostgreSQL.
4. **Configuración de las credenciales de conexión:**
   * En la pestaña **General**, introduce los siguientes parámetros basados en el contenedor Docker creado:
     * **Host:** `localhost` (indica que el servidor corre en tu máquina local).
     * **Port:** `5432` (el puerto estándar que mapeamos en el comando docker).
     * **User:** `postgres` (el superusuario por defecto de la imagen).
     * **Password:** `tu_contraseña_aqui` (la contraseña exacta que definiste en la variable `POSTGRES_PASSWORD`).
     * **Database:** Puedes dejarlo en blanco o escribir `postgres` para conectar inicialmente a la base de datos del sistema.
5. **Verificación de la conectividad:**
   * Haz clic en el botón **Test Connection** ubicado en la esquina inferior izquierda.
   * Si la configuración es correcta, aparecerá un mensaje con un check verde mostrando la versión de PostgreSQL y el tiempo de respuesta.
6. **Guardar cambios:** Haz clic en **Apply** y luego en **OK** para cerrar la ventana y guardar la conexión.

---

## 3. Creación de la base de datos PostgreSQL desde DataGrip

Una vez establecida la conexión con el servidor, sigue estos pasos para estructurar y dar de alta tu primera base de datos relacional mediante sentencias SQL:

1. **Abrir la consola de consultas (Query Console):**
   * En el panel izquierdo **Database**, haz clic derecho sobre la conexión que acabas de crear (por defecto tendrá un nombre similar a `postgres@localhost`).
   * Selecciona la opción **New** -> **Query Console**. Esto abrirá un editor de texto en blanco vinculado directamente a tu servidor.
2. **Escribir la sentencia de creación:**
   * En el editor de la consola, escribe el comando estándar de SQL:
     ```sql
     CREATE DATABASE mi_primera_bd;
     ```
3. **Ejecutar el comando SQL:**
   * Posiciona el cursor sobre la línea de código.
   * Haz clic en el botón verde con forma de **Play (Execute)** en la barra de herramientas superior de la consola, o presiona el atajo de teclado `Ctrl + Enter` (`Cmd + Enter` en macOS).
   * Verifica en la pestaña inferior **Services / Output** que la sentencia se ejecutó correctamente con el mensaje `Completed successfully`.
4. **Actualizar y visualizar la nueva base de datos:**
   * Para hacer visible el cambio en la interfaz gráfica, regresa al panel izquierdo **Database**.
   * Haz clic derecho sobre el nombre de tu conexión y selecciona **Refresh** (o presiona la tecla `F5`).
   * Despliega el árbol de carpetas de la conexión; ahora verás listada `mi_primera_bd` junto a la base de datos por defecto.
Usa el código con precaución.Si deseas que agreguemos algo más, dime si tienes pensado crear tablas iniciales o si prefieres que te explique cómo estructurar los directorios en GitHub para subir esta tarea de forma ordenada.
