# [Embedded-PaymentForm-JavaScript]
##  Índice
* [1. Introducción](#introduccion)
* [2. Requisitos previos](#2-requisitos-previos)
* [3. Despliegue](#3-despliegue)
* [4. Datos de conexión](#4-datos-de-conexión)
* [5. Transacción de prueba](#5-transacción-de-prueba)
* [6. Implementación de la IPN](#6-implementación-de-la-ipn)
* [7. Personalización](#7-personalización)
* [8. Consideraciones](#8-consideraciones)
## 1. Introducción <a name="introduccion"></a>
En este manual podrás encontrar una guía paso a paso para configurar un proyecto de <span style="color:red">[JavaScript]</span> con la pasarela de pagos de IZIPAY. Te proporcionaremos instrucciones detalladas y credenciales de prueba para la instalación y configuración del proyecto, permitiéndote trabajar y experimentar de manera segura en tu propio entorno local.
Este manual está diseñado para ayudarte a comprender el flujo de la integración de la pasarela para ayudarte a aprovechar al máximo tu proyecto y facilitar tu experiencia de desarrollo.

<p align="center">
  <img src="https://i.postimg.cc/FzGzG9Jd/Whats-App-Image-2024-01-30-at-10-02-40.jpg" alt="Formulario" width="350"/>
</p>

<a name="Requisitos_Previos"></a>
 
## 2. Requisitos previos <a name="2-requisitos-previos"></a>
* Extraer credenciales del Back Office Vendedor. [Guía Aquí](https://github.com/izipay-pe/obtener-credenciales-de-conexion)
* Tener instalado Visual Studio Code

## 3. Despliegue <a name="3-despliegue"></a>
### Instalar Live Server
Live Server, extensión para Visual Studio Code que simula un servidor web. Para instalarlo:
1. Ingresar a la sección "Extensiones" de Visual Studio Code
2. Buscar "Live Server "
3. Instalar extensión

**Nota**: Tener en cuenta que, para que el desarrollo de tu proyecto, eres libre de emplear tus herramientas preferidas

<p align="center">
  <img src="https://i.postimg.cc/qvVXWwtk/Live-Server.png" alt="Formulario" />
</p>

### Clonar el proyecto:
  ```sh
  git clone [https://github.com/izipay-pe/Embedded-PaymentFormT1-JavaScript.git]
  ```
### Ejecutar proyecto
Accede al archivo `index.html` dentro de la carpeta `src` y de clic derecho dentro del código HTML, busca la opción `open with Live Server` para ejecutarlo, se abrirá en su navegador el proyecto y podrá ver el resultado en: 
```sh
http://127.0.0.1:5500/src/index.html
 ```
<p align="center">
  <img src="https://i.postimg.cc/qqykNpp6/ejecutar.png" alt="Formulario" width="350"/>
</p>


## 4. Datos de conexión 

**Nota**: Reemplace **[CHANGE_ME]** con sus credenciales de `API REST` extraídas desde el Back Office Vendedor, ver [Requisitos Previos](#Requisitos_Previos).

* Editar en src/index.html en la sección HEAD:

```html
<script 
    type="text/javascript"
    src="https://api.micuentaweb.pe/static/js/krypton-client/V4.0/stable/kr-payment-form.min.js" 
    kr-public-key="~~CHANGE_ME_PUBLIC_KEY~~"
    kr-get-url-success="~~CHANGE_ME_PAGE_REDIRECTION~~"       
    kr-language="es-ES"
>
</script>
``` 

* Crear y editar el endpoint el cual retornara el formtoken [Manual Aquí](https://github.com/izipay-pe/Response-FormToken), se cambiara `YOUR_SERVER/payment/init`por la nueva url creada, ruta donde se tiene que realizar el cambio: src/app.js.

```javascript 
	request.open('POST', 'YOUR_SERVER/payment/init', true);
	request.setRequestHeader('Content-Type', 'application/json');
```

## 5. Transacción de prueba
Antes de poner en marcha su pasarela de pago en un entorno de producción, es esencial realizar pruebas para garantizar su funcionamiento correcto. 

Puede intentar realizar una transacción utilizando una tarjeta de prueba con la barra de herramientas de depuración (en la parte inferior de la página).

<p align="center">
  <img src="https://i.postimg.cc/3xXChGp2/tarjetas-prueba.png" alt="Formulario"/>
</p>

* También puede encontrar tarjetas de prueba este enlace. [Tarjetas de prueba](https://secure.micuentaweb.pe/doc/es-PE/rest/V4.0/api/kb/test_cards.html)
 
## 6. Implementación de la IPN
La IPN es una notificación de servidor a servidor (servidor de Izipay hacia el servidor del comercio) que facilita información en tiempo real y de manera automática cuando se produce un evento, por ejemplo, al registrar una transacción.
Los datos transmitidos en la IPN se reciben y analizan mediante un script que el vendedor habrá desarrollado en su servidor.
* Ver manual de implementación de la IPN. [Aquí]( https://secure.micuentaweb.pe/doc/es-PE/rest/V4.0/kb/payment_done.html)
* Vea el ejemplo de la respuesta IPN con PHP. [Aquí](https://github.com/izipay-pe/Redirect-PaymentForm-IpnT1-PHP).
* Vea el ejemplo de la respuesta IPN con NODE.JS. [Aquí](https://github.com/izipay-pe/Response-PaymentFormT1-Ipn).

## 7. Personalización
Si deseas aplicar cambios específicos en la apariencia de la pasarela de pago, puedes lograrlo mediante la modificación de código CSS. En este enlace [Código CSS - Incrustado](https://github.com/izipay-pe/Personalizacion-PaymentForm-Incrustado) podrá encontrar nuestro script para un formulario incrustado.

## 8. Consideraciones
Para obtener más información, echa un vistazo a:
- [Formulario incrustado: prueba rápida](https://secure.micuentaweb.pe/doc/es-PE/rest/V4.0/javascript/quick_start_js.html).
- [Primeros pasos: pago simple](https://secure.micuentaweb.pe/doc/es-PE/rest/V4.0/javascript/guide/start.html).
- [Servicios web - referencia de la API REST](https://secure.micuentaweb.pe/doc/es-PE/rest/V4.0/api/reference.html).
