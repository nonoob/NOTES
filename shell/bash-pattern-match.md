Use `man bash` for help, `parameter` is the whole string(s) to be manipulate, delete those matched.

```bash
${parameter#word}      #matches beginning
${parameter##word}     #matches beginning
${parameter%word}      #matches tail
${parameter%%word}     #matches tail
```
```bash
FILE="example.tar.gz"
echo "${FILE%%.*}"     #example
echo "${FILE%.*}"      #example.tar
echo "${FILE#*.}"      #tar.gz
echo "${FILE##*.}"  #gz
```

- change prefix of several file names: 

```bash
$ ls
old old.c old.tar.gz
$ for file in old*;do mv $file new${file#old};done;ls
new new.c new.tar.gz
```