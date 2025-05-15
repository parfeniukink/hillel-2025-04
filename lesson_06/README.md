### status code match/case
```python
status_code: int = 300

match status_code:
    case 200 | 300:
        print("OK")
    case 400:
        print("Bad Request")
    case 500:
        print("Server Error")
    case _:
        print("Unknown error")
```

### points match/case
```python
piont: tuple[float, float] = (12.3, 89.2)

match point:
    case (0, 0):
        print("Zero point")
```


### while, iterator

```python
users = ["john", "marry"]
iterator = iter(users)


while True:
    try:
        print(next(iterator))
        # iterator.__next__()
    except StopIterationError:
        break

for user in users:
    print(user)
```


### context manager PoC
```python
import requests


class OpenAIClient:
    def __init__(self):
        self._client: requests.Client | None = None

    def __enter__(self):
        self._client = requests.Client(base_url="https://openai.com/api/v1/chat")
        return self

    def __exit__(self):
        self._client.close()

    @property
    def client(self) -> requests.Client:
        if self._client is None:
            raise Exception("Client is not initialized")
        else:
            return self._client

    def get_complition(self):
        response = self.client.chat("Who is Tim?")
        return response.text



with OpenAIClient() as client:
    result = client.get_complition()
```


### generators

#### files reading
```python
def read_file(filename: str):
    with open(filename) as file:
        while (line := file.readline()) is not None:
            yield line


for line in read_file("rockyou.txt"):
    print(line)
```


#### gen id
```python
students = {
    1: "John",
    2: "Marry",
}


def get_next_id():
    used_ids: set = set(students.keys())

    while True:
        id_ = max(used_ids) + 1
        used_ids.add(id_)

        yield id_

id_gen = get_next_id()

def add(name: str):
    students[next(id_gen)] = name

    students[next(id_gen)] = name


add("Mark")

print(students)
```
