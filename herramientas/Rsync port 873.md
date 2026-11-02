similar a smb o ftp, sirve para compartir archivos.

### Ver banner de servicio
```
rsync rsyc://target1.ine.local
```

### Ver archivos de una carpeta
```
rsync rsyc://target1.ine.local/carpeta
```

### Descagar  carpeta entera
```
rsync -av rsync://target1.ine.local/carpeta .

-a -> descargar archivos de la ruta dada
-v -> verbose
```

### Descargar archivo de carpeta
```
rsync -av rsync://target1.ine.local/carpeta/archivo.txt .
```

