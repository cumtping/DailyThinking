### 1 如何将linux shell当前目录缩进？
```
vim ~/.bashrc
if [ "$color_prompt" = yes ]; then
    PS1="\[\033[1;32m\][\w]\[\033[0m\]\n\[\033[1;36m\]\u\[\033[1;33m\]-> "
else
    PS1="\[\033[1;32m\][\w]\[\033[0m\]\n\[\033[1;36m\]\u\[\033[1;33m\]-> "
```
### 2 log 查看工具：glogg

    优点：搜索功能方便；
    
### 3 统计当前目录下各个文件夹下的md文件字数
```
function gitstat(){
    for file in ./*
    do
        stty -echo
        stat=`find $file -name "*.md" -print0 | xargs -0 cat | wc -m`
        stty echo
        echo $file $stat
    done
}
```
Q:如何将两次统计结果自动做对比？</br>
A：</br>
Q：如何用Python实现？</br>
A：</br>

