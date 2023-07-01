

# Tutorials
## 1. File objects

1. Syntax of open is open(<FILE PATH>, 'mode')\
The modes are\
'r' - read\
'a' - append\
'w' - write\
etc....\

2. Also, we have to close the file after use. BecauseClosing a file after use is important because\ 
it frees up system resources that are being used by the file.\


```python
f = open('test.txt','r')
print(f.name)
f.close()
```
Here,\
f.name = name of file\
f.mode = mode of file Eg. 'r' , 'w' etc.

4. Using context managers like 'with' will automatically close the file once we exit the block.\
It'll also close the file if any exception was thrown.\
The 'f' here will be file object.\

```python
  with open('test.txt', 'r') as f:
      pass
  print(f.read())
```
The above code will throw an exception as the file is closed.

5. Using this following code, read() method will return file text as it is.

```python
with open('test.txt', 'r') as f:
    f_contents = f.read()
    print(f_contents)
```

6. But readlines() method read every line & contents of each line are returned as a list i.e each element in the
   list represents contents of each line.

```python
with open('test.txt', 'r') as f:
    f_contents = f.read()
    print(f_contents)
```

7.  readline() method reads one by one from the top.

```python
with open('test.txt', 'r') as f:
    f_contents = f.readline()
    print(f_contents,end='')

    f_contents = f.readline()
    print(f_contents,end='')

    f_contents = f.readline()
    print(f_contents,end='')
```
The above code will print the first 3 lines of the txt file only. end='' was added at send since it prints output with newline for each line.

8. The file object is also an iterable. This is better if memory is an issue, and cannot afford to store like in readlines() bcoz files has
   1000+ lines. 

```python
with open('test.txt', 'r') as f:
    for lines in f:
        print(lines, end='')
```
