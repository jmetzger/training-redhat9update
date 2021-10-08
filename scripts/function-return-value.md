# Bash-script function with return value 

```
# log.sh 

source config.sh

loggen(){

  echo "hallo"
  return 2

}

loggen
echo $?
```
