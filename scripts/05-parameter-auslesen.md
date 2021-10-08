# Parameter auslesen 

## Einfaches Beispiel 

```
# parameter.sh 
source config.sh

loggen(){

  echo $(date):$1 >> $LOGTO
  return 0

}

# name des aufgeführen scriptes inkl pfad
echo $0
# erster parameter 
echo $1
# zweiter parameter 
echo $2
# anzahl parameter 
echo $#


#loggen "param1 ist ein toller parameter"
# echo $?

```

```
./parameter.sh 'erster parameter mit leerzeichen' DEBUG 

```

## Parameter begrenzen 

```
# params.sh 


if [ $# -gt 2 ]
then
  echo "Sorry, nur max. 2 parameter moeglich"
  exit 1
fi

```


```
chmod  u+x params.sh
./params.sh param1 param2 param3 
```
