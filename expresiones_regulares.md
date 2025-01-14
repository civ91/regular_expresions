# Guía de Expresiones Regulares en Linux

Las expresiones regulares (regex) son una herramienta poderosa para buscar, manipular y analizar texto. En Linux, se utilizan ampliamente con herramientas como `grep`, `sed`, `awk`, y más. A continuación, se presenta una recopilación de expresiones regulares comunes con ejemplos prácticos.

## Tabla de Contenidos
1. [Metacaracteres Básicos](#metacaracteres-básicos)
2. [Cuantificadores](#cuantificadores)
3. [Grupos y Alternancias](#grupos-y-alternancias)
4. [Anclas](#anclas)
5. [Clases de Caracteres](#clases-de-caracteres)
6. [Referencias y Capturas](#referencias-y-capturas)
7. [Ejemplos Comunes](#ejemplos-comunes)
8. [Recursos Adicionales](#recursos-adicionales)

---

## Metacaracteres Básicos

| Carácter   | Significado               | Ejemplo                          |
|------------|---------------------------|----------------------------------|
| `.`        | Cualquier carácter        | `a.b` coincide con `aab`, `acb` |
| `\`       | Escapa un metacaracter    | `\.` busca un punto literal     |
| `[]`       | Conjunto de caracteres    | `[aeiou]` busca vocales          |
| `[^]`      | Negación de conjunto      | `[^0-9]` busca no dígitos        |

```bash
# Buscar cualquier carácter
grep 'a.b' archivo.txt

# Buscar un punto literal
grep '\.' archivo.txt
```

## Cuantificadores

| Carácter   | Significado                                   | Ejemplo                             |
|------------|-----------------------------------------------|-------------------------------------|
| `*`        | Cero o más repeticiones                      | `ab*` coincide con `a`, `ab`, `abb`|
| `+`        | Una o más repeticiones                       | `ab+` coincide con `ab`, `abb`     |
| `?`        | Cero o una repetición                        | `ab?` coincide con `a`, `ab`       |
| `{n}`      | Exactamente `n` repeticiones                 | `a{3}` coincide con `aaa`          |
| `{n,}`     | Al menos `n` repeticiones                    | `a{2,}` coincide con `aa`, `aaa`   |
| `{n,m}`    | Entre `n` y `m` repeticiones                 | `a{1,3}` coincide con `a`, `aa`    |

```bash
# Buscar palabras con una o más 'b'
grep 'ab+' archivo.txt

# Buscar exactamente 3 'a'
grep 'a{3}' archivo.txt
```

## Grupos y Alternancias

| Carácter   | Significado                     | Ejemplo                                |
|------------|---------------------------------|----------------------------------------|
| `()`       | Grupo de caracteres            | `(abc)+` coincide con `abc`, `abcabc` |
| `|`        | Alternancia (OR lógico)        | `a|b` coincide con `a` o `b`          |

```bash
# Buscar patrones alternativos
grep 'cat\|dog' archivo.txt

# Buscar repeticiones de un grupo
grep '\(abc\)+' archivo.txt
```

## Anclas

| Carácter   | Significado                       | Ejemplo                            |
|------------|-----------------------------------|------------------------------------|
| `^`        | Inicio de línea                  | `^abc` coincide con líneas que empiezan con `abc` |
| `$`        | Final de línea                   | `abc$` coincide con líneas que terminan con `abc` |
| `\b`      | Frontera de palabra              | `\bword\b` coincide con `word` completo |
| `\B`      | No frontera de palabra           | `\Babc` coincide dentro de palabras |

```bash
# Buscar líneas que comienzan con 'abc'
grep '^abc' archivo.txt

# Buscar líneas que terminan con 'xyz'
grep 'xyz$' archivo.txt
```

## Clases de Caracteres

| Clase       | Significado                     | Ejemplo                           |
|-------------|---------------------------------|-----------------------------------|
| `\d`       | Dígitos (equivale a `[0-9]`)    | `\d+` busca uno o más dígitos    |
| `\D`       | No dígitos (equivale a `[^0-9]`)| `\D+` busca no dígitos           |
| `\w`       | Caracteres alfanuméricos        | `\w+` busca palabras             |
| `\W`       | No alfanuméricos                | `\W+` busca símbolos             |
| `\s`       | Espacios en blanco              | `\s+` busca espacios             |
| `\S`       | No espacios en blanco           | `\S+` busca no espacios          |

```bash
# Buscar dígitos en el texto
grep -E '\d+' archivo.txt

# Buscar palabras alfanuméricas
grep -E '\w+' archivo.txt
```

## Referencias y Capturas

| Carácter   | Significado                     | Ejemplo                             |
|------------|---------------------------------|-------------------------------------|
| `\n`       | Referencia al grupo n           | `(\w)\1` busca caracteres repetidos |

```bash
# Buscar caracteres repetidos
grep -E '(.)\1' archivo.txt
```

## Ejemplos Comunes

1. **Buscar líneas vacías:**
   ```bash
   grep '^$' archivo.txt
   ```
2. **Eliminar espacios en blanco con sed:**
   ```bash
   sed 's/\s//g' archivo.txt
   ```
3. **Extraer direcciones de correo:**
   ```bash
   grep -Eo '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b' archivo.txt
   ```
4. **Validar números de teléfono:**
   ```bash
   grep -E '^\+?[0-9]{10,15}$' archivo.txt
   ```

## Recursos Adicionales
- [Documentación oficial de `grep`](https://www.gnu.org/software/grep/manual/)
- [Guía de sed](https://www.gnu.org/software/sed/manual/sed.html)
- [Regex101](https://regex101.com) - Herramienta interactiva para probar regex.
