
 script /dev/null -c bash
 ctrl + z

 stty raw -echo; fg
 reset xterm

 export TERM=xterm

### Tratamiento usando python3

python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm

### Tratamiento usando perl

perl -e 'exec "/bin/bash";'

### Tratamiento usando ruby

ruby: exec "/bin/bash"

------
#### Aumentar tamaño de la tty

```
stty rows <number>
stty cols <number>
```

Cantidad estandar es 44 - 184
```
stty rows 44 columns 184
```

