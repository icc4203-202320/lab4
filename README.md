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

Los smartphones modernos utilizan una combinación de sensores y tecnologías para obtener las coordenadas GPS. La determinación de la posición a través de estas técnicas se llama posicionamiento GNSS (Sistema Global de Navegación por Satélite). GPS es el sistema GNSS desarrollado por Estados Unidos, pero hay otros sistemas similares en funcionamiento o en desarrollo, como GLONASS (Rusia), Galileo (Unión Europea) y BeiDou (China).

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

La API estándar de geolocalización está soportada en todos los [https://caniuse.com/?search=navigator.geolocation](navegadores web principales desde el período 2010-2012). Esta API sólo puede utilizarse en contextos seguros (contra orígenes servidos al navegador web por HTTPS). Los navegadores web tolerarán el uso de la API contra el dominio `localhost` sin requerir una conexión segura. Además, los navegadores web permiten utilizar la API desde páginas accedidas desde el sistema de archivos local (_schema_ `file://`). Junto con este enunciado encontrarás un ejemplo básico de uso de la API de geolocalización (`ejemplo1.html`). Si abres el ejemplo en el navegador web en tu PC o Mac, deberás dar al navegador web los permisos necesarios para que pueda obtener la ubicación; esto se configura tanto en el sistema operativo como en el navegador web. Además, es necesario que leas las siguientes guías de MDN referentes a este tema:

* [https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API](Geolocation API)
* [https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API/Using_the_Geolocation_API](Using the Geolocation API)

### API de Google Maps para uso de geolocalización con mapas

La API de Google para utilización de mapas (Google Maps API) existe desde el año 2005, y actualmente va en su versión 3.5. Existen numerosas formas de obtener código cliente preparado para utilizar esta API, y crear componentes de React clientes de ella. 


## Objetivos de la Entrega del Proyecto 1.4

1. Captar las coordenadas GPS a través de geolocation API en un componente React.
2. Buscar estas coordenadas con Google Maps API y desplegarlas en el mapa.
3. Permitir crear un placemark y guardarlo en la base de datos.
4. Que un usuario pueda tener un conjunto de placemarks guardado (destinations de su viaje en TravelLog)
5. Que al visualizar el viaje aparezca el mapa con todas las destinations, sus fechas, y acceso a los posts desde el mapa.

## Forma de trabajo y entrega

En esta entrega del proyecto deberán continuar su trabajo en el repositorio del Proyecto 1.3. Se les revisarán sus commits a dicho repositorio. Se evaluará el último commit realizado hasta el 10 de septiembre a las 23:59 hrs.

