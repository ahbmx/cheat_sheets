## Basic progress bar

### Loop over anything iterable

```python
from tqdm import tqdm
import time

for i in tqdm(range(100)):
    time.sleep(0.01)
```

---

## With lists, dicts, generators

```python
my_list = list(range(50))

for x in tqdm(my_list):
    time.sleep(0.02)
```

```python
my_dict = {"a": 1, "b": 2, "c": 3}

for k, v in tqdm(my_dict.items()):
    time.sleep(0.5)
```

```python
def gen():
    for i in range(10):
        yield i

for i in tqdm(gen(), total=10):
    time.sleep(0.3)
```

> 💡 For generators, **always pass `total=`** so tqdm knows how long it is.

---

## Pandas integration (very common)

### Enable tqdm for pandas

```python
from tqdm import tqdm
tqdm.pandas()
```

### `progress_apply`

```python
df["new_col"] = df["old_col"].progress_apply(lambda x: x * 2)
```

### `progress_map`

```python
df["new_col"] = df["old_col"].progress_map(str)
```

---

## Nested progress bars

```python
from tqdm import tqdm
import time

for i in tqdm(range(3), desc="Outer loop"):
    for j in tqdm(range(5), desc="Inner loop", leave=False):
        time.sleep(0.2)
```

* `desc` → label
* `leave=False` → inner bar disappears when done

---

## Custom descriptions & units

```python
for i in tqdm(range(100), desc="Processing files", unit="file"):
    time.sleep(0.01)
```

Output example:

```
Processing files:  45%|█████▍ | 45/100 [00:01<00:01, 49.2file/s]
```

---

## Manual progress bar (when you don’t have a loop)

```python
from tqdm import tqdm
import time

pbar = tqdm(total=100)

for _ in range(10):
    time.sleep(0.5)
    pbar.update(10)

pbar.close()
```

---

## Updating progress with variable steps

```python
pbar = tqdm(total=100)

pbar.update(3)
pbar.update(17)
pbar.update(80)

pbar.close()
```

---

## Logging / printing without breaking the bar

❌ Don’t use `print()`
✅ Use `tqdm.write()`

```python
from tqdm import tqdm
import time

for i in tqdm(range(5)):
    tqdm.write(f"Finished step {i}")
    time.sleep(0.5)
```

---

## Disable tqdm (config or debugging)

```python
for i in tqdm(range(100), disable=True):
    ...
```

---

## tqdm with multiprocessing

```python
from tqdm import tqdm
from multiprocessing import Pool

def f(x):
    return x * x

with Pool(4) as p:
    results = list(tqdm(p.imap(f, range(100)), total=100))
```

---

## tqdm in notebooks (Jupyter)

```python
from tqdm.notebook import tqdm
```

If bars look weird in notebooks, this usually fixes it.

---

## Common gotchas

* 🔢 **Wrong total** → bar never reaches 100%
* 🧵 **Multiprocessing without `total`** → no progress
* 🖨️ **print() inside loop** → broken bar
* 🐼 **Forgot `tqdm.pandas()`** → no `progress_apply`

---


