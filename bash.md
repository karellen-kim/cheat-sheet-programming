# Bash Cheat Sheet

## Input
```sh
read -p "Name : " NAME
NAME=${name:-"KIM"}
```

## Pattern matching
```sh
if [[ $1 =~ .*port=([0-9]+).* ]]
then
  echo "Matched ${BASH_REMATCH[1]}"
else
  echo "Not match"
fi

```

## File
### Iterate
```sh
FILES=$(find . -type f -name "filename")
for FILE in $FILES
do
  echo $(cat $FILE)
done
```
### Delete old files
```sh
find . -maxdepth 1 -mtime +90 -type d -name "20*" | xargs rm -rf
```
