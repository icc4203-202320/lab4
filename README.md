# Proyecto 1.4 - Geolocalización en Aplicaciones Web Móviles

## Introducción a la Geolocalización

La geolocalización es una tecnología fundamental para desarrollar aplicaciones móviles que presentan utilidad a los usuarios cuando se encuentran en terreno. A través de la geolocalización el dispositivo móvil puede informar a las aplicaciones con un alto grado de precisión la ubicación del usuario, y ello permite que las aplicaciones puedan dar una interacción al usuario con mayor información sobre el contexto. Es decir, la geolocalización facilita el desarrollo de aplicaciones móviles sensibles al contexto del usuario. En el caso de una bitácora de viajes, como la de la aplicación Travel Log, la obtención de coordenadas GPS facilita que el usuario pueda ingresar sus publicaciones (_posts_) vinculadas a la ubicación actual en forma transparente y automática.

### Sistema GPS y localización

El Sistema de Posicionamiento Global (GPS, por sus siglas en inglés) es un sistema que permite determinar la posición de un objeto (una persona, un vehículo, un teléfono móvil, etc.) en cualquier parte del mundo. El sistema GPS se basa en una constelación de al menos 24 satélites en órbita alrededor de la Tierra. Estos satélites envían señales a los receptores en la superficie de la Tierra, y los receptores usan estas señales para determinar su propia posición. A continuación, explicaremos cómo funciona este sistema de coordenadas y posicionamiento:

Satélites GPS: Estos satélites orbitan la Tierra a aproximadamente 20,200 kilómetros de altura. La constelación de satélites está dispuesta de manera que en cualquier momento y en cualquier lugar de la Tierra, al menos cuatro satélites son visibles en el cielo.

Trilateración: La posición se determina usando un principio llamado trilateración. Básicamente, si se conoce la distancia entre un sujeto y tres puntos en el espacio, se puede determinar la posición exacta del sujeto. Cada satélite envía una señal que incluye la hora exacta en la que fue transmitida y la posición del satélite. El receptor compara la hora de transmisión con la hora de recepción para determinar cuánto tiempo tardó la señal en llegar. Con esta información y la velocidad de la luz, el receptor puede determinar la distancia exacta entre él y el satélite.

Coordenadas: Una vez que el receptor GPS ha determinado su distancia con respecto a al menos cuatro satélites, puede determinar su posición en un sistema de coordenadas tridimensional. Las coordenadas resultantes se expresan generalmente en latitud, longitud y altitud.

* Latitud: Es el ángulo entre cualquier punto y el ecuador. Los valores varían entre -90° (Polo Sur) y 90° (Polo Norte).
* Longitud: Es el ángulo entre el meridiano principal (Greenwich) y el punto en cuestión. Puede variar entre -180° y 180°.
* Altitud: Representa la altura sobre o bajo el nivel del mar.
* Correcciones y precisiones: Diversos factores pueden afectar la precisión del GPS, como la atmósfera y las señales reflejadas (llamadas "multipath"). Para corregir estos errores, se puede usar el Servicio de Augmentación de Área Amplia (WAAS, por sus siglas en inglés) o sistemas similares que proporcionan correcciones en tiempo real.

Aplicaciones de uso: Además de determinar la posición, el GPS también puede ser usado para proporcionar la hora exacta. Esta capacidad se utiliza en muchas aplicaciones, desde la navegación para automóviles y barcos hasta la agricultura de precisión, la investigación científica, y más.

### ¿Cómo obtienen los _smartphones_ las coordenadas GPS?

Los _smartphones_ modernos utilizan una combinación de sensores y tecnologías para obtener las coordenadas GPS. La determinación de la posición a través de estas técnicas se llama posicionamiento GNSS (Sistema Global de Navegación por Satélite). GPS es el sistema GNSS desarrollado por Estados Unidos, pero hay otros sistemas similares en funcionamiento o en desarrollo, como GLONASS (Rusia), Galileo (Unión Europea) y BeiDou (China).

Los _smartphones_ obtienen las coordenadas GPS de la siguiente manera:

Receptor GPS: En su núcleo (SoC), cada smartphone tiene un receptor GPS integrado. Este receptor capta las señales de los satélites GPS que orbitan la Tierra. Como explicamos antes, el receptor necesita señales de al menos cuatro satélites para calcular una posición en 3D (latitud, longitud y altitud).

Trilateración: Al igual que los dispositivos GPS dedicados, los smartphones utilizan la trilateración para determinar la ubicación. Basándose en la señal de al menos tres satélites y conociendo su posición exacta y la distancia a cada uno, el smartphone puede determinar su ubicación en la superficie de la Tierra. La señal de un cuarto satélite se utiliza para corregir errores y determinar la altitud.

Asistencia A-GPS (GPS Asistido): Para acelerar la adquisición de señales de satélite (un proceso que a veces puede tardar minutos si se hace desde cero), muchos smartphones utilizan A-GPS. Este sistema utiliza la conexión de datos del teléfono (ya sea a través de redes móviles o Wi-Fi) para obtener datos de almanaque y efemérides de los satélites, información sobre la ubicación aproximada del teléfono, y otras informaciones que facilitan y aceleran la localización por satélite.

Otros sensores y fuentes de datos: Además del GPS, los _smartphones_ tienen una variedad de sensores que pueden ayudar a mejorar la precisión del posicionamiento o a proporcionar posicionamiento cuando el GPS no está disponible. Esto incluye:

* Wi-Fi: Al escanear las redes Wi-Fi cercanas y conocer la ubicación de esas redes (a través de bases de datos), el smartphone puede obtener una estimación de su ubicación.
* Redes móviles: El smartphone puede determinar su proximidad a las torres de telefonía celular y usar esa información para una ubicación aproximada.
* Sensores inerciales: Sensores como el acelerómetro, giroscopio y brújula magnética pueden ayudar en el cálculo de la posición, especialmente cuando las señales GPS son débiles o no están disponibles.
* Barómetro: Algunos smartphones incluyen un barómetro que puede ayudar a determinar la altitud basada en la presión atmosférica.
Combinación de datos: Los sistemas de software en los smartphones (como el sistema operativo y las aplicaciones de mapas) combinan datos de todas estas fuentes para proporcionar una ubicación lo más precisa posible al usuario.

Es importante mencionar que aunque el GPS y otros sistemas GNSS son muy precisos, la precisión real que experimenta un usuario en su smartphone puede verse afectada por diversos factores, como edificios altos, árboles, condiciones atmosféricas y señales reflejadas.

### ¿Cómo puede obtener un dispositivo móvil su geolocalización sin que esté operando el sensor de GPS?

En una variedad de situaciones en las que el hardware de GPS en un teléfono móvil puede verse en dificultades para captar con precisión la ubicación del usuario. Esto incluye ubicaciones en las que la línea de vista a los satélites se ve interrumpida por bloqueos físicos, dentro de edificios, en subterráneos, en túneles, y en otro tipo de recintos cerrados. En estos casos, el sistema operativo recurre a otras alternativas para aproximar la ubicación del usuario y proveerla a las aplicaciones. Las alternativas son comúnmente las siguientes:

* Red Wi-Fi: Si el dispositivo móvil está conectado a una red Wi-Fi, el navegador puede enviar los nombres y direcciones MAC _de las redes Wi-Fi cercanas_ a un servicio de geolocalización, como el que ofrece Google. Este servicio tiene una enorme base de datos de puntos de acceso Wi-Fi y sus ubicaciones geográficas conocidas. Al comparar los puntos de acceso Wi-Fi visibles con esta base de datos, el servicio puede estimar la ubicación del dispositivo. Esta técnica puede ser sorprendentemente precisa en áreas urbanas densamente pobladas donde hay muchos puntos de acceso Wi-Fi, pero menos precisa en áreas rurales o suburbanas.
* Dirección IP: Si no se pueden detectar redes Wi-Fi o el dispositivo móvil está conectado a través de otra interfaz de red, la resolución de la ubicación puede realizarse con base a la dirección IP obtenida. Los servicios de geolocalización tienen bases de datos que asocian direcciones IP con ubicaciones geográficas. Sin embargo, este método es generalmente menos preciso que la geolocalización basada en Wi-Fi y puede ofrecer una ubicación aproximada a nivel de ciudad o incluso de país, pero no a nivel de calle.
* Otros factores: Las aplicaciones web móviles también pueden utilizar información de otros sensores disponibles en el dispositivo, como las lecturas de señal de redes cercanas o datos proporcionados por plugins o aplicaciones del sistema.

La precisión de la medición varía según el método utilizado. La geolocalización basada en Wi-Fi puede ser precisa hasta unos pocos metros en las mejores condiciones, pero generalmente es más adecuado decir que tiene una precisión de decenas de metros en áreas urbanas. La geolocalización basada en direcciones IP, por otro lado, puede variar desde precisión a nivel de ciudad hasta precisión a nivel de país. Es importante que las aplicaciones que utilicen la API Web de Geolocation sean conscientes de estas limitaciones y las comuniquen a los usuarios.

Por último, es importante destacar que al usar la API estándar de Geolocation en un navegador web, se pide permiso al usuario antes de permitir el acceso a la información de ubicación. Esto es esencial para proteger la privacidad del usuario.

## Herramientas para implementar Geolocalización en dispositivos móviles

### API web estándar de geolocalización

La API estándar de geolocalización está soportada en todos los [navegadores web principales desde el período 2010-2012](https://caniuse.com/?search=navigator.geolocation). Esta API sólo puede utilizarse en contextos seguros (contra orígenes servidos al navegador web por HTTPS). Los navegadores web tolerarán el uso de la API contra el dominio `localhost` sin requerir una conexión segura. Además, los navegadores web permiten utilizar la API desde páginas accedidas desde el sistema de archivos local (_schema_ `file://`). Junto con este enunciado encontrarás un ejemplo básico de uso de la API de geolocalización (`ejemplo1.html`). Si abres el ejemplo en el navegador web en tu PC o Mac, deberás dar al navegador web los permisos necesarios para que pueda obtener la ubicación; esto se configura tanto en el sistema operativo como en el navegador web. Además, es necesario que leas las siguientes guías de MDN referentes a este tema:

* [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)
* [Using the Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API/Using_the_Geolocation_API)

### API de Google Maps para uso de geolocalización con mapas

La API de Google para utilización de mapas (Google Maps API) existe desde el año 2005, y actualmente va en su versión 3.5. Existen numerosas formas de obtener código cliente preparado para utilizar esta API, y crear componentes de React clientes de ella. Lo primero para usar esta API es tener una cuenta de usuario de Google (@miuandes.cl sería apropiada) para usar Google Cloud Platform (GCP) ([console.cloud.google.com](console.cloud.google.com)) y activar el acceso a la API. El uso de la Maps API tiene una capa gratuita de 200 dólares, o cerca de 30000 despliegues de mapas. Sin embargo, para usar GCP y sus APIs requieres una tarjeta de crédito. La tarjeta de crédito la puedes obtener gratuitamente a través de [MACH de BCI](https://somosmach.com). Registrándote en MACH obtienes una cuenta vista gratuita en BCI, y además una tarjeta de crédito virtual VISA que puedes usar con GCP. 

Una vez que tienes tu acceso funcional a GCP, necesitas crear tus propias credenciales para usar las APIs de Google, incluyendo Google Maps API. Los pasos para realizar esto los encuentras en las siguientes fuentes:

* [Set up your Google Cloud Project)](https://developers.google.com/maps/documentation/javascript/cloud-setup): Guía oficial de Google para comenzar a usar GCP.
* [Getting started with Google Maps Platform)](https://developers.google.com/maps/get-started): Guía oficial de Google para comenzar a usar la API de Google Maps.
* [How to Use Google Maps API (YouTube))](https://www.youtube.com/watch?v=eycjk3APuoI): Este vídeo no oficial te mostrará cómo habilitar la API de Google Maps y cómo crear una API key para usarla.

Importante: Existen buenas prácticas de seguridad para generar y usar API keys que aplican a GCP y a otras plataformas con APIs que puedan requerir en el futuro. Las buenas prácticas para uso de API keys con GCP las encuentran en [https://developers.google.com/maps/api-security-best-practices](https://developers.google.com/maps/api-security-best-practices).

Dado que ustedes trabajarán en grupos compuestos por dos alumnos, y además los ayudantes requieren revisar su aplicación, es importante que su API key de GCP la mantengan resguardada y no la suban a su repositorio. La práctica común para hacer esto es crear un archivo `.env` (en Unix, loa archivos cuyo nombre parte con `.` son archivos ocultos) en la raíz del proyecto de frontend de React, en donde puedan definir variables de entorno a las que la aplicación React puede acceder cuando es levantada en el servidor. El archivo `.env` debe ser agregado a `.gitignore`. La variable de entorno puede ser definida como `REACT_APP_GAPI_KEY`:

```sh
REACT_APP_GAPI_KEY=#insertar llave de GCP aquí
```

Es importante notar que toda variable de entorno accesible desde el código de React debe tener el prefijo `REACT_APP_` cuando se usa el módulo `create-react-app`, como lo es el caso en el proyecto de frontend. Luego, las variables son accesibles desde el código de React, siguiendo [los pasos descritos en esta guía](https://create-react-app.dev/docs/adding-custom-environment-variables/). En particular, para acceder a una variable de entorno definida en el código React, se usa el módulo `process.env`:

```es6
process.env.REACT_APP_NOT_SECRET_CODE
```

Se debe tener cuidado pues *esta no es una solución robusta desde el punto de vista de la seguridad*, dado que el browser termina conociendo la API key y usándola en todas las peticiones. Mantener la API key completamente oculta del frontend requiere que el backend haga las peticiones a GCP, y que toda petición del frontend a GCP pase a través del backend. La explicación y solución a este problema [la encuentran aquí](https://stackoverflow.com/questions/48699820/how-do-i-hide-an-api-key-in-create-react-app).
 
### API de Google Maps

El uso básico de la API de Google Maps está cubierto en la clase 5 del curso. Aquí te entregamos una serie de referencias útiles que puedes consultar para guiar tu trabajo:

* [Conceptos de la API de Google Maps](https://developers.google.com/maps/documentation/javascript/basics): Explica sobre los tipos de mapas disponibles, los mapas y coordenadas, localización en los mapas, versionamiento de la API, parámetros en URL, mejores prácticas, y uso de métodos asíncronos a través de promesas de ES6+.
* [React Google Maps](https://www.npmjs.com/package/react-google-maps?activeTab=readme): Alternativa #1 para usar Google Maps API con React. Módulo no oficial que permite la integración de Google Maps con su aplicación React. Ejemplo de uso [disponible en codesandbox.io](https://codesandbox.io/s/react-google-maps-example-forked-dr2hjs?file=/index.js). En línea 19, cambiar API key por la propia. La documentación está [disponible aquí](https://tomchentw.github.io/react-google-maps/). La utilización de este módulo requiere conocer una técnica en React conocida como _Higher Order Components_ (HOC). Para mayor información sobre HOCs y su uso en apliaciones React, pueden ver [aquí una explicación simple](https://gist.github.com/claudio-alvarez/d2f00242e0bacad1e6dadf5fc8df6aad), y acá una [guía más avanzada escrita por Robin Wieruch](https://www.robinwieruch.de/react-higher-order-components/).
* [Google Map React](https://www.npmjs.com/package/google-map-react): Alternativa #2. Módulo no oficial, vigente actualmente, para integrar Google Maps con su aplicación React. Documentación disponible en [sitio en GitHub](https://github.com/google-map-react/google-map-react).

Nota: En las instrucciones de instalación, considerar que el proyecto en que Uds están trabajando (desde entrega anterior) utiliza NPM para instalación de paquetes, por lo que pueden omitir las instrucciones para usar Yarn. 

## Objetivos de la Entrega del Proyecto 1.4

Los objetivos de esta entrega son dar funcionalidad de geolocalización y mapas a la aplicación Travel Log. Deberán continuar trabajando en el repositorio de la entrega 3, extendiéndolo con la funcionalidad necesaria. Además, podrán modificar la aplicación de backend si lo estiman necesario. Vean la sección siguiente para mayores detalles.

1. [1.0] En componente de creación de destino (`Destination`) de la aplicación Travel Log, desplegar mapa de Google Maps utilizando componentes de React.
2. [1.0] Permitir encontrar ubicación en mapa ingresando su nombre en un input de tipo texto, parte de un componente React - posiblemente, del mismo componente que despliega el mapa.
3. [1.0] Como alternativa a ingresar el nombre de un lugar en campo de texto, permitir encontrar ubicación en mapa desde coordenadas GPS actuales mediante Geolocation API, al presionar un botón.
4. [1.0] Crear un "_placemark_" (marcador de lugar) en el mapa para el lugar encontrado. El marcador debe quedar asociado al destino en la aplicación Travel Log, asociado a algún viaje (el que ustedes definan), y guardado en la base de datos.
5. [1.0] Al desplegar un viaje, dar la posibilidad de ver el mapa del viaje mostrando todos los destinos marcados en el mapa (placemarks).
6. [1.0] Al hacer tap en uno de los placemarks, permitir navegar a la vista detallada del destino respectivo.

## Forma de trabajo y entrega

En esta entrega del proyecto deberán continuar su trabajo en el repositorio del Proyecto 1.3 (frontend). Además, podrán realizar modificaciones al backend (Proyecto 1.1) para actualizar controladores o incluso el modelo de datos (crear migraciones). Lo importante es que todo endpoint expuesto por el backend se mantenga REST. Se les revisarán sus commits a dicho repositorio. Se evaluará el último commit realizado hasta el 10 de septiembre a las 23:59 hrs.

