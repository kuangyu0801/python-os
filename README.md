# python-os

Learning repo for Using Python to Interact with the Operating System on Coursera

python -m venv osenv

`pip freeze > requirements.txt`

`pip install -r requirements.txt`

`osenv/bin/activate`

## Module-2: Managing Files with Python

What happens to the previous contents of a file when we open it using "w" ("write" mode)?
The old contents get deleted as soon as we open the file.

### CSV Files

Dialects are rules that define how a .csv file is structured, and parameters are formed to control the behavior of the .csv reader and writer and live within dialects. The following  features are supported by dialects:

## Module-3: Regular Expressions

- Regular expressions robust way to find text

grep

-i: ignore case
`.`: single character
`^`: starting
`$`: ending

```python
# python module
import re

re.search(...)
re.findall(...)
```

character class within braces `[]` or it could be empty

```python
print(re.search(r"[Pp]ython", "Python))
print(re.search(r"[a-zA-Z]ython", "Python))
```

```python
import re
def check_punctuation(text):
  result = re.search(r"[.?!]$", text)
  return result != None

print(check_punctuation("This is a sentence that ends with a period.")) # True
print(check_punctuation("This is a sentence fragment without a period")) # False
print(check_punctuation("Aren't regular expressions awesome?")) # True
print(check_punctuation("Wow! We're really picking up some steam now!")) # True
print(check_punctuation("End of the line")) # False
```

### Repetition Qualifiers

repeated matches
`*`: greedy

```python
import re
print(re.search(r"Py.*n", "Pygmalion"))
print(re.search(r"Py.*n", "Python Programming"))
print(re.search(r"Py[a-z]*n", "Python Programming"))
print(re.search(r"Py[a-z]*n", "Pyn"))
```

`+`: more than one occurance

```python
print(re.search(r"o+l+", "goldfish"))
print(re.search(r"o+l+", "woolly"))
print(re.search(r"o+l+", "boil")) // False
```

`?`: 0 or 1 occurance

```python
print(re.search(r"p?each", "To each their own"))
print(re.search(r"p?each", "I like peaches"))
```

### Escaping Characters

backslash`\`
`\n`: newline
`\w`: match number, alphabet, dash

regex101.com

`r”\d{3}-\d{3}-\d{4}”`  This line of code matches U.S. phone numbers in the format 111-222-3333.

`r”^-?\d*(\.\d+)?$”`  This line of code matches any positive or negative number, with or without decimal places.

`r”^/(.+)/([^/]+)/$”` This line of code is often used to extract specific parts of URLs or file paths, such as the directory names or filenames.

```regex
"^([\w \.-]*), ([\w \.-]*)$"
```

```python
print(re.search(r"[a-zA-Z]{5}", "a scary ghost appeared"))
print(re.findall(r"[a-zA-Z]{5}", "a scary ghost appeared"))

print(re.findall(r"\b[a-zA-Z]{5}", "a scary ghost appeared"))
```

`\b` matches full word

`regex = r"\[(\d+)\]"`

```python
import re

def extract_pid(log_line):
    regex = r"\[(\d+)\],([A-Z]*)"
    result = re.search(regex, log_line)
    if result is None:
        return None
    return "{} ({})".format(reuslt[1], result[2])

print(extract_pid("July 31 07:51:48 mycomputer bad_process[12345]: ERROR Performing package upgrade")) # 12345 (ERROR)
print(extract_pid("99 elephants in a [cage]")) # None
print(extract_pid("A string that also has numbers [34567] but no uppercase message")) # None
print(extract_pid("July 31 08:08:08 mycomputer new_process[67890]: RUNNING Performing backup")) # 67890 (RUNNING)
```
