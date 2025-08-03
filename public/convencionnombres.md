# Guía de **naming conventions** (formatos de escritura) para código

> **Objetivo**: Tener un documento de consulta rápida con definiciones, reglas y ejemplos de los formatos de nombres más usados en programación (variables, funciones/métodos, clases, constantes, archivos, carpetas, columnas SQL, etc.), con recomendaciones por lenguaje y casos prácticos.

---

## 1) Glosario de formatos (con ejemplos)

> Para los ejemplos usaré la frase base: **"mi variable grande"**.

### camelCase (lowerCamelCase)
- **Definición**: Primera palabra en minúscula; cada palabra siguiente inicia con mayúscula. Sin espacios ni separadores.
- **Ejemplos**:
  - Palabra base → `miVariableGrande`
  - JS/TS: `const totalClientesActivos = 120;`
  - Java: `int cantidadPedidosHoy;`
  - PHP: `$montoTotalVenta = 0;`
- **Uso típico**: variables y funciones en **JavaScript/TypeScript**, **Java**, **PHP** (cuando se sigue PSR-12 es usual para propiedades/métodos camelCase), **C#** (métodos locales), **Kotlin**.

### PascalCase (UpperCamelCase)
- **Definición**: Igual que camelCase, pero **la primera palabra también inicia con mayúscula**.
- **Ejemplos**:
  - Palabra base → `MiVariableGrande`
  - Clases/Tipos: `class ClienteService {}`, `interface UserRepository {}`
  - C#: `public class OrderController {}`
  - Java: `public class VentaMensual {}`
- **Uso típico**: **Clases**, **Interfaces**, **Enums**, **Records** y **Tipos** en lenguajes OO (Java, C#, TypeScript), y **nombres de archivos** de clases en Java/C#.

### snake_case
- **Definición**: Todas las palabras en minúsculas unidas por guión bajo.
- **Ejemplos**:
  - Palabra base → `mi_variable_grande`
  - Python: `def calcular_total_factura():`
  - SQL: `SELECT total_bruto FROM ventas_mensuales;`
- **Uso típico**: **Python** (funciones, variables), **Base de datos** (tablas y columnas), **Ruby** (métodos), **C** (funciones), **Go** (a veces para constantes privadas).

### SCREAMING_SNAKE_CASE (MACRO_CASE / CONSTANT_CASE)
- **Definición**: snake_case pero **en mayúsculas**, usado para **constantes**.
- **Ejemplos**:
  - Palabra base → `MI_VARIABLE_GRANDE`
  - JS/TS: `const MAX_RETRIES = 3;`
  - Python: `DEFAULT_TIMEOUT = 30`
  - PHP: `const IVA_CHILE = 0.19;`
- **Uso típico**: **Constantes** y **macros** (C/C++), flags de configuración, valores inmutables.

### kebab-case (lisp-case / dash-case)
- **Definición**: palabras en minúsculas separadas por guiones medios.
- **Ejemplos**:
  - Palabra base → `mi-variable-grande`
  - Archivos web: `user-profile-card.tsx`, `main-layout.css`
  - URLs: `/api/v1/productos-mas-vendidos`
- **Uso típico**: **Nombres de archivos** en front-end, **clases CSS**, **URLs**, **packages** npm/yarn, **repositorios**, **branches** (a veces). **No se usa** para variables en la mayoría de lenguajes (el signo `-` es resta).

### Train-Case (Header-Case con guiones y Mayúscula Inicial)
- **Definición**: Como kebab-case, pero **cada palabra inicia con mayúscula**.
- **Ejemplo**:
  - Palabra base → `Mi-Variable-Grande`
- **Uso típico**: Títulos legibles en documentación, algunos **nombres de componentes** en front-end (menos común).

### Title Case (Títulos, sin guiones)
- **Definición**: Cada palabra inicia con mayúscula, sin guiones ni guiones bajos.
- **Ejemplo**: `Mi Variable Grande`
- **Uso típico**: Títulos de **documentación**, **commits** (subtítulos), **mensajes** legibles.

### dot.case
- **Definición**: palabras en minúsculas separadas por punto.
- **Ejemplo**: `mi.variable.grande`
- **Uso típico**: **Claves de configuración**, **keys** en archivos `.env` anidados (no estándar), rutas lógicas en herramientas de build. No es común para código fuente.

### UPPERCASE / lowercase
- **Definición**: todo en mayúsculas o todo en minúsculas.
- **Ejemplos**: `MIVARIABLEGRANDE`, `mivariablegrande`
- **Uso típico**: **Flags** muy cortos, **DOM IDs** legacy, **nombres de esquema** en DB (con cuidado), **comandos** (minúsculas). Rara vez para identificadores complejos.

### Prefijo con guión bajo (`_private`)
- **Definición**: Prefijar con `_` para marcar **privado** o **interno** por convención.
- **Ejemplos**: `_buffer`, `_id`, `_parseInternal()`
- **Uso típico**: **Python** (indicativo de “no público”), **JS/TS** en librerías (cuando no hay `#private` o `private`), **C/C++** como “internal”.

### Notación Húngara (Hungarian Notation) — (en desuso)
- **Definición**: Prefijos que denotan tipo/uso: `strNombre`, `iContador`, `bActivo`.
- **Ejemplo**: `pszName`, `dwSize`
- **Estado**: **Desaconsejada** en la mayoría de proyectos modernos; los tipos estáticos y linters la vuelven innecesaria. Considerar sólo si un **código legado** ya la usa.

### Prefijos y sufijos semánticos útiles
- **Booleanos**: `is`, `has`, `can`, `should` → `isActive`, `hasChildren`, `canRetry`
- **Acciones**: `get`, `set`, `create`, `update`, `delete`, `find`, `list`, `count`
- **IDs**: `_id` (DB), `Id` (Java/C#): `cliente_id`, `orderId`
- **Patrones**: `DTO`, `VO`, `Impl`, `Service`, `Repo`, `Controller`, `Handler`, `Factory`

---

## 2) Reglas y buenas prácticas generales

1. **Consistencia primero**: usa una convención y mantenla en **todo el proyecto**.
2. **Sin acentos, ñ ni espacios**: usar ASCII básico (`n` en lugar de `ñ`, sin tildes).
3. **Nombres descriptivos**: prioriza claridad sobre brevedad (`obtenerVentasMensuales` mejor que `obtenerVM`).
4. **Evitar abreviaturas crípticas**: si abrevia, que sea estándar (`cfg`, `tmp`, `ref`, `dto`).
5. **Acrónimos**: elige un estilo y sé consistente. Dos opciones comunes:
   - **Java-like**: `HttpServer`, `XmlHttpRequest`
   - **All-caps acrónimo** en mayúscula inicial si corresponde: `HTTPServer`, `UUIDGenerator` (menos frecuente).
6. **Idioma**: elige **inglés o español** y mantén coherencia. En equipos internacionales, preferir **inglés**.
7. **Evita nombres genéricos**: `data`, `info`, `obj` → intenta `venta`, `cliente`, `pedido`.
8. **Longitud razonable**: nombres largos pero claros son aceptables; evita frases innecesarias.
9. **Plurales**: usa plural cuando representan colecciones (`clientes`, `orders`).
10. **Funciones deben “decir lo que hacen”**: verbos para funciones/métodos; sustantivos para clases/objetos.

---

## 3) Recomendaciones por lenguaje (resumen)

### JavaScript / TypeScript
- Variables/funciones: **camelCase** → `totalClientes`, `renderChart()`
- Clases/Interfaces/Enums/Tipos: **PascalCase** → `UserService`, `IUser`
- Constantes: **SCREAMING_SNAKE_CASE** → `DEFAULT_LIMIT`
- Archivos (front): **kebab-case** → `user-service.ts`, `ventas-dashboard.tsx`
- CSS classes: **kebab-case** → `.main-header`, `.user-card`
- Paquetes npm: **kebab-case** o todo minúsculas → `mi-paquete-ui`

### Python
- Variables/funciones: **snake_case** → `total_clientes`, `calcular_total()`
- Clases: **PascalCase** → `ClienteService`
- Constantes: **SCREAMING_SNAKE_CASE** → `DEFAULT_TIMEOUT`
- Archivos/módulos: **snake_case** → `ventas_clientes.py`

### PHP (PSR-12)
- Clases: **PascalCase** → `VentaController`
- Métodos/propiedades: **camelCase** → `getMontoTotal()`
- Constantes: **SCREAMING_SNAKE_CASE** → `IVA_CHILE`
- Archivos de clase: **PascalCase** (si 1 clase/archivo) o **snake/kebab** según estructura de proyecto.
- Namespaces: **PascalCase** por segmento → `App\Services\Ventas`

### Java / Kotlin
- Paquetes: **lowercase** con puntos → `cl.com.factronica.erp`
- Clases/Interfaces/Enums: **PascalCase**
- Métodos/variables: **camelCase**
- Constantes: **SCREAMING_SNAKE_CASE**

### C#
- Namespaces/Clases/Interfaces: **PascalCase** (interfaces a veces con `I`: `IRepository`)
- Métodos/propiedades: **PascalCase** (C# usa Pascal también para métodos públicos)
- Variables locales/privadas: **camelCase** (a veces `_camelCase` para campos privados)
- Constantes: **SCREAMING_SNAKE_CASE**

### Go
- Exportado (público): **PascalCase** → `func GetUser()`
- No exportado (privado): **camelCase** (iniciando en minúscula) → `func getUser()`
- Paquetes: **lowercase** cortos → `bytes`, `http`

### Rust
- Módulos/variables/funciones: **snake_case**
- Tipos/Traits/Enums: **PascalCase**
- Constantes/estáticas: **SCREAMING_SNAKE_CASE**

### SQL (DDL/DML)
- Tablas/columnas: **snake_case** → `tbl_usuarios`, `fecha_emision`
- Claves primarias: `id` o `tabla_id` → `usuario_id`
- Índices/constraints: nombres claros → `idx_ventas_fecha`, `fk_factura_cliente`

### CSS / HTML
- Clases CSS: **kebab-case** → `.main-container`, `.btn-primary`
- IDs: **kebab-case** o **snake_case** (consistencia)
- Custom properties (CSS variables): **kebab-case** → `--brand-primary`

### YAML/JSON
- Keys: **snake_case** o **kebab-case** o **camelCase** (elige 1 por proyecto)
- Ejemplo JSON (camelCase):
  ```json
  {
    "apiBaseUrl": "https://api.ejemplo.cl",
    "maxRetries": 3
  }
  ```

---

## 4) Nombres de archivos, carpetas, URLs y DB

- **Archivos front-end**: **kebab-case** → `ventas-diarias.component.ts`
- **Archivos Python**: **snake_case** → `gestion_clientes.py`
- **Archivos Java**: **PascalCase** (1 clase por archivo) → `VentaController.java`
- **Carpetas**: minúsculas y **kebab-case** o **snake_case** → `core-utils`, `data_access`
- **Rutas/Endpoints**: **kebab-case** en **plural** → `/api/v1/clientes-activos`
- **Base de datos**: **snake_case** para tablas/columnas → `tbl_proveedores`, `fecha_creacion`
- **Migraciones**: prefijo de fecha + descripción kebab → `2025_08_03_create_tbl_usuarios.sql`

---

## 5) Tabla “chuleta” (conversión de la frase base)

| Formato                     | Ejemplo de “mi variable grande”      |
|----------------------------|---------------------------------------|
| camelCase                  | `miVariableGrande`                    |
| PascalCase                 | `MiVariableGrande`                    |
| snake_case                 | `mi_variable_grande`                  |
| SCREAMING_SNAKE_CASE       | `MI_VARIABLE_GRANDE`                  |
| kebab-case                 | `mi-variable-grande`                  |
| Train-Case                 | `Mi-Variable-Grande`                  |
| Title Case                 | `Mi Variable Grande`                  |
| dot.case                   | `mi.variable.grande`                  |

---

## 6) Ejemplos prácticos integrados

### 6.1 JavaScript/TypeScript (frontend)
```ts
// archivo: ventas-dashboard.tsx
type VentaResumen = {
  totalBruto: number;        // camelCase
  totalNeto: number;
  fechaCorte: string;
};

const DEFAULT_LIMIT = 50;     // SCREAMING_SNAKE_CASE

export class VentasDashboard { // PascalCase
  private totalClientes = 0;   // camelCase

  constructor(private apiBaseUrl: string) {}

  async obtenerVentasMensuales(): Promise<VentaResumen[]> { // camelCase
    const url = `${this.apiBaseUrl}/api/v1/ventas-mensuales`; // kebab-case en URL
    const res = await fetch(url);
    return res.json();
  }
}
```

### 6.2 Python (backend / scripts)
```py
# archivo: ventas_mensuales.py
DEFAULT_TIMEOUT = 30  # SCREAMING_SNAKE_CASE

class VentaService:    # PascalCase
    def __init__(self, db_conn):
        self.db_conn = db_conn  # snake_case

    def obtener_ventas_mensuales(self):  # snake_case
        with self.db_conn.cursor() as cur:
            cur.execute("SELECT fecha, total_bruto FROM ventas_mensuales")
            return cur.fetchall()
```

### 6.3 PHP (PSR-12, API)
```php
<?php
// archivo: src/Controller/VentaController.php
declare(strict_types=1);

namespace App\Controller;

class VentaController // PascalCase
{
    private const IVA_CHILE = 0.19; // SCREAMING_SNAKE_CASE

    public function getVentasMensuales(): array // camelCase
    {
        // ...
        return ['ok' => true];
    }
}
```

### 6.4 SQL (DDL)
```sql
-- archivo: 2025_08_03_create_tbl_usuarios.sql
CREATE TABLE tbl_usuarios (
  usuario_id     BIGINT PRIMARY KEY,
  nombre         VARCHAR(100) NOT NULL,
  clave_hash     VARCHAR(255) NOT NULL,
  fecha_creacion TIMESTAMP     NOT NULL DEFAULT NOW()
);
CREATE INDEX idx_usuarios_nombre ON tbl_usuarios (nombre);
```

---

## 7) Herramientas que ayudan a imponer estilos

- **JavaScript/TypeScript**: ESLint, Prettier
- **Python**: Black, Ruff/Flake8, isort
- **PHP**: PHP-CS-Fixer, PHP_CodeSniffer (PSR-12), Rector
- **Java**: Checkstyle, Spotless, Google Java Format
- **C#**: EditorConfig + Roslyn analyzers, StyleCop
- **Go**: `gofmt`, `golangci-lint`
- **Rust**: `rustfmt`, Clippy

> Configura **pre-commit hooks** (Husky, pre-commit, etc.) para validar estilos antes de cada push.

---

## 8) Checklist rápida para tu equipo

- [ ] Elegimos **idioma** del código (es/en) y lo mantenemos.
- [ ] Acordamos **convención por tipo**: variables/funciones, clases, constantes.
- [ ] Definimos **nombres de archivos/carpetas** y **rutas**.
- [ ] Estándar para **DB** (tablas, columnas, índices).
- [ ] Reglas para **acrónimos** (Http vs HTTP).
- [ ] Linters/formatters y **pre-commit hooks** activos.
- [ ] Documentamos excepciones y **legado** (ej. módulos externos).

---

## 9) Reglas rápidas por tipo de identificador

- **Clases/Interfaces/Enums/Tipos** → **PascalCase**
- **Variables/funciones/métodos** → **camelCase** (Python: **snake_case**)
- **Constantes** → **SCREAMING_SNAKE_CASE**
- **Archivos** → **kebab-case** (front), **snake_case** (Python), **PascalCase** (Java/C# class files)
- **DB (tablas/columnas)** → **snake_case**
- **CSS/URLs** → **kebab-case**

---

> Mantener un estilo uniforme reduce bugs, acelera el onboarding y mejora la legibilidad. Si ya existe código legado, adopta estas reglas **progresivamente** (boy-scout rule: deja el código un poco mejor que como lo encontraste).
