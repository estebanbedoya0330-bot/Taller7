# Taller7


# ---------------------------------------------------------------
# UTILIDADES DE ENTRADA CON VALIDACIÓN
# ---------------------------------------------------------------

def leer_entero(mensaje, minimo=0):
    while True:
        try:
            valor = int(input(mensaje))
            if valor < minimo:
                print(f"Ingrese un número mayor o igual a {minimo}.")
                continue
            return valor
        except ValueError:
            print("Entrada inválida. Ingrese un número entero.")


def leer_decimal(mensaje, minimo=0):
    while True:
        try:
            valor = float(input(mensaje))
            if valor < minimo:
                print(f"Ingrese un número mayor o igual a {minimo}.")
                continue
            return valor
        except ValueError:
            print("Entrada inválida. Ingrese un número.")


# ---------------------------------------------------------------
# ACTIVIDAD GUIADA 1: GESTIÓN DE INVENTARIO
# ---------------------------------------------------------------

def actividad_guiada():
    print("\n=== ACTIVIDAD GUIADA 1: INVENTARIO ===")

    inventario = {
        "cuaderno": 12,
        "lapiz": 30,
        "borrador": 8
    }

    # 1. Tipo de dato de claves y valores
    for clave, valor in inventario.items():
        print(
            f"Clave: {clave!r} -> {type(clave).__name__} | "
            f"Valor: {valor} -> {type(valor).__name__}"
        )

    # 2. Consulta segura de reglas
    print("Cantidad de reglas:", inventario.get("reglas", 0))

    # 3. Agregar regla con valor 10
    inventario["regla"] = 10
    print("Tras agregar 'regla':", inventario)

    # 4. Modificar cuaderno a 15
    inventario["cuaderno"] = 15
    print("Tras modificar 'cuaderno':", inventario)

    # 5. Suma total de existencias
    total = sum(inventario.values())
    print("Total de existencias:", total)


# ---------------------------------------------------------------
# EJERCICIO 1: DIRECTORIO DE CONTACTOS
# ---------------------------------------------------------------

def consultar_contacto(directorio):
    nombre = input("Nombre a consultar: ").strip().title()
    telefono = directorio.get(nombre)

    if telefono is None:
        print(f"El contacto '{nombre}' no existe en el directorio.")
    else:
        print(f"{nombre}: {telefono}")


def guardar_contacto(directorio):
    nombre = input("Nombre del contacto: ").strip().title()

    if not nombre:
        print("El nombre no puede estar vacío.")
        return

    telefono = input("Número de teléfono: ").strip()

    if not telefono:
        print("El teléfono no puede estar vacío.")
        return

    if nombre in directorio:
        print(f"Se actualizó el número de {nombre}.")
    else:
        print(f"Se registró a {nombre}.")

    directorio.update({nombre: telefono})


def listar_contactos(directorio):
    print(f"\n{'NOMBRE':<15}{'TELÉFONO':<15}")
    print("-" * 30)

    for nombre, telefono in directorio.items():
        print(f"{nombre:<15}{telefono:<15}")


def ejercicio_1():
    print("\n=== EJERCICIO 1: DIRECTORIO DE CONTACTOS ===")

    directorio = {
        "Laura": "3001112233",
        "Carlos": "3012223344",
        "Mariana": "3023334455",
        "Andres": "3034445566",
        "Sofia": "3045556677"
    }

    while True:
        print("\n1. Consultar")
        print("2. Actualizar/Registrar")
        print("3. Listar")
        print("4. Volver")

        opcion = input("Opción: ").strip()

        if opcion == "1":
            consultar_contacto(directorio)
        elif opcion == "2":
            guardar_contacto(directorio)
        elif opcion == "3":
            listar_contactos(directorio)
        elif opcion == "4":
            break
        else:
            print("Opción no válida.")


# ---------------------------------------------------------------
# EJERCICIO 2: FRECUENCIA DE PALABRAS
# ---------------------------------------------------------------

def ejercicio_2():
    print("\n=== EJERCICIO 2: FRECUENCIA DE PALABRAS ===")

    parrafo = "python es versatil y python es legible y practico"

    # a) Dividir en palabras
    palabras = parrafo.split()
    print("Palabras:", palabras)

    # b) Diccionario de frecuencias
    frecuencias = {}

    for palabra in palabras:
        frecuencias[palabra] = frecuencias.get(palabra, 0) + 1

    # c) Mostrar el recuento
    for palabra, cantidad in frecuencias.items():
        print(f"{palabra:<10} -> {cantidad}")


# ---------------------------------------------------------------
# EJERCICIO 3: REGISTRO DE CALIFICACIONES
# ---------------------------------------------------------------

def ejercicio_3():
    print("\n=== EJERCICIO 3: CALIFICACIONES ===")

    calificaciones = {
        "Carlos": [4.0, 3.5, 4.5],
        "Mariana": [4.8, 5.0, 4.7],
        "Andres": [3.0, 2.8, 3.5]
    }

    # a) Promedio de cada estudiante
    print("Promedios iniciales:")

    for estudiante, notas in calificaciones.items():
        promedio = sum(notas) / len(notas)
        print(f"{estudiante}: {promedio:.2f}")

    # b) Nueva calificación de 4.0 a Carlos
    calificaciones["Carlos"].append(4.0)

    print(
        "\nNotas de Carlos tras agregar 4.0:",
        calificaciones["Carlos"]
    )

    # c) Estudiante con el promedio más alto
    mejor_estudiante = ""
    mejor_promedio = -1

    print("\nPromedios finales:")

    for estudiante, notas in calificaciones.items():
        promedio = sum(notas) / len(notas)
        print(f"{estudiante}: {promedio:.2f}")

        if promedio > mejor_promedio:
            mejor_promedio = promedio
            mejor_estudiante = estudiante

    print(
        f"\nPromedio más alto: {mejor_estudiante} "
        f"({mejor_promedio:.2f})"
    )


# ---------------------------------------------------------------
# PROYECTO INTEGRADOR: CATÁLOGO DE TIENDA
# ---------------------------------------------------------------

catalogo = {
    "P01": {
        "nombre": "Cuaderno argollado",
        "precio": 6500,
        "stock": 20
    },
    "P02": {
        "nombre": "Caja de micropuntas",
        "precio": 18000,
        "stock": 12
    },
    "P03": {
        "nombre": "Resma de papel",
        "precio": 15000,
        "stock": 8
    }
}


def buscar_producto(catalogo):
    """1. Búsqueda segura por código."""

    codigo = input("Código del producto: ").strip().upper()
    producto = catalogo.get(codigo)

    if producto is None:
        print(
            f"ADVERTENCIA: el código '{codigo}' "
            "no existe en el catálogo."
        )
        return

    print(f"\nCódigo : {codigo}")
    print(f"Nombre : {producto['nombre']}")
    print(f"Precio : ${producto['precio']:,}")
    print(f"Stock  : {producto['stock']} unidades")


def ingresar_existencias(catalogo):
    """2. Incrementa el stock de un producto."""

    codigo = input("Código del producto: ").strip().upper()
    producto = catalogo.get(codigo)

    if producto is None:
        print(
            f"ADVERTENCIA: el código '{codigo}' "
            "no existe en el catálogo."
        )
        return

    cantidad = leer_entero("Cantidad a ingresar: ", minimo=1)

    producto["stock"] += cantidad

    print(
        f"Stock actualizado de {producto['nombre']}: "
        f"{producto['stock']}"
    )


def registrar_producto(catalogo):
    """3. Registra un producto nuevo."""

    codigo = input("Código del nuevo producto: ").strip().upper()

    if not codigo:
        print("El código no puede estar vacío.")
        return

    if codigo in catalogo:
        existente = catalogo[codigo]["nombre"]

        resp = input(
            f"El código {codigo} ya existe ({existente}). "
            "¿Sobreescribir? (s/n): "
        ).strip().lower()

        if resp != "s":
            print("Operación cancelada. No se modificó el catálogo.")
            return

    nombre = input("Nombre: ").strip()

    if not nombre:
        print("El nombre no puede estar vacío.")
        return

    precio = leer_decimal("Precio unitario: ", minimo=0)
    stock = leer_entero("Cantidad en bodega: ", minimo=0)

    if precio == int(precio):
        precio = int(precio)

    catalogo[codigo] = {
        "nombre": nombre,
        "precio": precio,
        "stock": stock
    }

    print(f"Producto {codigo} registrado correctamente.")


def valor_inventario(catalogo):
    """4. Valor monetario total del inventario."""

    total = 0

    print(
        f"\n{'CÓDIGO':<8}{'NOMBRE':<22}"
        f"{'PRECIO':>10}{'STOCK':>8}{'SUBTOTAL':>14}"
    )

    print("-" * 62)

    for codigo, datos in catalogo.items():
        subtotal = datos["precio"] * datos["stock"]
        total += subtotal

        print(
            f"{codigo:<8}{datos['nombre']:<22}"
            f"{datos['precio']:>10,}"
            f"{datos['stock']:>8}"
            f"{subtotal:>14,}"
        )

    print("-" * 62)

    print(
        f"{'VALOR TOTAL DEL INVENTARIO:':<48}"
        f"${total:>13,}"
    )


def proyecto_integrador():
    print("\n=== PROYECTO: CATÁLOGO DE TIENDA ===")

    while True:
        print("\n1. Buscar producto")
        print("2. Ingresar existencias")
        print("3. Registrar producto nuevo")
        print("4. Valor total del inventario")
        print("5. Volver")

        opcion = input("Opción: ").strip()

        if opcion == "1":
            buscar_producto(catalogo)
        elif opcion == "2":
            ingresar_existencias(catalogo)
        elif opcion == "3":
            registrar_producto(catalogo)
        elif opcion == "4":
            valor_inventario(catalogo)
        elif opcion == "5":
            break
        else:
            print("Opción no válida.")


# ---------------------------------------------------------------
# MENÚ PRINCIPAL
# ---------------------------------------------------------------

def main():
    while True:
        print("\n===== TALLER 7: DICCIONARIOS =====")
        print("1. Actividad guiada 1 (inventario)")
        print("2. Ejercicio 1 (contactos)")
        print("3. Ejercicio 2 (frecuencia de palabras)")
        print("4. Ejercicio 3 (calificaciones)")
        print("5. Proyecto integrador (catálogo)")
        print("6. Salir")

        opcion = input("Opción: ").strip()

        if opcion == "1":
            actividad_guiada()
        elif opcion == "2":
            ejercicio_1()
        elif opcion == "3":
            ejercicio_2()
        elif opcion == "4":
            ejercicio_3()
        elif opcion == "5":
            proyecto_integrador()
        elif opcion == "6":
            print("¡Hasta luego!")
            break
        else:
            print("Opción no válida.")


if __name__ == "__main__":
    main()


