# Graficos
En este repositorio podremos visualizar el segmento de código correspondiente a los gráficos; 
dónde tambien podremos detectar los errores y omisiones para posteriormente corregirlas, 
además de establecer la interación Tester-Programador


A continuación, les anexo el código con el que estamos trabajando para la elaboración de los gráficos de respuestas para apoyo a la adminsitadora (Psicologa):


<----------------------------------------------------------------------------------- ALUMNOS POR GRUPO ---------------------------------------------------------------------------------------->


<?php

	include("conexion.php");
	

	$alumnos = mysql_query("SELECT COUNT(*) FROM respuestasAlum where seccion='seccion' AND grupo='grupo' GROUP BY num_control"); /*Consultamos para obtener el total de los alumnos de esta seccion, grupo, que esten agrupados por numeros de control*/

	$tabla = mysql_query("SELECT * FROM respuestasAlum where seccion='seccion' AND grupo='grupo' ");/*Sleccionamos todas las respuestas de esta "seccion" y de este "grupo".*/
	
	$datos = array();
	
	while ($arreglo=mysql_fetch_array($tabla)){/*Obtenemos respuestas y las sumamos acomulándolas en vectores*/
		
		if($arreglo["respuesta"]==1){
				$datos[1]++;
		}elseif ($arreglo["respuesta"]==2) {
			# code...
				$datos[2]++
		}elseif ($arreglo["respuesta"]==3) {
			# code...
				$datos[3]++:
		}elseif ($arreglo["respuesta"]==4) {
			# code...
				$datos[4]++;
		}elseif ($arreglo["respuesta"]==5) {
			# code...
				$datos[5]++;
		}		
		
	}

	$calculo = 0;

	for ($i=0; $i<count($datos); $i++) {
		$calculo += ( $datos[$i]*(5-$i) );    		
	}

	$estadistica = $calculo/$alumnos;
	
?>

<!DOCTYPE html>
<html>
<head>
	<title></title>
	<script type="text/javascript" src="https://www.google.com/jsapi"></script><!-- Libreria para gráficos -->
	
	<script type="text/javascript">

	    google.load("visualization", "1", {packages:["corechart"]} );
	    
	    google.setOnLoadCallback(graficaVotos);

	    google.setOnLoadCallback(graficaEstadisticas);

	    function graficaEstadisticas(){// Metodo para graficar promedio

	    	var data = google.visualization.arrayToDataTable(
		      	
		      	[
			        ["Element", "", { role: "style" } ],    
			        ["Promedio General",<?php echo $estadistica ?>, "color: blue"]
		        ]
	    	);

		      var view = new google.visualization.DataView(data);
		      view.setColumns( 
		      		[
      				   0, 
      				   1,
                       { 
                       		calc: "stringify",
	                        sourceColumn: 1,
	                        type: "string",
	                        role: "annotation" 
	                    },
	                    2
                   ]
		        );

		      var options = {
		        title: "Gráfica por estadistica",
		       
		        bar: {groupWidth: "20%"},
		        legend: { position: "none" },
		      };

		      var elementoDeVista = new google.visualization.ColumnChart(document.getElementById("GraficaEstadisticas"));
	       	
	       	elementoDeVista.draw(view, options);
		       
	    }

	    function graficaVotos() {//Méotodo para graficar votos por respuesta.

	      	var data = google.visualization.arrayToDataTable(
		      	
		      	[
			        ["Element", "Votos", { role: "style" } ],
			        ["Siempre",<?php echo $datos[0];?>, "color: blue"],
			        ["Casi Siempre",<?php echo $datos[1];?>, "color: green"],
			        ["A Veces", <?php echo $datos[2];?>, "color: yellow"],
			        ["Casi Nunca",<?php echo $datos[3];?> , "color: orange"],
			        ["Nunca",<?php echo $datos[4];?>, "color: red"]
		        ]
	    	);

	      var view = new google.visualization.DataView(data);
	      view.setColumns([0, 1,
	                       { 
	                       		calc: "stringify",
		                         sourceColumn: 1,
		                         type: "string",
		                         role: "annotation" },
		                         2
	                       ]
	                      );

	      var options = {
	        title: "Gráfica por votos",
	       
	        bar: {groupWidth: "95%"},
	        legend: { position: "none" },
	      };

	      var elementoDeVista = new google.visualization.ColumnChart(document.getElementById("GraficaVotos"));

	      
	       elementoDeVista.draw(view, options);
	  }



	  </script>

</head>
<body>
	<div id="GraficaVotos" style="width: 98%; height: 300px;"></div>
	<div id="GraficaEstadisticas" style="width: 98%; height: 300px;"></div>
</body>
</html>

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

<----------------------------------------------------------------------------------- ALUMNOS POR GRUPO Y SEXO -------------------------------------------------------------->
<?php

	include("conexion.php");
	
	

	$datos = array();

	$alumnos = mysql_query("SELECT COUNT(*) FROM respuestasAlum where seccion='$seccion' AND grupo='$grupo' AND sexo='$sexo' GROUP BY num_control");/*Igual pero ahora obtenemos el total de alumnos pero por sexo*/

/*	$tabla = mysql_query("SELECT * FROM respuestasAlum where seccion='$seccion' AND grupo='$grupo' AND sexo='$sexo' "); //Lo mismo pero por grupo
	$alumno = array();

	while ($arreglo=mysql_fetch_array($tabla)){//Cuento respuestas
		
		if($arreglo["respuesta"]==1){
				$datos[1]++;
		}elseif ($arreglo["respuesta"]==2) {
			# code...
				$datos[2]++
		}elseif ($arreglo["respuesta"]==3) {
			# code...
				$datos[3]++:
		}elseif ($arreglo["respuesta"]==4) {
			# code...
				$datos[4]++;
		}elseif ($arreglo["respuesta"]==5) {
			# code...
				$datos[5]++;
		}		
		
	}*/

	$calculo = 0;

	for ($i=0; $i<count($datos); $i++) {
		$calculo += ( $datos[$i]*(5-$i) );    		
	}

	$estadistica = $calculo/$alumnos;
	
?>

<!DOCTYPE html>
<html>
<head>
	<title></title>
	<script type="text/javascript" src="https://www.google.com/jsapi"></script>
	
	<script type="text/javascript">

	    google.load("visualization", "1", {packages:["corechart"]} );
	    
	    google.setOnLoadCallback(graficaVotos);

	    google.setOnLoadCallback(graficaEstadisticas);

	    function graficaEstadisticas(){

	    	var data = google.visualization.arrayToDataTable(
		      	
		      	[
			        ["Element", "", { role: "style" } ],    
			        ["Promedio General",<?php echo $estadistica ?>, "color: blue"]
		        ]
	    	);

		      var view = new google.visualization.DataView(data);
		      view.setColumns( 
		      		[
      				   0, 
      				   1,
                       { 
                       		calc: "stringify",
	                        sourceColumn: 1,
	                        type: "string",
	                        role: "annotation" 
	                    },
	                    2
                   ]
		        );

		      var options = {
		        title: "Gráfica por estadistica",
		       
		        bar: {groupWidth: "20%"},
		        legend: { position: "none" },
		      };

		      var elementoDeVista = new google.visualization.ColumnChart(document.getElementById("GraficaEstadisticas"));
	       	
	       	elementoDeVista.draw(view, options);
		       
	    }

	    function graficaVotos() {

	      	var data = google.visualization.arrayToDataTable(
		      	
		      	[
			        ["Element", "Votos", { role: "style" } ],
			        ["Siempre",<?php echo $datos[0];?>, "color: blue"],
			        ["Casi Siempre",<?php echo $datos[1];?>, "color: green"],
			        ["A Veces", <?php echo $datos[2];?>, "color: yellow"],
			        ["Casi Nunca",<?php echo $datos[3];?> , "color: orange"],
			        ["Nunca",<?php echo $datos[4];?>, "color: red"]// Color para hombre.
		        ]
	    	);

	      var view = new google.visualization.DataView(data);
	      view.setColumns([0, 1,
	                       { 
	                       		calc: "stringify",
		                         sourceColumn: 1,
		                         type: "string",
		                         role: "annotation" },
		                         2
	                       ]
	                      );

	      var options = {
	        title: "Gráfica por votos",
	       
	        bar: {groupWidth: "95%"},
	        legend: { position: "none" },
	      };

	      var elementoDeVista = new google.visualization.ColumnChart(document.getElementById("GraficaVotos"));

	      
	       elementoDeVista.draw(view, options);
	  }



	  </script>

</head>
<body>
	<div id="GraficaVotos" style="width: 98%; height: 300px;"></div>
	<div id="GraficaEstadisticas" style="width: 98%; height: 300px;"></div>
</body>
</html>

<?php

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

<----------------------------------------------------------------------------------- ALUMNOS EN GENERAL ---------------------------------------------------------------------------------------->
	include("conexion.php");
	


	$alumnos = mysql_query("SELECT COUNT(*) FROM respuestasAlum GROUP BY num_control");//Obtenemos todo en general; todos los alumnos.

	$tabla = mysql_query("SELECT * FROM respuestasAlum ");//Seleccionamos todas las respuestas
	
	$datos=array();

	while ($arreglo=mysql_fetch_array($tabla)){//Cotamos y sumamos respuestas.
		
		if($arreglo["respuesta"]==1){
				$datos[1]++;
		}elseif ($arreglo["respuesta"]==2) {
			# code...
				$datos[2]++
		}elseif ($arreglo["respuesta"]==3) {
			# code...
				$datos[3]++:
		}elseif ($arreglo["respuesta"]==4) {
			# code...
				$datos[4]++;
		}elseif ($arreglo["respuesta"]==5) {
			# code...
				$datos[5]++;
		}		
		
	}*/

	$calculo = 0;

	for ($i=0; $i<count($datos); $i++) {
		$calculo += ( $datos[$i]*(5-$i) );    		
	}

	$estadistica = $calculo/$alumnos;
	
?>

<!DOCTYPE html>
<html>
<head>
	<title></title>
	<script type="text/javascript" src="https://www.google.com/jsapi"></script>
	
	<script type="text/javascript">

	    google.load("visualization", "1", {packages:["corechart"]} );
	    
	    google.setOnLoadCallback(graficaVotos);

	    google.setOnLoadCallback(graficaEstadisticas);

	    function graficaEstadisticas(){

	    	var data = google.visualization.arrayToDataTable(
		      	
		      	[
			        ["Element", "", { role: "style" } ],    
			        ["Promedio General",<?php echo $estadistica ?>, "color: blue"]
		        ]
	    	);

		      var view = new google.visualization.DataView(data);
		      view.setColumns( 
		      		[
      				   0, 
      				   1,
                       { 
                       		calc: "stringify",
	                        sourceColumn: 1,
	                        type: "string",
	                        role: "annotation" 
	                    },
	                    2
                   ]
		        );

		      var options = {
		        title: "Gráfica por estadistica",
		       
		        bar: {groupWidth: "20%"},
		        legend: { position: "none" },
		      };

		      var elementoDeVista = new google.visualization.ColumnChart(document.getElementById("GraficaEstadisticas"));
	       	
	       	elementoDeVista.draw(view, options);
		       
	    }

	    function graficaVotos() {

	      	var data = google.visualization.arrayToDataTable(
		      	
		      	[
			        ["Element", "Votos", { role: "style" } ],
			        ["Siempre",<?php echo $datos[0];?>, "color: blue"],
			        ["Casi Siempre",<?php echo $datos[1];?>, "color: green"],
			        ["A Veces", <?php echo $datos[2];?>, "color: yellow"],
			        ["Casi Nunca",<?php echo $datos[3];?> , "color: orange"],
			        ["Nunca",<?php echo $datos[4];?>, "color: red"]
		        ]
	    	);

	      var view = new google.visualization.DataView(data);
	      view.setColumns([0, 1,
	                       { 
	                       		calc: "stringify",
		                         sourceColumn: 1,
		                         type: "string",
		                         role: "annotation" },
		                         2
	                       ]
	                      );

	      var options = {
	        title: "Gráfica por votos",
	       
	        bar: {groupWidth: "95%"},
	        legend: { position: "none" },
	      };

	      var elementoDeVista = new google.visualization.ColumnChart(document.getElementById("GraficaVotos"));

	      
	       elementoDeVista.draw(view, options);
	  }



	  </script>

</head>
<body>
	<div id="GraficaVotos" style="width: 98%; height: 300px;"></div>
	<div id="GraficaEstadisticas" style="width: 98%; height: 300px;"></div>
</body>
</html>
