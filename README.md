# Sales of a textile store: Analyzing Data with Power BI

## Resumen del proyecto

En este proyecto se busca hacer uso de los datos obtenidos con la IA Generativa Postgres, los cuales simulaban las ventas de una tienda textil a lo largo del año 2023 para crear un dashboard con Power BI que nos permita extraer información útil para el comercio. 

Para poder hacer dichas visualizaciones se hará un proceso de transformación de los datos obtenidos, se usarán expresiones DAX para poder crear nuevas columnas y tablas que ayuden a obtener más resultados con los que trabajar, aunque pasaré por alto a posta un error que no señalaré hasta el momento de explicar las conclusiones. 
Por último, se sacarán algunas conclusiones a partir de los datos obtenidos y se intentará dar una explicación a dichas conclusiones.

## Desarrollo del proyecto

En un proyecto anterior ya hemos visto cómo podemos usar la GenAI para crear bases de datos y llenar dichas bases con datos ficticios. En dicho proyecto se ha creado una tabla que simula las ventas de una tienda del sector textil de venta al por menor y se ha creado un archivo CSV a partir de una sentencia SELECT.

Power BI nos permite importar tablas de distintas fuentes, siendo esta una de las propiedades más importantes de esta herramienta. Entre todas estas fuentes, está la importación de archivos CSV, como podemos ver en la figura 1, que también poseen otras herramientas del ecosistema Office de Microsoft, como lo es Excel.

![image](https://github.com/user-attachments/assets/98a682d8-4eb0-4fdb-8060-d328cc725460)

<b>Figura 1:</b> Proceso para importar datos a Power BI.

Para poder importar los datos basta con ir al menú situado en la parte superior de la ventana y, al clickar en “Obtener datos”, vemos que se nos abre un menú desplegable. De entre las opciones que aparecen de manera inmediata en dicho desplegable podemos ver la opción “Texto o CSV”, como ya hemos visto en la figura 1.

Al importar los datos, se nos abrirá una ventana, la de la figura 2, donde veremos la estructura de la tabla y los datos contenidos en esta. Como ya dije en el proyecto donde genero la tabla con Postgres, los datos no se importan correctamente al haber conflictos con los separadores decimales, lo que da como resultado que los precios de los artículos se vean modificados de forma que no nos van a ser útiles. 

![image](https://github.com/user-attachments/assets/4dd5ea97-d8ef-48bc-923d-196c30914065)

<b>Figura 2:</b> Vista previa de la tabla importada.

Para poder hacer los arreglos previos necesarios, haremos click en el botón “Transformar datos”, que se sitúa en la parte inferior de la ventana que se nos ha abierto. Con ello, se nos abre el editor de Power Qwery, una herramienta que ya se poseía con Excel que nos permite trabajar con nuestros datos para poder prepararlos para su posterior visualización y análisis.

En la figura 3 se puede ver cómo modificar la columna “precio” para que pase de ser una columna de datos de tipo número entero, a una columna de datos de tipo número decimal fijo, siendo necesario dividir todos los valores por un factor 100 para obtener los valores reales. 

![image](https://github.com/user-attachments/assets/2ea576b5-adde-4332-b1f2-7ded2e093f5e)

<b>Figura 3:</b> Transofrmación de datos con Power Query.

El último paso, que puede verse en la figura 4, convierte la columna precio a un formato de moneda, pudiendo también seleccionar la moneda con la que va a trabajar el comercio.

![image](https://github.com/user-attachments/assets/2264a1c6-623d-49ec-ac74-ed33162e22fc)

<b>Figura 4:</b> Retoques finales.

Ahora que tenemos los datos importados, se tiene que dejar claro qué se quiere ver y qué datos nos sirven para nuestro análisis y cuáles no nos lo son. Para este proyecto, nos vamos a enfocar en el número de ventas por mes, los ingresos obtenidos por esas ventas y en los artículos de cada tipo que se han vendido y los ingresos que nos han aportado.

Si miramos las columnas de la tabla en la figura 4, vemos que no tenemos lo que se ha ingresado por el total de los artículos, algo que acabamos de declarar como un dato de interés. Como esta columna no se ha proporcionado, voy a crearla insitu. Para ello hago click en “Nueva columna”, selecciono la nueva columna que se ha creado y escribo la sentencia “Ingreso = ventas_articulos_actualizado[precio]*ventas_articulos_actualizado[cantidad]”, obteniendo como salida el total ingresado por la venta de ese día, tal y como puede verse en la figura 5.

Figura 5 aquí

Ahora que tengo todo lo necesario, voy a crear un pequeño dashboard, el de la figura 6, donde presente dos gráficos de barras donde muestre el total de las ventas realizadas cada mes y el total del dinero ingresado por dicho total de ventas. También añado dos gráficos de tipo disco para que se pueda ver el porcentaje de artículos vendidos de cada tipo para cada mes. Por último, añado una serie de botones que funcionarán como filtro para poder enfocarse en un mes o serie de meses concretos.

Figura 6 aquí

Ya con lo que tenemos aquí es posible extraer algunas conclusiones que pueden saltar a simple vista, pero esto lo dejaremos para el final. Ahora vamos a centrarnos en el aporte que ha tenido cada artículo a la caja del comercio.

Para crear la comparativa de lo que ha aportado cada artículo, se va a crear una tabla nueva empleando la función DAX SUMMARIZE, la cual nos permitirá extraer una serie de columnas de otras tablas que tengamos y agrupar los datos en acuerdo al contenido de dichas columnas y por último usaremos la instrucción SUM para obtener el total de artículos vendidos de un mismo tipo a lo largo del mes, así como los ingresos obtenidos de dichas ventas. La tabla obtenida como resultado, así como el código empleado para su confección, pueden apreciarse en la figura 7.

Figura 7 aquí.

En la figura 8 podemos ver el dashboard con los gráficos, los valores promedio de los artículos vendidos y los ingresos obtenidos en promedio por cada artículo y los botones que funcionan a modo de filtro donde se aprecia la evolución mes a mes de las ventas de cada tipo de artículo y lo que ello ha supuesto para los ingresos del comercio, pudiéndose apreciar un aumento de las ventas de edredones en el último cuatrimestre del año y una ausencia de ventas de este mismo artículo en los meses de verano, lo cual es consistente con lo que le habíamos pedido a la IA. 

Figura 8 aquí

De aquí pueden extraerse algunas conclusiones que podrían resultar interesantes. 

* El primero de ellos es precisamente la concentración de las ventas de edredones a lo largo del otoño, lo que explicaría su reducido número de unidades vendidas y de ingresos obtenidos. 
* Se podría intentar una rebaja del precio de los edredones en los meses de verano o hacer algún tipo de oferta que incentive la compra temprana de este artículo o un aumento del precio en los meses de mayor demanda. 
* Con relación a los ingresos a lo largo del año, la caída de ingresos de casi el 50% en los meses de enero y febrero se ve compensada por el aumento de ventas en el último cuatrimestre el año (de casi el 50%). Esto permite tener unos ingresos mensuales promedio de 11000€.
* Para la aportación de cada artículo, en promedio tenemos que las toallas nos han proporcionado unos ingresos de 1800€/mes, siendo el artículo que menos ha aportado, mientras que las sábanas y los edredones nos han proporcionado 2500 y 2800€/mes respectivamente.
* Otro dato interesante es el número de cada artículo que hemos vendido cada mes, lo que puede dar una idea del stock que se espera que acabe vendiéndose. Esto reduciría el número de existencias que acabemos teniendo que guardar en el almacén en caso de no tener el número de ventas esperado.
* Si se desease, se podrían ver los colores que más y que menos se han comprado. Esto podría ser una información que pudiese ser interesante, pero que aquí no voy a ponerme a analizar por no hacer más engorroso el proyecto.

Ahora que ya hemos extraído una serie de resultados de los gráficos que he hecho, tendríamos que pasar a dar una explicación a lo que hemos estado viendo. 

Hay cosas que ya he comentado, como la compensación de las ventas de los dos primeros meses del año con los últimos cuatro o como la estrategia a abordar para intentar aumentar el número de ventas o los ingresos de los edredones. Pero también hay cosas que no he tratado y que debería haber saltado ya a la vista. 

Se ha dicho que el ingreso neto de las ventas de edredones es de 2800€/mes. Si comparamos dicho valor con lo que se supone que hemos obtenido a lo largo del año por este artículo, deberíamos ver que algo no cuadra.

Si tomamos el valor de los ingresos anuales de los edredones que tenemos en el gráfico de disco de la figura 6 y lo dividimos entre los doce meses del año, vemos que el valor promedio de ingresos de este artículo no casa con esos 2800€/mes. En concreto, el valor que tenemos aquí es de 1906,7€/mes. Una diferencia nada desdeñable.

¿Por qué es eso? La razón está en cómo ha calculado Power BI el promedio en la figura 8, que ha sido dividiendo entre los ocho meses donde ha habido ventas en lugar de los doce meses del año. 

¿Y por qué lo ha hecho así? Porque, si nos fijamos en la tabla de la figura 7, no hay entradas para los meses donde no se han hecho ventas. Eso ha hecho que Power BI los obvie. Si quisiésemos que el cálculo fuese correcto, tendríamos que tener una serie de entradas con un número de ventas igual a 0.

Este error es uno que podría darse en una situación real y el analista podría no darse cuenta en un inicio a la hora de trabajar con las tablas o hacer los dashboards, pero es algo que tiene que saber ver y entender cuando haga el análisis de los datos e intente extraer las conclusiones y darles una explicación.

Aquí ya sería cosa del analista el informar de la falta de estas entradas en la base de datos, para que se pueda corregir lo antes posible y que otros compañeros no se encuentren con el mismo fallo. También, para poder seguir trabajando y no ir acumulando retrasos, el analista puede incluir los datos en caso de que estos sean conocidos (si no lo son se deben de pedir para no falsear los resultados) alterando las tablas como corresponda.

En un entorno real, los datos podrían ser mucho más disparejos y mostrar ciertas tendencias en las ventas, siendo también interesante el analizar posibles correlaciones e intentar predecir el comportamiento futuro de los clientes, pero como estos son datos creados por una IA, van a tender a ser lo más próximo posible a un escenario donde todo sea igual y donde haya una causalidad entre más ventas = más ingresos, algo que en la vida real no tiene por qué ser cierto (por ejemplo, podemos vender 100 bolígrafos a 0.70€ e ingresar 70€, o podemos vender un set de cuatro ruedas de coches a 20€ cada rueda, ingresando 80€). 

Otro detalle a tener en cuenta es que la IA ha asignado un precio similar a cada tipo de artículo, así como también ha asignado ventas muy parecidas entre unos y otros, lo que hace que el intentar inferir algo a través de los precios acabe siendo un ejercicio poco enriquecedor para el proyecto.

## Palabras finales.

En este proyecto hemos pasado por todo el proceso de importación, transformación, visualización y análisis de datos de una base de datos muy sencilla que simula las ventas de una tienda de venta al por menor. 

A la hora de importar las tablas en Power BI, había datos que nos faltaban (los ingresos obtenidos por las ventas realizadas), teniendo que crear dichas columnas ad hoc, así como también he creado una tabla nueva que me ha servido para poder obtener aún más resultados que con los datos importados como tal no eran tan inmediatos de ver.

Luego de crear las visualizaciones, he analizado los datos proporcionados, obteniendo algunas conclusiones relevantes y he apuntado a las razones del porqué de dichas conclusiones.

También he señalado un posible error a la hora de hacer el análisis de los datos, haciendo hincapié en la importancia de fijarse en los detalles, escarbar en el por qué las cosas son como son y no dar por sentado todo lo que vemos a simple vista, algo que es en extremo importante para aquellos que buscan comprender el mundo a través de los datos.
