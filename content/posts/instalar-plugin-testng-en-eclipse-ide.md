---
title: "Instalar plugin TestNG en Eclipse IDE"
date: 2023-02-02T16:20:19-03:00
draft: false
tags: ['testng','eclipse']
---
## Introducción

Para quienes trabajamos en automatización de pruebas de software es necesario siempre contar con herramientas que nos ayuden a optimizar el tiempo de creación de nuestros scripts de pruebas. Además, si sumamos que trabajamos con el lenguaje [Java](https://framorac.github.io/tags/java/), se hace imprescindible que conozcas [TestNG](https://testng.org/doc/index.html). **TestNG** es un framework de testing inspirado en [JUnit](https://junit.org/junit5/) y [NUnit](https://nunit.org/) dos de los más importantes fremeworks para pruebas unitarias, el primero para *Java* y el segundo para plataforma *.NET*.

**TestNG** se orienta a una **N**ueva **G**eneración de **Test**, la cual, nos ofrece las siguientes bondades:

+ Anotaciones.
+ Ejecutar test en pool de hilos.
+ Test con configuraciones flexibes.
+ Soporte DDT a través de ```@DataProvider```.
+ Soporte de parámetros.
+ Soporte para la mayoría de IDE's del mercado.
+ Soporte Maven.
+ entre otras..

Es por esto, que a continuación veremos cómo instalar su plugin en el IDE Eclipse.

## Requisitos

TestNG necesita lo siguiente para poder instalarse sin problemas:

1. Java 1.7 o superior.
2. Versión de *Eclipse IDE* superior a la 4.2

## Instalación por repositorio de software

En Eclipse para configurar el repositorio de software de TestNG, hacemos la ruta ```Help->Install New Software...```, luego pulsamos el botón ```Add...```, se despliega un cuadro de diálogo para configurar el *location* del nuevo repositorio y completar de la siguiente manera:

1. **Name**: TestNG
2. **Location**: ```https://testng.org/testng-eclipse-update-site/```
3. Pulsar el botón ```Add```
4. Seleccionamos nuestro nuevo repositorio en ```Work with:```
5. Marcar el check de todas los plugins desplegados en el listado bajo la glosa **TestNG**.
6. Pulsamos ```Next```
7. Nuevamente ```Next```
8. Aceptamos la licencia y pulsamos ```Finish```
9. Esperamos a que termine la instalación y eclipse solicitará reiniciar el IDE para completar los cambios.

La imágen siguiente refleja la configuración del repositorio correctamente:

![TestNG Available Software](/listadosoftware.png "TestNG Available Software")

## Instalación por Eclipse Marketplace

El Eclipse [Marketplace](https://marketplace.eclipse.org/) es el centro de aplicaciones de Eclipse y es la forma más sencilla de encontrar plugins, themes y extensiones las cuales nos harán la vida más fácil cuando desarrollamos en este IDE. Es por ello que el plugin de *TestNG* puede ser encontrado aquí también. Para ello hacemos la ruta ```Help->Eclipse Marketplace...``` y en el cuadro de diálogo que se desplega escribimos **TestNG** en la barra de búsqueda. Luego pulsar el botón ```Install``` en el plugins **TestNG for Eclipse**.

![TestNG for Eclipse](/marketplace.png "TestNG for Eclipse")

Por último, pulsar el botón ```Install Now``` y aceptar la licencia con un reinicio del IDE posteriormente.

Y con este pequeño tutorial de instalación tendremos la opción de generar clases de test usando las opciones que nos entrega TestNG. En próximos artículos veremos como empezar a crear nuestros scripts con este plugins.

Hasta la próxima, si te ha sido útil favor no dudes en compartirlo...
