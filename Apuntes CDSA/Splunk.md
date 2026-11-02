| Comando            | Descripción                                          | Ejemplo de uso                                                   |
| ------------------ | ---------------------------------------------------- | ---------------------------------------------------------------- |
| `search`           | Realiza una búsqueda (normalmente es implícito).     | `search index=main EventCode=4624`                               |
| `AND`, `OR`, `NOT` | Operadores lógicos para combinar condiciones.        | `EventCode=4624 NOT Account_Name=SYSTEM`                         |
| `*`                | Comodín para cualquier texto.                        | `index=main "*powershell*"`                                      |
| `fields`           | Incluye o excluye campos.                            | `... \| fields Image, User`                                      |
| `fields -`         | Excluye campos.                                      | `... \| fields - User`                                           |
| `table`            | Muestra únicamente las columnas indicadas.           | `... \| table _time Image User`                                  |
| `rename`           | Cambia el nombre de un campo.                        | `... \| rename Image AS Process`                                 |
| `dedup`            | Elimina registros duplicados.                        | `... \| dedup Image`                                             |
| `sort`             | Ordena resultados.                                   | `... \| sort - _time`                                            |
| `stats`            | Realiza agregaciones estadísticas.                   | `... \| stats count by Image`                                    |
| `chart`            | Genera tablas para gráficos.                         | `... \| chart count by Image`                                    |
| `eval`             | Crea o modifica campos.                              | `... \| eval filename=lower(Image)`                              |
| `rex`              | Extrae datos mediante expresiones regulares.         | `... \| rex field=Image "(?P<file>[^\\\\]+)$"`                   |
| `lookup`           | Cruza información con un archivo CSV.                | `... \| lookup malware_lookup.csv filename OUTPUTNEW is_malware` |
| `inputlookup`      | Muestra el contenido de un Lookup.                   | `\| inputlookup malware_lookup.csv`                              |
| `transaction`      | Agrupa eventos relacionados.                         | `... \| transaction Image maxspan=1m`                            |
| `fieldsummary`     | Resume todos los campos encontrados.                 | `... \| fieldsummary`                                            |
| `metadata`         | Muestra metadatos de índices, fuentes o sourcetypes. | `\| metadata type=sourcetypes`                                   |
| `eventcount`       | Cuenta eventos por índice.                           | `\| eventcount summarize=false index=*`                          |
| `bucket`           | Agrupa eventos por intervalos de tiempo.             | `... \| bucket _time span=1d`                                    |
| `rare`             | Encuentra los valores menos comunes.                 | `... \| rare limit=10 ParentImage`                               |
| `top`              | Encuentra los valores más comunes.                   | `... \| top limit=20 Image`                                      |
| `where`            | Filtra resultados usando expresiones.                | `... \| where count < 100`                                       |
| `sistats`          | Estadísticas rápidas por índice, host, source, etc.  | `... \| sistats count by index,sourcetype`                       |

---

# Funciones útiles dentro de `eval`

|Función|¿Qué hace?|Ejemplo|
|---|---|---|
|`lower()`|Convierte a minúsculas.|`eval user=lower(User)`|
|`upper()`|Convierte a mayúsculas.|`eval proc=upper(Image)`|
|`split()`|Divide una cadena.|`split(Image,"\\\\")`|
|`mvindex()`|Obtiene un elemento de un campo multivalor.|`mvindex(filename,-1)`|
|`mvdedup()`|Elimina duplicados de un campo multivalor.|`mvdedup(split(Image,"\\\\"))`|

---

# Filtros de tiempo

|Uso|Ejemplo|
|---|---|
|Últimos 7 días|`earliest=-7d`|
|Última hora|`earliest=-1h`|
|Últimos 30 minutos|`earliest=-30m`|
|Hasta ahora|`latest=now`|

---

# Búsquedas comunes en Threat Hunting

|Objetivo|SPL|
|---|---|
|Procesos creados|`EventCode=1`|
|Conexiones de red Sysmon|`EventCode=3`|
|Inicio de sesión Windows|`EventCode=4624`|
|Buscar PowerShell|`Image="*powershell.exe"`|
|Ver línea de comandos|`\| table Image CommandLine User`|
|Contar procesos|`\| stats count by Image`|
|Ver procesos únicos|`\| dedup Image`|
|Ordenar por fecha|`\| sort - _time`|
|Procesos raros|`\| rare Image`|
|Procesos frecuentes|`\| top Image`|

---

# Plantilla base de una consulta SPL

```
index=<indice>
sourcetype=<tipo>
EventCode=<evento>
| fields campo1 campo2
| eval nuevo_campo=...
| rex ...
| stats count by campo
| sort - count
```

---

## Los comandos más importantes para aprender primero

Si tu objetivo es investigar incidentes o trabajar como analista SOC, te recomiendo memorizar estos primero:

1. `search`
2. `fields`
3. `table`
4. `stats`
5. `sort`
6. `dedup`
7. `eval`
8. `rex`
9. `lookup`
10. `transaction`
11. `top`
12. `rare`
13. `fieldsummary`
14. `metadata`

--------

# 2. Campos que deberías conocer de memoria ⭐⭐⭐⭐⭐

Estos aparecen prácticamente en todas las búsquedas.

| Campo         | Qué representa    |
| ------------- | ----------------- |
| `_time`       | Hora del evento   |
| `host`        | Equipo origen     |
| `source`      | Fuente del log    |
| `sourcetype`  | Tipo de log       |
| `Image`       | Ejecutable        |
| `CommandLine` | Línea de comandos |
| `ParentImage` | Proceso padre     |
| `User`        | Usuario           |
| `EventCode`   | ID del evento     |
# 3. Arquitectura de Splunk ⭐⭐⭐⭐

Muy preguntado en entrevistas.

```
Forwarder
      │
      ▼
 Indexer
      │
      ▼
 Search Head
```

## Universal Forwarder (UF)

- Muy liviano.
- Solo recopila y envía datos.
- No procesa eventos.

## Heavy Forwarder (HF)

- Más pesado.
- Puede transformar datos.
- Puede filtrar.
- Puede enrutar.
- Incluso puede indexar localmente.

## Indexer

- Recibe eventos.
- Los indexa.
- Los almacena.
- Responde búsquedas.

## Search Head

- Ejecuta las consultas SPL.
- Genera dashboards.
- Genera reportes.
- Coordina búsquedas.
# 4. Orden lógico para escribir una consulta SPL ⭐⭐⭐⭐⭐

Casi todas siguen esta estructura:

```
Buscar datos
    ↓
Filtrar
    ↓
Crear campos (eval/rex)
    ↓
Agrupar (stats/chart)
    ↓
Mostrar (table)
    ↓
Ordenar (sort)
```

Ejemplo:

```
index=main EventCode=1
| rex ...
| eval ...
| stats count by Image
| sort - count
| table Image count
```


-----

## Consultar los sourcetype disponibles
```
index="main" | stats count by sourcetype
```

