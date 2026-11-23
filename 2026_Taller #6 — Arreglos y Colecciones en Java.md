# Taller #6 — Arreglos y Colecciones en Java

## Encabezado

| Campo | Detalle |
| --- | --- |
| **Materia** | Desarrollo Web |
| **Taller** | #6 |
| **Módulo** | 4 — Arreglos y Colecciones en Java |
| **Modalidad** | Grupal (parejas de 2) |
| **Duración estimada** | 60 – 90 minutos |
| **Repositorio base** | https://github.com/SarmientoEdu/Taller6-java (rama `main`) |

## Objetivos

Al finalizar este taller la pareja será capaz de:

1. Declarar, inicializar y recorrer arreglos de una y dos dimensiones en Java.
2. Crear arreglos de objetos y manipular sus elementos.
3. Usar `ArrayList` y `LinkedList` para almacenar y procesar colecciones dinámicas.
4. Colaborar con Git desde dos computadoras distintas sobre la misma rama de trabajo.

## Instrucciones Generales

Este taller es **guiado**: cada parte te muestra el código completo, explica línea por línea qué hace, y luego te pide ejecutarlo, observar la salida y responder preguntas. Al final de cada parte hay una sección **"Ahora modifica"** donde cambian valores para ver qué pasa.

### Cómo trabajar en pareja

- **Integrante A** es el dueño del fork y abre el PR al final.
- **Integrante B** hace push a la misma rama desde su computadora.
- Ambos deben aparecer como autores de commits (cada uno hace al menos un commit).
- Coordínense: solo uno hace push a la vez para evitar conflictos.

### Lo que SÍ pueden hacer

- Consultar los apuntes del módulo 4.
- Buscar la documentación oficial de Java.
- Discutir entre ustedes la explicación de cada bloque.

### Lo que NO deben hacer

- Copiar código de otros grupos.
- Saltarse la sección de preguntas sin responderlas.
- Dejar los `TODO` sin completar.

## Flujo Git para Grupos

### Integrante A — Configuración inicial

```bash
# 1. Fork de SarmientoEdu/Taller6-java en GitHub (botón Fork)
# 2. Habilitar Actions en el fork (pestaña Actions)
# 3. Clonar
git clone https://github.com/USUARIO-A/Taller6-java.git
cd Taller6-java

# 4. Crear la rama del grupo
git checkout -b taller6-apellidoA-apellidoB
# Ejemplo: git checkout -b taller6-gonzalez-ramos

# 5. Configurar identidad
git config --global user.name "ApellidoA NombreA"
git config --global user.email "correoA@universidad.edu"

# 6. Subir la rama vacía para que B pueda unirse
git push origin taller6-apellidoA-apellidoB
```

### Integrante B — Unirse a la rama

```bash
# B clona el fork de A (no hace fork propio)
git clone https://github.com/USUARIO-A/Taller6-java.git
cd Taller6-java

# Cambiar a la rama del grupo
git checkout taller6-apellidoA-apellidoB

# Configurar identidad de B
git config --global user.name "ApellidoB NombreB"
git config --global user.email "correoB@universidad.edu"
```

### Flujo de trabajo conjunto

Cada vez que uno de los dos quiera hacer push:

```bash
# 1. Bajar los cambios del otro primero
git pull origin taller6-apellidoA-apellidoB

# 2. Agregar y hacer commit
git add src/ParteX.java respuestas/parteX.txt
git commit -m "parteX: descripción de lo que hicieron"

# 3. Subir
git push origin taller6-apellidoA-apellidoB
```

### Commits requeridos

| Commit | Responsable sugerido | Prefijo |
| --- | --- | --- |
| Parte 1 completa | Integrante A | `p1:` |
| Parte 2 completa | Integrante B | `p2:` |
| Parte 3 completa | Integrante A | `p3:` |
| Parte 4 completa | Integrante B | `p4:` |
| PR abierto | A | — |

> Mínimo **4 commits** de **2 autores distintos**. El PR lo abre el Integrante A hacia `SarmientoEdu/Taller6-java`. Título: `[Taller6] ApellidoA-ApellidoB`.

## Parte 1 — Arreglos de una dimensión

**Archivo:** `src/Parte1.java`

### ¿Qué es un arreglo de una dimensión?

Un arreglo es una estructura que almacena **varios valores del mismo tipo** bajo un solo nombre. Cada valor se accede por su índice, que empieza en **0**.

```
nombres[0]  nombres[1]  nombres[2]  nombres[3]  nombres[4]
  "Ana"       "Luis"     "Carla"     "Pedro"     "Marta"
    0            1           2           3           4
```

### Código completo — cópialo exactamente en `src/Parte1.java`

```java
import javax.swing.JOptionPane;

public class Parte1 {
    public static void main(String[] args) {

        // 1. DECLARACIÓN Y CREACIÓN del arreglo
        //    int[] notas  → declara la variable
        //    = new int[5] → crea el arreglo con espacio para 5 enteros
        int[] notas = new int[5];

        // 2. LLENADO: pedimos 5 notas al usuario
        for (int i = 0; i < notas.length; i++) {
            String entrada = JOptionPane.showInputDialog(
                "Ingresa la nota " + (i + 1) + " (0-100):"
            );
            notas[i] = Integer.parseInt(entrada);
        }

        // 3. CÁLCULO de suma y promedio
        int suma = 0;
        for (int i = 0; i < notas.length; i++) {
            suma = suma + notas[i];   // acumula cada nota
        }
        double promedio = (double) suma / notas.length;

        // 4. BÚSQUEDA de nota máxima y mínima
        int maximo = notas[0];   // asumimos que el primero es el mayor
        int minimo = notas[0];   // asumimos que el primero es el menor
        for (int i = 1; i < notas.length; i++) {
            if (notas[i] > maximo) maximo = notas[i];
            if (notas[i] < minimo) minimo = notas[i];
        }

        // 5. CONSTRUCCIÓN del reporte
        StringBuilder reporte = new StringBuilder();
        reporte.append("=== REPORTE DE NOTAS ===\n");
        reporte.append("Notas ingresadas: ");
        for (int i = 0; i < notas.length; i++) {
            reporte.append(notas[i]);
            if (i < notas.length - 1) reporte.append(", ");
        }
        reporte.append("\n");
        reporte.append(String.format("Suma     : %d%n", suma));
        reporte.append(String.format("Promedio : %.2f%n", promedio));
        reporte.append(String.format("Máxima   : %d%n", maximo));
        reporte.append(String.format("Mínima   : %d%n", minimo));

        JOptionPane.showMessageDialog(null, reporte.toString());
    }
}
```

### Explicación línea por línea

| Línea / bloque | Qué hace |
| --- | --- |
| `int[] notas = new int[5]` | Declara y crea un arreglo de 5 enteros. Todos inician en 0. |
| `notas.length` | Propiedad que devuelve el tamaño del arreglo (5 aquí). |
| `notas[i] = Integer.parseInt(entrada)` | Guarda el valor en la posición `i` del arreglo. |
| `maximo = notas[0]` | Inicializa con el primer elemento para comparar con los demás. |
| `(double) suma / notas.length` | El cast `(double)` hace que la división no sea entera. |
| `StringBuilder` | Acumula texto eficientemente para mostrarlo todo junto. |

### ▶ Ejecuta el programa

1. Compila: `javac src/Parte1.java`
2. Ejecuta: `java -cp src Parte1`
3. Ingresa estas 5 notas cuando el programa las pida: **75, 90, 60, 85, 70**

### Salida esperada con esos datos

```
=== REPORTE DE NOTAS ===
Notas ingresadas: 75, 90, 60, 85, 70
Suma     : 380
Promedio : 76.00
Máxima   : 90
Mínima   : 60
```

### 📸 Captura de pantalla

Toma una captura de la ventana de JOptionPane con el resultado y guárdala como `imagenes/p1_resultado.png`.

### ❓ Responde en `respuestas/parte1.txt`

1. ¿Qué índice tiene el último elemento de un arreglo de tamaño 5?
2. ¿Qué pasa si intentas acceder a `notas[5]` en este arreglo? ¿Qué error esperas?
3. ¿Por qué se inicializa `maximo = notas[0]` en vez de `maximo = 0`?
4. ¿Qué significa `(double)` antes de `suma`? ¿Qué pasaría si lo quitas?

### 🔧 Ahora modifica

Cambia el arreglo para que almacene **8 notas** en vez de 5. Ajusta solo la línea de creación. Prueba con: 55, 72, 88, 91, 44, 67, 78, 83. Verifica que el promedio, máximo y mínimo sean correctos.

> Haz commit con mensaje `p1: arreglo 1D de notas con promedio max y min`

## Parte 2 — Arreglos de dos dimensiones

**Archivo:** `src/Parte2.java`

### ¿Qué es un arreglo de dos dimensiones?

Es un arreglo de arreglos: imagínalos como una **tabla con filas y columnas**.

```
          col 0   col 1   col 2
fila 0  [  85,     72,     90  ]   ← estudiante 0
fila 1  [  60,     88,     75  ]   ← estudiante 1
fila 2  [  95,     70,     80  ]   ← estudiante 2
```

En este ejemplo: 3 estudiantes × 3 materias.

### Código completo — cópialo en `src/Parte2.java`

```java
import javax.swing.JOptionPane;

public class Parte2 {
    public static void main(String[] args) {

        // Dimensiones de la tabla
        int filas    = 3;  // estudiantes
        int columnas = 3;  // materias

        // Declaración del arreglo 2D
        int[][] calificaciones = new int[filas][columnas];

        // Nombres de materias (arreglo 1D paralelo)
        String[] materias = {"Matematica", "Español", "Ciencias"};

        // Nombres de estudiantes
        String[] estudiantes = {"Ana", "Luis", "Carla"};

        // LLENADO con datos fijos (sin pedir al usuario para enfocarnos en el 2D)
        calificaciones[0][0] = 85;  calificaciones[0][1] = 72;  calificaciones[0][2] = 90;
        calificaciones[1][0] = 60;  calificaciones[1][1] = 88;  calificaciones[1][2] = 75;
        calificaciones[2][0] = 95;  calificaciones[2][1] = 70;  calificaciones[2][2] = 80;

        // IMPRIMIR la tabla
        StringBuilder reporte = new StringBuilder();
        reporte.append("=== TABLA DE CALIFICACIONES ===\n");
        reporte.append(String.format("%-10s", "Alumno"));
        for (String m : materias) {
            reporte.append(String.format("%-12s", m));
        }
        reporte.append("Promedio\n");
        reporte.append("-".repeat(50)).append("\n");

        // Recorrer FILAS (estudiantes)
        for (int f = 0; f < filas; f++) {
            int sumaFila = 0;
            reporte.append(String.format("%-10s", estudiantes[f]));

            // Recorrer COLUMNAS (materias) de este estudiante
            for (int c = 0; c < columnas; c++) {
                reporte.append(String.format("%-12d", calificaciones[f][c]));
                sumaFila += calificaciones[f][c];
            }
            double promedioFila = (double) sumaFila / columnas;
            reporte.append(String.format("%.2f\n", promedioFila));
        }

        // Promedio por COLUMNA (materia)
        reporte.append("-".repeat(50)).append("\n");
        reporte.append(String.format("%-10s", "Prom.mat"));
        for (int c = 0; c < columnas; c++) {
            int sumaCol = 0;
            for (int f = 0; f < filas; f++) {
                sumaCol += calificaciones[f][c];
            }
            reporte.append(String.format("%-12.2f", (double) sumaCol / filas));
        }

        JOptionPane.showMessageDialog(null, reporte.toString());
    }
}
```

### Explicación clave

| Concepto | Explicación |
| --- | --- |
| `int[][] calificaciones = new int[3][3]` | Crea 3 filas, cada una con 3 columnas. Total: 9 celdas. |
| `calificaciones[f][c]` | Accede a la fila `f`, columna `c`. |
| Bucle doble `for` | El externo recorre filas; el interno recorre columnas de esa fila. |
| `String.format("%-10s", texto)` | Alinea el texto a la izquierda en un campo de 10 caracteres. |

### ▶ Ejecuta el programa

1. `javac src/Parte2.java`
2. `java -cp src Parte2`

### Salida esperada

```
=== TABLA DE CALIFICACIONES ===
Alumno    Matematica  Español     Ciencias    Promedio
--------------------------------------------------
Ana       85          72          90          82.33
Luis      60          88          75          74.33
Carla     95          70          80          81.67
--------------------------------------------------
Prom.mat  80.00       76.67       81.67
```

### 📸 Captura de pantalla

Guarda la captura como `imagenes/p2_resultado.png`.

### ❓ Responde en `respuestas/parte2.txt`

1. ¿Cómo accedes al valor `88` (Luis en Español) usando índices?
2. ¿Cuántos bucles `for` necesitas para recorrer todos los elementos de un arreglo 2D? ¿Por qué?
3. Si agregas un cuarto estudiante, ¿qué línea de código tendrías que cambiar?
4. ¿Qué significa `String.format("%-12d", valor)`? ¿Qué cambia si quitas el `-`?

### 🔧 Ahora modifica

Agrega un **cuarto estudiante** llamado `"Pedro"` con notas `78, 65, 92`. Ajusta el arreglo, el nombre y los datos. Verifica que los promedios de columna se recalculen automáticamente.

> Haz commit con mensaje `p2: tabla de calificaciones con arreglo 2D`

## Parte 3 — Arreglos de Objetos

**Archivos:** `src/Producto.java` y `src/Parte3.java`

### ¿Qué es un arreglo de objetos?

En vez de guardar números o texto simples, guardamos **objetos** (instancias de una clase). Cada posición del arreglo apunta a un objeto con sus propios atributos.

```
productos[0] → Producto { nombre="Laptop",   precio=850.00, stock=5 }
productos[1] → Producto { nombre="Mouse",    precio=25.50,  stock=20 }
productos[2] → Producto { nombre="Teclado",  precio=45.00,  stock=15 }
productos[3] → Producto { nombre="Monitor",  precio=320.00, stock=8 }
```

### Paso 1 — Crear la clase `Producto`

Guarda este código en `src/Producto.java`:

```java
/**
 * Clase que representa un producto de inventario.
 * Un arreglo de objetos Producto forma el inventario.
 */
public class Producto {

    // ATRIBUTOS del objeto
    String nombre;
    double precio;
    int    stock;

    // CONSTRUCTOR: inicializa el objeto con sus datos
    public Producto(String nombre, double precio, int stock) {
        this.nombre = nombre;   // "this." distingue el atributo del parámetro
        this.precio = precio;
        this.stock  = stock;
    }

    // MÉTODO: calcula el valor total en inventario
    public double valorTotal() {
        return precio * stock;
    }

    // MÉTODO: representación en texto del objeto
    public String toString() {
        return String.format("%-12s  $%7.2f   stock: %3d   valor: $%8.2f",
            nombre, precio, stock, valorTotal());
    }
}
```

### Paso 2 — Usar el arreglo de objetos en `Parte3.java`

```java
import javax.swing.JOptionPane;

public class Parte3 {
    public static void main(String[] args) {

        // 1. DECLARACIÓN Y CREACIÓN del arreglo de objetos
        //    Cada elemento es una referencia a un objeto Producto
        Producto[] productos = new Producto[4];

        // 2. CREACIÓN de cada objeto con su constructor
        productos[0] = new Producto("Laptop",   850.00, 5);
        productos[1] = new Producto("Mouse",     25.50, 20);
        productos[2] = new Producto("Teclado",   45.00, 15);
        productos[3] = new Producto("Monitor",  320.00, 8);

        // 3. ACCESO y VISUALIZACIÓN de cada elemento
        StringBuilder reporte = new StringBuilder();
        reporte.append("=== INVENTARIO DE PRODUCTOS ===\n");
        reporte.append(String.format("%-12s  %-9s  %-11s  %s\n",
            "Nombre", "Precio", "Stock", "Valor Total"));
        reporte.append("-".repeat(55)).append("\n");

        double valorTotalInventario = 0;
        Producto masEconomico  = productos[0];
        Producto masValioso    = productos[0];

        for (int i = 0; i < productos.length; i++) {
            // toString() se llama automáticamente al concatenar con "+"
            reporte.append(productos[i].toString()).append("\n");

            // Acumular valor total
            valorTotalInventario += productos[i].valorTotal();

            // Buscar más económico (menor precio)
            if (productos[i].precio < masEconomico.precio) {
                masEconomico = productos[i];
            }
            // Buscar más valioso (mayor valorTotal)
            if (productos[i].valorTotal() > masValioso.valorTotal()) {
                masValioso = productos[i];
            }
        }

        reporte.append("-".repeat(55)).append("\n");
        reporte.append(String.format("Valor total inventario: $%.2f\n", valorTotalInventario));
        reporte.append("Producto más económico : ").append(masEconomico.nombre).append("\n");
        reporte.append("Mayor valor inventario : ").append(masValioso.nombre).append("\n");

        // 4. MANIPULACIÓN: aplicar 10% de descuento al producto más caro
        //    (el de mayor precio individual)
        Producto masCaro = productos[0];
        for (int i = 1; i < productos.length; i++) {
            if (productos[i].precio > masCaro.precio) {
                masCaro = productos[i];
            }
        }
        reporte.append("\n--- Descuento aplicado ---\n");
        reporte.append("Antes : ").append(masCaro.toString()).append("\n");
        masCaro.precio = masCaro.precio * 0.90;  // modifica el atributo directamente
        reporte.append("Después: ").append(masCaro.toString()).append("\n");

        JOptionPane.showMessageDialog(null, reporte.toString());
    }
}
```

### Explicación clave

| Concepto | Explicación |
| --- | --- |
| `Producto[] productos = new Producto[4]` | Crea 4 casillas vacías (`null`). Todavía no hay objetos. |
| `new Producto("Laptop", 850.00, 5)` | Llama al constructor y crea el objeto en memoria. |
| `productos[i].precio` | Accede al atributo `precio` del objeto en posición `i`. |
| `productos[i].valorTotal()` | Llama al método `valorTotal()` del objeto en posición `i`. |
| `masEconomico = productos[i]` | No copia el objeto: ambas variables apuntan al mismo. |

### ▶ Ejecuta el programa

1. Compila ambos archivos juntos:

   ```bash
   javac src/Producto.java src/Parte3.java
   ```
2. Ejecuta:

   ```bash
   java -cp src Parte3
   ```

### Salida esperada

```
=== INVENTARIO DE PRODUCTOS ===
Nombre        Precio     Stock       Valor Total
-------------------------------------------------------
Laptop        $  850.00   stock:   5   valor: $ 4250.00
Mouse         $   25.50   stock:  20   valor: $  510.00
Teclado       $   45.00   stock:  15   valor: $  675.00
Monitor       $  320.00   stock:   8   valor: $ 2560.00
-------------------------------------------------------
Valor total inventario: $7995.00
Producto más económico : Mouse
Mayor valor inventario : Laptop

--- Descuento aplicado ---
Antes : Laptop        $  850.00   stock:   5   valor: $ 4250.00
Después: Laptop        $  765.00   stock:   5   valor: $ 3825.00
```

### 📸 Captura de pantalla

Guarda como `imagenes/p3_resultado.png`.

### ❓ Responde en `respuestas/parte3.txt`

1. ¿Qué contiene `productos[0]` antes de ejecutar `new Producto(...)`?
2. ¿Qué diferencia hay entre `productos[i].precio` y `productos[i].valorTotal()`?
3. Cuando haces `masEconomico = productos[i]`, ¿se copian los datos del objeto o solo la referencia? ¿Qué implica eso?
4. Después del descuento, ¿el `valorTotalInventario` impreso refleja el nuevo precio? ¿Por qué?

### 🔧 Ahora modifica

Agrega un quinto producto: `"Audífonos"`, precio `$75.00`, stock `30`. Luego aplica un **15% de descuento** al producto con **mayor stock** (en vez del más caro). Imprime el nombre del producto afectado.

> Haz commit con mensaje `p3: inventario con arreglo de objetos Producto`

## Parte 4 — Colecciones ArrayList y LinkedList

**Archivo:** `src/Parte4.java`

### ¿Por qué colecciones si ya tenemos arreglos?

Los arreglos tienen **tamaño fijo**: si declaras `int[5]`, siempre son 5. Las colecciones son **dinámicas**: crecen y encogen según necesites. Además ofrecen métodos útiles como `add`, `remove`, `contains`, `size`.

### ArrayList vs LinkedList — diferencia clave

|  | ArrayList | LinkedList |
| --- | --- | --- |
| Acceso por índice | Rápido (`get(i)`) | Lento (recorre desde el inicio) |
| Insertar/eliminar al medio | Lento (desplaza elementos) | Rápido (redirige referencias) |
| Uso típico | Leer datos frecuentemente | Insertar/eliminar frecuentemente |
| Ambas implementan | `List` | `List` |

### Código completo — cópialo en `src/Parte4.java`

```java
import javax.swing.JOptionPane;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Collections;

public class Parte4 {
    public static void main(String[] args) {

        // ════════════════════════════════
        // SECCIÓN A: ArrayList de Strings
        // ════════════════════════════════

        // 1. CREACIÓN — sin tamaño fijo
        ArrayList<String> ciudades = new ArrayList<>();

        // 2. ADD — agregar elementos
        ciudades.add("Panamá");
        ciudades.add("Colón");
        ciudades.add("David");
        ciudades.add("Santiago");
        ciudades.add("Chitré");

        // 3. SIZE — tamaño actual
        StringBuilder sb = new StringBuilder();
        sb.append("=== ArrayList de ciudades ===\n");
        sb.append("Tamaño: ").append(ciudades.size()).append("\n");

        // 4. GET — acceso por índice
        sb.append("Primera ciudad: ").append(ciudades.get(0)).append("\n");
        sb.append("Última ciudad : ").append(ciudades.get(ciudades.size() - 1)).append("\n");

        // 5. CONTAINS — verificar existencia
        sb.append("¿Contiene 'David'? ").append(ciudades.contains("David")).append("\n");
        sb.append("¿Contiene 'Bocas'? ").append(ciudades.contains("Bocas")).append("\n");

        // 6. RECORRER con for-each
        sb.append("\nLista completa:\n");
        for (String ciudad : ciudades) {
            sb.append("  - ").append(ciudad).append("\n");
        }

        // 7. REMOVE — eliminar por valor
        ciudades.remove("Colón");
        sb.append("\nDespués de eliminar 'Colón': ").append(ciudades).append("\n");

        // 8. ADD en posición específica
        ciudades.add(1, "Bocas del Toro");  // inserta en índice 1
        sb.append("Después de insertar en pos 1: ").append(ciudades).append("\n");

        // 9. SORT — ordenar
        Collections.sort(ciudades);
        sb.append("Ordenadas alfabéticamente: ").append(ciudades).append("\n");

        JOptionPane.showMessageDialog(null, sb.toString());
        sb.setLength(0); // limpiar el StringBuilder

        // ════════════════════════════════
        // SECCIÓN B: ArrayList de enteros con operaciones
        // ════════════════════════════════

        ArrayList<Integer> numeros = new ArrayList<>();
        int[] datos = {34, 12, 78, 56, 23, 89, 45, 67};
        for (int d : datos) {
            numeros.add(d);
        }

        int suma = 0;
        int mayor = numeros.get(0);
        for (int n : numeros) {
            suma += n;
            if (n > mayor) mayor = n;
        }

        sb.append("=== ArrayList de números ===\n");
        sb.append("Lista: ").append(numeros).append("\n");
        sb.append("Suma  : ").append(suma).append("\n");
        sb.append(String.format("Prom  : %.2f\n", (double) suma / numeros.size()));
        sb.append("Mayor : ").append(mayor).append("\n");

        // Eliminar todos los menores a 50
        ArrayList<Integer> mayoresDe50 = new ArrayList<>();
        for (int n : numeros) {
            if (n >= 50) mayoresDe50.add(n);
        }
        sb.append("Mayores o iguales a 50: ").append(mayoresDe50).append("\n");

        JOptionPane.showMessageDialog(null, sb.toString());
        sb.setLength(0);

        // ════════════════════════════════
        // SECCIÓN C: LinkedList como cola (FIFO)
        // ════════════════════════════════

        LinkedList<String> cola = new LinkedList<>();

        // addLast = agregar al final (enqueue)
        cola.addLast("Cliente 1");
        cola.addLast("Cliente 2");
        cola.addLast("Cliente 3");
        cola.addLast("Cliente 4");

        sb.append("=== LinkedList como Cola (turno bancario) ===\n");
        sb.append("Cola inicial: ").append(cola).append("\n\n");

        // removeFirst = atender al primero (dequeue)
        sb.append("Atendiendo clientes:\n");
        while (!cola.isEmpty()) {
            String cliente = cola.removeFirst();
            sb.append("  Atendido: ").append(cliente);
            sb.append(" | Restantes en cola: ").append(cola.size()).append("\n");
        }
        sb.append("\nCola vacía. Fin de atención.\n");

        // addFirst = urgencia (enqueue al frente)
        cola.addLast("Cliente A");
        cola.addLast("Cliente B");
        cola.addFirst("URGENTE");  // salta al frente
        sb.append("\nNueva cola con urgencia: ").append(cola).append("\n");

        JOptionPane.showMessageDialog(null, sb.toString());
    }
}
```

### Explicación clave

| Método | Qué hace |
| --- | --- |
| `add(elemento)` | Agrega al final de la lista |
| `add(índice, elemento)` | Inserta en una posición específica |
| `get(índice)` | Devuelve el elemento en esa posición |
| `remove("valor")` | Elimina la primera ocurrencia del valor |
| `size()` | Devuelve cuántos elementos tiene |
| `contains("valor")` | Devuelve `true` si el elemento existe |
| `Collections.sort(lista)` | Ordena la lista de menor a mayor |
| `addFirst / addLast` | Solo en `LinkedList`: agregar al inicio o final |
| `removeFirst / removeLast` | Solo en `LinkedList`: quitar del inicio o final |
| `isEmpty()` | Devuelve `true` si la lista está vacía |

### ▶ Ejecuta el programa

```bash
javac src/Parte4.java
java -cp src Parte4
```

Aparecerán 3 ventanas de JOptionPane en secuencia (una por sección). Cierra cada una para ver la siguiente.

### Salida esperada — Ventana 1 (ArrayList ciudades)

```
=== ArrayList de ciudades ===
Tamaño: 5
Primera ciudad: Panamá
Última ciudad : Chitré
¿Contiene 'David'? true
¿Contiene 'Bocas'? false

Lista completa:
  - Panamá
  - Colón
  - David
  - Santiago
  - Chitré

Después de eliminar 'Colón': [Panamá, David, Santiago, Chitré]
Después de insertar en pos 1: [Panamá, Bocas del Toro, David, Santiago, Chitré]
Ordenadas alfabéticamente: [Bocas del Toro, Chitré, David, Panamá, Santiago]
```

### Salida esperada — Ventana 2 (ArrayList números)

```
=== ArrayList de números ===
Lista: [34, 12, 78, 56, 23, 89, 45, 67]
Suma  : 404
Prom  : 50.50
Mayor : 89
Mayores o iguales a 50: [78, 56, 89, 67]
```

### Salida esperada — Ventana 3 (LinkedList cola)

```
=== LinkedList como Cola (turno bancario) ===
Cola inicial: [Cliente 1, Cliente 2, Cliente 3, Cliente 4]

Atendiendo clientes:
  Atendido: Cliente 1 | Restantes en cola: 3
  Atendido: Cliente 2 | Restantes en cola: 2
  Atendido: Cliente 3 | Restantes en cola: 1
  Atendido: Cliente 4 | Restantes en cola: 0

Cola vacía. Fin de atención.

Nueva cola con urgencia: [URGENTE, Cliente A, Cliente B]
```

### 📸 Capturas de pantalla

Guarda las 3 capturas como:

- `imagenes/p4a_ciudades.png`
- `imagenes/p4b_numeros.png`
- `imagenes/p4c_cola.png`

### ❓ Responde en `respuestas/parte4.txt`

1. ¿Cuál es la diferencia entre `add("valor")` y `add(1, "valor")`?
2. ¿Qué ocurre si intentas hacer `ciudades.get(10)` en una lista de 5 elementos?
3. ¿Por qué usamos `ArrayList<Integer>` y no `ArrayList<int>`?
4. ¿Cuál es el orden de atención en una cola (FIFO)? ¿Cuál sería el orden en una pila (LIFO) con `addFirst/removeFirst`?
5. ¿Cuándo preferirías usar `LinkedList` sobre `ArrayList` y viceversa?

### 🔧 Ahora modifica

En la **Sección B**, cambia el filtro de `>= 50` a `>= 40` y agrega también la **suma de los elementos filtrados**. En la **Sección C**, simula que llegan 2 clientes nuevos (`"Cliente 5"` y `"Cliente 6"`) mientras ya hay clientes en cola, y muestra la cola completa antes de seguir atendiendo.

> Haz commit con mensaje `p4: colecciones ArrayList y LinkedList`

## Qué modificar después

Antes de abrir el PR, verifica esta lista:

- [ ] `src/Parte1.java` ejecuta sin errores y la salida coincide con la esperada.
- [ ] `src/Parte2.java` muestra la tabla correctamente con los 3 (o 4) estudiantes.
- [ ] `src/Producto.java` y `src/Parte3.java` compilan juntos y aplican el descuento.
- [ ] `src/Parte4.java` muestra las 3 ventanas de JOptionPane.
- [ ] Los archivos de respuestas (`respuestas/parte1.txt` … `parte4.txt`) están completos.
- [ ] Hay al menos **6 imágenes** en `imagenes/` (p1, p2, p3, p4a, p4b, p4c).
- [ ] Hay al menos **4 commits** con **2 autores distintos**.
- [ ] La rama tiene el formato `taller6-apellidoA-apellidoB`.

### Abrir el Pull Request (Integrante A)

```bash
git push origin taller6-apellidoA-apellidoB
```

Luego en GitHub:

1. Ve a tu fork → botón **Compare & pull request**.
2. Base: `SarmientoEdu/Taller6-java` → `main`.
3. Título: `[Taller6] ApellidoA-ApellidoB`
4. Descripción: respondan **¿cuál fue la diferencia más notable que observaron entre ArrayList y LinkedList al modificar el código?**
5. Clic en **Create pull request**.

### Rúbrica rápida

| Criterio | Puntos |
| --- | --- |
| Parte 1 — código funciona + preguntas + modificación | 20 |
| Parte 2 — tabla correcta + preguntas + 4to estudiante | 20 |
| Parte 3 — inventario correcto + preguntas + modificación | 25 |
| Parte 4 — 3 secciones + preguntas + modificaciones | 25 |
| Git — 2 autores, 4+ commits, rama correcta, PR | 10 |
| **Total** | **100** |
