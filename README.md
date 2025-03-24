Parte I
1. Falso
2. Verdadero
3. Verdadero
4. Falso

Parte II
1. B
2. B
3. B

Parte III

class Person:
     def __init__(nombre,edad):
        nombre = nombre
        edad = edad

    def saludar(self):
        return f¨Hola, soy {self.nombre}, y tengo {self.edad} años.¨
p = Persona(¨Carlos¨, 25)
print(p.saludar)

El error del codigo es la falta definir la clase hija que hereda de Persona

Parte IV

class Cliente:
    def __init__(self, cedula, edad, sexo, referido_colegio, tipo_vehiculo):
        self.cedula = cedula
        self.edad = edad
        self.sexo = sexo
        self.referido_colegio = referido_colegio
        self.tipo_vehiculo = tipo_vehiculo

class ClaseManejo:
    def __init__(self, cliente, horas):
        self.cliente = cliente
        self.horas = horas
        self.tarifa_automatica = 25
        self.tarifa_sincronico = 35

    def calcular_monto(self):
        if self.cliente.tipo_vehiculo == "Automático":
            monto = self.horas * self.tarifa_automatica
        else:
            monto = self.horas * self.tarifa_sincronico

        descuento = 0
        if self.cliente.referido_colegio:
            descuento += monto * 0.25
        if self.cliente.edad < 18:
            descuento += monto * 0.20
        if self.horas > 3:
            descuento += monto * 0.15

        monto_total = monto - descuento
        return monto_total, descuento

clientes = []
clases = []

def registrar_cliente():
    cedula = input("Cédula de Identidad: ")
    edad = int(input("Edad: "))
    sexo = input("Sexo: ")
    referido = input("¿Viene referido por algún colegio? (Sí/No): ").lower() == "sí"
    tipo_vehiculo = input("Tipo de vehículo (Automático/Sincrónico): ").capitalize()

    cliente = Cliente(cedula, edad, sexo, referido, tipo_vehiculo)
    clientes.append(cliente)
    print("Cliente registrado con éxito.")

def registrar_clase():
    cedula = input("Cédula del cliente: ")
    cliente = next((c for c in clientes if c.cedula == cedula), None)
    if not cliente:
        print("Cliente no encontrado.")
        return

    horas = int(input("Número de horas de clase: "))
    clase = ClaseManejo(cliente, horas)
    clases.append(clase)
    print("Clase registrada con éxito.")

def generar_recibo():
    cedula = input("Cédula del cliente: ")
    clase = next((c for c in clases if c.cliente.cedula == cedula), None)
    if not clase:
        print("Clase no encontrada para este cliente.")
        return

    monto_total, descuento = clase.calcular_monto()

    print("\n--- Recibo ---")
    print(f"Cédula: {clase.cliente.cedula}")
    print(f"Tipo de Vehículo: {clase.cliente.tipo_vehiculo}")
    print(f"Descuentos: ${descuento:.2f}")
    print(f"Monto Total: ${monto_total:.2f}")

def estadisticas_del_dia():
    total_clientes = len(clientes)
    clientes_automatico = sum(1 for c in clientes if c.tipo_vehiculo == "Automático")
    clientes_sincronico = sum(1 for c in clientes if c.tipo_vehiculo == "Sincrónico")

    total_descuento = sum(c.calcular_monto()[1] for c in clases)
    
    facturacion_automatica = sum(c.calcular_monto()[0] for c in clases if c.cliente.tipo_vehiculo == "Automático")
    facturacion_sincronico = sum(c.calcular_monto()[0] for c in clases if c.cliente.tipo_vehiculo == "Sincrónico")
    
    contador_auto = sum(1 for c in clases if c.cliente.tipo_vehiculo == 'Automático')
    contador_sincro = sum(1 for c in clases if c.cliente.tipo_vehiculo == 'Sincrónico')

    promedio_automatica = facturacion_automatica / contador_auto if contador_auto > 0 else 0
    promedio_sincronico = facturacion_sincronico / contador_sincro if contador_sincro > 0 else 0

    cliente_mas_horas = max(clases, key=lambda c: c.horas).cliente.cedula if clases else "N/A"

    print("\n--- Estadísticas del Día ---")
    print(f"Total de Clientes: {total_clientes}")
    print(f"Clientes Automático: {clientes_automatico}")
    print(f"Clientes Sincrónico: {clientes_sincronico}")
    print(f"Descuento Total: ${total_descuento:.2f}")
    print(f"Promedio Facturación Automático: ${promedio_automatica:.2f}")
    print(f"Promedio Facturación Sincrónico: ${promedio_sincronico:.2f}")
    print(f"Cliente con Más Horas: {cliente_mas_horas}")

while True:
    print("\n--- Autoescuela La Rápida ---")
    print("1. Registrar Cliente")
    print("2. Registrar Clase")
    print("3. Generar Recibo")
    print("4. Estadísticas del Día")
    print("5. Salir")

    opcion = input("Seleccione una opción: ")

    if opcion == "1":
        registrar_cliente()
    elif opcion == "2":
        registrar_clase()
    elif opcion == "3":
        generar_recibo()
    elif opcion == "4":
        estadisticas_del_dia()
    elif opcion == "5":
        break
    else:
        print("Opción no válida.")
