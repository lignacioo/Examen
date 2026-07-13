# Examen

# Codigo del Examen de Programación
repositorio
# https://github.com/lignacioo/Examen.git
juegos = {
    'G001': ['Eclipse Runner', 'PC', 'accion', 'T', True, 'NovaStudio'],
    'G002': ['Puzzle Atlas', 'Switch', 'puzzle', 'E', False, 'BrightWorks'],
    'G003': ['Sky Legends', 'PS5', 'aventura', 'T', True, 'OrionGames'],
    'G004': ['Racing Pulse', 'PC', 'carreras', 'E', True, 'VelocityLab'],
    'G005': ['Mystic Farm', 'Switch', 'simulacion', 'E', False, 'GreenSeed'],
    'G006': ['Shadow Tactics', 'Xbox', 'estrategia', 'M', False, 'IronGate']
}

inventario = {
    'G001': [9990, 7],
    'G002': [19990, 0],
    'G003': [42990, 3],
    'G004': [14990, 5],
    'G005': [17990, 9],
    'G006': [39990, 2]
}
# ===========================
# FUNCIONES DE VALIDACIoN
# ===========================

def validar_codigo(codigo):
    codigo = codigo.strip()

    if codigo == "":
        return False

    return True

def validar_titulo(titulo):
    titulo = titulo.strip()

    if titulo == "":
        return False

    return True

def validar_plataforma(plataforma):
    plataforma = plataforma.strip()

    if plataforma == "":
        return False

    return True

def validar_genero(genero):
    genero = genero.strip()

    if genero == "":
        return False

    return True

def validar_clasificacion(clasificacion):

    clasificacion = clasificacion.upper()

    if clasificacion == "E" or clasificacion == "T" or clasificacion == "M":
        return True

    return False

def validar_multiplayer(multiplayer):

    multiplayer = multiplayer.lower()

    if multiplayer == "s" or multiplayer == "n":
        return True

    return False

def validar_editor(editor):

    editor = editor.strip()

    if editor == "":
        return False

    return True

def validar_precio(precio):

    if precio > 0:
        return True

    return False

def validar_stock(stock):

    if stock >= 0:
        return True

    return False


def buscar_codigo(codigo, juegos):

    codigo = codigo.upper()

    for cod in juegos:

        if cod.upper() == codigo:
            return cod

    return None
# ===========================
# OPCIÓN 1
# STOCK POR PLATAFORMA
# ===========================

def stock_plataforma(plataforma, juegos, inventario):

    total_stock = 0

    for codigo in juegos:

        if juegos[codigo][1].lower() == plataforma.lower():

            total_stock += inventario[codigo][1]

    print("El total de stock disponibles es:", total_stock)


# ===========================
# OPCIÓN 2
# BÚSQUEDA POR PRECIO
# ===========================

def busqueda_precio(p_min, p_max, juegos, inventario):

    lista_juegos = []

    for codigo in inventario:

        precio = inventario[codigo][0]
        stock = inventario[codigo][1]

        if precio >= p_min and precio <= p_max and stock > 0:

            titulo = juegos[codigo][0]

            lista_juegos.append(titulo + "--" + codigo)

    lista_juegos.sort()

    if len(lista_juegos) == 0:

        print("No hay juegos en ese rango de precios.")

    else:

        print("Los juegos encontrados son:")

        for juego in lista_juegos:

            print(juego)


# ===========================
# OPCIÓN 3
# ACTUALIZAR PRECIO
# ===========================

def actualizar_precio(codigo, nuevo_precio, juegos, inventario):

    codigo = buscar_codigo(codigo, juegos)

    if codigo == None:

        return False

    inventario[codigo][0] = nuevo_precio

    return True
# ===========================
# OPCIÓN 4
# AGREGAR JUEGO
# ===========================

def agregar_juego(codigo,
                  titulo,
                  plataforma,
                  genero,
                  clasificacion,
                  multiplayer,
                  editor,
                  precio,
                  stock,
                  juegos,
                  inventario):

    if buscar_codigo(codigo, juegos) != None:

        return False

    juegos[codigo.upper()] = [
        titulo,
        plataforma,
        genero,
        clasificacion.upper(),
        multiplayer,
        editor
    ]

    inventario[codigo.upper()] = [
        precio,
        stock
    ]

    return True


# ===========================
# OPCIÓN 5
# ELIMINAR JUEGO
# ===========================

def eliminar_juego(codigo, juegos, inventario):

    codigo = buscar_codigo(codigo, juegos)

    if codigo == None:

        return False

    del juegos[codigo]
    del inventario[codigo]

    return True

# ===========================
# MENÚ PRINCIPAL
# ===========================

def mostrar_menu():

    print("========== MENÚ PRINCIPAL ==========")
    print("1. Stock por plataforma")
    print("2. Búsqueda de juegos por rango de precio")
    print("3. Actualizar precio de juego")
    print("4. Agregar juego")
    print("5. Eliminar juego")
    print("6. Salir")
    print("=====================================")


def leer_opcion():

    return input("Ingrese opción: ")


def main():

    while True:

        mostrar_menu()

        opcion = leer_opcion()

        if opcion == "1":

            plataforma = input("Ingrese plataforma a consultar: ")

            stock_plataforma(plataforma, juegos, inventario)

        elif opcion == "2":

            while True:

                try:

                    minimo = int(input("Ingrese precio mínimo: "))
                    maximo = int(input("Ingrese precio máximo: "))

                    if minimo >= 0 and maximo > minimo:

                        break

                    else:

                        print("Debe ingresar un rango válido.")

                except ValueError:

                    print("Debe ingresar valores enteros")

            busqueda_precio(minimo, maximo, juegos, inventario)

        elif opcion == "3":

            while True:

                codigo = input("Ingrese código del juego: ")

                while True:

                    try:

                        nuevo_precio = int(input("Ingrese nuevo precio: "))

                        if nuevo_precio > 0:

                            break

                        else:

                            print("El precio debe ser mayor que cero.")

                    except ValueError:

                        print("Debe ingresar valores enteros")

                if actualizar_precio(codigo, nuevo_precio, juegos, inventario):

                    print("Precio actualizado")

                else:

                    print("El código no existe")

                respuesta = input("¿Desea actualizar otro precio (s/n)?: ").lower()

                if respuesta == "n":

                    break

        elif opcion == "4":

            codigo = input("Ingrese código del juego: ")
            titulo = input("Ingrese título: ")
            plataforma = input("Ingrese plataforma: ")
            genero = input("Ingrese género: ")
            clasificacion = input("Ingrese clasificación: ")
            multiplayer = input("¿Es multiplayer? (s/n): ")
            editor = input("Ingrese editor: ")

            try:

                precio = int(input("Ingrese precio: "))
                stock = int(input("Ingrese stock: "))

            except ValueError:

                print("Precio y stock deben ser enteros.")
                continue

            if not validar_codigo(codigo):

                print("Código inválido.")

            elif buscar_codigo(codigo, juegos) != None:

                print("El código ya existe")

            elif not validar_titulo(titulo):

                print("Título inválido.")

            elif not validar_plataforma(plataforma):

                print("Plataforma inválida.")

            elif not validar_genero(genero):

                print("Género inválido.")

            elif not validar_clasificacion(clasificacion):

                print("Clasificación inválida.")

            elif not validar_multiplayer(multiplayer):

                print("Valor de multiplayer inválido.")

            elif not validar_editor(editor):

                print("Editor inválido.")

            elif not validar_precio(precio):

                print("Precio inválido.")

            elif not validar_stock(stock):

                print("Stock inválido.")

            else:

                if multiplayer.lower() == "s":

                    multiplayer = True

                else:

                    multiplayer = False

                if agregar_juego(
                    codigo,
                    titulo,
                    plataforma,
                    genero,
                    clasificacion,
                    multiplayer,
                    editor,
                    precio,
                    stock,
                    juegos,
                    inventario):

                    print("Juego agregado")

                else:

                    print("El código ya existe")

        elif opcion == "5":

            codigo = input("Ingrese código del juego: ")

            if eliminar_juego(codigo, juegos, inventario):

                print("Juego eliminado")

            else:

                print("El código no existe")

        elif opcion == "6":

            print("Programa finalizado.")

            break

        else:

            print("Debe seleccionar una opción válida")


main()
