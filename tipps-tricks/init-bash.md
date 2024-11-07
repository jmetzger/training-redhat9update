# Get into your system without password

```
1. Reboot und in bootmanager gehen (ESC) -> e für edit der 1. Zeile 
2. Zeile linux, und schreiben ans Ende: init=/bin/bash 
3. CTRL x 
4. mount -o remount,rw / 
5. Passwort ändern 
passwd
6. touch /.autorelabel 
7. -> vm stopen/schliessen
8. neu starten 
9. einloggen mit root mit neuem Passwort
```
