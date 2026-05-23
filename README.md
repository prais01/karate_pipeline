# API Ejercicios - Team G2 2026

## 📋 Descripción del Proyecto

Proyecto de automatización de pruebas BDD (Behavior Driven Development) para testing de APIs usando **Karate Framework**. Este proyecto incluye casos de prueba para validar la funcionalidad de gestión de cuentas y tarjetas en una API bancaria.

**API Base:** `https://bankapi-n1t8.onrender.com`

---

## 🏗️ Estructura del Proyecto

```
api-ejercicios-team-g2-2026/
├── src/
│   └── test/
│       └── java/
│           ├── bdd/
│           │   ├── auth/
│           │   │   └── login.feature          # Features de autenticación
│           │   ├── card.feature               # Features de gestión de tarjetas
│           │   ├── ConfigTest.java            # Configuración de pruebas
│           │   └── TestRunner.java            # Runner principal
│           ├── resources/
│           │   ├── csv/
│           │   │   └── auth/
│           │   │       ├── cuentas.csv        # Datos para creación de cuentas
│           │   │       └── tarjeta.csv        # Datos para creación de tarjetas
│           │   └── json/
│           │       ├── Cards/
│           │       │   ├── cardRequest.json   # Requests para opciones de tarjetas
│           │       │   └── cardSchemas.json   # Schemas de validación
│           │       └── auth/
│           │           └── loginRequest.json  # Requests de autenticación
│           ├── karate-config.js               # Configuración global de Karate
│           └── logback-test.xml               # Configuración de logs
├── target/
│   ├── karate-reports_*/               # Reportes de ejecución por timestamp
│   ├── karate.log                      # Archivo de log principal
│   └── generated-test-sources/         # Código generado
├── pom.xml                             # Configuración Maven
└── README.md                           # Este archivo
```

---

## 🔧 Requisitos Previos

- **Java 8+** (`java -version`)
- **Maven 3.6+** (`mvn -v`)
- Conexión a Internet (para acceder a la API)
- IDE: IntelliJ IDEA, Eclipse, VS Code (con extensiones de Karate)

---

## 📦 Dependencias Principales

```xml
<dependency>
    <groupId>com.intuit.karate</groupId>
    <artifactId>karate-junit5</artifactId>
    <version>1.3.1</version>
    <scope>test</scope>
</dependency>
```

- **Karate Framework 1.3.1** - Framework BDD para testing de APIs
- **JUnit 5** - Framework de testing
- **Java 1.8** - Versión mínima requerida

---

## 🚀 Instalación y Configuración

### 1. Clonar o descargar el proyecto
```bash
cd C:\Users\USUARIO\Desktop\karateAutomatizacion2026\karate-qa-practice\api-ejercicios-team-g2-2026
```

### 2. Instalar dependencias
```bash
mvn clean install
```

### Configuración Global

El archivo `karate-config.js` contiene la configuración base:

```javascript
var config = {
  env: env,                                          // Ambiente actual
  urlBase: 'https://bankapi-n1t8.onrender.com'      // URL base de la API
}
```

### TestRunner Configurado

El archivo `TestRunner.java` está configurado para ejecutar automáticamente todos los archivos `.feature` del paquete `bdd`:

```java
@Karate.Test
public Karate testAll() {
    return Karate.run().relativeTo(getClass());
}
```

**Ventaja:** No requiere especificar classpath explícitamente. Solo necesitas los tags en la línea de comandos.

---

## 🏃 Ejecutar Pruebas

### Ejecución General (Todos los tests)
```bash
mvn clean test
```

### Ejecución por Tags
Karate permite ejecutar tests usando tags definidos en los archivos `.feature`. El `TestRunner.java` está configurado para detectar automáticamente todos los archivos `.feature` en el paquete `bdd` sin necesidad de especificar classpath.

#### Sintaxis General
```bash
mvn test -Dkarate.options="--tags @nombreTag"
```

#### Ejemplo: Ejecutar un tag específico
```bash
mvn test -Dkarate.options="--tags @tarjeta"
```

#### Sintaxis con Múltiples Tags (AND lógico)
```bash
mvn test -Dkarate.options="--tags @tag1,@tag2"
```

#### Sintaxis con Tags Alternativos (OR lógico)
```bash
mvn test -Dkarate.options="--tags @tag1 or @tag2"
```

#### Sintaxis para Excluir Tags
```bash
mvn test -Dkarate.options="--tags !@tag1"
```

---

## 🏷️ Tags Disponibles en card.feature

| Tag | Escenario | Descripción |
|-----|-----------|-------------|
| `@tarjeta` | Feature completo | Tag general para todos los casos de tarjetas |
| `@crearCuenta` | CP01-Crear cuenta | Crea una nueva cuenta bancaria |
| `@crearTarjeta` | CP02-Crear tarjeta | Crea una tarjeta asociada a una cuenta |
| `@obtenerTarjeta` | CP03-Obtener tarjeta | Obtiene detalles de una tarjeta específica |
| `@consultarTarjeta` | CP04-Consultar tarjeta | Lista todas las tarjetas del usuario |
| `@añadirFondos` | CP05-Añadir fondos | Deposita fondos en una tarjeta |
| `@transaccionesTarjeta` | CP06-Transacciones | Obtiene el historial de transacciones |

---

## 📋 Ejemplos de Ejecución

### Ejemplo 1: Ejecutar solo la creación de cuenta
```bash
mvn test -Dkarate.options="--tags @crearCuenta"
```

### Ejemplo 2: Ejecutar creación de tarjeta
```bash
mvn test -Dkarate.options="--tags @crearTarjeta"
```

### Ejemplo 3: Ejecutar obtención de tarjeta
```bash
mvn test -Dkarate.options="--tags @obtenerTarjeta"
```

### Ejemplo 4: Ejecutar operación de fondos
```bash
mvn test -Dkarate.options="--tags @añadirFondos"
```

### Ejemplo 5: Ejecutar transacciones
```bash
mvn test -Dkarate.options="--tags @transaccionesTarjeta"
```

### Ejemplo 6: Ejecutar todos los tests de tarjetas
```bash
mvn test -Dkarate.options="--tags @tarjeta"
```

### Ejemplo 7: Ejecutar múltiples tags (AND lógico)
```bash
mvn test -Dkarate.options="--tags @crearCuenta,@crearTarjeta"
```

### Ejemplo 8: Ejecutar múltiples tags (OR lógico)
```bash
mvn test -Dkarate.options="--tags @crearCuenta or @obtenerTarjeta"
```

### Ejemplo 9: Excluir un tag
```bash
mvn test -Dkarate.options="--tags ~@obtenerTarjeta"
```

### Ejemplo 10: Ejecución completa con reporte
```bash
mvn clean test -Dkarate.options="--tags @tarjeta"
```

---

## 🎯 Ejecución Avanzada por Tags

### Sintaxis de Tags en Karate

**AND lógico (coma):** Solo ejecuta escenarios que tengan AMBOS tags
```bash
mvn test -Dkarate.options="--tags @tarjeta,@crearTarjeta"
```

**OR lógico (palabra clave "or"):** Ejecuta escenarios que tengan CUALQUIERA de los tags
```bash
mvn test -Dkarate.options="--tags @crearCuenta or @crearTarjeta"
```

**NOT (tilde ~):** Excluye escenarios con ese tag
```bash
mvn test -Dkarate.options="--tags ~@obtenerTarjeta"
```

### Combinaciones Avanzadas

**Ejecutar tarjetas pero excluir consulta:**
```bash
mvn test -Dkarate.options="--tags @tarjeta,~@consultarTarjeta"
```

**Ejecutar solo creación o adición de fondos:**
```bash
mvn test -Dkarate.options="--tags (@crearTarjeta or @añadirFondos)"
```

---

## 📊 Flujo de Ejecución

El proyecto sigue un flujo de dependencias encadenado:

```
CP01: Crear Cuenta
    ↓
CP02: Crear Tarjeta (usa ID de la cuenta)
    ↓
CP03: Obtener Tarjeta (usa ID de la tarjeta)
    ↓
CP04: Consultar Tarjetas
    ↓
CP05: Añadir Fondos (usa ID de la tarjeta)
    ↓
CP06: Transacciones (usa ID de la tarjeta con fondos)
```

### Uso de `call read()` para Reutilización
Los escenarios utilizan `call read()` para invocar otros escenarios y reutilizar sus datos:

```gherkin
* def reusableId = call read('@crearTarjeta')
* def idTarjeta = reusableId.id
```

---

## 📝 Estructura de Datos

### CSV - Datos de Entrada

**cuentas.csv:**
```
# Contiene parámetros para la creación de cuentas
```

**tarjeta.csv:**
```
# Contiene parámetros para la creación de tarjetas (cardType, cardHolderName)
```

### JSON - Requests y Schemas

**cardRequest.json:**
```json
{
  "createAccountRequest": { /* estructura de solicitud */ }
}
```

**cardSchemas.json:**
```json
{
  "accountsResponseSchema": { /* validación de respuesta */ },
  "cardResponseSchema": { /* validación de respuesta */ },
  "AddFundsResponseSchema": { /* validación de respuesta */ },
  "TransaccionCardsResponseSchema": { /* validación de respuesta */ }
}
```

---

## 🔐 Autenticación

Todos los requests incluyen autenticación por token Bearer:

```gherkin
* def reusableToken = call read('classpath:bdd/auth/login.feature@token')
* def tokenLogin = reusableToken.token
* header Authorization = 'Bearer ' + tokenLogin
```

---

## 📈 Reportes

Los reportes se generan automáticamente en:

```
target/karate-reports_<timestamp>/
├── karate-summary.html           # Resumen de ejecución
├── karate-execution.html         # Detalles de ejecución
└── karate-features.html          # Features ejecutados
```

### Ver último reporte
Abre `target/karate-reports_<ultima-carpeta>/karate-summary.html` en un navegador

---

## 🐛 Troubleshooting

### Error: "No tests executed"
- Verifica que los archivos `.feature` estén en `src/test/java`
- Asegúrate de que los tags estén escritos correctamente
- Ejecuta `mvn clean test` sin suministrar tags primero

### Error: "Connection refused"
- Verifica que la API esté disponible: `https://bankapi-n1t8.onrender.com`
- Comprueba tu conexión a Internet

### Error: "401 Unauthorized"
- El token de autenticación puede haber expirado
- Verifica el archivo `login.feature` en `bdd/auth/`

### Error de Encoding
- El proyecto está configurado con UTF-8
- Verifica que tu IDE esté configurado con UTF-8 en las preferencias

---

## 📚 Recursos Útiles

- [Documentación Oficial de Karate](https://karateframework.com/)
- [Karate Testing Examples](https://github.com/intuit/karate/tree/master/examples)
- [GherkinSyntax](https://docs.behat.org/en/v2.5/guides/1.gherkin.html)

---

## 👥 Información del Proyecto

- **Versión:** 1.0-SNAPSHOT
- **Group ID:** com.qateam
- **Artifact ID:** template-karate-qa-team
- **Equipo:** Team G2 2026

---

## 📝 Notas Importantes

1. **Dependencias Entre Escenarios:** Los escenarios están diseñados para ser ejecutados en orden, ya que utilizan datos generados por escenarios previos.

2. **IDs Dinámicos:** Cada ejecución genera nuevos IDs, lo que permite ejecutar los tests múltiples veces sin conflictos.

3. **Validación de Respuestas:** Se utiliza `match` para validar que las respuestas cumplan con los schemas definidos.

4. **Datos de Prueba:** Los datos se leen de archivos CSV y JSON, permitiendo fácil mantenimiento y ampliación.

---

## 🔄 Workflow de CI/CD

Para integrar este proyecto en un pipeline de CI/CD, usa:

```bash
mvn clean verify -Dkarate.options="--tags @tarjeta"
```

---

**Última actualización:** 2026-05-22


