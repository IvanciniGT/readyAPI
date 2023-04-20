# Pruebas de servicios REST 

## Qué es eso? de los servicios REST?

Basado en protocolo HTTP.

Es una petición a un aplicativo, que puede tener varios métodos.
Es una interfaz que interviene entre un core y una app.
Para recuperar datos o modificarlos.

## API REST?

API : Application Programming Interface

---

Antaño montabamos sistemas MONOLITICOS... esto nos daba muchos problemas.

Nos planteábamos una aplciación con un TODO. Una única unidad.

# WEB Loterias hace 20 años.

Aplicacion web que se ejecutaría en un servidor de aplicaciones:
Lenguaje: JAVA
Serv de aplciaciones: 
- Weblogic
- Websphere
- Tomcat *
- Jboss  *

Hace 20 años, me habría planteado la aplicación como un todo: Hablabamos de una app web

# WEB? 

Arquitectura para montar apps (lo crea Tim Berners Lee ... a finales de los 1990).
Se basa / utiliza INTERNET.
Internet es un conjunto de redes descentralizado. Que me sirven para mandar datos entre computadoras (pc, servidor, smartphone).
Sobre Internet ofrecemos o disponemos de servicios de distinta naturaleza. Uno es la WEB... Pero hay muchos otros:
- email (pop3, smtp, imap)
- iptv
- voz ip
- juegos

Para montar la WEB: Tim Berners Lee diseña: 
- Lenguaje HTML:                        Hyper text markup language
    Es un lenguaje pensado para seres humanos. Para representar información que sea visualizada/consumida por seres humanos
    <a> <html> <p> <b>(bold) <i>(italic) <table> <img> <ul>
    Esto se usa en combinación con lo que llamamos hojas de estilo CSS (estilos, como los del word)
- Protocolo de comunicaciones HTTP:     Hyper text transfer protocol

La web es una arquitectura CLIENTE - SERVIDOR. 

Servidor: Encargado de almacenar datos y gestionar esos datos
Cliente:  Nos ofrece una forma de acceder a los datos del servidor y a la gestión de los datos que nos hace el servidor.

Cliente: computadora                                                        otra computadora - servidor
            v                                                                       v
        navegador de internet <----------------mensaje-------------------->      aplicación     <> BBDD1
            Escribo una URL                                                       (java)        <> BBDD2
            https://loterias.es/premios/hoy 
                    Para que el servidor y el cliente puedan hablar necesitamos:
                        - Un lenguaje: HTML
                        - Un protocolo: HTTP

Hace 20 años, la app que tenía en el servidor se encargaba de todo:
- Gestionaba una BBDD
- Con sistemas de mensajería y notificaciones (email)
- Se encargaba de generar el HTML que se envíaba a los clientes (navegadores)

Desgraciadamente o no... el mundo ya no es igual que hace 20 años... Y hoy en día... 
Accedemos a la información (consumimos recursos) desde navegadores WEB? SI
Pero solo? NO
Desde qué otras fuentes accedemos a recursos en servidores?
- Aplicaciones de teléfonos móviles
- Aplicaciones de Smart TVs
- Asistentes de voz: Alexa, OK Google, Siri

Que mandaba antes (hace 20 años) un servidor cuando le pedía un dato: Dame el resultado del sorteo de HOY !?
Un HTML, que estaba pensado para su representación gráfica en un navegador... y que un ser humano lo viera con sus OJITOS !!!!

Y a la ALEXA... esa me muestra las cosas por los ojitos???? NOP por los oiditos !
Y el teléfono... ese si por los ojitos.. pero de una forma diferente

Sigue sirviendo que la applicación que está en el servidor me mande datos en HTML? NO... al menos SOLO NO
YA que no consumo datos SOLO desde un navegador de Internet.

Necesitamos de otros lenguajes para que los servidores nos manden INFORMACION: XML, JSON

El servidor (las aplciaciones que ponemos ahí) vamos a hacer que generen información PARA CUALQUIER TIPO DE DISPOSITIVO: Movil, Navegador PC, SmartTV, Asistente de voz
Eso nos implica un formato NEUTRO de transmisión de información

Pero el punto es que en el servidor NO QUIERO 800 veces el mismo PROGRAMA....
- Programa para saber qué numero ha sido el ganador hoy en la loteria en HTML
- Programa para saber qué numero ha sido el ganador hoy en la loteria en audio
- Programa para saber qué numero ha sido el ganador hoy en la loteria en XML

TE hago UN SOLO PROGRAMA.

Ese programa (servicio) será consultado por otros programas: Programas de FRONT END
- App de un teléfono movil
- App de un smart TV
- Asistentes de voz
- Programa en JS que genera en un navegador de internet un documento HTML

Para ese programa necesitaré definir un protocolo de COMUNICACION... Pues ya tengo uno que usaba antes: HTTP, lo usaba en el mundo WEB.
Esos servicios que usan el protocolo HTTP los llamamos "servicios WEB"

Igual que antes manaba ficheros HTML y tenía un protocolo especializado en mandar ese tipo de archivos HTTP,
Hoy en día, para mandar datos en formato neutro hemos adoptado:
- XML       --->            SOAP (Protocolo para arquitecturas orientadas a servicios)
- JSON      --->            REST (Transferencia de estados representacional)<- Este no es un protocolo
                            ^  ^                                               Son restricciones sobre la
                          XML  YAML                                            forma en que usamos el procolo HTTP 
## API REST

API: Application Programming Interface

Interfaz? Forma de comunicarme con un sistema informático para conseguir que ese sistema haga lo que necesito.
- Necesito el número de la loteria de hoy!
- Apunta el número de la loteria de hoy!
- Borra los números de hace 5 años!
- Me he equivocado.. y te pasé mal el dato del ganador... cambialo por este otro.
- Avisame cuando salgan los resultados del nuevo sorteo

El conjunto de todas las operaciones que puedo pedir a un sistema informático, junto con la forma de pedirlas es lo que llamamos un API.

Un API REST es una forma de comunicarme con un sistema a través de peticiones basadas en protocolo REST (que no es tal protocolo... sino unas restricciones sobre HTTP)

## API RESTful

Esto es un API REST... en el cuál el servidor no almacena información de la secuencia de peticiones que se han ido realizando. NO SE GUARDA INFORMACION DE ESTADO !

Antiguamente, cuando montábamos una aplicación, y esa aplicación se montaba como un todo en el servidor...
Y en el servidor íbamos generando el HTML que se mandaba a cada cliente, en el servidor se iba recopilando 
información acerda del estado de una coneción de un cliente:

1- El cliente desde un navegador hace login... Y esa info se guarda en el servidor... que tal persona está conectada
2- El cliente aprieta el formulario de búsqueda y rellena en el campo fecha el día de hoy
  Y esa información se anota en el servidor... que tal persona que está conectada ha realizado esa búsqueda
...
De forma que si persona en un momento dado:
4- Vuelve al formulario de búsqueda, el servidor, como sabe que ha hecho una determinada búsqueda (el resultado del sorteo del día de hoy), por defecto ya le genera un HTML con ese dato relleno.
  Eso lo puede hacer gracias a que el servidor va controlando/registrando TODAS LAS OPERACIONES que va haciendo un cliente. El servidor GUARDA INFORMACION DEL ESTADO DE UNA CONEXION

Hoy en día, las aplciaciones NO FUNCIONAN ASI. Hacemos que el servidor NO GUARDE todo ese tipo de información... Esa responsabilidad la delegamos en las aplicaciones de FRONTEND (app del telefono movil, en la app del navegador...etc)
Descargamos el servidor.

---

Un servicio REST es un programa que tengo en un servidor, al que llamos siguiendo protocolo HTTP + algun protocolo o restricciones adicionales (SOAP + REST). 
Hago una petición... y obtengo una respuesta. 
Al hacer la petición a una URL (dirección) puedo enviar ciertos datos si se requieren(body) y sus correspondientes metadatos (header), entre los cuales destacan el CONTENT-TYPE y el METODO HTTP(GET, POST, PUT, DELETE, HEAD).
El programa, alojado en un servidor, ofrecerá una respuesta, que contendrá:
- Un body: si es que tiene que devolver algo
- Y unos metadatos, entre los que destacan:
    - El content-type, indicando el tipo de información que se ha devuelto
    - El return code (status code) que indica el éxito de la operación:
      - 2XX OK
      - 3XX REDIRECCION
      - 4XX ERROR CLIENTE
      - 5XX ERROR SERVIDOR

Un API REST es el conjunto de todas las funcionalidades (programas) que se ofrecen por un sistema

---

## Pruebas que vamos a hacer sobre esos APIs REST/RESTful

??

## Pruebas de software

En función del nivel de prueba:
                            OBJETIVO:                                       CUANTAS QUIERO HACER?
- Unitarias                 Comprobar un elemento de forma AISLADA          Montonones: al menos 1 por cada elemento
                            Elemento:
                                - función
                                - BBDD
                                - componente web
                                - servicio rest
- Integración               Comprobar la comunicación entre elementos       Montón... Al menos una para cada comunicación
- Sistema (End2End)         Comprobar el comportamiento de un sistema       Menos
                            en su conjunto
  - Aceptación              Las que me piden                                Las que sean... pero serán pocas


Esa clasificación va en paralelo con esta otra: 
- Pruebas estáticas         Las que no requieren poner el sistema en funcionamiento para realizar la prueba:
                                - Revisión de calidad de código: DESARROLLADOR SENIOR -> AUTOM -> SONARQUBE
                                - Revisión de requisitos -> TESTER
                                    REQUISITO OPCION A: El sistema debe dar unos tiempos de respuesta aceptables!      MIERDULI !!!!! 
                                    REQUISITO OPCION B: El sistema debe tardar menos de 200ms en contestar una petición MIERDULI !!!!
                                    REQUISITO OPCION C: El sistema instalado en un entorno con estas características,
                                                        cuando está sometido a ESTA CARGA DE TRABAJO,
                                                        responderá el 95% de las peticiones en menos de X ms...         GUAY !!!!
- Pruebas dinámica
  - Pruebas funcionales       Comprobar el correcto funcionamiento del ???
  - Pruebas no funcionales
      - Rendimiento                 Tiempo en hacer una operación
      - Carga                       Cuanta carga soporta puntualmente un sistema
      - Estres                      Como se comporta el sistema: DEGRADACION
                                  - Según pasa el Tiempo
                                          ^
                                  - Según se cargan más y más datos
      - Seguridad
      - Alta disponibilidad
      - Experiencia de usuario

---

Antiguamente haciamos las pruebas a MANITA !!!!!
Y esto vale a día de hoy? NO vale! hay algunas que nop me queda más remedio... pero en general ... no me vale!

Por qué digo que no nos vale...
Bueno... la razón es sencilla: Los desarrolladores han cambiado la forma en la que montaban una aplicación... Y vamos con ellos de la mano. Y ese cambio nos afecta.

Antiguamente, los desarrolladores usaban METODOLOGIAS EN CASCADA (WATERFAL). Cuantas veces se hacían las pruebas? 1 vez... al acabar el desarrollo

Hoy en día trabajamos con METODOLOGIAS AGILES ! (SCRUM, XTREME PROGRAMMING...): agilemanifesto.org

METODOLOGIA AGIL = Vamos a entregar el producto de forma INCREMENTAL

A los 15 días del inicio del proyecto, ya hay una versión en producción del mismo
    10% del sistema (una triste pantalla de login)          pero 100% funcional
        Aquí necesito hacer PRUEBAS ... pero PRUEBAS DE PRODUCCION !!!! de las buenas !
        Aquí que pruebo?        el 10% del sistema

A los 30 días del inicio del proyecto, ya hay otra versión en producción del mismo
    +5% del sistema                                         pero 100% funcional
        Aquí necesito hacer PRUEBAS ... pero PRUEBAS DE PRODUCCION !!!! de las buenas !
        Aquí que pruebo?        el 5% nuevo + 10% anterior... que he tocao código... a ver si me he cargado algo

A los 45 días del inicio del proyecto, ya hay una versión en producción del mismo
    +5% del sistema                                         pero 100% funcional
        Aquí necesito hacer PRUEBAS ... pero PRUEBAS DE PRODUCCION !!!! de las buenas !

A los 60 días del inicio del proyecto, ya hay una versión en producción del mismo
    +10% del sistema                                         pero 100% funcional
        Aquí necesito hacer PRUEBAS ... pero PRUEBAS DE PRODUCCION !!!! de las buenas !

Metodología TDD:
Donde el tester primero diseña las pruebas, se las pasa al desarrollador y el desarrollador las va ejecutando hasta que las pasa.
....
Y llegará un momento en que te haya entregado el producto entero

Esto nos permite tener una retroalimentación ULTRARAPIDA

Las metodologías ágiles nos han resuleto un problemón, con los requisitos cambiantes y el feedback del proyecto.
Pero han traido sus propios problemas de la mano:
- Qué pasa con las pruebas? Se multiplican... y además son repetitivas
Y tengo pasta para ello? Ni de coña! 
Este problema SOLO TIENE UNA SOLUCIÓN: AUTOMATIZAR LAS PRUEBAS (al menos TODO lo que pueda ser automatizado)

---


# Protocolo?

Es un conjunto de reglas.

## Protocolos de comunicación

Es un conjunto de reglas que posibilitan una comunicación.

## Comunicación entre 2 interlocutores:

### Ejemplo 1

EMISOR    ---->      mensaje   --- canal de comunicación ----->     RECEPTOR
               (idioma o lenguaje)

Y aquí falta una cosa: PROTOCOLO

Comunicación con un amigo a través de un walky-talkie: PROTOCOLO: 
CAMBIO: Ahí se entiende que yo ya no voy a hablar más... y mi compañero puede comenzar a hablar
CORTO y CAMBIO: Ahí se entiende que YA HE TERMINADO DEFINITIVAMENTE 

### Ejemplo 2

Pido un poster del Mandaloriano!!!!! a Amazon.

ALMACEN DE AMAZON   -- mensaje(poster del mandaloriano) -->        MI CASA
EMISOR                                                             RECEPTOR
Navegador de internet                                              aplciación alojada en un servidor

Canal de comunicación:  Vehículo que viaja por una Carretera
                        Internet

Protocolo: Hay varios:
- Controlar el tráfico de datos: Reglas de circulación por carretera: Vehiculo: Semaforo, rotonda, ceda el paso
                                 TCP/IP:                              Paquetes se mueven sobre una red
- Empaquetar los datos que quiero mandar: El poster viene en una caja: Por qué?
                                            - Proteger los datos (poster) - Asegurar la integridad del poster
                                            - Proteger mi identidad y el contenido
                                            - La caja da opción de añadir una etiqueta, pegadita por fuera, con información adicional (meta-datos)
                                              - Mi horario
                                              - Dirección
                                              - Fragil
                                              - Peso
                                              - Si es contra reembolso
                                          HTTP... es igual que cuando AMAZON mete el poster en una caja
                                          Nuestro dato que mandamos en ese ejemplo en un fichero HTML
                                            El fichero se mete en una caja: BODY 
                                            Y en la caja, por fuera, se le pone una pegatina, con metadatos:
                                            En HTTP es lo que llamos los HEADERS

                                    

# URL?

El equivalente a la Dirección

Uniform Resouce Locator

Me permite identificar un recurso... en un servidor

# Estructura de una URL
                                                    context
                                                    endpoint        parámetros
protocolo       ://     servidor        : puerto    /path       ?   queryString
http                    dominio             80
https                                      443
                                                    ^ Dentro de un servidor, me idenditifica un recurso, programa, página web


https  ://    www.google.es  :443   /search      ?
                                                    q=hola+felipe 
                                                    
# HTTP

Es un protocolo de comunicación síncrona entre un cliente y un servidor.

Se basa en el concepto de REQUEST y RESPONSE

Es un protocolo de comunicaciones   síncrono:   llamada por teléfono, donde el receptor (servidor) tiene que
                                                estar presente en el momento de la comunicación
                                    asíncrona:  whatsapp

El emisor(navegador) emite un REQUEST (una petición)
El receptor(apliación en un servidor) emite un RESPONSE (una respuesta)

El REQUEST se hace contra una URL (dirección)
    Y en ese request mando una CAJA (body), que tendrá o no cositas dentro (datos de login, el término que busco en google, el tipo de poster que quiero en amazon)
    Y además, pegado por fuera de la caja, mandamos una pegatina con metadatos: HEADERS
    - METODO HTTP: Esto es como si en un paquete que mando a una empresa pongo: PARA REPARAR, PARA DEVOLVER
        - GET       Quiero que me des algo a cambio de mi petición (REQUEST)
        - POST      Quiero mandarte algo
        - DELETE    Quiero que borres algo
        - PUT       Quiero mandarte algo (similar al POST)... para que lo modifiques
        - HEAD      Quiero saber si lo que te pregunto EXISTE -> SI o NO
    - CONTENT_TYPE: Tipo de cosa que va dentro de la caja... si es que va algo dentro de la caja
                    - text/html
                    - application/json
                    - application/xml
                    - application/form-data
    - SIZE (length)... equivalente en el paquete de amazon al PESO DEL PAQUETE
    Puede ser que mande la caja vacía de IDA... en el request

El SERVIDOR cuando contesta: RESPONSE , también manda UNA CAJA, con un contenido: BODY
    Y una pegatina por fuera con metadatos: HEADERS... entre ellos destaca:
    - RESPONSE CODE
      - 2XX         OK
      - 3XX         Redirección
      - 4XX         Error de cliente / error en petición
      - 5XX         Error de servidor -> BUG en la aplicación, se ha caido la BBDD... 

## Herramientas de automatización de pruebas de servicios web:

- Postman
- SoapUI
- ReadyAPI
- JMeter
- LoadRunner
- Cypress
- Karate

---

# DEV --> OPS

Filosofía, Cultura, Movimiento en pro de la AUTOMATIZACION!

# Integración Continua! C I

Voy a tener continuamente en el entorno de integración la última versión que hagan los desasrrolladores sometida a pruebas automatizadas.

Entornos de trabajo:
- desarrollo
- integración - testing - pruebas - preproducción
- producción

# Entrega Continua - C Delivery

Poner en manos de mi cliente la última versión probada de mi sistema DE FORMA AUTOMATICA 

# Despliegue Continuo - C Deployment

Donde ya instalo en producción en automático sin mediación humana.
Nadie haciendo pruebas, nadie instalando el sistema . No hay gente que intervenga en el proceso


---

# JSON

JavaScript Object Notation

```js
var numero = 7;
var texto = "hola";
var logico = true;
var listas = [1,2,3];
var mapa = {
    "clave1": "valor1",
    "clave2": "valor2"
};
```


"hola" es JSON
true es JSON
7 es JSON

# Estructuras de almacenamiento de información:

Cola
Array
Matriz
Pila - Stack
Arbol, lo podeis asemejar a la estructura de directorios que veis en el explorador de archivos de windows
Mapa

# JSON

Un documento JSON es un ARBOL
```json
3                               Número
```

```json
true                            Lógico
```

```json
[                               Lista / Array
    "item1",                     |- Texto
    "item2",                     |- Texto
    "item3"                      |- Texto
]
```


```json
{                                Mapa / Diccionario / Array asociativo / Objeto: Conjunto de datos identificados por claves
    "nombre": "Ivan",                     |- Texto
    "edad": 44,                           |- Número
    "hijos": true,                        |- Lógico
    "padres": [                           |- Lista 
        "Isidoro",                              |- Texto
        "Maria de los Angeles"                  |- Texto
    ]
}
```

En JSON, en YAML, en XML, en todos ellos aparece un concepto: ESQUEMA
Los esquemas nos permite definir la estructura que tiene un documento.

Cuando recibimos un documento JSON, en algunos casos me plantearé extraer información de él. Cuándo me puede interesar eso?
- Para trabajar con él
- Para hacer una modificación sobre él
- Porque lo uso en una prueba futura
- Porque quiera establecer una validación sobre él

Para sacar un dato concreto de un documento JSON, usamos un lenguaje JSONPath
Para sacar un dato concreto de un documento XML,  usamos un lenguaje XPath


```yaml
nombre: Ivan
edad: 44
hijos: true
padres:
    - Isidoro
    - Maria de los Ángeles
```

```xml
<persona>
    <nombre>Ivan</nombre>
    <edad>44</edad>
    <hijos>true</hijos>
    <padres>
        <padre>Isidoro</padre>
        <madre>Maria de los Ángeles</madre>
    </padres>
</persona>
```

# JSON PATH

Signos y expresiones que usamos:
    $     Representa el nodo raiz del documento
    .     Me permite bajar un nivel en la jerarquía y tomar un hijo
    ..    Me permite bajar todos los niveles que sean necesarios en la jerarquia
    []    Me permiten elegir elementos de listas. Dentro pondré el NUMERO del elemento que quiero sacar, comenzando en 0
    [1:3] Quiero del segundo al cuarto(no incluido)
    [:3]  Quiero hasta el cuarto(no incluido)
    [1:]  Quiero desde el segundo en adelante incluido
    [0,2] Quiero el primero y el tercero
    *     Cualquier dato



{
    "nombre": "Ivan",
    "edad": 44,
    "hijos": true,
    "padres": {
        "padre": {
                    "nombre": "Isidoro",
                    "edad": 72
                },
        "madre":{
                    "nombre": "Angeles",
                    "edad": 65
                }
    },
    "telefonos":[
        {
            "tipo": "fijo",
            "numero": "911111111"
        },
        {
            "tipo": "movil",
            "numero": "667788998"
        }
    ]
}

---

# SWAGGER

Es una herramienta que nos permite documentar fácilmente apis rest

Primero escribo la documentación -> esqueleto del codigo que necesita el desarrollador
Escribo el código -> genero la documentación en formato swagger

El tener un documento swagger, generado de cualquier forma, en general TODOS los programas
de pruebas automatizadas de servicios y APIs REST son capaces de leer ese fichero y 
generarme un monton de pruebas en base a lo que ahi esté definido


---

QUIERO AÑADIR FUNCIONALIDAD A MI SISTEMA: Al año de tener la tienda en funcionamiento... vamos bien !!!!
- Ahora los animalitos pueden tener asociados VIDEOS !

                                                Tienda de mascotas ANIMALES MAGICOS®

test de pruebas de los servicios REST V1  ->>>>>>>>>>>>>>>>> Modificar estas pruebas
        vvvvvv
test de pruebas de los servicios REST V2  ->>>>>>>>>>>>>>>>>

animalesmagicos.comV2                                                            SERVIDOR                       BBDD
                                                                                                                Las mascotas en venta
                                                HTTP                             Servicio REST                      - nombre
app telefonos AndroidV2       ----> REQUEST  ----->                              - mascotasDisponiblesV1.0.1   >    - tipo
AnimalesMagicos PlayStore!           (URL)         <------ RESPONSE ------                                          - fotos
                                     metadatos          datos de las mascotas (JSON, XML)                           - videos
                                      METODO: GET              
app telefonos IOS                                                                - mascotasDisponiblesV2*
Animales Magicos AppleStore!                        <------ RESPONSE ------
                                                            datos de las mascotas + videos
Alexa


App De escritorio(V2), que usan los dependientes de la Tienda                       - altaDeMascotaV2
- Consultar animales? SI                            <----- RESPUESTA -------
- Añadir animales?    SI    -------> REQUEST ----->             Cómo ha ido: Return Code (Status Code) 200
                                      (URL)                     Me podría devolver por ejemplo el ID
                                      metadatos:                Me podría devolver todos los datos junto con el ID
                                       METODO: POST
                                      datos del animal (JSON, XML)
                                      nombre, tipo, fotos
                                        +videos

- Cambiar las fotos de una mascota? SI 
        Metodo PUT
                                                                                API REST : Es el conjunto de TODOS ESOS SERVICIOS !
------
Ver las mascotas
De cada mascota quiero:
- nombre
- tipo
- fotos


---

## Sobre las URLs en las APIs REST

URL:  protocolo     ://     dominio/servidor    : PUERTO        /endpoint
        http                                        80
        https                                      443

### Los endpoints en APIs REST

Se intentan normalizar mucho

Por ejemplo, si queremos trabajar con mascotas, podriamos usar el endpoint /api/v1/pet
Por ejemplo, si queremos trabajar con UNA mascota, podriamos usar el endpoint /api/v1/pet/{id de la mascota}

http://servidor.animalesmagicos.com/api/v1/pet

    GET : Pedir las mascotas
    POST: Añadir una mascota

http://servidor.animalesmagicos.com/api/v1/pet/17

    GET:    Dame los datos con detalle de esa mascota
    PUT:    Modificar los datos de la mascota
    DELETE: Borrar la mascota
    HEAD:   Si esa mascota existe en la tienda


---

# Gestión de APIs

# MICROSERVICIOS

JAVA - SPRINGBOOT -> SWAGGER POR CADA SERVICIO
                     SWAGGER GLOBAL



                    Programa / Servicio REST
                        listadoDeMascotas               Desarrollador
                            GET /v1/pets
                                Devuelve unos datos

Cuánta gente hay ahora mismo consumiendo este programa?     Ni idea ! lo que hayan
Para ese programa, que los desarrolladores han liberado, desde el departamento de Q&A hacemos unas pruebas AUTOMATIZADAS:

                                                                              JENKINS < Integración Continua
                                                                                 V
    Realmente no estamos haciendo PRUEBAS ... qué es lo que estamos haciendo? PROGRAMA que prueba los servicios 
        Me temo... que sin daros cuenta... os han cambiado el contrato...
            Donde ponía TESTER o QA
                ahora pone PROGRAMADOR 
    Y en mis pruenas.... no he detectado ningún problema... todo parece OK. PREGUNTA? Tengo garantizado que el sistemna esté libre de errores? NUNCA ESTA LIBRE DE ERRORES 

                        listadoDeMascotas               Desarrollador
                            GET /v2/pets
                                Devuelve los datos de antes y algunos más y otros menos

Desde testing... qué hacemos? 
    Modifico los programas de pruebas que tengo? NI DE BROMA ! NUNCA ! JAMAS !

    Yo tengo ahora OTRO PROGRAMA QUE PROBAR, el programa en V2.... y lo debo tratar A TODOS LOS EFECTOS como un programa nuevo!
    Por qué?

    Bueno... porque ni los desarrolladores ni los tester somos perfectos y nos equivocamos. TODOS!

    Cuanta gente está consumiendo la versión v2 del programa? Nadie.... y dentro de un mes? Ni idea ! lo que hayan

# VERSIONES

2.0.0
1.2.3

1: MAYOR        Se incrementa cuando se hacen cambios que pueden implicar NO RETROCOMPATIBILIDAD
2: MINOR        Se incrementa para añadir funcionaldiad
3: MICRO        Se incrmenta para arreglar un bug


---
Cuando nos incrementa MAYOR, debemos tratar el proyecto de pruebas como si fuera uno nuevo!
Yo ya no tengo un único proyecto de pruebas, tengo 2 proyectos de pruebas: V1 -> V2, que debo mantenerlos por separado!

1.2.3
1.2.4           API V1
2.0.0
2.0.1           API v2

----
1.2.3
    funcionalidad A que marco como obsoleta. Si yo quito esa funcionalidad -> MAYOR
2.0.0

El problema es que ante estas situaciones... No es tan sencillo modificar el proyecto de pruebas

1.2.3
1.2.4
        Se ha arreglado un bug... Y básicamente mis pruebas no habría ni que tocarlas....
        O quizás si... para meter el caso de pruebas que se me pasó.
1.3.0   
        Se ha añadido funcionalidad -> Nuevas pruebas
2.0.0
        Esto es locura! me pueden haber quitado cosas, renombrado cosas, añadido otras.
        Qué podré reaprovechar? Habrá que verlo... pero ya no es evidente el escenario.

---
En ReadyAPI lo primero será definir un API
Una vez tengamos el API, comenzaemos a hacer pruebas:
- Funcionales
- Rendimiento
- Seguridad

----
MOCK-> Simulador

En readyAPI podemos crearnos un simulador de un servicio:
    http://localhost:9999/api/v1/animalitos
        GET
            Devuelves este JSON {}

Esto a nosotros nos vale de algo?

---
                                                Tengo que probarlo... o yo soy mejor y cometo menos errores que los desarrolladores
                                                vvvv
Nosotros estamos montando un programa        -> Programa que prueba el API
    Les exijo que su programa lo metan en un sistema de control de versión
    Les exijo que pasen unas pruebas -> Les convencí de que hacer pruebas les ayuda, tardan menos, tienen menos problemas <<<<
    Les pido pruebas unitarias, y luego de integración

Igual que los desarrolladores montan el suyo -> API
    Les exijo que su programa lo metan en un sistema de control de versión
    Les exijo que pasen unas pruebas -> Les convencí de que hacer pruebas les ayuda, tardan menos, tienen menos problemas <<<<
    Les pido pruebas unitarias, y luego de integración
---

El punto no es si tengo facilidad o no para acceder a datos.
Ni si puedo probar mi programa contra datos reales.

---
Dentro de ReadyAPI, tenemos al trabajar el concepto de Entornos:
Sería un reflejo de mis entornos dentro de la empresa:
- Producción. El entorno donde se ejecuta un software para su cometido real   <-> El entorno de Integración del API
                                                |-> Mi proyecto de pruebas
- Integración / Pruebas
- Desarrollo. El entorno donde los desarrolladores van creando y jugando con su código
                                        |-> Los testers ---> Quiera pruebas unitarias : Entorno donde trabajar con MOCKS
                                                                                        Virtual services



---
Doy de alta un animal
    ---> Me devuelven el id 27

             Pido el animal 27
                 ---> Me devuelven ? el que? El 43?

---
Estamos haciendo un caso de prueba:

Recuperación de un animal? BIEN
    GET

Alta y recuperación de un animal
    POST    x       Se ha guardado el contenido en la BBDD? 
        Al desarrollador se le volvido poner                        pet.save() <<< PROBABILIDAD? ALTA !

        POST ----> MANDA DATOS (RAM) ----> Programa (RAM)       -----> BBDD
                        <---- datos                                     ^
                                                                        |
    GET -----------------------------------------------------------------

Para que sirven las pruebas?
- Para comprobar si algo está bien o No <- Validar el cumplimiento de un requisito
- Valorar la calidad de un producto
- Identificar problemas en el desarrollo / equipo de desarrollo. Carencias, Situaciones anómalas
- Aportar luz sobre un problema (defecto)

errores:    sometidos por seres humanos
defectos:   Al cometer un error introducimos un defecto en un producto          <<< Intentamos identificar
fallos:     Ese defecto puede manifestarse en forma de error ... o no           *** A través de los fallos que producen

Y me interesa hacer un análisis de causas raices: ERRORES

Quien identifica un defecto?                        DESARROLLO
Como se llama el proceso de identificar defectos?   DEBUG

Nosotros buscamos FALLOS -> Para que los desarrolladores puedan hacer debug e identifiquen DEFECTOS

Mi trabajo como tester es, CUANDO IDENTIFICO UN FALLO, intentar aportar LUZ para que desarrollador pueda identificar el DEFECTO: Guardamos log, capturas de pantalla

----

Tu estás haciendo un programa para probar un API

Pero tu tienes que probar tu programa que funciona.

Y lo pruebas contral el programa que no sabes si funciona que quieres probar? 

Estás probando tu programa de pruebas contra el API que no sabes si funciona y por eso lo quieres probar con tu programa

Yo hago mi programa, lo pruebo en un entorno QUE SE QUE FUNCIONA (mi virtual service)
Y ahora que tengo garantias de que mi programa funciona, lo ejecuto sobre el API, que no se si funciona, para saber si funciona !


---

Update -> Micro / Minor
    Nuevos servicios, Nuevos métodos y nuevos parámetros

    Tan solo modifica el API
    No toca las pruebas, las deja como están

Refactor -> Mayor
    pet (DELETE)  ->  pet(DELETE)
    Cambios
        pet -> mascota
        pet (POST) -> pet (PUT)
        pet?id=   -> pet?petId=
    Bajas
        x /pet/findByName 

    Modifica el API
    Pero además modifica las pruebas
        Si yo soy capaz de decirle, que lo que antes estaba probando pet(POST) -> pet(PUT)

    Siempre antes de hacer un refactor -> Nueva rama en git


----

Herramienats tipo Jenkins: Servidores de automatización

Jenkins lo que hace es ejecutar nuestro proyecto de pruebas.
Solo que a Jenkins le puedo meter disparadores!



Desarroladores van a coger y suben su código a un sistema de control de versión: GITHUB

Por nuestro lados, nuestros programas de pruebas -> proyecto READYAPI -> GITHUB

En ocasiones tanto pruebas como el proyecto principal se meten en el mismo repo
En ocasiones se meten en repos separados

REPO de GIT 

En GIT generamos un REPOSITORIO, que es una BBDD donde guardamos FOTOGRAFIAS DEL PROYECTO: COMMITs
Los commits a su vez se guardan en RAMAS dentro del REPOSITORIO
cada RAMA me permite controlar una linea de evolución PARALELA EN EL TIEMPO

MERGE


CADA PERSONA DEL PROEYCTO TIENE SU PROPIO REPOSITORIO con sus cosas.
Y hay que compartirlas. Para ello usamos REPOSITORIOS REMOTOS

PUSH    Mandar mis fotos a un REPO REMOTO
PULL    Descargar las fotos que otros han puesto en un repo REMOTO

---

En Jenkins creamos un PIPELINE -> PROGRAMA de automatición y orquestación de tareas

Le pediremos a Jenkins en ese pipeline que:
PIPELINE 1: compilar-api-loteria
    1- Se haga con una copia de lo que hay en un REPO de git DE LOS DESARROLLADORES
    2- Le pediré que compile ese codigo
    3- Le pediré que lo pase por un SONARQUBE
    4- Lo instalaré en el servidor de INTEGRACION/TEST
PIPELINE 2: probar-servicios-rest
    5- Se haga con lo que hay en el repo de GIT de los testers
    6- Que ejecute las pruebas que ahi haya definidas

---
Por un lado un servidor de JENKINS


JENKINS <- Plugin READYAPI + READY API (+licencia)
   V
   Pipeline (Tarea) -......-> Ejecutar unas pruebas con READY API


python -> groovy -> java

---
Antiguamente en git se trabajaba con la rama MASTER
Esa rama es muy importante y tiene regla de oro: EN ELLA NO SE PONE NADA QUE NO ESTE LISTO PARA PRODUCCION

MASTER (tiene connotaciones ESCLAVISTAS: MASTER - SLAVE) -> MAIN

GITHUB: USA MAIN
READY API: USA MAIN
GIT: Master
Jenkins: Master