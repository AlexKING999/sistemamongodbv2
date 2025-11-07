# Tienda Tecnológica - Sistema de Gestión con Streamlit y MongoDB

Este proyecto ha sido actualizado para ser compatible con el despliegue en **Streamlit Cloud**.

## Cambios Realizados para Streamlit Cloud

1.  **Uso de `st.secrets` para la Conexión a MongoDB:**
    *   La URI de conexión a MongoDB ya no está codificada directamente en `config.py`.
    *   Ahora se lee de los secretos de Streamlit (`st.secrets["mongodb"]["uri"]`), lo cual es la práctica recomendada para manejar credenciales de forma segura en Streamlit Cloud.

2.  **Estructura de Archivos:**
    *   Se ha creado el directorio `.streamlit` y el archivo `secrets.toml` para guiar la configuración de secretos.

## Pasos para el Despliegue en Streamlit Cloud

Para que la aplicación funcione correctamente en Streamlit Cloud, debes seguir estos pasos:

### 1. Configurar la Conexión a MongoDB Atlas

Streamlit Cloud no puede acceder a bases de datos locales (`localhost`). Debes usar una base de datos en la nube, como **MongoDB Atlas**.

1.  **Obtén tu URI de Conexión:**
    *   Inicia sesión en tu cuenta de MongoDB Atlas.
    *   Ve a la sección **Database Deployments** y haz clic en **Connect** en tu clúster.
    *   Selecciona **Drivers** y copia la cadena de conexión (URI). Asegúrate de reemplazar `<username>`, `<password>`, y el nombre de la base de datos si es necesario.

    **Ejemplo de URI:**
    `mongodb+srv://usuario:contraseña@cluster0.abcde.mongodb.net/tienda_tecnologica?retryWrites=true&w=majority`

### 2. Configurar los Secretos en Streamlit Cloud

1.  **Despliega la Aplicación:**
    *   Sube tu código (incluyendo los archivos modificados `app.py`, `config.py`, `requirements.txt`) a un repositorio de GitHub.
    *   En Streamlit Cloud, selecciona **New app** y conecta tu repositorio.

2.  **Añade el Archivo de Secretos (`secrets.toml`):**
    *   En la configuración de la aplicación en Streamlit Cloud, busca la sección **Advanced settings** o **Secrets**.
    *   Debes añadir el contenido del archivo `secrets.toml` (que se encuentra en el directorio `.streamlit` de este proyecto) como secretos de la aplicación.

    El formato debe ser:

    ```toml
    # .streamlit/secrets.toml
    [mongodb]
    uri = "TU_URI_DE_CONEXION_DE_MONGODB_ATLAS"
    ```

    **Reemplaza `TU_URI_DE_CONEXION_DE_MONGODB_ATLAS`** con la URI que obtuviste en el paso 1.

### 3. Archivo `requirements.txt`

Asegúrate de que tu archivo `requirements.txt` esté en la raíz de tu repositorio y contenga las dependencias necesarias:

```
pymongo==4.6.0
streamlit==1.28.1
pandas==2.1.1
```

### 4. Inicializar la Base de Datos (Opcional)

Si necesitas poblar la base de datos con datos iniciales, puedes ejecutar el script `init_database.py` localmente una vez, o adaptarlo para que se ejecute en un entorno seguro si es necesario.

---

**¡Con estos pasos, tu aplicación debería desplegarse y conectarse a MongoDB Atlas sin problemas en Streamlit Cloud!**
