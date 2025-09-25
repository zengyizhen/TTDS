
`
# TTDS: Lab 0
#### --- Basic Text Processing
How to read a text file from hard-disk. This lab is optional for those who are not fully confident about their programming skills. There is nothing specific to be done in this lab more than reading a text file from HD word by word, which is the most basic skill you need to have to be able to take the course.

## PROGRAMMING LANGUAGES

You need to have Perl or Python on your machine (you still can use something else) if you prefer.
If you are using Dice, then you should have them there. Check with demonstrators how to run them.
## DOWNLOAD A SAMPLE TEXT FILE

查看当前路径：`pwd`

Download the following file, which has the text of the Bible: link


`
wget -O pg10.txt "https://opencourse.inf.ed.ac.uk/sites/default/files/https/opencourse.inf.ed.ac.uk/ttds/2023/pg10.txt"
`
## SKILLS TO DO WITH THE FILE

You need to be confident with the following skills with any programming language when dealing with a text file:

1. Reading and Writing into text files


2. Reading text by word, and calling functions to process word if required (e.g. lower case word letters)
3. Regular expressions would be very useful to know
Count the number of occurences of the words: "lord", "to", and "36"


## PROCESS
```
cat pg10.txt |perl -p -e "s/[^\w]+/\n/g" > moveNoneWords.txt
cat moveNoneWords.txt | tr "A-Z" "a-z" > 2low.txt
cat 2low.txt | sort > 3sort.txt
cat 3sort.txt | uniq -c >4uniqCount.txt
cat 4uniqCount.txt | sort -n > 5sortn.txt
grep -w 'lord' 5sortn.txt
   7964 lord
grep -w 'to' 5sortn.txt
  13680 to
grep -w '36' 5sortn.txt
     36 104
     ......
     36 twentieth
    474 36
awk '$2=="36"{print $0}' 5sortn.txt
    474 36
```

## Useful Shell Commands 
Print frequency of unique terms in a given collection: 
- cat pg10.txt | tr " " "\n" | tr "A-Z" "a-z" | sort | uniq -c | sort -n > terms.freq 
- cat text.file | perl -p -e "s/[^\w]+/\n/g" | tr "A-Z" "a-z" | sort | uniq -c | sort -n > terms.freq
>**read file**
>
>```cat pg10.txt```
>
>**turn space (" ") in to new line**
>  
>```tr " " "\n" ```
>
>**Perl 的“替换”正则表达式（substitution）**
>
>```perl -p -e 's/[^\w]+/\n/g'```
>- perl -p(print what in -e) -e(execute) s(substitute)/正则表达式/替换内容/修饰符
>- 正则 `[^\w]+`
>- \w：word character（单词字符）。在 Perl 默认里是 [A-Za-z0-9_]。
>- ^ 在 [] 里表示取反，即“不是单词字符”。
>- [^\w] → 任意非单词字符。
>- [^\w]+ → 连续的一段非单词字符（比如空格、标点、符号等）。
>- 替换为 \n
>    
>- 相较于tr可以去掉标点符号
>  
>**sort**
>
>**uniq-c**