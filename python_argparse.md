

## 1. Basic setup

```python
import argparse

parser = argparse.ArgumentParser(
    description="My awesome CLI tool"
)

args = parser.parse_args()
```

Run:

```bash
python script.py
```

---

## 2. Positional arguments (required, order matters)

```python
parser.add_argument("input_file", help="Input file path")
parser.add_argument("output_file", help="Output file path")
```

Run:

```bash
python script.py data.txt result.txt
```

Access:

```python
args.input_file
args.output_file
```

---

## 3. Optional arguments (flags)

### Simple flag with value

```python
parser.add_argument("--epochs", help="Number of epochs")
```

```bash
python script.py --epochs 10
```

```python
args.epochs  # '10' (string by default)
```

---

### With short + long name

```python
parser.add_argument("-e", "--epochs", help="Training epochs")
```

```bash
python script.py -e 10
```

---

## 4. Type conversion

```python
parser.add_argument("--epochs", type=int, default=5)
parser.add_argument("--lr", type=float, default=0.001)
```

```bash
python script.py --epochs 20 --lr 0.01
```

```python
args.epochs  # int
args.lr      # float
```

---

## 5. Boolean flags (store_true / store_false)

### Turn something ON

```python
parser.add_argument("--verbose", action="store_true")
```

```bash
python script.py --verbose
```

```python
args.verbose  # True
```

Without flag:

```python
args.verbose  # False
```

---

### Turn something OFF

```python
parser.add_argument("--no-cache", action="store_false", dest="cache")
```

Default:

```python
args.cache  # True
```

```bash
python script.py --no-cache
```

```python
args.cache  # False
```

---

## 6. Default values

```python
parser.add_argument("--batch-size", type=int, default=32)
```

```bash
python script.py
```

```python
args.batch_size  # 32
```

---

## 7. Choices (restricted values)

```python
parser.add_argument(
    "--mode",
    choices=["train", "test", "eval"],
    default="train"
)
```

```bash
python script.py --mode test
```

Invalid input:

```bash
python script.py --mode debug
# error: invalid choice
```

---

## 8. Required optional arguments

```python
parser.add_argument(
    "--config",
    required=True,
    help="Path to config file"
)
```

```bash
python script.py
# error: the following arguments are required: --config
```

---

## 9. Multiple values

### Fixed number

```python
parser.add_argument("--coords", nargs=2, type=float)
```

```bash
python script.py --coords 3.5 7.2
```

```python
args.coords  # [3.5, 7.2]
```

---

### Any number

```python
parser.add_argument("--files", nargs="+")
```

```bash
python script.py --files a.txt b.txt c.txt
```

```python
args.files  # ['a.txt', 'b.txt', 'c.txt']
```

---

## 10. List with defaults

```python
parser.add_argument(
    "--layers",
    nargs="+",
    type=int,
    default=[64, 64]
)
```

---

## 11. Count flags (verbosity levels)

```python
parser.add_argument("-v", "--verbose", action="count", default=0)
```

```bash
python script.py
python script.py -v
python script.py -vv
```

```python
args.verbose  # 0, 1, or 2
```

---

## 12. Custom destination name

```python
parser.add_argument("--dry-run", dest="dry_run", action="store_true")
```

```python
args.dry_run
```

---

## 13. Help text & auto `--help`

```python
parser.add_argument("--epochs", help="Number of training epochs")
```

```bash
python script.py --help
```

Auto-generated usage:

```
--epochs EPOCHS  Number of training epochs
```

---

## 14. Subcommands (git-style CLIs)

```python
parser = argparse.ArgumentParser()
subparsers = parser.add_subparsers(dest="command")

train = subparsers.add_parser("train")
train.add_argument("--epochs", type=int)

test = subparsers.add_parser("test")
test.add_argument("--checkpoint")
```

```bash
python script.py train --epochs 10
python script.py test --checkpoint model.pt
```

```python
args.command  # "train" or "test"
```

---

## 15. Full mini example

```python
import argparse

parser = argparse.ArgumentParser(description="Training script")

parser.add_argument("data")
parser.add_argument("--epochs", type=int, default=10)
parser.add_argument("--lr", type=float, default=0.001)
parser.add_argument("--verbose", action="store_true")

args = parser.parse_args()

print(args)
```

```bash
python script.py dataset.csv --epochs 20 --verbose
```

---

## 16. Common gotchas (bookmark this)

* **Everything is a string** unless you use `type=`
* `store_true` defaults to `False`
* Optional args use `--`, positional don’t
* `nargs="+"` requires at least one value
* Use `choices=` to prevent invalid input early

---
