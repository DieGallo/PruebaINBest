# Instrucciones API Backend
### Paso 1: Instalación de Librerías
Instalamos las librerías en nuestro VSCode.  
Las librerías las podemos encontrar en *requirements.txt*
 - pip install **Django**
 - pip install **djangorestframework**
 - pip install **Pillow**
 - pip install **djangorestframework-simplejwt**
 - pip install **psycopg2-binary**
### Paso 2: Migración de bases de datos (PostgreSQL)
Migramos nuestra base de datos ingresando a **settings.py**  
Ingresamos nuestras credenciales.
~~~
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'api',
        'USER': 'root',
        'PASSWORD': 'tu_contraseña',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
~~~
Una vez ingresadas las credenciales escribimos la migración.
- python manage.py **makemigrations**
- python manage.py **migrate**
### Paso 3: Ejecutamos la API
Antes de ejecutar la API, creamos un super usuario ó con un Endpoint
- python manage.py **createsuperuser**
- py manage.py **runserver** 
    
Abrimos Postman e ingresamos la colección del repositorio
**Paso 3.1: Obtener el Token**
- http://127.0.0.1:8000/api/token/
  - Seleccionamos método **POST**
  - Seleccionamos **Body**
  - Seleccionamos en **raw**
  - Ingresamos el siguiente **JSON**
    ~~~
    {
    "username": "diego", (Nombre del SuperUser)
    "password": "diego123" (Contraseña del SuperUser)
    }  
    ~~~
  - Nos retornará el Endpoint 2 Tokens - **Acceso** y **Refresh**:
    ~~~
    {
    "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTczMjgwNDIxNSwiaWF0IjoxNzMyNzE3ODE1LCJqdGkiOiIxMDVlYTdlYjk2YTI0YTA4YjlmMmY1NmJjOGNiM2VjZSIsInVzZXJfaWQiOjF9.L3dTmI84cAYMmh2J4DkIS_IH2j9eZJCMpHMLDujtrKI",
    "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzMyNzE4MTE1LCJpYXQiOjE3MzI3MTc4MTUsImp0aSI6ImU4NmMyNmY5ZTY2ZTQzMTFiYmU0NDAxOWFiYmUzYTFlIiwidXNlcl9pZCI6MX0.peB-WqxUfaQXR9OwAU-twZS-EmjfqKwRxNxDbJRAfqk"
    }
    ~~~
**Paso 3.2: Subir imágen**
- http://127.0.0.1:8000/api/images/
    - Seleccionamos método **POST**
    - Selecconamos **Headers**
      - **Key:** Authorization
      - **Value:** Bearer + **AccessToken**
    - Regresamos a **Body**
      - Seleccionamos **form-data**
      - **Key:** file
        - El combobox seleccionamos **File**
      - **Value:** *Subimos nuestra imágen*
        - Presionamos en **New file from local machine**
        - Subimos la foto presionamos este ícono
          
          ![image](https://github.com/user-attachments/assets/0afbf390-dc71-49f0-9d98-02904125ee31)
      - Se cargará la imágen y presionamos en **Send**
    - Nos retornará el siguiente **JSON**
      ~~~
      {
        "id": 5,
        "user": 1,
        "original_image": "/media/original_images/foto3.jpg",
        "processed_image": "/media/processed_images/processed_5.jpg",
        "upload_date": "2024-11-27T14:31:35.153598Z",
        "process_date": "2024-11-27T08:31:35.355385Z",
        "processing_details": {
            "resize": "800x800",
            "color": "grayscale"
        }
      }
      ~~~
    - Tendremos dos enlaces, **original_image** y **processed_image**
    - Podemos usar la combinación de teclas **Ctrl + Click** en cualquiera de estos enlaces.
    - Se nos mostrarán las fotos, la original y la procesada a escala de grises.
### IMPORTANTE: Guardado de las imágenes.  
En donde se encuentra las directorios **backend** y **imageAPP** se nos creará una carpeta llamado **media**
- backend
- imageAPP
- media
  - original_images
    - *fotos subidas*
  - processed_images
    - *fotos subidas a escala de grises*
    
