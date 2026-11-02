Aplicativo para desencriptar.

https://hashcat.net/wiki/doku.php?id=example_hashes -> lista de algoritmos (-m numero)
-a 0: attack mode = straight dictionary attack → try each password from list.
-a 1: attack mode = combination
-a 3: attack mode = brute-force
-a 6: attack mode = hybrid wordlist + mask
-a 7: attack mode = hybrid mask + wordlist


hashcat -a 0 -m 1800 h6.txt /usr/share/wordlists/rockyou.txt — force 

