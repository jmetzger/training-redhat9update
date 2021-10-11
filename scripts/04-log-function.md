# Log - Function 

``` shell
source config.sh

loggen(){

  echo $(date):$1 >> $LOGTO
  return 0

}

loggen "param1 ist ein toller parameter"
# echo $?

```
