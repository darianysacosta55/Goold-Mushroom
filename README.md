# 1. TUPLA: Datos fijos (Inmutables)

info_tienda = ("Frutería Annya", "USD") 

# 2. DICCIONARIO: Relación Clave-Valor (Producto-Precio)
inventario = {
    "manzana": 1.5, 
    "banana": 0.8, 
    "naranja": 1.2,
    "fresa": 2.5,
    "mango": 1.8,
    "piña": 3.0,
    "uva": 2.0
}

# 3. LISTA: Para el historial (Dinámica)
historial_ventas = [] 

continuar = True

print(f"--- Bienvenido a {info_tienda[0]} ---")

while continuar:
    print("\nMenú Principal:")
    print("1. Ver catálogo de productos")
    print("2. Registrar una compra")
    print("3. Salir del sistema")
    
    opcion = input("Seleccione una opción (1-3): ")

    if opcion == "1":
        print("\n--- NUESTRO CATÁLOGO ---")
        for fruta, precio in inventario.items():
            print(f" • {fruta.capitalize()}: {precio} {info_tienda[1]}")

    elif opcion == "2":
        comprando = True
        while comprando:
            fruta = input("\n¿Qué fruta desea comprar? (o escribe 'volver' para ir al menú): ").lower()
            
            if fruta == "volver":
                comprando = False
            elif fruta in inventario:
                try:
                    cantidad = int(input(f"¿Cuántas unidades de {fruta} quiere? "))
                    total = inventario[fruta] * cantidad
                    
                    # Guardamos la venta como una tupla dentro de la lista historial
                    historial_ventas.append((fruta, cantidad, total))
                    print(f" ¡Agregado! {cantidad} {fruta}(s) por {total} {info_tienda[1]}")
                    
                    otra = input("¿Desea agregar otro producto? (si/no): ").lower()
                    if otra != "si":
                        comprando = False
                except ValueError:
                    print(" Por favor, ingrese un número para la cantidad.")
            else:
                print(" Ese producto no está en el inventario.")

    elif opcion == "3":
        # Finalizamos el bucle
        continuar = False
        print("\n--- RESUMEN DE VENTAS ---")
        total_dia = 0
        
        if not historial_ventas:
            print("No se registraron ventas hoy.")
        else:
            for venta in historial_ventas:
                # Desempaquetamos la tupla (fruta, cantidad, total)
                f, c, t = venta
                print(f"Venta: {c} {f} | Subtotal: {t} {info_tienda[1]}")
                total_dia += t

        print(f"\nTOTAL RECAUDADO: {total_dia} {info_tienda[1]}")
        print("¡Gracias por usar el sistema!"
              , "¡Vuelva pronto a frutería Anyya!")
    
    else:
        print("Opción no válida, intente de nuevo.")
