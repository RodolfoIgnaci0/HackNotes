# Chainsaw
(https://github.com/WithSecureLabs/chainsaw/wiki/Usage#command-examples)
### Command Examples
### search
_buscar usando por string_

```
./chainsaw search mimikatz -i evtx_attack_samples/
```

_buscan usando eventid_

```
./chainsaw search -t 'Event.System.EventID: =4104' evtx_attack_samples/
```

| Event Type                   | Event ID |
| ---------------------------- | -------- |
| Process Creation (Sysmon)    | 1        |
| Network Connections (Sysmon) | 3        |
| Image Loads (Sysmon)         | 7        |
| File Creation (Sysmon)       | 11       |
| Registry Events (Sysmon)     | 13       |
| Powershell Script Blocks     | 4104     |
| Process Creation             | 4688     |
| Scheduled Task Creation      | 4698     |
| Service Creation             | 7045     |
_Buscan usando regex y salida json_

```
./chainsaw search -e "DC[0-9].insecurebank.local" evtx_attack_samples --json
```
-----
### Hunt
_Hunt en logs evtx usando reglas Sigma para deteccion_
```
./chainsaw hunt evtx_attack_samples/ -s sigma/ --mapping mappings/sigma-event-logs-all.yml
```

_Hunt en logs evtx usando reglas Sigma y reglas Chainsaw para detección, con salida en CSV con salida en carpeta results
```
./chainsaw hunt evtx_attack_samples/ -s sigma/ --mapping mappings/sigma-event-logs-all.yml -r rules/ --csv --output results
```

_Hunt en logs evtx usando reglas Sigma, con fecha especifica y salida en json_
```
 ./chainsaw hunt evtx_attack_samples/ -s sigma/ --mapping mappings/sigma-event-logs-all.yml --from "2019-03-17T19:09:39" --to "2019-03-17T19:09:50" --json
```

### Analyse
```
./chainsaw analyse srum --software ./SOFTWARE ./SRUDB.dat --output ./output.json
```

### Dump
Dump the SOFTWARE hive
```
./chainsaw dump ./SOFTWARE.hve --json --output ./output.json
```


------
------
## Plaso
https://github.com/log2timeline/plaso
https://plaso.readthedocs.io/en/latest/
ejercicios: https://tryhackme.com/room/dfirtimelineanalysis

### Creación del timeline
log2timeline.py 2020JimmyWilson.E01 --storage-file output.plaso (disco duro y como sera la salida del timeline -puede demorar horas dependiendo del tamaño del disco- )
```
log2timeline.py 2020Jimmy.E01 --storage-file output.plaso
```
version rapida 
```
psteal.py --source image.raw -o dynamic -w registrar.csv
```

![[Pasted image 20260227175856.png]]

![[Pasted image 20260227180436.png]]
en la medida que va procesando nos dice la cantidad de hilos activos, id de proceso, total de eventos extraidos y ultimo archivo revisado
##### Listo los analizadores disponibles
```
log2timeline.py --parser list 
```
##### Si quiero usar uno especifico
```
log2timeline.py --parser winevt --artifact-filters WindowsEventLogSystem --storage-file output_WinEvent.plaso 2020JimmyWilson.E01

en caso de pasar archivo con filtros, se puede usar -f filter_windows.txt
```
------
##### Brinda detalles de la cantidad de eventos obtenidos
```
pinfo.py output.plaso
-v para mas detalles
```
-----
### psort.py

Se pueden agregar pluggins que generan analisis y tagean información dentro del reporte final, para ver lista de pluggins
```
psort.py --analysis list
```

taggear archivo .plaso en base a tags disponibles en tag_windows.txt
```
psort.py -o null --analysis tagging --tagging-file tag_windows.txt Jimmy_timeline.plaso
```

listar los posibles formatos a los que se pueden exportar la información para generar el timeline
```
psort.py -o list
```

generar timeline en csv
```
psort.py -o dynamic -w timeline_output.csv output.plaso
```

