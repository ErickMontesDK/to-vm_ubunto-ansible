<i class="time"></i>
<div class="head"><h1>Containers</h1></div>

````ad-abstract
Un contenedor es una unidad estándar de software que <mark style="background: #ABF7F7A6;">empaqueta el código y todas sus dependencias para que la aplicación se ejecute de forma rápida y fiable</mark> desde un entorno informático a otro. 

Los contenedores <mark style="background: #ABF7F7A6;">incluyen todo lo necesario para que un software se ejecute.</mark> Se usan como máquinas virtuales pero suelen utilizarse para levantar máquinas independientes con sistemas operativos muy ligeros. 

Los contenedores virtualizan el sistema operativo de un servidor. 

![[Pasted image 20221122203217.png]]

Una imagen de contenedor es una imagen ligera, un paquete de software independiente y ejecutable que <mark style="background: #ABF7F7A6;">incluye todo lo necesario para ejecutar una aplicación:</mark> código, tiempo de ejecución, sistema ms, bibliotecas del sistema
y ajustes.

Una **imagen en es un archivo** o _file_ que se encuentra compuesto de diversas capas y **que <mark style="background: #ABF7F7A6;">se utiliza con el objetivo de ejecutar un código dentro de un contenedor.*</mark>* Estas imágenes contienen todo el sistema de ficheros inicial en los que se va a basar el _container_ para su funcionamiento, así como su punto de entrada o _entrypoint_.
````
```ad-example
[[Build and run a container with a Dockerfile#^e00ee8]]
```

`````ad-info
title:## Diferencias entre Virtual Machines y Containers
![[Pasted image 20221122202731.png]]
```ad-warning
title:Tamaño
collapse:
-   Los contenedores se miden en megabytes. El elemento más grande que empaquetan es una aplicación y todos los archivos necesarios para su ejecución. Esto<mark style="background: #FFF3A3A6;"> permite trasladarlos entre los distintos entornos con mucha facilidad.</mark>
-  Las máquinas virtuales se miden en gigabytes. Suelen tener su propio sistema operativo, lo cual les <mark style="background: #FFF3A3A6;">permite realizar varias funciones con uso intensivo de los recursos al mismo tiempo</mark>. 
```
```ad-warning
title:Kernel
collapse:
- Con un contenedor, la aplicación está en un espacio aislado dentro de las funciones de aislamiento que proporciona un contenedor, pero aún <mark style="background: #FFF3A3A6;">comparte el mismo [[kernel]] que otros contenedores en el mismo host.</mark> Como resultado, <mark style="background: #FFF3A3A6;">los procesos que se ejecutan dentro de los contenedores son visibles desde el sistema host</mark>.
- Con una máquina virtual, <mark style="background: #FFF3A3A6;">todo lo que se ejecuta dentro de la VM es independiente del sistema operativo host o hipervisor</mark>. La plataforma de máquina virtual inicia un proceso (monitor de máquina virtual) para administrar el proceso de virtualización para una VM específica, y el sistema host asigna algunos de sus recursos de hardware a la VM. Sin embargo, lo que es fundamentalmente diferente con una máquina virtual es que, <mark style="background: #FFF3A3A6;">en el momento del inicio, inicia un kernel nuevo y dedicado para este entorno de VM e inicia un conjunto (a menudo bastante grande) de procesos del sistema operativo.</mark>
```
```ad-warning
collapse:
title: Recursos
* Virtualización: El software llamado <mark style="background: #FFF3A3A6;">hipervisor separa los recursos de las máquinas físicas para que puedan dividirse y destinarse a las máquinas virtuales</mark>. Cuando un usuario emite una instrucción de una <mark style="background: #FFF3A3A6;">máquina virtual que requiere recursos adicionales del entorno físico, el hipervisor transmite la solicitud al sistema físico</mark> y almacena los cambios en la memoria caché. <mark style="background: #FFF3A3A6;">Las máquinas virtuales parecen servidores físicos y actúan como tales, lo que puede multiplicar las desventajas</mark> de las dependencias de las aplicaciones y los grandes footprints del sistema operativo. Incluso, en la mayoría de los casos, ese footprint no se necesita para ejecutar una sola aplicación o microservicio.
* Contenedores: <mark style="background: #FFF3A3A6;">Los contenedores contienen un microservicio o una aplicación y todo lo que necesita para ejecutarse. Lo que está dentro de un contenedor se conserva en lo que llamamos imagen: un archivo basado en un código que incluye todas las bibliotecas y las dependencias.</mark> Estos archivos pueden considerarse una instalación de la distribución de Linux, porque la imagen viene con paquetes RPM y archivos de configuración. <mark style="background: #FFF3A3A6;">Como los contenedores son tan pequeños, suele haber cientos de ellos con un nivel de acoplamiento bajo</mark>, así que se utilizan plataformas de organización de contenedores para configurarlos y gestionarlos.
```
``````
````ad-danger
title: ## Estructura de un Dockerfile

```Dockerfile
FROM node:8.9-a1pine
ENV NODE_ENV production
WORKDIR /usr/src/app
COPY ["package.json","package-lock.json*","npm-shrinkwrap.json*","./"]
RUN npm install --production --silent && mv node_modules ../
COPY . .
EXPOSE 3000
MAINTAINER name
CMD npm start
```
<ul>
<li><b>FROM:</b> Especifica la imagen a usar como base</li>
<li><b>ENV: </b> Para crear una variable de entorno. Podemos acceder a los valores de ENV durante la compilación, así como una vez que se ejecuta el contenedor.</li>
<li><b>WORKDIR:</b> Especifica la carpeta de trabajo dentro del contenedor</li>
<li><b>COPY:</b> Copia los ficheros de origen en destino. Copia solo el package.json y package-lock.json</li>
<li><b>RUN:</b> Ejecuta el comando en el momento de la creación de la imagen</li>
<li><b>COPY:</b> Para agrupar el código adentro de la imagen de Docker</li>
<li><b>EXPOSE: </b>Informamos que el puerto que usa es el 8080</li>
<li><b>CMD:</b> Ejecuta el comando al ejecutar el contenedor. Inicia el archivo main.js</li>
</ul>

````
