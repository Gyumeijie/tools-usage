```bash
#!/bin/bash

NEW="lib64"
OLD="lib64_phone"

mkdir diff

for file in `find ./$NEW -name "*.so"`
do
   file_="${file##.*/}"
   if [ ! -f  "$OLD/$file_" ];
   then
        cp "./$NEW/$file_" diff
        echo "copy $file_"
        continue
   fi

   cmp "$NEW/$file_" "$OLD/$file_"
   if [[ $? -eq 0 ]];
   then
        echo "same file $file_"
   else
        cp "./$NEW/$file_" diff
        echo "diff file $file_"
   fi
done
```
