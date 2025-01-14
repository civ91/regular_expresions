# Introducción a la Programación en Bash

El shell de Bash (Bourne Again SHell) es uno de los intérpretes de comandos más populares en sistemas Linux y macOS. Aprender a programar en Bash te permitirá automatizar tareas, trabajar eficientemente con el sistema y desarrollar scripts personalizados.

---

## Tabla de Contenidos
1. [¿Qué es Bash?](#que-es-bash)
2. [Primeros Pasos](#primeros-pasos)
   - [Tu Primer Script](#tu-primer-script)
   - [Hacerlo Ejecutable](#hacerlo-ejecutable)
3. [Conceptos Básicos](#conceptos-basicos)
   - [Comentarios](#comentarios)
   - [Variables](#variables)
   - [Entrada y Salida](#entrada-y-salida)
4. [Control de Flujo](#control-de-flujo)
   - [Condicionales](#condicionales)
   - [Bucles](#bucles)
5. [Funciones](#funciones)
6. [Ejemplos Prácticos](#ejemplos-practicos)
7. [Recursos Adicionales](#recursos-adicionales)

---

## ¿Qué es Bash?

Bash es un intérprete de comandos que te permite interactuar con el sistema operativo. Además de ejecutar comandos, Bash soporta scripting, lo que significa que puedes escribir programas completos para automatizar tareas repetitivas.

---

## Primeros Pasos

### Tu Primer Script
Un script de Bash es simplemente un archivo de texto que contiene comandos ejecutables. Para empezar, crea un archivo llamado `hola_mundo.sh`:

```bash
#!/bin/bash
# Esto es un comentario

echo "¡Hola, mundo!"
```

### Hacerlo Ejecutable

1. Guarda el archivo.
2. Hazlo ejecutable utilizando el comando:
   ```bash
   chmod +x hola_mundo.sh
   ```
3. Ejecuta el script:
   ```bash
   ./hola_mundo.sh
   ```

Si ves el mensaje "¡Hola, mundo!", ¡has creado tu primer script en Bash!

---

## Conceptos Básicos

### Comentarios
Los comentarios en Bash comienzan con el carácter `#`. Todo lo que esté después de `#` en una línea no será ejecutado:

```bash
# Esto es un comentario
```

### Variables
Puedes almacenar valores en variables para usarlos más tarde:

```bash
nombre="Carlos"
echo "Hola, $nombre"
```

### Entrada y Salida
- **Entrada del usuario:** Puedes pedir datos al usuario con el comando `read`:
  ```bash
  echo "¿Cómo te llamas?"
  read nombre
  echo "Hola, $nombre"
  ```

- **Salida:** Usa `echo` para imprimir texto en la terminal.

---

## Control de Flujo

### Condicionales
Los condicionales permiten tomar decisiones basadas en condiciones:

```bash
if [ $1 -gt 10 ]; then
  echo "El número es mayor que 10."
else
  echo "El número es menor o igual a 10."
fi
```

### Bucles
Los bucles te permiten repetir tareas:

- **`for` loop:**
  ```bash
  for i in 1 2 3; do
    echo "Número: $i"
  done
  ```

- **`while` loop:**
  ```bash
  contador=1
  while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    contador=$((contador + 1))
  done
  ```

---

## Funciones
Las funciones te permiten organizar tu código:

```bash
saludar() {
  echo "Hola, $1"
}

saludar "Carlos"
```

---

## Ejemplos Prácticos

1. **Script para hacer una copia de seguridad:**
   ```bash
   #!/bin/bash
   archivo_origen="/ruta/a/origen"
   archivo_destino="/ruta/a/destino"
   cp $archivo_origen $archivo_destino
   echo "Copia de seguridad completada."
   ```

2. **Contador de líneas en un archivo:**
   ```bash
   #!/bin/bash
   archivo="$1"
   lineas=$(wc -l < "$archivo")
   echo "El archivo $archivo tiene $lineas líneas."
   ```

---

## Recursos Adicionales

- [Guía Oficial de Bash](https://www.gnu.org/software/bash/)
- [Tutorial de Bash para Principiantes](https://ryanstutorials.net/bash-scripting-tutorial/)
- [Referencia Rápida de Comandos de Linux](https://ss64.com/bash/)
