<h1> Hackaton RIIA 2021 'JusticIA para los desaparecidos'</h1>

<h2>Reto 1: Limpieza de imágenes y reconocimiento de objetos.</h2>
<h3>Nombre del Equipo:</h3>
<h4> Black Mamba </h4>
<h3>Integrantes del equipo:</h3>
<ul>
  <li> Daniel Vallejo Aldana </li>
  <li> Oscar D. Zendejas Rangel </li>
  <li> Emilio Villa Cueva </li>
</ul>
<h3> Descripción </h3>
<h4> En este repositorio se encuentran los notebooks y scrypts utilizados para la realzación del proyecto, además de los archivos usados para la implementación y los archivos generados por el script. La forma de ejecutarlos lo explicamos en la sección de Pipeline.</h4>
<h4>Objetivo: proponer y desarrollar un flujo de pre-procesamiento para mejorar la calidad de las imágenes y detectar los objetos que componen la imagen, su ubicación y clasificación por similitud de acuerdo a categorías generales incluyendo sellos, firmas, texto a mano, texto a máquina y fotografías.</h4>
<h3> Pipeline </h3>
<ul>
  <li> Lo primero que realizamos fue la creación de etiquetas mediante la herramienta de Roboflow, esto nos permite pasar información de los objetos a detectar en los modelos a entrenar. Esta herramienta funciona haciendo recortes a imágenes de los objetos que se quisieran detectar y clasificar, sin embargo el problema que encontramos es que no existe una distribución equitativa de las clases, por lo que tuvimos que ingresar imagenes de Google de firmas genéricas, sellos de forma circular y huellas dactilares, procurando que las imágenes fueran lo más parecido a las que pudieramos encontrar. Es importante mencionar que para la obtención de dichas clases nos basamos solamente en los archivos de expedientes, pues eran más ricos de información detectable.</li>
  <li> Luego de obtener las etiquetas trabajamos sobre un modelo existente de YOLOv5 basado en la librería de pytorch. Este modelo funciona como cualquier red neuronal, necesitamos darle imágenes de entrenamiento, en esta fase sí usamos lotes de los 3 bancos de datos. Para que no hubiera problemas al detectar, agremamos las etiquetas existentes de OCB, las cuales cuentan con 20 etiquetas genéricas(auto, avión, etc.). </li>
  <li> Para la limpieza de imágenes usamos una arquitectura compuesta por una red UNet, esto nos ayuda a resaltar el texto en las imágenes al filtrarla por la red. La red se entreno con parches de datasets para binarización públicos (DIBCO) y por tanto procesa por parches la fotografía completa a limpiar. La implementación de esta red se encuentra dentro de la carpeta UNet_enhance, se tienen dos notebooks, UNetMejora_training.ipynb donde se muestra el proceso de entrenamiento de la red y <b> UNetMejora_demo.ipynb donde se muestra el funcionamiento sobre el conjunto de imagenes de validación </b>, además de los ejemplos mostrados en dicho notebook, todas las imágenes del conjunto de validación se pasaron por el filtro de la red y el resultado se encuentra en la carpeta UNet_enhance/valEnhanced.</li> 
</ul>
<h3> Cómo correr el código </h3>
Contamos con 2 notebooks con una funcionalidad distinta cada uno. El notebook titulado 'RIIA Detección de Objetos" requiere un script de python titulado "...". En este script se encuentras las funciones necesarias para YOLOv5. El contenido del notebook está disponible para correrse directamente, sólo se tendría que cambiar la ruta de ubicación de los archivos. Finalmente nos arroja el archivo csv con los contenidos solicitados. \n
Hay dos notebooks destinados a limpieza de imágenes, uno donde se muestra el proceso de entrenamiento titulado como "UNet_enhance/UNetMejora_training.ipynb" y otro que funciona como demostracion "UNet_enhance/UNetMejora_demo.ipynb". Para correr el segundo notebook sólo es necesario especificar la ruta de acceso para la carga de las imágenes.

<h3> Notas </h3>
<h4> Es necesario aclarar que para que ambos notebooks trabajen se requiere una GPU para poder hacer los procesos, de otra manera no funcionará. </h4>
