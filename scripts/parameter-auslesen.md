# Parameter auslesen 

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

