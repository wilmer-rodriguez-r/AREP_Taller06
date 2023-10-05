# AREP_Taller06

Este taller trabajaremos con una maquina virtual desplegada en AWS, donde construiremos una miniarquitectura con ayuda de docker.

Se dividio el proyecto en dos partes, la primera es la que se presenta en este repositorio que es la fachada, mientras que la otra se encuentra alojada en el siguiente [repositorio](https://github.com/wilmer-rodriguez-r/AREP_Taller06Logs.git) y corresponde a nuestra api que conecta a base de datos.

## Iniciando

### Prerrequisitos

* Git 
* Java
* Maven
* Docker

### Instalando el proyecto

Lo primero será traer del repositorio remoto el proyecto a la máquina local, para esto ejecutamos el siguiente comando por medio de consola.

```
git clone https://github.com/wilmer-rodriguez-r/AREP_Taller06.git
```

Esto creará un directorio nuevo, en el cual ejecutaremos nuestro proyecto.

### Corriendo con Docker

En la carpeta de este proyecto se econtrara el archivo docker-compose.yml.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/0b1d74e6-f9b9-4541-857f-c26fe65af568)

Como se puede ver en este archivo, se crea una instancia de la fachada, tres de logservices que es la api y una instancia de mongo. Las imagenes se encuentran en docker hub y se pueden ver en los siguientes enlaces:

  - Fachada: https://hub.docker.com/repository/docker/wilmerrodriguez/arep-facade/general
  - Logservices: https://hub.docker.com/repository/docker/wilmerrodriguez/arep-logservices/general

Para construir las imagenes anteriores en nuestro computador debemos ejecutar los siguiente comandos.

```
docker run -d -p 34000:6000 --name facadaweb wilmerrodriguez/arep-facade
````

```
docker run -d -p 34000:6000 --name logservice wilmerrodriguez/arep-logservices
````

#### Corriendo localmente

Si desea correr localmente el proyecto puede ejecutar el siguiente comando que construira el docker-compose.

```
docker-compose up -d
```

Esto le mostrara lo siguiente, lo que significa que esta trayendo las imagenes correspondientes para correr los contenedores.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/d4acbd6e-c645-4b0a-988f-a66d97d071a6)

En docker-desktop puede ver los contenedores corriendo.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/56bb868f-a28e-4a9b-8085-0e024b93786c)

Como se puede apreciar el contenedor "web" es el que nos interesa, para acceder a el de manera local toca ir al siguiente enlace http://localhost:34000.

#### Corriendo con AWS

Para poder correrlo en AWS, nos debemos asegurar que nuestra maquina virtual posea como minimo git y docker instalados, posterior a esto se debera traer el proyecto a la maquina con el comando del principio.

Al conectarnos con nuestra maquina por medio de ssh podemos ejecutar el mismo comando que hicimos de manera local para poder construir el docker-compose.

```
docker-compose up -d
```

Esto mostrara lo siguiente.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/c1587e93-4697-4e00-a59a-a17768bf1af5)

Para poder acceder a estos servicios debemos ver que dominio posee nuestra maquina.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/4bf07ca7-8b9a-4ebc-b67b-cc224fa9290c)

Al igual que de manera local nuestro servicio importante correra en el puerto 34000.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/81a4bef4-2d9b-4e44-a35f-eecd56016078)

### Desplegado

Cuando se ingresa al servidor web, podemos ver que se pueden agregar registros o consultarlos.

Si agregamos nuevos registros nos mostrara lo siguiente.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/68a01881-8cb0-423c-87c6-3f2fb4c57fd1)

Y al consultarlos, podemos ver que nos lista los que acabamos de añadir.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/0228517f-a62f-47c3-9649-c5912aa31689)

Este seria nuestra aplicación en funcionamiento.

## Diagrama de clases

Como se menciono en un principio nuestro proyecto se dividio en dos, la primera parte correspondería a al fachada que es la siguiente clase.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/4805e982-13a6-4fc3-9c24-f0dfd3168d61)

Esta además actua de balanceador de cargas para realizar la consultas a nuestra demas instancias.

Y las otras dos clases se encuentran en el siguiente [repositorio](https://github.com/wilmer-rodriguez-r/AREP_Taller06Logs.git), y posee las siguientes clases.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/8610e4f3-6be7-419b-ab64-fef8ec0b0b84)

La primera es la que ofrece los endpoints para el servicio de logs, mientras que la segunda es la que realiza la conexión a la base de datos. El contenido de estas clases es el siguiente.

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/c9cbc782-771e-4a0b-b79d-23cc4f289647)


![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/c0177ecd-d412-4583-87e3-87533517270a)


## Arquitectura

La arquitectura que se realizo fue la siguiente, si miramos con detalle el docker-compose, se puede ver que la fachada es el RoundRobin. Además de que desplegamos 3 instancias de logservices junto con una de mongodb. Todo esto se realizo tanto de manera local como desde la maquina de AWS para ver que nuestro proyecto desplegaba sin ningun problema

![image](https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/f8c2b31e-d0c9-4347-8f8e-71c3581fad31)

## Videos

Corriendo desde el docker local.

https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/f43d5b10-794d-4ac8-8e54-d7779a3e8083

Corriendo desde la maquina virtual.

https://github.com/wilmer-rodriguez-r/AREP_Taller06/assets/77862048/ec4766ba-1ec4-466c-8435-8b6be20704ae

## Construido con

* [Maven](https://maven.apache.org/) - Administrador de dependencias




## Version

1.0-SNAPSHOT

## Autores

Wilmer Arley Rodríguez Ropero - [wilmer-rodriguez-r](https://github.com/wilmer-rodriguez-r)

## Licencia

GNU General Public License family

## Agradecimientos

* Luis Daniel Benavides Navarro

## Referencias

[1] 	B. N. L. Daniel, "Introducción a esquemas de nombres, redes, clientes y servicios con Java," p. 18, 20 Agosto 2020.
