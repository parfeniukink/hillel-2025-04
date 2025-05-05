# Permissions

john, marry
f1, f2

john -> r,w,x f1
marry -> r,w,x f2

f1
john rwx
marry ---



# Repository

```python
class Repository:
    """
    STORAGE: PATH / ADDRESS
    METHODS
    """

    def __init__(self):
        self.data = open(STORAGE_FILE_NAME / "data/students.csv")

    def get_students(self):
        pass

    def save_student(self, data):
        pass
```