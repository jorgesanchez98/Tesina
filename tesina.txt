Capítulo 1. Introducción

1.1 Contexto del Problema
En la última década, la tecnología ha revolucionado el ámbito deportivo, particularmente en el análisis y optimización del rendimiento de los jugadores. En el béisbol, la capacidad de capturar y analizar datos en tiempo real ha abierto nuevas oportunidades para mejorar la estrategia y el entrenamiento. Técnicas avanzadas de visión por computadora, como los algoritmos de detección de objetos, han permitido a equipos y analistas obtener una comprensión más profunda del juego, identificando patrones y comportamientos que antes eran imposibles de detectar con métodos tradicionales.
La detección precisa de objetos en imágenes deportivas es crucial para el análisis detallado del rendimiento de los jugadores, especialmente en deportes dinámicos como el béisbol, donde cada acción se desarrolla rápidamente y con una gran variabilidad. Sin embargo, el reto radica en desarrollar algoritmos que puedan operar con alta precisión y en tiempo real, sin ser afectados por condiciones cambiantes como la iluminación y el movimiento rápido.

1.2 Motivo del Trabajo
La motivación principal de este trabajo es explorar y mejorar las técnicas de detección de objetos aplicadas al análisis deportivo, centrándose en el béisbol. A medida que la tecnología continúa evolucionando, existe una necesidad creciente de métodos más eficientes y precisos para procesar y analizar grandes volúmenes de datos visuales. Este documento busca contribuir a este campo mediante la evaluación y comparación de algoritmos avanzados como YOLO (You Only Look Once), que se ha destacado por su capacidad para realizar detecciones rápidas y precisas.
El béisbol, con su rica historia de análisis estadístico y su adopción temprana de la tecnología en el juego, proporciona un contexto ideal para aplicar y probar estas técnicas. Mejorar la precisión en la detección de objetos no solo beneficia a los analistas y entrenadores, sino que también puede enriquecer la experiencia de los espectadores y aumentar la justicia y transparencia en el deporte.

1.3 Objetivo del Trabajo 
El objetivo principal de este trabajo es investigar y evaluar la eficacia de diferentes técnicas de detección de objetos en aplicaciones deportivas, con un enfoque particular en el análisis del béisbol. Se busca implementar y comparar algoritmos avanzados de visión por computadora, como YOLO, para determinar su viabilidad y precisión en la detección de elementos clave durante el juego. Además, se exploran métodos complementarios como la sustracción de imágenes para mejorar la robustez de los sistemas de detección en diversas condiciones.

1.4 Estructura del Trabajo
El trabajo se encuentra estructurado en diferentes capítulos, que cubren los aspectos del proceso para realizarlo, a continuación, un breve resumen de cada uno de ellos.

Capítulo 2 Estado del Arte. Examina las técnicas más avanzadas en detección de objetos, con un enfoque en el algoritmo YOLO (You Only Look Once). Se exploran sus aplicaciones en el análisis deportivo, particularmente en la captura y evaluación de datos del béisbol.
Capítulo 3 Planteamiento del Problema y Justificación. Aborda los retos de la detección precisa de objetos en el béisbol, como la velocidad y precisión del pitcher, justificando la necesidad Comando+ para mejorar el análisis y la evaluación en tiempo real del rendimiento deportivo.
Capítulo 4 Propuesta de Solución. En este capítulo se detalla el desarrollo del sistema denominado Comando+, utilizando AWS Rekognition para rastrear el movimiento del guante del catcher y calcular la distancia entre las posiciones inicial y final del lanzamiento, para medir la precisión de los pitchers y encontrar la posible co-relación con la calidad de contacto de los bateadores
Capítulo 5 Metodología de Evaluación. El capítulo 5 Se realiza una comparación entre Comando+ y métricas tradicionales como el porcentaje de bases por bola, utilizando el coeficiente de Pearson para determinar cuál métrica ofrece una mejor predicción del hard hit rate de los bateadores. Se explora también el uso de Fielding Independent Pitching (FIP) como estándar de comparación.


Capítulo 2. Estado del arte

2.1 Introducción
La detección de objetos mediante imágenes es una técnica fundamental en el campo de la visión por computadora, con una gran variedad de aplicaciones. Este capítulo aborda el estado del arte de este campo y un análisis sobre las distintas aportaciones de proyectos relacionado, sus defectos y carencias
Para contextualizar adecuadamente este estudio, es necesario primero definir y comprender la terminología esencial en el campo de la visión por computadora y la detección de objetos. Conceptos como "detección de objetos", "algoritmos de aprendizaje profundo", "sustracción de imágenes" y otros serán revisados para asegurar una base sólida de comprensión.
A continuación, se examinan diversos proyectos y sistemas previos que han aplicado la detección de objetos en el béisbol. Entre ellos se destacan Stats+, Statcast y los trabajos de la compañía Inside Edge.
El capítulo también profundiza en los algoritmos de detección de objetos más relevantes y efectivos para este tipo de análisis. En particular, se abordará el algoritmo You Only Look Once (YOLO), conocido por su capacidad para realizar detección de objetos en tiempo real con alta precisión. Finalmente, se discutirá la técnica de sustracción de imágenes, que implica la comparación de imágenes secuenciales para identificar cambios y movimientos.
	

2.2 Terminología
2.2.1 Sabermetrics
Popularizado por Bill James y la ​​Society for American Baseball Research (SABR), Sabermetrics es el análisis empírico del béisbol con el motivo de medir los resultados en el campo y predecir el desempeño futuro a nivel jugador y a nivel equipo [17].
Compuesto por 3 niveles de análisis diferentes que en su conjunto buscan llevar plusvalía a los equipos que lo implementan, siendo esta: “scouting”, estadística y el lado económico [1]. 
Los equipos despliegan un ejército de scouts a diferentes partes del mundo para evaluar el talento de jugadores amateur y profesionales usando no mucho más que su amplio conocimiento del juego y algunas herramientas de medición como pistolas de velocidad. Con esto aprenden sobre los aspectos físicos, médicos y mentales de los jugadores.
La implementación de este conocimiento, junto con el análisis estadístico de los datos recopilados desde finales del siglo XIX muestran una imagen más completa sobre los jugadores y sus futuros, que los equipos pueden utilizar para tomar decisiones monetarias, pues no podemos olvidar que son instituciones con presupuestos y metas fijas.
Algo que agrega Bradley Woodrum, previo escritor para Fangraphs y actual coordinador de información para los Miami Marlins, es la constante búsqueda de lo desconocido, lo cual se resume en la ambición de los equipos de ganar una ventaja sobre los demás sabiendo algo que ellos aun no descubren 
2.2.2 Zona de strike
Definido por MLB como el área por encima del plato de Home desde el punto medio entre los hombros del bateador y el cinturón (comúnmente reconocido como la altura de las letras en el uniforme), hasta las rodillas del bateador. Una bola que toque cualquier punto de esta zona será considerada un strike [2].

    
Figura 2.1 Zona de Strike


2.2.3 Lanzamiento de bola rápida, rompiente y cambio de velocidad
La bola rápida es el lanzamiento más rápido y recto que tiene un pitcher en su arsenal, y usualmente también es el más frecuentemente utilizado, por su falta de movimiento es típicamente el lanzamiento más fácil de ubicar [3].
Las bolas rompientes son lanzamientos ligeramente más lentos que las bolas rápidas cuyo objetivo es generar amplio movimiento ya sea en el plano vertical u horizontal de manera drástica y repentina para engañar al bateador [4].
Los cambios de velocidad son lanzamientos muy similares a las bolas rápidas pero con mucha menor velocidad y menos movimiento que las bolas rompientes, su principal objetivo es interrumpir el ritmo de los bateadores que esperan una bola rápida [5].
2.2.4 Contacto suave
MLB define como contacto fuerte todas las pelotas en juego bateadas con una velocidad de salida mayor a 95 MPH, ya que es a partir de esa velocidad que vemos un incremento notable de resultados favorables para el bateador [6].




Figura 2.2 Gráfica relación velocidad de salida de pelota y valor ofensivo


Para motivos de este trabajo definiremos como contacto suave todas las pelotas en juego con velocidad de salida menor a 95 MPH

2.2.5 Porcentaje de bases por bola
Una base por bola es un evento en un partido de béisbol donde se le otorga un pase gratis al bateador para avanzar a base después de que el lanzador ponga la pelota fuera de la zona de strike 4 veces, El Porcentaje de bases por bola (BB% de ahora en adelante) es definido como el porcentaje de turnos al bat de un pitcher que terminan en una base por bola [7].

2.3 Trabajos relacionados
2.3.1 MLB Pipeline
MLB Pipeline es una plataforma creada por MLB para el seguimiento y análisis de los prospectos más prometedores en el béisbol profesional. Lanzado con el objetivo de ofrecer una evaluación detallada de los futuros talentos, MLB Pipeline proporciona informes, clasificaciones y videos sobre los prospectos de todas las organizaciones de MLB. 
Desde el 2004, una de sus características más destacadas es la lista anual de los 100 mejores prospectos en el juego, actualizada regularmente por los escritores empleados por MLB, para reflejar el desarrollo y rendimiento de los jugadores jóvenes. Para los pitchers, quienes son el enfoque de este trabajo, se les evalúa en una escala del 0 al 80 en incrementos de 5, calificando cada uno de los tipos de lanzamientos en su arsenal y su control sobre la localización de estos, esto a criterio de los scouts y analistas con constance acceso a los jugadores y sus números [8]
Es tal la autoridad de estos resultados que en el último acuerdo de negociación entre la liga y la unión de jugadores en 2023 se acordó utilizar la inclusión en esta lista para determinar la elegibilidad de un jugador novato y su equipo para ser acreedores a bonificaciones con valor de millones de dólares [9].

Además, MLB Pipeline cubre el Draft de la MLB y las firmas internacionales, ofreciendo a los aficionados y analistas información actualizada sobre el progreso de estos jugadores desde las ligas menores hasta su eventual debut en las Grandes Ligas. 
2.3.2 Stuff+, Location+, Pitching+
En 2023, las estadísticas previamente no disponibles para el público general fueron publicadas en el sitio Fangraphs, cortesía de sus autores Eno Sarris y Max Bay. Cabe resaltar que existen múltiples versiones de estás métricas que son propietarias instituciones privadas (Como lo es la versión de la compañía Driveline [10]) pero para motivos de esta investigación usaremos la versión mencionada como punto de referencia.
Stuff+ se enfoca en las características físicas del lanzamiento, específicamente el punto de lanzamiento, velocidad, movimiento horizontal y vertical, y revoluciones por minuto de la pelota.
Location+ es una métrica para juzgar la habilidad de un pitcher de poner la pelota en los lugares correctos ajustado a la cuenta del turno y el tipo de lanzamiento, sin tomar en cuenta los atributos físicos del lanzamiento. Para esto se asume que la intención detrás de cada lanzamiento en sus respectivos escenarios es igual alrededor de la liga, significando que una bola rompiente siempre debería de ir a una cierta posición dentro de la zona de strike para un bateador derecho en cada cuenta para obtener los mejores resultados. Cada lanzamiento posicionado correctamente en la zona óptima sumando a la calificación del pitcher.
Pitching+ es un tercer medidor que engloba ambos factores, sin embargo, utiliza su propia fórmula que los agrega para una calificación global sobre el desempeño del pitcher [11].

Estás métricas han comprobado ser increíblemente predictivas para el desempeño futuro de los lanzadores evaluados, teniendo una mejor raíz del error cuadrático [11] medio que incluso los sistemas de proyecciones utilizados a través de la industria como THE BAT, Steamer y ZiPS [12]


Figura  2.3 Comparación del desempeño de predictores de ERA


2.3.3 Statcast
Es un sistema de seguimiento y análisis de datos oficial utilizado en MLB. Desarrollado por MLB Advanced Media (MLBAM), Statcast combina tecnología de radar y cámaras de alta velocidad (300 fps) para medir y registrar con precisión diversos aspectos del juego. 
Recopila datos sobre la velocidad y el movimiento de la pelota, así como la velocidad y la ubicación de los jugadores en el campo. Los datos recopilados son procesados utilizando algoritmos patentados por MLBAM para generar métricas detalladas sobre el desempeño de los jugadores y las características del juego. Los informes y estadísticas generados por Statcast se publican oficialmente en el sitio web de MLB y se utilizan ampliamente por equipos, entrenadores, jugadores y aficionados para analizar el juego y tomar decisiones estratégicas [13].
Los equipos profesionales han instalado este sistema de medición en sus campos para tener hasta el más mínimo detalle del desempeño de sus jugadores (como por ejemplo las revoluciones por minuto de la pelota) y tomar las mejores decisiones posibles.

2.3.4 Inside Edge
Compañía fundada en 1987 por Jay Donchetz y Randy Istre, se dedican a la elaboración de reportes de scouting profundos sobre jugadores y sus tendencias. Desde su concepción han sido contratados por equipos ganadores de la Serie Mundial, cadenas de televisión y desarrolladores de videojuegos.
Recopilan datos como el ritmo de los pitchers y las intenciones detrás de cada lanzamiento con un ejército de internos [14] que dedican horas a ver los partidos e ingresar los datos a mano. Utilizan estos datos para llenar el vacío que tecnología como Statcast no puede llenar y proporcionar sus propios reportes.
Entre sus productos, se encuentra Quest, una visualización de datos lanzamiento por lanzamiento útil para desarrollo de jugadores y scouting que incluye: [15] 
Notas del repertorio del lanzador
Informes de bateador, lanzador y equipo
Bateador y lanzador por conteo
Informe post-juego del lanzador
Ubicación y distribución del bateador
Informe del juego
Informe del cuerpo de lanzadores
Evaluaciones de bateadores y lanzadores


Figura 2.4 Ejemplos de reportes generados por Inside Edge


2.3.5 Seguimiento en tiempo real de imágenes de tennis (YOLO)
Estudio y comparación de las versiones de YOLO para la aplicación al tenis en tiempo real por Claudia De Jeu Boronat. 
El trabajo de detección de movimiento en el deporte del tenis se realizó mediante el uso de técnicas de Deep Learning y visión artificial, enfocándose en la detección de los componentes esenciales del tenis, como la pelota, la raqueta y los jugadores. Para esto, se utilizó la red neuronal YOLO (You Only Look Once), conocida por su capacidad de detección de objetos en tiempo real. A lo largo del proyecto, se llevó a cabo un estudio y comparación de diferentes versiones de YOLO, analizando sus resultados en varios experimentos para determinar la mejor opción para la detección de objetos pequeños y de alta velocidad en partidos de tenis. Además, se creó y etiquetó una base de datos específica con el fin de entrenar el modelo en partidos reales y profesionales.
Las herramientas principales utilizadas fueron las diferentes versiones de la red neuronal YOLO, específicamente YOLOv3 y YOLOv4, y posteriormente YOLOv5 en sus variantes small (s6) y medium (m6). Los resultados mostraron que los modelos YOLOv5s6 y YOLOv5m6 ofrecían el mejor rendimiento, con el modelo small siendo particularmente efectivo para detectar la pelota de tenis debido a su velocidad y precisión, y el modelo medium siendo superior en la detección de la raqueta y otros objetos. Estos modelos se entrenaron con imágenes de alta resolución y un tamaño de entrada de 1280, utilizando Google Colab para manejar la alta carga computacional requerida [16].
2.3.5 Pixel subtraction
El artículo "A GPU-based Algorithm for Astronomical Image Subtraction Photometry" de Li, Jiajun; Yu, Ce; Sun, Jizhou; Xiao, J, presenta un algoritmo diseñado para mejorar la fotometría de sustracción de imágenes astronómicas mediante el uso de procesamiento en unidades de procesamiento gráfico (GPU). Este método se centra en la comparación de imágenes.
Los resultados del estudio muestran que el algoritmo GPU no sólo acelera el procesamiento de imágenes, sino que también mejora la precisión de la detección de objetos astronómicos. Los autores validaron su enfoque comparando los resultados con métodos convencionales y demostraron una reducción notable en los tiempos de procesamiento sin sacrificar la calidad de la detección. Esto es particularmente beneficioso para proyectos que requieren análisis en tiempo real, permitiendo a los astrónomos reaccionar rápidamente a eventos astronómicos de interés.
Sin embargo, los autores también identificaron varias complicaciones en la implementación del algoritmo. La principal dificultad fue la adaptación del algoritmo a diferentes arquitecturas de GPU y la optimización del uso de memoria. A pesar de estas dificultades, el estudio concluye que el uso de GPU en la fotometría de sustracción de imágenes astronómicas representa un avance prometedor, aunque se requiere trabajo adicional para perfeccionar la técnica y abordar los problemas identificados.


2.4 Conclusión
El análisis exhaustivo del estado del arte en la detección de objetos mediante imágenes, con un enfoque específico en aplicaciones deportivas, revela una evolución significativa en el uso de tecnologías avanzadas como el aprendizaje profundo y la sustracción de imágenes. La revisión de proyectos y sistemas existentes, como Stats+, Statcast y Inside Edge, destaca tanto los logros como las limitaciones actuales en este campo.
La evaluación de algoritmos de detección, particularmente el YOLO, muestra su capacidad para realizar detecciones en tiempo real con alta precisión, lo que es crucial para aplicaciones dinámicas como el béisbol. La integración de estas tecnologías no solo mejora la precisión y eficiencia de las evaluaciones, sino que también abre nuevas posibilidades para análisis más profundos y estrategias más informadas. En resumen, este capítulo establece una base sólida de conocimientos y metodologías que informarán y guiarán el desarrollo de nuevas soluciones en la detección de objetos en el ámbito deportivo.

Capítulo 3. Planteamiento del problema y justificación

3.1 Introducción
Habiendo definido la terminología necesaria para entender el proyecto propuesto y varios otros proyectos que proveen contexto para visualizar el contexto en el que nos encontramos, en este capítulo se describe la problemática que se busca resolver con la métrica propuesta Comando+ y la tecnología utilizada para implementarlo

3.2 Contexto y Justificación
De acuerdo con Josh Kalk, actual vicepresidente de Baseball Operations Strategy & Innovation, la secuenciación de lanzamientos en el béisbol implica estrategias complejas desarrolladas en la colaboración entre lanzadores, catcher y el equipo de entrenadores[18]. Esta práctica requiere comprender las fortalezas del lanzador, las debilidades del bateador y los contextos situacionales para elegir efectivamente la secuencia de lanzamientos. 
Información (definida en el estado del arte) que los equipos consiguen de empresas como Inside Edge[19], y solo con ese conjunto de actores arman un plan de ataque único que solamente ellos conocen.
Un pitcher puede optar por intencionalmente colocar un lanzamiento muy lejos del corazón de la zona de strike, o bien el caso contrario; decidir que puede obtener un mejor resultado cercano al corazón de la zona de strike. 
Como contexto para estas decisiones es importante tener en cuenta lo siguiente: 

Figura 3.1 Batter RAA/100P vs All Pitchers
La capacidad de cada lanzamiento de contener el daño tiene una alta correlación al cuadrante en el que se elija colocar, independientemente de las capacidades e historial del bateador. Refiérase a la gráfica 2.1, dónde se ilustra el aporte ofensivo obtenido por todos los bateadores de la temporada 2014, sin importar el contexto situacional, sino únicamente la colocación del lanzamiento

Figura 3.2. Aaron Judge wOBA
(En está gráfica, entre más rojo sea el fondo del cuadrante, más efectivas han sido las pelotas bateadas en esa zona, y el azul significando lo contrario)
Para un ejemplo específico sobre cómo pueden cambiar los planes de un lanzador y el equipo dependiendo de la situación, Aaron Judge, actualmente el jugador más peligroso según la medida woba[20] y muchas otras más, es efectivo tanto fuera de la zona como dentro, con 3 sectores siendo sus puntos débiles. Si un lanzador fuera a lanzar una pelota 10 centímetros fuera de la zona de strike, como sabremos si esto fue porque el equipo decidió que no valía la pena arriesgarse con este bateador o porque el pitcher fue incapaz de localizar la pelota.+.
Por lo tanto, se presenta la problemática sobre cómo evaluar la puntería de cualquier pitcher fuera de tu organización, cuando no sabes el objetivo que tiene con sus lanzamientos.
Tampoco podemos ignorar que esto también refleja  el desempeño del catcher y los coaches, pues métricas de puntería tradicionales (Como lo es porcentaje de bases por bola) ignoran el hecho de que pueden ser ellos los que estén tomando una decisión incorrecta al pedirle al pitcher que ponga su lanzamiento en algún lugar en específico al no tomar en cuenta la intención detrás de cada lanzamiento

3.3 Conclusión
El problema central radica en la falta de un proceso automatizado y preciso para medir el comando de los pitchers de manera automatizada que intente tomar en cuenta los planes internos de los equipos. 
Actualmente, tecnología extremadamente precisa como Statcast permite saber dónde llegó la pelota, pero ignora la intención detrás de los lanzamientos que no solo depende del lanzador. O  como Inside Edge que desde varios años proveen este tipo de datos a los equipos profesionales, sin embargo depende de análisis humano para determinar esto, lo cual es increíblemente caro y limita la cantidad de jugadores que pueden ser analizados.

Capítulo 4. Propuesta de Solución

En este capítulo se explicará a detalle una solución que cubra las áreas de oportunidad mencionadas previamente. Se hará mención de las tecnologías utilizadas, se explicará a profundidad la funcionalidad del sistema y su arquitectura.
Se propone que, mediante el uso de tecnologías avanzadas de reconocimiento de imágenes, el desarrollo de un sistema que mida la puntería del pitcher con una precisión comparable a los métodos actuales, reduciendo considerablemente la necesidad de personal humano. Este sistema, denominado Comando+, utiliza la plataforma AWS Rekognition para el seguimiento del movimiento del guante del catcher, con esta información obtener una medida para la puntería del pitcher tomando la posición inicial contra la posición final del guante, y encontrar la posible correlación con la calidad del contacto de los bateadores.

4.1 Panorama general del sistema
El proyecto fue desarrollado en AWS, donde se creó una pipeline para alcanzar su objetivo final de evaluar la puntería de cada pitcher. A continuación, se describe la estructura general del proyecto:

Figura 4.1 AWS Glove Finder Recokgnition

El proceso comienza cuando el usuario deposita las imágenes en un bucket S3 denominado "raw-pitches-source". Este bucket sirve como el punto de inicio donde se almacenan las imágenes sin procesar de los lanzamientos de los pitchers, preparándose para ser procesadas.
Una función Lambda se encarga de extraer la posición de los objetos de interés dentro de cada imagen. Esta función utiliza la SDK de AWS Rekognition, una herramienta avanzada de reconocimiento de imágenes que identifica y localiza el guante del catcher en las imágenes. La función Lambda analiza cada imagen para detectar y extraer las coordenadas del guante, que son críticas para evaluar la precisión del lanzamiento.
Una vez extraídos los datos de posición, estos se almacenan en una base de datos DynamoDB llamada "sorted-pitchers-pitches". Si el otro elemento del par de imágenes (es decir, el cuadro inicial o final) ya ha sido almacenado previamente, la función busca la entrada correspondiente y actualiza los datos con la nueva información obtenida. Si no se encuentra una entrada existente, se crea una nueva.
Para calcular la puntería, se dispara la función "AveragePitcherDist" a petición del usuario. Esta función calcula el promedio del atributo "dist" (distancia) de todas las entradas en "sorted-pitchers-pitches" para cada pitcher incluido en la tabla. El atributo "dist" representa la distancia entre las posiciones inicial y final del guante, proporcionando una medida cuantitativa de la precisión del lanzamiento.
La información recopilada por la función "AveragePitcherDist" se ingresa en una tabla llamada "command-plus-db". Esta tabla contiene los resultados finales generados por el sistema, permitiendo a los usuarios ver y analizar la puntería de los pitchers de manera clara y organizada.
4.2 Parámetros de entrada
MLB Filmroom es una plataforma digital lanzada por Major League Baseball que ofrece acceso a una vasta biblioteca de videos de juegos y jugadas, facilitando el análisis de momentos destacados del béisbol. Activa desde 2020, La plataforma permite a los usuarios explorar contenido que abarca desde juegos completos hasta momentos individuales, filtrados por jugador, equipo, tipo de jugada y más. 
El sistema acepta imágenes extensión .jpg (por ser más ligeras que .png, lo cual será beneficioso para el costo de almacenamiento) extraídas de transmisiones en vivo de partidos disponibles en MLB Filmroom. Este proveedor de videos fue seleccionado por la calidad profesional en que están almacenados los videos, la funcionalidad para buscar escenarios muy específicos dentro de los partidos para reducir el tiempo invertido en encontrar muestras de calidad.
También cabe resaltar que la estandarización en las transmisiones de equipos profesionales provee la mejor posibilidad para que el algoritmo de detección de objetos pueda aprender como se ve el guante desde ese ángulo (puede variar ligeramente entre televisoras) y después lo pueda encontrar dentro de imágenes similares

Figura 4.2 Imágenes de Transmisiones en vivo.

Transmisiones en vivo de diferentes equipos profesionales, cada equipo tiene un contrato con una televisora, la cual determina como se verá el video 
En el béisbol, cada lanzamiento sólo puede tener 4 escenarios posibles:
Contacto con la pelota: Este resultado ocurre cuando el bateador logra golpear la pelota con el bate. El contacto puede llevar a diferentes situaciones dependiendo de cómo y dónde se golpee la pelota (imparable, bola en juego, out, foul ball, foul tip). 
Swinging strike: Esto ocurre cuando el bateador hace un swing (intenta golpear la pelota) pero no logra hacer contacto.
No swing: El lanzador lanza la pelota y el bateador decide no intentar golpearla. Dependiendo de si la pelota pasó por la zona de strike o no, se marcará como bola o strike por parte del umpire.
Contacto con el jugador: Si la pelota golpea al bateador, se le otorga la base como si fuera una base por bola
Para evaluar correctamente la puntería del lanzador según el objetivo marcado por el guante del catcher ignoramos el primer y cuarto tipo de escenario ya que la pelota es impactada antes de que la pelota (por el bate o el bateador) tenga la oportunidad de entrar en contacto con el guante
Para la evaluación se necesitaran dos imágenes de momentos distintos del lanzamiento:
El cuadro cuando el catcher presenta el guante para indicarle al pitcher donde quiere que lance la pelota [21], el cual para motivos de esta investigación se definió como el momento en que el pitcher empieza su movimiento hacia el bateador para lanzar la pelota.

Figura 4.3 Primer imagen del lanzamiento a analizar
El cuadro antes de que la pelota entre en contacto con el guante. Este momento está definido como el último cuadro en el que la pelota es visible, ya que después de atrapar la pelota la fuerza de esta, hará que se cierre el guante y salga del campo de visión de la cámara

Figura 4.4 Segunda imagen del lanzamiento a analizar
Automatizar la detección de estos momentos exactos está fuera del alcance de este proyecto, por lo cual para la creación de la base de datos las imágenes fueron seleccionadas a mano por una persona y fueron editadas utilizando la librería Pillow en Python para reducirlas a un cuadro de 240px por 240px desde el centro de la imagen, manteniendo solamente en imagen el guante del catcher, lo cual es lo único que necesitamos para evaluar qué tan cerca estuvo el lanzador de su objetivo.
Se establece que las imágenes tendrán el siguiente estilo de nombramiento S-MMDDYYXXX-NiLN, que consiste de los siguientes elementos:
S: Define si la imagen es el cuadro inicial de la secuencia o el final, será ingresado como “i” o “f”
MMDDYY: La fecha del partido sin espacios en formato Mes Día Año e.g. 011323
XXX: El número de lanzamiento dentro de ese partido para ese pitcher en específico, cabe recalcar que es 235 es la mayor cantidad de lanzamientos hechos por un pitcher en un partido en la historia del deporte
NiLN: La inicial del primero nombre del lanzador concatenada con su primer apellido, todo en minúsculas e.g. Lance Lynn = llynn
Estos requisitos son necesarios para más adelante analizar el nombre del archivo y de ahí extraer los datos necesarios que en su momento alimentarán las tablas noSQL correspondientes, este paso será explicado a mayor profundidad más adelante.


4.4 Diseño de base de datos
Para justificar la decisión de utilizar la base de datos NoSQL DynamoDB de AWS para el sistema propuesto, se consideraron varios factores claves en comparación con otras opciones SQL y NoSQL disponibles dentro de AWS.
DynamoDB ofrece escalabilidad y rendimiento excepcionales, diseñados para manejar cargas de trabajo de cualquier escala automáticamente y con un rendimiento constante. Esta capacidad de escalar horizontalmente sin esfuerzo sería ideal para un futuro en el que este sistema se pudiera implementar en tiempo real como Statcast lo hace. DynamoDB se integra de manera fluida con otros servicios de AWS, incluyendo AWS Rekognition, facilitando la transferencia y almacenamiento de datos y simplificando la construcción del sistema. Además, la estructura NoSQL de DynamoDB permite manejar datos no estructurados, lo cual fue muy útil durante el desarrollo del sistema cuando los requisitos de información cambiaban constantemente
A continuación describiremos las bases de datos utilizadas en el proyecto:
Raw-pitches-data
PitchID: El nombre de archivo funciona como la Partition Key de la tabla
Pitcher: Nombre del lanzador en la imagen
GloveX: Posición del guante en el plano de X
GloveY: Posición del guante en el plano de Y
Order: Si es el cuadro inicial (i) o final (f)
Inicialmente todos los picheos irán a esta tabla, en un futuro será útil para hacer evaluaciones visuales de los picheos dibujando sobre las imágenes el cuadro donde el algoritmo encontró la bola.


PitchId(String)
(Partition Key)
Pitcher(String)



GloveX(String)


GloveY(String)


Order (String)


Ejemplo ->
i-051223006-lcastillo
Luis Castillo
0.5444
0.3355
i

                  Figura 4.5 Tabla Raw-pitches-data

Sorted-pitchers-pitches
pitcherPitchesID: El componente numérico concatenado con el nombre del pitcher funciona como la Partition Key de la tabla
Pitcher: Nombre del lanzador en la imagen
GloveIX: Posición del guante en el plano de X para el cuadro inicial
GloveIY: Posición del guante en el plano de Y para el cuadro inicial
GloveFX: Posición del guante en el plano de X para el cuadro final
GloveFY: Posición del guante en el plano de Y para el cuadro final
Distance: Distancia entre coordenada final y coordenada inicial
Paired: Si el set de imágenes está completo o no (imagen final e inicial de cada lanzamiento). Cuando se sube la primera imagen es N (No) y al entrar la segunda imagen del par se actualiza a Y (Yes)
Una tabla donde cada entrada es conformada por los datos de la posición del guante en cada una de las dos imágenes que representan el lanzamiento. Una vez que hayan sido registradas ambas imágenes se marca como Paired = Y y se calcula la distancia entre ambos puntos 


PitcherPitchesID
(String)
(Partition Key)
Pitcher
(String)



GloveIX
(String)


GloveIlY
(String)


GloveFX
(String)


GloveFY
(String)


Distance
(String)


Paired
(String)


Ejemplo ->
091523062
Lcastillo
Luis Castillo
0.5444
0.3355
0.5222
0.3366
0.0222
Y

Figura 4.6 Tabla Sorted-pitchers-pitches

Command-plus-db
PitcherID: El nombre de pitcher funciona como la Partition Key de la tabla
AvgDistance: Un promedio de la distancia entre las posiciones del guante en cada uno de sus lanzamientos registrados
PitchCount: Cantidad de pitcheos considerados en el cálculo de la distancia promedio
Finalmente, se recopilan los lanzamientos (marcados como Paired = Y) de todos los pitchers incluidos en la tabla Sorted-pitchers-pitches y se calcula el promedio de las distancias de ellos y finalmente este dato, junto con la cantidad de lanzamientos calculados, son ingresados en la tabla que será el resultado final del sistema


PitcherId
(String)
(Partition Key)

AvgDistance(String)


PitchCount(String)


Ejemplo ->
lcastillo
0.0222
1

		Figura 4.7 Command-plus-db



Capitulo 5. Metodología de evaluación

En este capítulo se detalla la metodología utilizada para evaluar la precisión de los pitchers en el béisbol utilizando tecnologías avanzadas de reconocimiento de imágenes y análisis de datos.
Para evaluar si los resultados obtenidos con Comando+ proporcionan una mejor correlación con el hard hit rate del lanzador en comparación con el uso exclusivo del porcentaje de bases por bola, se realizó una comparación entre estos dos factores utilizando el coeficiente de Pearson. Esta comparación tiene como objetivo determinar cuál de las dos métricas ofrece una mejor predicción de la calidad del contacto de los bateadores, contribuyendo así a un análisis más preciso y detallado de la efectividad de los pitchers.

5.1. Coeficiente de Pearson
La correlación de Pearson es una medida estadística que evalúa la fuerza y la dirección de una relación lineal entre dos variables cuantitativas. Su valor oscila entre -1 y 1, donde 1 indica una correlación positiva perfecta, -1 una correlación negativa perfecta y 0 ninguna correlación. Esto nos ayuda a determinar si un aumento o disminución en una variable está asociado con un aumento o disminución en la otra.


Figura 5.1 Gráfico de dispersión BB% vs Hardhit%

5.2 FIP vs Comando+
Como punto de partida utilizaremos Zone% para comparar los resultados obtenidos por Comando+ (ya que este número toma en cuenta es el porcentaje de los lanzamientos que tocaron la zona de strike), hecho de la siguiente manera




Zone%
Comando+
KK%
r
r
BB%
r
r
HR/FB
r
r


Figura 5.2 Comparación contra elementos de FIP


KK%, BB% y HR/FB son elegidos por ser elegidos por ser elementos que conforman FIP. Fielding Independent Pitching es una estadística en béisbol que mide la efectividad de un lanzador enfocándose solo en los eventos que puede controlar directamente: ponches, bases por bolas, pelotazos y jonrones. Excluye las jugadas que involucran a la defensa para proporcionar una imagen más clara del rendimiento real del lanzador. 
Para este ejercicio no tomaremos en cuenta pelotazos, ya que la cantidad de ocasiones que ocurre este evento en una temporada, incluso para los líderes en esta categoría, apenas rebasa los dos dígitos


Fórmula de FIP, donde :
HR equivale a los jonrones permitidos, 
BB las bases por bolas, 
HBP los bateadores golpeados con la pelota, 
K la cantidad de ponches,
IP las entradas totales lanzada y la 
constante de FIP, un número que cambia temporada por temporada para asegurar que FIP asemeje a ERA (Promedio de carreras admitidas) y sea más fácil de entender

FIP es utilizado como punto de comparación para el proyecto por su énfasis en el desempeño del pitcher y su poder como predictor del desempeño futuro del jugador, fue usado de esta manera por Owen McGrattan en su análisis del proyecto mencionado previamente en el Estado del Arte “Pitching+”[11]. De igual manera, Lucas Teske y sus colegas de Wake Forest Baptist Health están de acuerdo con el uso de FIP como estándar para aislar el desempeño del lanzador, usandolo en su trabajo Lower Extremity Biomechanics Predicts Major League Baseball Player Performance donde encuentran una correlación positiva entre los resultados de un examen neuromuscular aplicado a jugadores de ligas mayores y su FIP [22].



Zone%
Comando+
HardHit%
r
r
ERA
r
r


Figura 5.3 Comparación con Hardhit% y ERA

Además también se utilizará como tercer agente en la comparación HardHit% para representar el efecto que tiene la precisión del pitcher sobre la calidad del contacto de los bateadores, y finalmente ERA, el promedio de carreras admitidas, para tener un panorama general (aunque inexacto ya que ERA falla en tomar en cuenta el muy importante factor en el béisbol que es la suerte[23]) de la efectividad de los pitchers, pues esta ha sido la medida insignia para calificar el desempeño de los pitchers desde su invención a finales del siglo XIX por el padre del béisbol Henry Chadwick

5.3 Cumplimiento del objetivo
Para medir el rendimiento y la efectividad de mi métrica propuesta, Comando+, compararé los resultados del coeficiente de Pearson de Zone% con los obtenidos mediante Comando+. La expectativa es encontrar una mejor correlación utilizando Comando+, ya que esta métrica es más precisa al medir la puntería del lanzador. Al ser más detallado en la evaluación de la precisión, Comando+ debería proporcionar una correlación más fuerte con los factores de pitcheo expuestos en este capítulo, demostrando así que es una herramienta más eficaz para analizar el rendimiento del pitcher.










	

Capítulo 6. Resultados

En este capítulo, se presentan los resultados obtenidos a través del sistema Comando+. Se analizarán las correlaciones entre la precisión del lanzador y tanto las métricas tradicionales y avanzadas previamente mencionadas. Estos hallazgos proporcionarán una base para evaluar la efectividad de la métrica propuesta.

6.1 Comando+


Figura 6.1 Lanzamientos emparejados exitosamente, resultados extraídos de DynamoDB


De las 152 imágenes subidas al sistema, se logró conseguir 6 sets de imágenes donde AWS Rekognition fuera capaz de encontrar el guante tanto en el cuadro final como el inicial, lo cual permitió calcular el Comando+ de 3 pitchers distintos: Gerrit Cole, Lance Lynn, y Noah Syndergaard.




Figura 6.2 Resultados para Comando+, extraídos de DynamoDB



Figura 6.3 Ejemplos de entrada (GCOLE-060421039)

En las imágenes mostradas en la figura anterior vemos un ejemplo de un set de imágenes utilizadas por el sistema donde se puede ver la excelente puntería de Gerrit Cole, con una distancia de 0.023204183575309657 pixeles entre la posiciones del guante


Figura 6.4 Ejemplos de entrada (NSYNDERGAARD-041423036)

En otro ejemplo, tenemos uno de los lanzamiento de Noah Syndergaard, donde podemos observar que el catcher tuvo que mover su guante considerablemente más de lo que fue necesario con el lanzamiento de Gerrit Cole, con una distancia de 0.18243466502327715 pixeles entre la posiciones del guante.

6.2 Comparaciones

 Para evaluar los resultados obtenidos, se pusieron cara a cara los resultados de la regresión de Pearson como fue expuesto en el capítulo de Metodología de Evaluación y se compararon los siguientes resultados, donde la variable de precisión se estableció en el eje X, mientras que la de rendimiento en el eje Y para cada una de ellas.
 










Figura 6.5 Comparación de resultados Zone% y Comand+

En las 5 categorías observadas, la tendencias del coeficiente de Pearson es la misma para ambas variables Zone% y Comando+, sin embargo en algunos de ellas la correlación es mayor





Zone%
Comando+
ERA
0.5978596816
0.7596610279
K%
-0.7812730294
-0.8995184604
BB%
-0.7527675943
-0.5893814392
HR/FB
0.270556641
0.4758537925
HardHit%
-0.9999438927
-0.9777443768


Figura 6.6 Coeficientes de Pearson 

En la figura anterior podemos ver resultado en rojo de las categorías en el que el coeficiente de pearson demostró mayor correlación, siendo más alto en 3 instancias para Comando+ y en 2 para Zone%



Capítulo 7. Contribuciones y conclusión
La métrica Comando+ desarrollada y evaluada en esta tesis ha demostrado ser una herramienta prometedora para medir la precisión del pitcher y su correlación con los diferentes factores que afectan el éxito de un lanzador. Utilizando tecnologías avanzadas de reconocimiento de imágenes y almacenamiento en la nube, se logró crear un sistema automatizado que puede operar con mínima intervención humana, proporcionando resultados detallados. La pipeline desarrollada en AWS, desde el momento que se cargan las imágenes en S3 hasta el análisis en DynamoDB, ha mostrado ser eficiente para procesar grandes volúmenes de datos y extraer información relevante sobre los lanzamientos.
Los análisis comparativos realizados entre la métrica Comando+ y otras métricas tradicionales, indican que Comando+ puede ofrecer una evaluación al menos muy similar. En particular siendo demostrado al comparar los coeficientes de correlación de Pearson entre estas métricas.
Un posible escenario en el que este proyecto sería de gran beneficio para los equipos es en el scouting de ligas externas. Los equipos mandan a sus scouts por varios rincones del mundo a buscar talento nuevo[25] que pueda unirse algún día a las ligas mayores, pero con personal limitado siempre habrá jugadores que se estén perdiendo. 
Aquí es donde Comando+ entra en juego, utilizando solamente la transmisión en vivo de los juegos para brindar conocimiento sobre uno de los aspectos fundamentales del juego. El sistema aprovecha la gran disponibilidad de material que existe en internet para ligas de todo el mundo


Figura 7.1 Transmisión en Youtube de partido de Liga Australiana

Sin embargo, es notable la falta de mayor cantidad de datos para alcanzar resultados confiables, sobre todo con lo documentado que es la volatilidad de los tamaños de muestra pequeños y conocemos la cantidad de entradas mínimas para que se estabilice las estadísticas en el béisbol[24]. Esto en gran parte fue debido a que la resolución en las imágenes utilizadas era pobre en la mayoría, una solución para esto sería encontrar tomas con mayor enfoque como las que usan las televisoras en las tomas en cámara lenta que aparecen en los análisis post partido.

Toma con mayor zoom y detalles más nítidos
Otra opción para mejorar la proporción de imágenes identificadas sería utilizar otro algoritmo donde se efectúe el entrenamiento por medio de aprendizaje supervisado como YOLO o en AWS Rekognition, donde también es posible agregar al algoritmo etiquetas personalizadas para que detecte nuevos objetos, de esta manera sería posible entrenar el algoritmo para encontrar el guante desde ángulos y resoluciones poco favorables
7.1 Conclusión
Estos hallazgos sugieren que la implementación de Comando+ podría mejorar significativamente las estrategias de evaluación y entrenamiento en el béisbol, proporcionando una herramienta valiosa para jugadores, entrenadores y analistas del deporte. Al ofrecer una medida más detallada y exacta de la precisión del pitcher que toma en cuenta la intención detrás de cada lanzamiento, Comando+ permitiría identificar conocimiento previamente oculto para los equipos. En resumen, la adopción de esta métrica avanzada podría representar un avance importante en la optimización del rendimiento de los pitchers y una oportunidad para que los equipos hagan valer más sus inversiones en el departamento de scouting, aportando una nueva dimensión de análisis al béisbol moderno.
