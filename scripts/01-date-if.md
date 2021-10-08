# Script Datum und If 

## Version 1

```
#!/bin/bash

date +%Y%m%d

if test ! -d xy
then
  echo xy existiert nicht
fi
```

## Version 2

```
#!/bin/bash

# pwd
cd /var/log
DIRECTORY=$(date +%Y%m%d)

if test ! -d $DIRECTORY
then
  echo $DIRECTORY existiert nicht, ich lege es an
  xmkdir $DIRECTORY
  LASTRESULT=$?
  if test $LASTRESULT -gt 0
  then
     echo "Anlegen des Verzeichnisses nicht erfolgreich"
     exit 1
  else
     exit 0

  fi
fi
```
