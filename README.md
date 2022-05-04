# Sitio estatico dentro de Amazon Web Service.

Para la publicacion de sitios webs estaticos sin utilizar servidores de renderizado, se utilizaria un Bucket S3 con otros componentes para dicha publicacion.

## 📋| Pre-requisitos 

 ![aws](https://img.shields.io/badge/Cloud-AWS-green?style=flat&logo=amazonaws) La instalacion se realizara dentro de **_Amazon Web Service_** .

![buckets3](https://img.shields.io/badge/Repositorio-BucketS3-red?style=flat&logo=amazons3), Se utilizara como repositorio de los documentos, html, css, img, entre otros contenidos estaticos, un **Bucket S3** privado.

![cloudfront](https://img.shields.io/badge/Distribuidor-CloudFront-blue?style=flat&logo=cloudflare), para la publicacion segurizada y con servicios de cache se utilizara **AWS CloudFront**

![route53](https://img.shields.io/badge/DNS-Route53-yellow?style=flat&logo=amazon), para una mejor experiencia se utilizara un alias de **DNS en un Dominio Publico** para que el internauta acceda de forma directo o simple.

![OAI](https://img.shields.io/badge/Identidad-OAI-cyan?style=flat&logo=GreenSock), para resguardar el _bucket s3_ se utilizara una identidad de **OAI** que se utiliza en **AWS CloudFront**.


### 🚀| Creacion de un _Bucket S3_

Abrir consola de AWS Bucket S3 y crear un nuevo bucket. [![Bucket Console](https://img.shields.io/badge/Url-Bucket_S3_Console-0078D7?logo=Microsoft-edge&logoColor=white)](https://s3.console.aws.amazon.com/s3/home)

**Nombre de bucket:** `webstaticsm`

**Dejar todo seleccionado / bloqueado**

### ⚙️| Configurar _Bucket S3_

**Static Website Hosting** dentro de **Propiedades** del **_Bucket S3_** _(Abajo de todo)_

Habilitarlo tildando `Habilitar`

Configurar **Documento de Indice** `index.html` (o el archivo que se tiene como principal) 

Configurar **Reglas de redireccionamiento** (Esto depende del proyecto o sitio)
```
[
    {
        "Condition": {
            "HttpErrorCodeReturnedEquals": "403"
        },
        "Redirect": {
            "HostName": "webstaticsm.smg-re-argentina.com.ar",
            "Protocol": "https",
            "ReplaceKeyPrefixWith": "#!/"
        }
    },
    {
        "Condition": {
            "HttpErrorCodeReturnedEquals": "404"
        },
        "Redirect": {
            "HostName": "webstaticsm.smg-re-argentina.com.ar",
            "Protocol": "https",
            "ReplaceKeyPrefixWith": "#!/"
        }
    }
]
```
**Listo guardar configuracion**

### 📋| Subir los archivos al _Bucket S3_

En este GitHub hay unos archivos de ejemplos con nombre de carpeta `example` que se podriam usar para validar acceso a imagenes etc.

Codigo de `index.html` basico

```
<!DOCTYPE html>
<html lang="sp">
    <head>
        <meta charset="UTF-8">
        <title>Sitio Web Estatico de Prueba</title>
    </head>
    <body>
        <main>
            <h1>Bienvenido estamos probando el sitio estatico con un solo index.html</h1>
        </main>
    </body>
</html>
```

**Listo guardar configuracion**

### 📋| Obtener URL PATH del _Bucket S3_

Dentro del bucket s3 , en propiedades en el apartado **Alojamiento de sitios web estaticos**

**Por ejemplo:** `http://webstaticsm.s3-website-us-east-1.amazonaws.com`


## 📋| Creacion del _CloudFront_

Configuracion de Nuevo CloudFront

Abrir consola de **Aws CloudFront**. [![Bucket Console](https://img.shields.io/badge/Url-AWS_CloudFront-0078D7?logo=Microsoft-edge&logoColor=white)](https://console.aws.amazon.com/cloudfront/v3/home)


**Origin Domain Name** = `Nombre del bucket s3 o ALB.`

**View Protocol Policy** = `Redirect HTTP to HTTPS.`

**Name** = _Recomendamos que sea acorde a la solucion_ `Se pone automatico`

**S3 Bucket Access** = _Punto Importante_ `Yes use OAI (bucket can restrict access to only CloudFront`

- **Dos Opciones:** `Crear nueva Identidad y/o utilizar una pre-armada`

- **Tildar** `Si, Actualizar Bucket Policy` (Esto lo realizar automaticamente, se puede validar luego)

**Alternate Domain Name (CNAMEs)** = _Segun dns que se piense usar_ `webstaticsm.smg-re-argentina.com.ar`

**Custom SSL** = Seleccionado uno existente del root `*.smg-re-argentina.com.ar (a81bb7c31b51-43eb-ba5e-055905eeab1c)`

**Default Root Object** = `index.html`

**Descripcion** = `Se entiende que es Opcional pero es bueno aclarar que es este distribuidor, algo referente al mismo`


**Finalizar con la Creacion del distribuidor**

## 📄| Creacion de Route 53

Para la configuracion de la zona y/o el alias de DNS correcto.

Abrir consola de **Route 53**. [![Bucket Console](https://img.shields.io/badge/Url-Route_53_Console-0078D7?logo=Microsoft-edge&logoColor=white)](https://console.aws.amazon.com/route53/home)

**Nombre de DNS** = `webstaticsm.smg-re-argentina.com.ar`

**Tildar Alias** = `Tildado`

**Redirigir trafico a** = `Alias de distribucion de CloudFront`

**Seleccionar el** = `det17u9nsxzot.cloudfront.net`


## 🛠️| Construido con 🔥

* [Sebastian E. Magariños](http://www.linkedin.com/in/smagarinos)

## 📌| Version

Version 1.4

## ✒️| Autores 

_**Sebastián E. Magariños**_


---
