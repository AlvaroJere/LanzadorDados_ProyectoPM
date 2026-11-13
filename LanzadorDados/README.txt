LANZADOR DE DADOS - Proyecto 1ª Evaluación (Digitech FP)
=========================================================
Autores: [Alvaro Jeremias Barreto Diaz] y [Adrian Calderon]

QUÉ PERMITE HACER Y CÓMO SE USA
-------------------------------
Aplicación para realizar tiradas de dados y consultar las anteriores.
1. En la pantalla principal se ve el historial (vacío al empezar).
2. "Nueva tirada" abre la segunda pantalla: se escribe el nombre del jugador,
   se elige el dado (D4, D6, D8 o D20) y se pulsa "Tirar dado".
3. "Guardar" devuelve la tirada y aparece en el historial.
   "Cancelar" o el botón Atrás vuelven sin añadir nada.
4. "Borrar historial" vacía la lista.
Los datos se guardan solo en memoria durante la ejecución.

DÓNDE SE CUMPLE CADA REQUISITO
------------------------------
1. Dos actividades:        MainActivity.java (+ activity_main.xml) y
                           TiradaActivity.java (+ activity_tirada.xml);
                           ambas declaradas en AndroidManifest.xml.
2. Controles:              EditText (etJugador), Button (Tirar, Guardar, Cancelar,
                           Nueva tirada, Borrar) y Spinner (spDado). La opción del
                           Spinner fija el número de caras: TiradaActivity.tirar().
3. Modelo de datos:        Tirada.java (jugador, caras, resultado; constructor,
                           getters, setters; implements Serializable).
4. Intercambio de datos:   MainActivity usa ActivityResultLauncher + Intent;
                           TiradaActivity devuelve la Tirada con setResult(RESULT_OK,..)
                           y, si se cancela, setResult(RESULT_CANCELED) sin datos.
5. Colección:              ArrayList<Tirada> historial en MainActivity.
6. Vistas dinámicas:       item_tirada.xml se infla por cada Tirada en
                           MainActivity.mostrarHistorial(), que añade las vistas al
                           LinearLayout contenedorTiradas dentro de un ScrollView.
                           Se llama a removeAllViews() antes para evitar duplicados.
7. Recursos de texto:      res/values/strings.xml (textos fijos y string-array
                           dados_opciones del Spinner).

RESULTADO DE LAS CUATRO COMPROBACIONES
--------------------------------------
(Rellenar tras ejecutar la app en el emulador y confirmar cada punto.)
1. Estado inicial: aparece el título, "Tiradas realizadas: 0", el mensaje
   "Todavía no hay tiradas..." y la lista vacía.                    [ ] OK
2. Añadir 3 objetos: tres veces "Nueva tirada" -> nombre, dado, Tirar, Guardar.
   El historial muestra 3 tarjetas y el contador marca 3.           [ ] OK
3. Cancelar: "Nueva tirada" -> Tirar -> "Cancelar" (y también con Atrás).
   El historial y el contador no cambian.                           [ ] OK
4. Navegar: tras ir y volver varias veces, las tarjetas anteriores se
   conservan, la nueva se añade al final y no hay duplicados.       [ ] OK
