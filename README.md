Pruebas automatizadas frontend para BAZ super app 
-
#### ¿Qué herramientas necesitas antes de clonar el proyecto?
1. Pycharm
2. Git
3. GitHub Desktop
4. Appium Server
5. Appium inspector (Solo para automation)
6. Android Studio
7. Java JDK
8. Python 3
9. Allure framework
10. Xcode (Solo usuarios de Mac)

En el siguiente enlace podrás encontrar los instaladores y un tutorial de configuración para cada una de las herramientas:
https://drive.google.com/drive/folders/1d4aRMTjJOq0f6lTulzK5Tq3mhfnPfzj-?usp=sharing

_NOTA: Para GitHub se debera crear cuenta con correo personal y solicitar acceso al repositorio del proyecto 
a Arturo Tapia (arturo.tapiav@elektra.com.mx)_

#### Estructura de carpetas
El directorio APP contendrá el archivo APK de la version que deseemos usar para nuestra ejecución.

    Behave
       └── App

El directorio FEATURE contendrá una carpeta para cada programa que a su vez tendrán los archivos Gherkin para cada set de pruebas.

    Behave
       └── feature
              ├── canal
              │     ├── bottom.bar.feature
              │     ├── compras.tab.feature
              │     └── diversion.tab.feature
              ├── compras
              ├── dinero
              ├── launcher
              ├── login
              ├── negocio
              ├── nuevas_iniciativas
              └── pagos

El directorio REPORTS almacenarán los reportes generados después de cada ejecución, estos estarán separados por plataforma.

    Behave
       └── reports
              ├── android
              └── iOS

El directorio SCREENS contendrá una carpeta para cada programa que a su vez tendrán las clases python 
con el mapeo de los elementos de cada pantalla en la aplicación que serán usados en las clases steps.
El archivo _**base_actions.py**_ contiene los métodos reutilizables para cada script. 

    
    Behave
       └── screens
              ├── autentication
              ├── canal
              │     ├── bottom_bar.py
              │     ├── hazlo_facil_baz_screen.py
              │     └── launcher_button.py
              ├── compras
              ├── dinero
              ├── launcher
              ├── login
              ├── negocio
              ├── nuevas_iniciativas
              ├── pagos
              └── base_actions.py
    
El directorio SCREENSHOTS almacenarán las capturas generadas después de cada ejecución fallida, estas estarán separados por plataforma.

    Behave
       └── screenshots
              ├── android
              └── iOS
    
El directorio STEPS contendrá las carpetas por cada programa donde se definirán las llamadas de las funciones o elementos 
creados para completar un paso de cada escenario Gherkin y sus validaciones. 
El archivo _**base_steps.py**_ contiene los imports para cada una de las clases py de este directorio.
   
    Behave
       └── steps
              ├── canal
              │     ├── bottombar_steps.py
              │     └── canal_steps.py
              ├── compras
              ├── dinero
              ├── launcher
              ├── login
              ├── negocio
              ├── nuevas_iniciativas
              ├── pagos
              └── base_steps.py

El directorio UTILS contiene la definición de constantes utilizadas por los scripts de cada programa.
   
    Behave
       └── utils
              ├── dictionaries
                        ├── canal
                        │     └── login_texts.py
                        ├── compras
                        ├── dinero
                        └── nuevas_iniciativas

#### ¿Cómo clonar el proyecto en tu computadora?
1. Abrir el siguiente URL en github con tu sesión activa: https://github.com/Atapiave/QA_team.
2. Ir a la opción "Code", seleccionar la opción "Open with GitHub desktop" y este te reaccionará a la aplicación de tu computadora.
3. En GitHub desktop en la ventana que te despliega selecciona la carpeta donde se descargara el repositorio y dar click en "Clonar"
4. Una vez cargado el repositorio, valida que se encuentre en la carpeta que seleccionaste.

https://user-images.githubusercontent.com/11878964/180867063-56d9a8a0-fc0a-420c-8cb0-f385dfee6cad.mov

#### ¿Cómo generar tu branch de trabajo?
1. Seleccionar "Current branch"
2. Dar click en new branch y deberás poner un nombre que contenga el programa en el que estas /Tu_nombre.
Ejemplo : dinero/juan
3. En "create branch based on" selecciona la opción de "main" y da click en "create branch"

#### ¿Cómo sincronizar tu rama con los últimos cambios de Main?
1. Seleccionar "Current branch"
2. Dar click en "Choose a branch to marge into"
3. Seleccionar la rama "main" y dar click en "create a merge commit"


                            Dispositivo fisico Setup
Antes de correr las pruebas en nuestro dispositivo debemos tener el modo desarrollador activo y la opción de depuración USB activada, 
Además dar permisos de instalación a aplicaciones de fuentes desconocidas.

#### ¿Cómo obtener el nombre de tu dispositivo de pruebas?
1. Conectamos nuestro dispositivo via USB
2. Abrimos una nueva terminal en nuestra maquina y escribimos el siguiente comando:
 `adb devices` 
3. En "List of devices" copiamos el código alfanumérico que nos aparece

<img width="682" alt="adb_devices" src="https://user-images.githubusercontent.com/11878964/180867212-f8dd19e1-a377-4c60-abc5-f01ae94007f6.png">

 

                                Pycharm Setup
- Abrir la carpeta del proyecto recién clonado en pycharm.

#### Configurar el interpreter de Python

1. Ir a las preferencias del proyecto y buscar la opción "Interpreter"
2. Damos click en el icono del engranaje y seleccionamos la opción "add.."
3. Vamos a la opción de "System interpreter"
4. Seleccionamos en interpreter la instalación que aparece por default de Python
5. Dar click en "Ok", después en "Apply" y "OK"

https://user-images.githubusercontent.com/11878964/180867338-d69f5f6a-d100-4d58-b388-1420d80f4190.mov

#### Descargar las librerías necesarias
Abrir tu terminal de pycharm para ejecutar el siguiente comando apuntando a QA_team:
`pip install -r requirements.txt`

#### Configuración del runner para poder usar el debugger
1. Abrir la opción de "add configuration"
2. Damos click en el icono de más (+) y seleccionamos python
3. Le ponemos nombre para identificar nuestra configuración Ejemplo: dinero_e2e
4. En donde aparece "scrip path" damos click y lo cambiamos por "Module name", en el cuadro de texto ponemos "behave"
5. En "parameters" ponemos el siguiente comando:

Para Android
`-f allure_behave.formatter::AllureFormatter -o reports/android -f pretty --tags=debug -D platform=android -D device_name=[Device_Id] features/[path_feture_to_run]`

Para iOS
`-f allure_behave.formatter::AllureFormatter -o reports/ios -f pretty --tags=debug -D platform=ios -D device_name=[Device_Id] features/[path_feture_to_run]`

6. Validar que en "System interprete" tengamos el que configuramos previamente.
7. En "working directory", damos click en el icono de folder y seleccionamos "Behave" en el dom de archivos.
8. Por último damos click en "Apply" y "OK" para guardar los cambios

https://user-images.githubusercontent.com/11878964/180867516-a8c123bf-6dc0-4687-94a5-1ee786fc2663.mov

#### Configuración del .env para tus pruebas
Dentro del arbol del proyecto buscamos el archivo ".env-sample", le hacemos una copia y la nombramos".env".
Asegúrate que el nuevo archivo se encuentre al mismo nivel de behave.
Una vez creado el archivo como base debemos comenzar a llenar las siguientes variables:

`OTP_API_URL = '[OTP_URL]'`

`USER_PHONE_NUMBER = ''`

`USER_PASSWORD = ''`

`USER_PASSCODE = ''`

#### Manejo de apk para ejecución de scripts
Antes de correr los scripts debemos agregar la APK con la que deseemos ejecutar nuestras pruebas al folder llamado APP, 
el archivo .apk debe ser nombra de la siguiente manera _**baz-dev.apk**_

<img width="346" alt="Screen Shot 2022-07-26 at 14 12 17" src="https://user-images.githubusercontent.com/11878964/181092490-7386b9d2-2fc4-4e73-9552-3ffb4e3fc4c2.png">


                       ¿Cómo ejecutar nuestras pruebas?
1. Tener conectado via USB tu dispositivo de pruebas, asegúrate que esté desbloqueado para que puedan correr las pruebas.
2. Abrir Appium server y da click en "start server"
3. Luego ir a pycharm, hacemos click en el icono de play que se encuentra en la esquina superior derecha
4. o en la terminal de pycharm ejecutar lo siguiente apuntando a behave: 

Correr todos los features `paver run_all android [Device_Id]`

Correr un feature en específico `paver run_feature android [Device_Id] features/[path_feture_to_run]`



https://user-images.githubusercontent.com/11878964/181099509-c8fad166-92a2-40a4-bdd8-5580d4c26cf7.mov

