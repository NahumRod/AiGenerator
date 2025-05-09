
# 🛠️ Spring Boot Code Generator with OpenAI

Este microservicio genera automáticamente un proyecto Spring Boot a partir de un script SQL, utilizando OpenAI para generar el código por capas, incluyendo entidades, DTOs, servicios, repositorios, controladores y más.

---

## 🚀 ¿Qué hace este microservicio?

1. Recibe un archivo `.sql` y parámetros como lenguaje (`kotlin` o `java`), base de datos (`mysql`, `mongodb`, etc.) y tool (`maven`, `gradle`).
2. Descarga una base del proyecto desde [start.spring.io](https://start.spring.io).
3. Genera el código fuente usando OpenAI y un prompt avanzado.
4. Integra el código generado dentro del proyecto base.
5. Devuelve un `.zip` listo para compilar o desplegar.

---

## 📦 Estructura de Carpetas Generadas

```
src/
└── main/
    ├── java|kotlin/
    │   └── com/example/...
    │       └── cores/
    │           └── alumno/
    │               ├── dto/AlumnoRequestDto.kt
    │               ├── projection/AlumnoSummaryProjection.kt
    │               ├── domain/
    │               ├── application/
    │               └── infrastructure/
    └── resources/
```

---

## 🔧 Endpoint principal

`POST /api/generator/springboot`

### Parámetros esperados:

| Parámetro        | Tipo         | Descripción                                     |
|------------------|--------------|-------------------------------------------------|
| sql              | MultipartFile| Script SQL a analizar                           |
| packageName      | String       | Paquete base del proyecto generado              |
| applicationName  | String       | Nombre de la app / módulo base                  |
| dbType           | String       | `relational` o `non-relational`                |
| dbEngine         | String       | `mysql`, `mongodb`, etc.                        |
| language         | String       | `kotlin` o `java`                               |
| buildTool        | String       | `gradle-kotlin`, `gradle-groovy`, `maven`       |

### Respuesta:
Un `.zip` que contiene el proyecto generado.


## 📄 Prompt Inteligente

El prompt utilizado:
- Detecta relaciones `1:1`, `1:N`, `N:N`.
- Embebe entidades si aplica.
- Genera DTOs (`*Dto`), Proyecciones (`*Projection`).
- Usa convenciones de Spring Boot 3 y Jakarta EE.
- Ruta por lenguaje: `src/main/kotlin/...` o `src/main/java/...`

---

## 📁 Archivos de configuración esperados

Ubicar en `resources/prompts/`:

- `sql_to_kotlin_prompt_with_dto_projection.txt`
- `prompt_parameters.txt`

---

## ✅ Requisitos

- Java 17+
- Spring Boot 3.x
- Conexión con OpenAI (API Key)
- Gradle o Maven (según selección)

---
