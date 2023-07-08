
Note: This is not related to the project, but was written for my own understanding of certain concepts.

# Tutorials

## 1. setuptools

1. setuptools is a library used to help create packages which can be hosted in PyPi. From google, 'setuptools is a package development process library designed to facilitate packaging Python projects by enhancing the Python standard library distutils'.

2. A basic project setup will look like this, create a conda environment inside the directory project with python installed -> create setup.py, requirements.txt, & src folder with __init__.py file -> Use pip install -r requirements.txt to execute the setup.py through requirements.txt file -> Package is built.

3. The find_packages() is passed into the argument 'packages=' inside setup() which will check for __init__.py file in any folder and then turns the entire folder to a package. The 'instal_requires=' is passed with a list of dependencies for the package we're gonna build.

4. Modular programming refers to the process of breaking a large, unwieldy programming task into separate, smaller, more manageable subtasks or modules. Individual modules can then be cobbled together like building blocks to create a larger application.
5. A Python module is a file that has a .py extension, and a Python package is any folder that has modules inside it (or, in Python 2, a folder that contains an __init__.py file).
Module contents are made available to the caller with the import statement. 
Precursor for next section of tutorial is https://realpython.com/python-modules-packages/

6. From the above article, 
    - import statement basically imports objects from a module. But to only import certain objects use 
    from (MODULE_NAME) import (VARIABLE, CLASS, FUNCTION NAME ETC.)

    - To call the objects use Eg. x = MODULE_NAME.VARIABLE NAME 

## 2. File objects

1. Syntax of open is open('FILE_PATH', 'mode')\
The modes are\
'r' - read\
'a' - append\
'w' - write (Overwrite i.e all previous data is deleted)\
'x' - Create\
'r+' - read + write\
'rt' - read a text file\
'rb' - read a binary file\ 
etc....\

2. Also, we have to close the file after use. 

3. Closing a file after use is important because \
it frees up system resources that are being used by the file.


```python
f = open('test.txt','r')
print(f.name)
f.close()
```
Here,\
f.name = name of file\
f.mode = mode of file Eg. 'r' , 'w' etc.\
**NOTE: 'f' here is called a file object and it's read, written etc. only using the methods associated 
with file objects.**

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

6. But readlines() method read every line. Contents of each line are returned as a list i.e each element in the
   list represents contents of each line.

   ```python
   with open('text.txt', 'r') as f:
    f_contents = f.readlines()
    print(f_contents)
   ```

7. But the readline() method is different, as it reads one by one from the top.

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

12. While using the 'w' as mode, functions will overwrite an already existing file, so be careful. If file doesn't exist, it'll create it. This can be proved by passing a pass statement.

```python
with open('test2.txt','w') as f:
    pass
```

13. Notice the codes below,

```python
with open('test2.txt','w') as f:
    f.write('Test')

# Output of test2.txt file : Test

with open('test2.txt','w') as f:
    f.write('Test')
    f.write('Test')

# Output of test2.txt file : TestTest

with open('test2.txt','w') as f:
    f.write('Test\n')
    f.write('Test')

# Output of test2.txt file : 
# Test
# Test

```

14. Using seek() we can change the location of the insertion point for the next write.

```python
with open('test2.txt','w') as f:
    f.write('Test')
    f.seek(2)
    f.write('Test')

# Output of test2.txt file : TeTest

with open('test2.txt','w') as f:
    f.write('Test')
    f.seek(2)
    f.write('R')

# Output of test2.txt file : TeRt
```

15. The thing about overwritting is for all the above codes, the previously existing text will be deleted and replaced with passed text. So be careful.

16. To copy everything from a file to another file, refer the codes below. 

NOTE: rf.read() returns a string
```python
with open('test.txt', 'r') as rf:
    with open('test3.txt', 'w') as wf:
        wf.write(rf.read())
```

NOTE: rf is a file object and a iterable, which will give all characters in each line per iteration.
```python
with open('test.txt', 'r') as rf:
    with open('test2.txt', 'w') as wf:
        for line in rf:
            wf.write(line)
```

### Reading & Writing in binary mode

17. For binary mode, \
'rb' - read\
'wb' - write

Using this, we can do same functions but to files other than .txt like .jpg

## 3. Context managers ??

## 4. sys, os, logging modules ??

namespace & scope - https://realpython.com/python-namespaces-scope/
python packages - https://realpython.com/python-modules-packages/#python-packages
context managers - https://realpython.com/python-with-statement/#conclusion

## 5. sys module

1. Exceptions are composed of three parts: the type, the value, and the traceback. The sys module, exposes the current exception in three parallel variables, exc_type, exc_value, and exc_traceback, the sys.exc_info() function returns a tuple of these three parts, and the raise statement has a three-argument form accepting these three parts. 

2. Manipulating exceptions often requires passing these three things in parallel, which can be tedious and error-prone. Additionally, the except statement can only provide access to the value, not the traceback. Adding the __traceback__ attribute to exception values makes all the exception information accessible from a single place.

3. If the current thread is not handling any exception, exc_info returns (None,None,None).