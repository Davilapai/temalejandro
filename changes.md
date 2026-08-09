# Registro de Cambios y Optimizaciones (Tea Leaves Theme)

Este documento detalla todas las mejoras, correcciones y optimizaciones aplicadas al tema para VS Code **Tea Leaves**, garantizando un rendimiento óptimo al cargar y una experiencia visual de máxima calidad en todos los lenguajes, con énfasis especial en **C++** y **Python**.

---

## 1. Soporte Completo para C y C++ (`.c`, `.cpp`, `.h`, `.hpp`, `.cuda`)

Se integraron reglas dedicadas tanto en el motor de **TextMate** como en **Resaltado Semántico (Semantic Tokens)** para evitar fallos de carga o tokens sin colorizar en entornos como *C/C++ IntelliSense* y *clangd*:

- **Directivas de Preprocesador**: Resaltado diferenciado para `#include`, `#define`, `#ifdef`, `#ifndef`, `#endif`, `#pragma`, `#if`, `#elif` (`#d8866a` / Terracota).
- **Inclusiones de Archivos de Cabecera**: Soporte para `<iostream>`, `<vector>`, `"mi_header.h"` (`#408da1` / Azul Acero).
- **Tipos Primitivos de C/C++**: `int`, `char`, `float`, `double`, `void`, `bool`, `size_t`, `int32_t`, `uint64_t`, `auto`, `long`, `short`, `unsigned`, `signed` (`#5590a4` / Cían Atenuado).
- **Clases, Estructuras, Enums, Plantillas (Templates) y Tipos POSIX**: `entity.name.type.class.cpp`, `entity.name.type.struct.cpp`, `entity.name.type.enum.cpp`, `entity.name.type.template.cpp`, `support.type.posix-reserved.cpp` (`#5590a4` / Cían Atenuado).
- **Modificadores y Calificadores de Almacenamiento**: `const`, `constexpr`, `volatile`, `static`, `virtual`, `override`, `final`, `explicit`, `mutable`, `inline`, `noexcept`, `thread_local` (`#92ba92` / Verde Salvia).
- **Operador de Resolución de Ámbito (Scope Resolution `::`) y Espacios de Nombres (Namespaces)**: Resaltado nativo para `std::`, `namespace` y sintaxis `::` (`#92ba92` / Verde Salvia).
- **Constantes de Lenguaje**: Resaltado correcto para `nullptr` y `NULL` (`#d8866a` / Terracota).
- **Operadores y Casts Especiales**: `sizeof`, `alignof`, `static_cast`, `dynamic_cast`, `reinterpret_cast`, `const_cast` (`#92ba92` / Verde Salvia).

---

## 2. Soporte Completo para Python (`.py`, `.pyi`)

Se implementó cobertura integral para sintaxis de Python 3+, aprovechando al máximo servidores de lenguaje como **Pylance** y **Pyright**:

- **Definiciones y LLamadas a Funciones / Métodos**: Resaltado dorado para nombres de funciones en `def` y llamadas a funciones (`#e5c185` / Dorado Té).
- **Parámetros Especiales de Métodos**: Resaltado en cursiva dorada para `self` y `cls` (`variable.parameter.function.language.special.self.python`, `variable.parameter.function.language.special.cls.python`).
- **Decoradores (`@decorator`)**: Soporte completo para `@staticmethod`, `@classmethod`, `@property`, decoradores personalizados y sintaxis `@` (`#d8866a` / Terracota).
- **Cadenas Formateadas (F-strings)**: Marcado específico para prefijos `f`, `r`, `b`, `u` y marcadores de posición de formato dentro de cadenas `{variable}` (`#d8866a` / Terracota y `#4daaaa` / Turquesa).
- **Funciones Integradas (Built-ins)**: Resaltado para `print()`, `len()`, `range()`, `zip()`, `enumerate()`, `isinstance()`, `type()`, `open()`, `super()`, `sum()`, `min()`, `max()`, etc. (`#e5c185` / Dorado Té).
- **Métodos y Atributos Mágicos (Dunder)**: Resaltado especial para `__init__`, `__str__`, `__repr__`, `__name__`, `__file__`, `__main__`, `__doc__`, etc. (`#e5c185` / Dorado Té).
- **Excepciones Estándar**: Cobertura para `Exception`, `ValueError`, `TypeError`, `KeyError`, `IndexError`, `AttributeError`, `ImportError`, `FileNotFoundError`, etc. (`#5590a4` / Cían Atenuado).
- **Control de Flujo e Importaciones**: `if`, `elif`, `else`, `for`, `while`, `return`, `yield`, `raise`, `try`, `except`, `finally`, `with`, `as`, `import`, `from` (`#d8866a` / Terracota).
- **Operadores Lógicos de Python**: `and`, `or`, `not`, `in`, `is` (`#92ba92` / Verde Salvia).
- **Docstrings y Comentarios**: Cobertura para docstrings multilÍnea y comentarios en cursiva (`#60716d` / Gris Salvia).

---

## 3. Implementación de Resaltado Semántico (`semanticTokenColors`)

Anteriormente el tema contaba con únicamente 3 tokens semánticos definidos, lo que provocaba que al cargar lenguajes modernos (C++, Python, TypeScript, Rust) VS Code sobrescribiera los colores del editor con valores por defecto neutros.

Se añadió la especificación semántica completa:
- `class`, `struct`, `enum`, `enumMember`, `interface`, `type`, `typeParameter`, `concept`, `typeHint`, `exception` -> `#5590a4`
- `namespace` -> `#92ba92`
- `function`, `method`, `macro`, `magicFunction`, `builtinAttribute`, `event`, `label` -> `#e5c185`
- `preprocessor`, `decorator` -> `#d8866a`
- `variable`, `variable.readonly`, `variable.constant`, `parameter`, `property`, `customProperty` -> `#4daaaa`
- `selfParameter`, `clsParameter` -> `#e5c185` (italic)
- `keyword`, `modifier`, `operator` -> `#92ba92`
- `string`, `regexp` -> `#408da1`
- `number`, `boolean` -> `#d8866a`
- `comment` -> `#60716d` (italic)

---

## 4. Depuración y Eliminación de Ambigüedades en `tokenColors`

- **Eliminación de Ámbitos Duplicados**: Se detectaron y corrigieron conflictos de reglas duplicadas en `tokenColors` (por ejemplo en `keyword.operator.less`, `punctuation.section.embedded`, `entity.name.function`, `support.constant.color.w3c-standard-color-name.css`, `support.module.node`).
- **Normalización de Estructuras**: Se organizaron los 477 ámbitos de sintaxis de manera limpia y sin redundancias.
- **Validación de Formatos de Color**: Todos los colores hexadecimales fueron validados frente al estándar `#RRGGBB` / `#RRGGBBAA`.

---

## 5. Optimización del Manifiesto de la Extensión (`package.json`)

- **Categorización y Búsqueda**: Se agregaron palabras clave (`keywords`: `theme`, `dark`, `color-theme`, `cpp`, `c++`, `python`, `tea-leaves`) para optimizar la indexación en el Marketplace de VS Code.
- **Licencia y Descripción**: Se estableció la licencia `MIT` y una descripción detallada en el manifiesto.
- **Verificación de Esquema**: Estructura 100% compatible con las especificaciones de VS Code Engine `^1.72.0`.

---

## Resultado Final

El tema **Tea Leaves** ahora carga de forma fluida y sin advertencias ni inconsistencias visuales, ofreciendo una experiencia de desarrollo estéticamente armónica y con una legibilidad superior para **C++**, **Python** y el resto del ecosistema de desarrollo en VS Code.
