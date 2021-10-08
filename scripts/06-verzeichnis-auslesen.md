# Verzeichnis auslesen

´´´
#!/bin/bash

cd /etc

# for i in /etc/*

for i in *
do
  echo "--"
  echo "Determiniere den Typ von $i"
  ls -lad $i
  if test -d $i
  then
    echo   $i ist eine Verzeichnis
  fi
done

```
