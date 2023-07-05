

# Tutorials
## 1. File objects

1. Syntax of open is open('FILE_PATH', 'mode')\
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

### Reading files

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
9. Can also pass how many characters to read, with this we can approximate how long a file is. When the read for first 50 characters are over, the next 50 characters are printed. If the file runs out of characters the read() method will return an *Empty String*. This can be proved by giving a character to the 'end' keyword.

```python
with open('test.txt', 'r') as f:
    
    f_contents = f.read(50)
    print(f_contents, end='*')

    f_contents = f.read(50)
    print(f_contents, end='*')

    f_contents = f.read(50)
    print(f_contents, end='*')

    f_contents = f.read(50)
    print(f_contents, end='*')
```

10. The read() can also be used with while loop to print the file.

```python
with open('test.txt', 'r') as f:

    size_to_read = 10
    f_contents = f.read(size_to_read)
     
    while len(f_contents) > 0:    
        print(f_contents, end='*')
        f_contents = f.read(size_to_read)
```
Above, we can see how we call f_contents variable again so that, it'll read the next set of 10 characters. See how writing within the 'with' statement helps us.

11. If you hate printing sequentially like the above, use seek() method to reset. Give character number to decide where to start the next read

```python
with open('test.txt', 'r') as f:

    size_to_read = 10

    f_contents = f.read(size_to_read)
    print(f_contents, end='')

    f.seek(0)

    f_contents = f.read(size_to_read)
    print(f_contents, end='')
```

### Writing files
