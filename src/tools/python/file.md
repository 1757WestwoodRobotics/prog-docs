# Basic file IO

*Since we're running in a browser python environment, the following tutorial will not have anything that's runnable, if you want to try any of these examples for yourself, you can with your own computer environment*

```py.norepl
# Instead of try/finally to cleanup resources you can use a with statement
with open("myfile.txt") as f: # opens a new file to read
    for line in f: # f is an iterable
        print(line)

# Writing to a file
contents = {"aa": 12, "bb": 21}
with open("myfile1.txt", "w") as file: # notice we use the "w" flag to specify writing
    file.write(str(contents))        # writes a string to a file

import json # we'll look at module imports later
with open("myfile2.txt", "w") as file:
    file.write(json.dumps(contents))  # writes an object to a file

# Reading from a file
with open("myfile1.txt") as file:
    contents = file.read()           # reads a string from a file
print(contents)
# print: {"aa": 12, "bb": 21}

with open("myfile2.txt", "r") as file:
    contents = json.load(file)       # reads a json object from a file
print(contents)
# print: {"aa": 12, "bb": 21}
```

{{#authors lmaxwell24}}