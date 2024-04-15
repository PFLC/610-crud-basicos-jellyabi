
# Aplicación CRUD de PHP

Este repositorio contiene una aplicación PHP CRUD (Create, Read, Update, Delete) simple. Es una demostración básica de cómo integrar PHP con una base de datos MySQL para gestionar datos de usuarios. La aplicación permite a los usuarios agregar, ver, editar y eliminar información de usuario.

## Tecnologías Utilizadas

- **PHP:** Lenguaje de script del lado del servidor utilizado para el desarrollo web.
- **MySQL:** Sistema de gestión de base de datos utilizado para almacenar datos de usuario.
- **HTML & CSS:** Utilizados para estructurar y dar estilo a las páginas web.
- **Tailwind CSS:** Un framework de CSS utilitario para el desarrollo rápido de interfaces de usuario.

## Páginas y Funcionalidades

### 1. Página de Inicio (`display.php`)

![Página de Inicio](images/display.png)

- **Funcionalidad:** Muestra todos los usuarios de la base de datos en un formato de tabla.
- **Características:** 
  - Ver todos los usuarios.
  - Enlaces de navegación para agregar, editar o eliminar información de usuario.

### 2. Agregar Usuario (`user.php`)

![Agregar Usuario](images/add.png)

- **Funcionalidad:** Permite agregar un nuevo usuario a la base de datos.
- **Características:** 
  - Formulario para ingresar detalles del usuario (nombre, correo electrónico, teléfono móvil, contraseña).
  - Validación de datos y envío a la base de datos.

### 3. Editar Usuario (`edit.php`)

![Editar Usuario](images/edit.png)

- **Funcionalidad:** Permite editar detalles de usuarios existentes.
- **Características:** 
  - Formulario prellenado con la información actual del usuario.
  - Actualización de detalles del usuario en la base de datos.

### 4. Eliminar Usuario (`delete.php`)

- **Funcionalidad:** Facilita la eliminación de un usuario de la base de datos.
- **Características:** 
  - Eliminación de información de usuario basada en el ID de usuario.

## Conexión a la Base de Datos (`connect.php`)

- **Propósito:** Establece una conexión con la base de datos MySQL.
- **Credenciales:** Utiliza nombre de host, nombre de usuario, contraseña y nombre de la base de datos para la conexión.

## Cómo Ejecutar

1. Clona el repositorio en tu máquina local.
2. Configura un entorno PHP y MySQL (como XAMPP).
3. Crea la base de datos usando phpmyadmin.
4. Ejecuta la aplicación en un servidor local.

## Nota de Seguridad

Esta aplicación es una demostración básica y no implementa medidas avanzadas de seguridad. Es recomendable utilizar declaraciones preparadas (prepared statements) u ORM para las interacciones con la base de datos para prevenir ataques de inyección SQL.

---

Siéntete libre de contribuir a este proyecto o sugerir mejoras. Para cualquier consulta o problema, por favor abre un issue en este repositorio.

------------------------------------------------------------------------------------------------------------------------------------------------------------

INVESTIGACION

Un sistema CRUD se refiere a un sistema informático que realiza cuatro funciones básicas: Crear, Leer, Actualizar y Borrar (Create, Read, Update, Delete). Los formularios que forman parte de un sistema CRUD estarían diseñados para interactuar con una base de datos y realizar estas operaciones. Aquí hay una descripción de los formularios típicos que podrían formar parte de un sistema CRUD:

Formulario de Creación: Este formulario permite a los usuarios ingresar nueva información en la base de datos. Por lo general, incluye campos para cada atributo o dato que se necesita almacenar y un botón para enviar la información al sistema.

Formulario de Lectura: Este formulario permite a los usuarios ver los datos existentes en la base de datos. Puede mostrar los datos en forma de lista, tabla u otro formato adecuado. Por lo general, no permite la edición directa de los datos.

Formulario de Actualización: Este formulario permite a los usuarios modificar los datos existentes en la base de datos. Presenta los datos actuales en campos editables que los usuarios pueden cambiar según sea necesario. Incluye un botón para enviar los cambios al sistema.

Formulario de Eliminación: Este formulario permite a los usuarios eliminar datos existentes de la base de datos. Puede incluir una lista de elementos disponibles para eliminar, junto con un botón de confirmación para completar la acción.

Además de estos formularios básicos, un sistema CRUD también puede incluir otros elementos de interfaz de usuario, como mensajes de confirmación, validación de datos, paginación o filtros para facilitar la gestión de datos. Estos formularios son esenciales para permitir a los usuarios interactuar de manera efectiva con la base de datos y realizar operaciones CRUD de manera segura y eficiente.

Aquí tienes un ejemplo básico de cómo podrías implementar un CRUD de contactos utilizando un lenguaje de programación como Python y un sistema de gestión de bases de datos relacional como SQLite. Este ejemplo utiliza una aplicación de consola simple:

import sqlite3

# Función para crear la tabla de contactos
def create_table():
    conn = sqlite3.connect('contactos.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS contactos
                 (id INTEGER PRIMARY KEY, nombre TEXT, telefono TEXT, email TEXT)''')
    conn.commit()
    conn.close()

# Función para insertar un nuevo contacto
def insert_contact(nombre, telefono, email):
    conn = sqlite3.connect('contactos.db')
    c = conn.cursor()
    c.execute("INSERT INTO contactos (nombre, telefono, email) VALUES (?, ?, ?)", (nombre, telefono, email))
    conn.commit()
    conn.close()

# Función para mostrar todos los contactos
def show_contacts():
    conn = sqlite3.connect('contactos.db')
    c = conn.cursor()
    c.execute("SELECT * FROM contactos")
    rows = c.fetchall()
    for row in rows:
        print(row)
    conn.close()

# Función para actualizar un contacto existente
def update_contact(id, nombre, telefono, email):
    conn = sqlite3.connect('contactos.db')
    c = conn.cursor()
    c.execute("UPDATE contactos SET nombre=?, telefono=?, email=? WHERE id=?", (nombre, telefono, email, id))
    conn.commit()
    conn.close()

# Función para eliminar un contacto
def delete_contact(id):
    conn = sqlite3.connect('contactos.db')
    c = conn.cursor()
    c.execute("DELETE FROM contactos WHERE id=?", (id,))
    conn.commit()
    conn.close()

# Función principal para ejecutar la aplicación de consola
def main():
    create_table()
    while True:
        print("\nSelecciona una opción:")
        print("1. Agregar contacto")
        print("2. Mostrar contactos")
        print("3. Actualizar contacto")
        print("4. Eliminar contacto")
        print("5. Salir")
        opcion = input("Opción: ")

        if opcion == "1":
            nombre = input("Nombre: ")
            telefono = input("Teléfono: ")
            email = input("Email: ")
            insert_contact(nombre, telefono, email)
            print("Contacto agregado exitosamente.")

        elif opcion == "2":
            print("\nListado de contactos:")
            show_contacts()

        elif opcion == "3":
            id = input("ID del contacto a actualizar: ")
            nombre = input("Nuevo nombre: ")
            telefono = input("Nuevo teléfono: ")
            email = input("Nuevo email: ")
            update_contact(id, nombre, telefono, email)
            print("Contacto actualizado exitosamente.")

        elif opcion == "4":
            id = input("ID del contacto a eliminar: ")
            delete_contact(id)
            print("Contacto eliminado exitosamente.")

        elif opcion == "5":
            print("¡Hasta luego!")
            break

        else:
            print("Opción inválida. Por favor, selecciona una opción válida.")

if __name__ == "__main__":
    main()




