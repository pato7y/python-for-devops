## 1. Directory Listing and Creation

### Directory Listing (`os.scandir`)

The `os.scandir()` function returns an iterator of `DirEntry` objects corresponding to the entries in the directory, which is more efficient than `os.listdir()`.

```python
import os

# List all entries
with os.scandir('.') as entries:
    for entry in entries:
        print(entry.name)

# List only files
with os.scandir('.') as entries:
    for entry in entries:
        if entry.is_file():
            print(entry.name)

# List only directories
with os.scandir('.') as entries:
    for entry in entries:
        if entry.is_dir():
            print(entry.name)

```

### Making Directories (`os.mkdir` and `os.makedirs`)

* `os.mkdir()`: Creates a single directory.
* `os.makedirs()`: Creates a directory and any missing intermediate parent directories recursively.

```python
import os

# Create a single directory
os.mkdir('example_directory')

# Create nested directories (e.g., 2018/10/05)
os.makedirs('2018/10/05')

```

---

## 2. Filename Pattern Matching & Directory Traversal

### Filename Pattern Matching (`fnmatch`)

Useful for filtering filenames using Unix shell-style wildcards.

```python
import fnmatch
import os

for filename in os.listdir('.'):
    if fnmatch.fnmatch(filename, 'data_*_backup.txt'):
        print(filename)

```

### Traversing Directories (`os.walk`)

`os.walk()` generates the file names in a directory tree by walking the tree either top-down or bottom-up.

```python
import os

for dirpath, dirnames, files in os.walk('.'):
    print(f'Found directory: {dirpath}')
    for file_name in files:
        print(file_name)

```

---

## 3. Temporary Directories (`tempfile`)

The `tempfile` module creates temporary files and directories securely. `TemporaryDirectory` creates a temporary directory that is automatically cleaned up when the context manager exits.

```python
import tempfile
import os

with tempfile.TemporaryDirectory() as tmpdir:
    print('Created temporary directory:', tmpdir)
    print(os.path.exists(tmpdir))  # True

# Directory contents have been automatically removed outside the block
print(os.path.exists(tmpdir))  # False

```

---

## 4. Deleting, Copying, and Moving Files/Directories

### Deleting Files and Directories

```python
import os
import shutil

data_file = 'test.txt'

if os.path.isfile(data_file):
    os.remove(data_file)  # Delete a file
else:
    os.rmdir(data_file)  # Remove an empty directory

# Recursively delete a directory and its entire contents
trash_dir = 'my_documents/bad_dir'
try:
    shutil.rmtree(trash_dir)
except OSError as e:
    print(f'Error: {trash_dir} : {e.strerror}')

```

### Copying Files and Directories (`shutil`)

```python
import shutil

src = 'path/to/file.txt'
dst = 'path/to/dest_dir'

shutil.copy(src, dst)         # Copy file
shutil.copy2(src, dst)        # Copy file and preserve metadata
shutil.copytree('data_1', 'data1_backup')  # Copy directory recursively

```

### Moving and Renaming (`shutil` and `os`)

```python
import shutil
import os

# Move dir_1 into backup/ (if backup/ exists) or rename dir_1 to backup (if it doesn't)
shutil.move('dir_1/', 'backup/')

# Rename file
os.rename('first.zip', 'first_01.zip')

```

---

## 5. Archiving and Compression

### Using `zipfile`

```python
import os
import zipfile

# Creating a zip archive
with zipfile.ZipFile("file.zip", "w") as zf:
    for dirpath, dirnames, files in os.walk("any_directory"):
        zf.write(dirpath)
        for filename in files:
            zf.write(os.path.join(dirpath, filename))

# Extracting a zip archive
with zipfile.ZipFile('file.zip', 'r') as zf:
    zf.extractall(path='extract_dir')

```

### Easiest Archiving with `shutil`

`shutil` provides high-level helpers for creating and unpacking archives (supports zip, tar, gztar, bztar, xztar).

```python
import shutil

# Create an archive (base_name, format, root_dir)
shutil.make_archive('data/backup', 'zip', 'data/')

# Unpack an archive
shutil.unpack_archive('backup.tar', 'extract_dir/')

```