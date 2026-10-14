# Preentrega: sistema de gestión de artículos

Proyecto `herencia_polimorfismo_tostring`, por MAXIMILIANO CARLOS RATTI. Aplicación Java por consola, con datos en memoria.

## Ejecución en VS Code

1. Descomprimir en una carpeta nueva.
2. Abrir la carpeta `herencia_polimorfismo_tostring`, que contiene `src` y `.vscode`.
3. Tener instalado JDK 17 o superior y Extension Pack for Java.
4. Abrir `src/com/techlab/articulo/App.java`.
5. Ejecutar `main` con Run y responder en la terminal.

Desde PowerShell, dentro de la carpeta del proyecto:

```powershell
New-Item -ItemType Directory -Force -Path out | Out-Null
$fuentes = @(Get-ChildItem src -Recurse -Filter *.java | ForEach-Object { $_.FullName })
javac -encoding UTF-8 --release 17 -d out $fuentes
java -cp out com.techlab.articulo.App
```

## Estructura

- `com.techlab.articulo.App`: Scanner, listas, menú, operaciones y métodos auxiliares.
- `com.techlab.articulo.model.Categoria`: codigo, nombre, descripcion; constructor, getters, setters y toString.
- `Articulo`: clase abstracta; codigo, nombre, precio, categoria privados; constructor y accesores; métodos abstractos getTipoArticulo/getDetalleEspecifico; toString común.
- `ArticuloElectronico`: garantía en meses y teléfono de mesa de ayuda; sobrescribe métodos abstractos y toString.
- `ArticuloAlimenticio`: días para vencimiento; sobrescribe métodos abstractos y toString.

## Menú

1 Ingresar artículo, 2 Listar artículos, 3 Consultar por código, 4 Modificar, 5 Eliminar, 6 Listar categorías, 0 Salir.

Se precargan las categorías Electrónica, Periféricos, Alimentos y Limpieza con los códigos y descripciones de la consigna. El código del artículo lo ingresa el usuario: si está repetido, el alta se cancela. La modificación cambia nombre, precio, categoría y dato específico; no cambia el código.

## Validaciones

Se controlan opciones y tipos inexistentes, códigos duplicados, textos vacíos, números mal escritos, precios negativos/no finitos, garantía o días negativos, categorías inexistentes, artículos inexistentes y operaciones sobre listas vacías. Los precios aceptan punto o coma decimal, sin separadores de miles.

## Prueba guiada

1. Listar artículos sin cargar ninguno: debe avisar que la lista está vacía.
2. Listar categorías: deben mostrarse las cuatro.
3. Ingresar electrónico: código 100, Notebook, precio 850000, categoría 1, garantía 12.
4. Ingresar alimenticio: código 200, Café, precio 5000, categoría 3, vencimiento 60 días.
5. Listar: ambos muestran tipo, categoría y detalle específico, más la marca de subtipo.
6. Intentar otro artículo con código 100: debe rechazar el duplicado.
7. Consultar 100 y luego un código inexistente.
8. Modificar 100: Notebook Pro, 900000, categoría 2, garantía 24. Consultar y comprobar los cambios.
9. Modificar 200: Café Premium, 6000, categoría 3, vencimiento 90. Consultar y comprobar.
10. Eliminar 100 y comprobar que ya no aparece.
11. Probar letras como opción, tipo 3, categoría 99, nombre vacío, precio -1/NaN/Infinity, garantía y vencimiento negativos. Debe solicitar nuevamente el dato que no es válido.
12. Salir con 0.

## Conceptos para explicar

Encapsulamiento: atributos private y getters/setters. Herencia: las subclases utilizan extends y super para reutilizar el constructor. Abstracción: Articulo define lo común y obliga a implementar dos métodos. Polimorfismo: ArrayList<Articulo> contiene ambos tipos; imprimir cada objeto ejecuta su toString real. Sobrescritura: @Override en los métodos de las subclases. Colaboración: cada Articulo referencia una Categoria. instanceof y casting permiten modificar los atributos específicos.

Los setters de este ejemplo son accesores sencillos; la validación de entradas se realiza en App, siguiendo el código de clase. No se incluyen stock, pedidos, interfaces, base de datos, persistencia ni interfaz gráfica. Al cerrar se pierden los artículos ingresados. Los días para vencimiento son un número ingresado manualmente, no una fecha que se actualiza sola.

La consigna pide comprender y desarrollar el proyecto: revisar cada clase y poder explicar su función antes de presentarlo.
