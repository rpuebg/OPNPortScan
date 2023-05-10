import nmap
import time
import os

# Función para limpiar la pantalla
def clear_screen():
    os.system('cls' if os.name == 'nt' else 'clear')

# Función para imprimir el título del programa
def print_title(title):
    clear_screen()
    print(f"\033[1;32;40m{'='*50}")
    print(f"{' '*15}{title.upper()}")
    print(f"{'='*50}\033[0m\n")

# Función para imprimir una barra de progreso
def print_progress_bar(iteration, total, prefix='', suffix='', decimals=1, length=50, fill='█', print_end="\r"):
    percent = ("{0:." + str(decimals) + "f}").format(100 * (iteration / float(total)))
    filled_length = int(length * iteration // total)
    bar = fill * filled_length + '-' * (length - filled_length)
    print(f'\r{prefix} |{bar}| {percent}% {suffix}', end=print_end)
    if iteration == total:
        print()

# Función para escanear la red
def scan_network(ip_address):
    print_title("OPNPortScan by rpuebg")
    print(f"Escaneando la red {ip_address}\n")
    
    # Crea una instancia de nmap.PortScanner
    nm = nmap.PortScanner()

    # Escanea la red en busca de puertos abiertos
    nm.scan(hosts=ip_address, arguments='-sV')

    # Recorre cada host encontrado en la red
    for i, host in enumerate(nm.all_hosts()):
        print_progress_bar(i+1, len(nm.all_hosts()), prefix=f"Procesando {host}:", suffix="Completado", length=30)
        # Imprime la información del host
        print(f'Host: {host} ({nm[host].hostname()})')
        print(f'Estado: {nm[host].state()}')

        # Recorre cada puerto encontrado en el host
        for proto in nm[host].all_protocols():
            # Recorre cada puerto encontrado en el protocolo
            lport = list(nm[host][proto].keys())
            lport.sort()
            for port in lport:
                # Imprime la información del puerto
                print(f'Port : {port}\tState : {nm[host][proto][port]["state"]}')

    print("\nEscaneo completo.")

# Función para mostrar el menú
def show_menu():
    while True:
        print_title("OPNPortScan by rpuebg")
        print("1. Escanear red")
        print("2. Salir")
        choice = input("Ingrese una opción: ")

        if choice == '1':
            ip_address = input("Ingrese la dirección IP de la red a escanear (Ejemplo: 192.168.1.0/24): ")
            scan_network(ip_address)
            input("Presione Enter para continuar...")
        elif choice == '2':
            clear_screen()
            break
        else:
            input("Opción inválida. Presione Enter para continuar...")

# Llamada a la función show_menu para iniciar el programa
show_menu()
