# WebStatic_AWS_S3

![buckets3](https://img.shields.io/badge/Cloud-AWS-green?style=flat&logo=amazonaws)


![buckets3](https://img.shields.io/badge/Coding-PowerShell-green?style=flat&logo=buckets3)



# Sitio web estatico en AWS BUCKET S3

_Acá va un párrafo que describa lo que es el proyecto_

### 📋| Pre-requisitos 

_Preparacion de Bucket S3 + CloudFront + Route53_

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

### ⚙️| Configurar _Bucket S3_

Configurar los permisos / policy para la utilizacion del Bucket S3
Ejemplo:

**Bucket Policy** dentro de permisos del Bucket S3: _Recordar cambiar el nombre del bucket en la policy "webstaticsm"_
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
### 📋| Obtener URL PATH del _Bucket S3_

Dentro del bucket s3 , en propiedades en el apartado **Alojamiento de sitios web estaticos**

Show the URL
```
http://webstaticsm.s3-website-us-east-1.amazonaws.com
```


### 📋| Creacion del _CloudFront_

Configuracion de Nuevo CloudFront

**Origin Domain Name** = Nombre del bucket s3 o NLB.
**View Protocol Policy** = Redirect HTTP to HTTPS.
**Alternate Domain Name (CNAMEs)** = _webstaticsm.smg-re-argentina.com.ar_
**Custom SSL** = Seleccionado uno existente del root _*.smg-re-argentina.com.ar (a81bb7c31b51-43eb-ba5e-055905eeab1c) _

### 📄| Creacion de Route 53

Para la configuracion de la zona y/o el alias de DNS correcto.

**Nombre de DNS:** webstaticsm _.smg-re-argentina.com.ar_
**Tildar Alias** Tildado
**Redirigir trafico a:** _Alias de distribucion de CloudFront_
**Seleccionar el :** _det17u9nsxzot.cloudfront.net_

## 🛠️| Construido con 

* [Sebastian E. Magariños](http://www.linkedin.com/in/smagarinos)

## 📌| Version

Version 1.0

## ✒️| Autores 

_**Sebastián E. Magariños**_

---
