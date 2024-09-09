# Actualizar un archivo mediante un algoritmo

## Escenario

Vamos a hacer esta actividad en la que trabajaremos con archivos de texto dentro de un algoritmo de Python, y lo actualizaremos con este mismo.

Nuestra tarea es crear un algoritmo que utilice código Python para comprobar si la lista de permitidos (**allow_list.txt**) contiene alguna dirección IP identificada en la lista de eliminados(**remove_list**). Si es así, debemoss eliminar esas direcciones IP del archivo que contiene la lista de permitidos. 

El archivo `allow_list.txt` podría tener el siguiente contenido, que incluirá las IPs de `remove_list` junto con algunas IPs adicionales:

```python
192.168.97.225
192.168.158.170
192.168.201.40
192.168.58.57
192.168.1.1
10.0.0.1
172.16.0.1
```

El codigo quedaria asi:

```python
# Nombre del archivo que contiene la lista de IPs permitidas
import_file = "allow_list.txt"

# Lista de IPs que queremos eliminar
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# Paso 1: Abrir el archivo en modo lectura para obtener las IPs actuales
with open(import_file, 'r') as file:
    # Leer el contenido del archivo y almacenarlo en una variable
    ip_addresses = file.read()

# Paso 2: Convertir el contenido del archivo (una cadena) en una lista de IPs
ip_addresses_list = ip_addresses.split("\n")

# Paso 3: Iterar sobre la lista de IPs que se deben eliminar (remove_list)
for element in remove_list:
    
    if element in ip_addresses_list:
        
        ip_addresses_list.remove(element)

# Paso 4: Convertir la lista actualizada de IPs nuevamente en una cadena
updated_ip_addresses = "\n".join(ip_addresses_list)

# Paso 5: Abrir el archivo en modo escritura ('w') y escribir la lista de IPs actualizada
with open(import_file, 'w') as file:
    
    file.write(updated_ip_addresses)

print("Las IPs han sido eliminadas correctamente del archivo.")
```



#### **Paso 1: Abrir el archivo `allow_list.txt` en modo lectura**

```python
with open(import_file, 'r') as file:
    ip_addresses = file.read()
```

- En este paso, usamos la declaración `with` para abrir el archivo(**file**) en modo de lectura (`'r'`). Esto garantiza que el archivo se cierre automáticamente después de terminar de leerlo.
- **`file.read()`** lee todo el contenido del archivo como una cadena y lo almacena en la variable `ip_addresses`.

#### **Paso 2: Convertir el contenido del archivo a una lista**

```python
ip_addresses_list = ip_addresses.split("\n")
```

- El contenido del archivo es inicialmente una cadena larga en la que cada dirección IP está separada por una nueva línea. Para manipular las IPs de manera efectiva, convertimos esta cadena en una lista utilizando el método **`.split("\n")`**, que divide la cadena en cada salto de línea, creando una lista donde cada elemento es una dirección IP.

#### **Paso 3: Iterar sobre la lista de IPs que se deben eliminar**

```python
for element in remove_list:
    if element in ip_addresses_list:
        ip_addresses_list.remove(element)
```

- En este paso, definimos la lista `remove_list` con las IPs que queremos eliminar.
- Usamos un **bucle `for`** para iterar sobre cada elemento de `remove_list`.
- Para cada dirección IP en `remove_list`, verificamos si está presente en la lista `ip_addresses_list`. Si la IP está en la lista, la eliminamos usando el método **`.remove()`**.

#### **Paso 4: Convertir la lista actualizada de IPs en una cadena**

```python
updated_ip_addresses = "\n".join(ip_addresses_list)
```

- Después de eliminar las IPs no deseadas, necesitamos volver a convertir la lista `ip_addresses_list` en una cadena para escribirla en el archivo.
- Utilizamos el método **`.join()`** con el separador `"\n"` para unir los elementos de la lista en una cadena, donde cada IP estará en una línea separada por un salto de línea.

#### **Paso 5: Sobrescribir el archivo con la lista de IPs actualizada**

```python
with open(import_file, 'w') as file:
    file.write(updated_ip_addresses)
```

- Abrimos nuevamente el archivo, pero esta vez en modo de escritura (`'w'`), lo que sobrescribirá el contenido anterior del archivo.
- Usamos el método **`.write()`** para escribir la cadena `updated_ip_addresses` en el archivo, reemplazando el contenido antiguo con la lista de IPs actualizada.