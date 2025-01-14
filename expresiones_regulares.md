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
echo -e "aab\nacb\nab" | grep 'a.b'

# Buscar un punto literal
echo -e "file.txt\nfile1txt" | grep '\.'

# Buscar vocales
echo "hola mundo" | grep '[aeiou]'

# Buscar caracteres que no sean dígitos
echo "abc123" | grep '[^0-9]'
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
# Buscar palabras con cero o más 'b'
echo -e "a\nab\nabb" | grep 'ab*'

# Buscar una o más 'b'
echo -e "a\nab\nabb" | grep 'ab+'

# Buscar exactamente 3 'a'
echo -e "aa\naaa\naaaa" | grep 'a{3}'

# Buscar al menos 2 'a'
echo -e "a\naa\naaa" | grep 'a{2,}'

# Buscar entre 1 y 3 'a'
echo -e "a\naa\naaa\naaaa" | grep 'a{1,3}'
```

## Grupos y Alternancias

| Carácter   | Significado                     | Ejemplo                                |
|------------|---------------------------------|----------------------------------------|
| `()`       | Grupo de caracteres            | `(abc)+` coincide con `abc`, `abcabc` |
| `|`        | Alternancia (OR lógico)        | `a|b` coincide con `a` o `b`          |

```bash
# Buscar patrones alternativos
echo -e "cat\ndog\nrat" | grep 'cat\|dog'

# Buscar repeticiones de un grupo
echo -e "abc\nabcabc\nab" | grep '\(abc\)+'
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
echo -e "abc\ndef\nabcde" | grep '^abc'

# Buscar líneas que terminan con 'xyz'
echo -e "xyz\nabcxyz\nabc" | grep 'xyz$'

# Buscar palabra completa 'word'
echo -e "word\nsword\nwords" | grep '\bword\b'

# Buscar 'abc' dentro de palabras
echo -e "abcde\nsabc" | grep '\Babc'
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
echo -e "abc123\n456" | grep -E '\d+'

# Buscar no dígitos
echo -e "abc123\n456" | grep -E '\D+'

# Buscar palabras alfanuméricas
echo -e "hola_mundo\n123" | grep -E '\w+'

# Buscar símbolos
echo -e "@#%\n123" | grep -E '\W+'

# Buscar espacios en blanco
echo -e "hola mundo" | grep -E '\s+'

# Buscar no espacios en blanco
echo -e "hola mundo" | grep -E '\S+'
```

## Referencias y Capturas

| Carácter   | Significado                     | Ejemplo                             |
|------------|---------------------------------|-------------------------------------|
| `\n`       | Referencia al grupo n           | `(\w)\1` busca caracteres repetidos |

```bash
# Buscar caracteres repetidos
echo -e "aabb\nabc" | grep -E '(.)\1'
```

## Ejemplos Comunes

1. **Buscar líneas vacías:**
   ```bash
   echo -e "\nabc\n" | grep '^$'
   ```
2. **Eliminar espacios en blanco con sed:**
   ```bash
   echo "hola mundo" | sed 's/\s//g'
   ```
3. **Extraer direcciones de correo:**
   ```bash
   echo "correo@ejemplo.com texto" | grep -Eo '\b[A-Za-z0-9
