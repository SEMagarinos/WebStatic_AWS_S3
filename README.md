# WebStatic_AWS_S3
 
![buckets3](https://img.shields.io/badge/Coding-PowerShell-green?style=flat&logo=powershell)

# Sitio web estatico en AWS BUCKET S3

_Acá va un párrafo que describa lo que es el proyecto_

### 📋| Pre-requisitos 

_Que cosas necesitas para instalar el software y como instalarlas_

```
Da un ejemplo
```

### 🚀| Creacion de un _Bucket S3_


Nombre de bucket:
```
webstaticsm
```

_Des-Seleccionar y aceptar el riesgo en el apartado:_
```
Configuración de bloqueo de acceso público para este bucket
-
Desactivar el bloqueo de todo acceso público puede provocar que este bucket y los objetos que contiene se vuelvan públicos
```

### 📋| Configurar _Bucket S3_

Configurar los permisos / policy para la utilizacion del Bucket S3
Ejemplo:

Edit **Bucket Policy** dentro de permisos del Bucket S3: _Recordar cambiar el nombre del bucket en la policy "webstaticsm"_
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::webstaticsm/*"
        }
    ]
}
```

Configurar "Static Website Hosting" dentro de "Propiedades" del _Bucket S3_

Habilitarlo tildando **"Enable"** 
Configurar *Index Dcoument*
Configurar *Reglas de redireccionamiento*
```
[
    {
        "Condition": {
            "HttpErrorCodeReturnedEquals": "403"
        },
        "Redirect": {
            "HostName": "aws.md.md",
            "Protocol": "https",
            "ReplaceKeyPrefixWith": "#!/"
        }
    },
    {
        "Condition": {
            "HttpErrorCodeReturnedEquals": "404"
        },
        "Redirect": {
            "HostName": "aws.md.md",
            "Protocol": "https",
            "ReplaceKeyPrefixWith": "#!/"
        }
    }
]
```


### 📋| Subir los archivos al _Bucket S3_

**Nombre: index.html**
```
<!DOCTYPE html>
<html lang="sp">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Sitio Web Estatico de Prueba</title>
        <link rel="stylesheet" href="./style.css">
        <link rel="icon" href="./favicon.ico" type="image/x-icon">
    </head>
    <body>
        <main>
            <h1>Bienvenido estamos probando el sitio estatico con un solo index.html</h1>
        </main>
        <script src="index.js">

        </script>
        </body>
    
</html>
```




Mira **Deployment** para conocer como desplegar el proyecto.

### 🔧| Instalación 

_Una serie de ejemplos paso a paso que te dice lo que debes ejecutar para tener un entorno de desarrollo ejecutandose_

_Dí cómo será ese paso_

```
Da un ejemplo
```

_Y repite_

```
hasta finalizar
```

_Finaliza con un ejemplo de cómo obtener datos del sistema o como usarlos para una pequeña demo_

## ⚙️| Ejecutando las pruebas 

_Explica como ejecutar las pruebas automatizadas para este sistema_

### 🔩| Analice las pruebas end-to-end 

_Explica que verifican estas pruebas y por qué_

```
Da un ejemplo
```

### ⌨️| Las pruebas de estilo de codificación 

_Explica que verifican estas pruebas y por qué_

```
Da un ejemplo
```

## 📦| Despliegue

_Agrega notas adicionales sobre como hacer deploy_

## 🛠️| Construido con 

_Menciona las herramientas que utilizaste para crear tu proyecto_

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - El framework web usado
* [Maven](https://maven.apache.org/) - Manejador de dependencias
* [ROME](https://rometools.github.io/rome/) - Usado para generar RSS

## Versionado 📌

Usamos [SemVer](http://semver.org/) para el versionado. Para todas las versiones disponibles, mira los [tags en este repositorio](https://github.com/tu/proyecto/tags).

## ✒️| Autores 

_Menciona a todos aquellos que ayudaron a levantar el proyecto desde sus inicios_

* **Andrés Villanueva** - *Trabajo Inicial* - [villanuevand](https://github.com/villanuevand)
* **Fulanito Detal** - *Documentación* - [fulanitodetal](#fulanito-de-tal)

También puedes mirar la lista de todos los [contribuyentes](https://github.com/your/project/contributors) quíenes han participado en este proyecto. 

## 📄| Licencia 

Este proyecto está bajo la Licencia (Tu Licencia) - mira el archivo [LICENSE.md](LICENSE.md) para detalles

## 🎁| Expresiones de Gratitud :D

* Comenta a otros sobre este proyecto 📢
* Invita una cerveza 🍺 o un café ☕ a alguien del equipo. 
* Da las gracias públicamente 🤓.
* Paypal


---