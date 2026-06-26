I'll create an extensive Python cheat sheet module with comprehensive coverage of Python features. This will include a main module with all the cheat sheet content and a showcase script that demonstrates each feature.

## File 1: `cheat_sheet.py` - The Main Cheat Sheet Module

```python
"""
Python Cheat Sheet Module
A comprehensive reference for Python programming
"""

# ============================================
# 1. BASIC SYNTAX AND DATA TYPES
# ============================================

class BasicSyntax:
    """Basic Python syntax and data types cheat sheet"""
    
    @staticmethod
    def data_types():
        """Common Python data types"""
        # Numbers
        integer = 42
        float_num = 3.14159
        complex_num = 3 + 4j
        
        # Strings
        string = "Hello, World!"
        multi_line = """This is a
        multi-line string"""
        raw_string = r"Raw string\nignores escape"
        
        # Booleans
        true_val = True
        false_val = False
        
        # None
        nothing = None
        
        return {
            'integer': integer,
            'float': float_num,
            'complex': complex_num,
            'string': string,
            'multi_line': multi_line,
            'raw_string': raw_string,
            'boolean': true_val,
            'none': nothing
        }
    
    @staticmethod
    def variables_and_naming():
        """Variable naming conventions"""
        # Snake case (recommended)
        user_name = "John"
        total_score = 100
        
        # Constants (uppercase)
        MAX_SIZE = 1000
        PI = 3.14159
        
        # Multiple assignment
        a, b, c = 1, 2, 3
        x = y = z = 0
        
        # Unpacking
        coordinates = (10, 20)
        x_pos, y_pos = coordinates
        
        return {
            'user_name': user_name,
            'total_score': total_score,
            'MAX_SIZE': MAX_SIZE,
            'a': a, 'b': b, 'c': c,
            'x': x, 'y': y, 'z': z,
            'x_pos': x_pos, 'y_pos': y_pos
        }


# ============================================
# 2. COLLECTIONS / DATA STRUCTURES
# ============================================

class Collections:
    """Python collections cheat sheet"""
    
    @staticmethod
    def lists():
        """List operations"""
        # Creation
        empty_list = []
        number_list = [1, 2, 3, 4, 5]
        mixed_list = [1, "two", 3.0, [4, 5]]
        
        # List comprehension
        squares = [x**2 for x in range(10)]
        even_numbers = [x for x in range(20) if x % 2 == 0]
        
        # Operations
        number_list.append(6)           # Add to end
        number_list.insert(0, 0)        # Insert at index
        number_list.extend([7, 8])      # Extend with another list
        popped = number_list.pop()      # Remove and return last
        removed = number_list.remove(0) # Remove first occurrence
        index = number_list.index(3)    # Find index
        count = number_list.count(2)    # Count occurrences
        number_list.sort()              # Sort in place
        number_list.reverse()           # Reverse in place
        
        # Slicing
        first_three = number_list[:3]
        last_two = number_list[-2:]
        reverse_copy = number_list[::-1]
        copy = number_list[:]           # Shallow copy
        
        return {
            'mixed_list': mixed_list,
            'squares': squares,
            'even_numbers': even_numbers,
            'number_list': number_list,
            'first_three': first_three,
            'last_two': last_two,
            'reverse_copy': reverse_copy
        }
    
    @staticmethod
    def tuples():
        """Tuple operations (immutable)"""
        # Creation
        empty_tuple = ()
        single_tuple = (1,)             # Comma is required
        tuple_data = (1, 2, 3, "four")
        
        # Unpacking
        a, b, c, d = tuple_data
        
        # Tuple methods (limited)
        count = tuple_data.count(1)
        index = tuple_data.index(2)
        
        # Named tuples (using class)
        from collections import namedtuple
        Point = namedtuple('Point', ['x', 'y'])
        point = Point(10, 20)
        x_val = point.x
        y_val = point.y
        
        return {
            'tuple_data': tuple_data,
            'a': a, 'b': b, 'c': c, 'd': d,
            'point': point,
            'x_val': x_val,
            'y_val': y_val
        }
    
    @staticmethod
    def dictionaries():
        """Dictionary operations"""
        # Creation
        empty_dict = {}
        person = {
            'name': 'Alice',
            'age': 30,
            'city': 'New York'
        }
        
        # Dict comprehension
        squares_dict = {x: x**2 for x in range(5)}
        
        # Operations
        name = person['name']           # Access
        person['email'] = 'alice@email.com'  # Add/Update
        age = person.get('age', 0)      # Get with default
        person.pop('city')              # Remove and return
        
        # Iteration
        keys = person.keys()
        values = person.values()
        items = person.items()
        
        # Merging (Python 3.9+)
        dict1 = {'a': 1, 'b': 2}
        dict2 = {'c': 3, 'd': 4}
        merged = {**dict1, **dict2}     # Merge dictionaries
        
        return {
            'person': person,
            'squares_dict': squares_dict,
            'name': name,
            'age': age,
            'merged': merged
        }
    
    @staticmethod
    def sets():
        """Set operations (unique elements)"""
        # Creation
        empty_set = set()
        number_set = {1, 2, 3, 4, 5}
        set_from_list = set([1, 2, 2, 3, 3, 4])  # {1, 2, 3, 4}
        
        # Set comprehension
        even_set = {x for x in range(10) if x % 2 == 0}
        
        # Operations
        number_set.add(6)
        number_set.remove(1)            # Raises KeyError if not found
        number_set.discard(10)          # No error if not found
        popped = number_set.pop()       # Remove arbitrary element
        
        # Set operations
        set_a = {1, 2, 3, 4}
        set_b = {3, 4, 5, 6}
        
        union = set_a.union(set_b)      # {1, 2, 3, 4, 5, 6}
        intersection = set_a.intersection(set_b)  # {3, 4}
        difference = set_a.difference(set_b)      # {1, 2}
        symmetric_diff = set_a.symmetric_difference(set_b)  # {1, 2, 5, 6}
        
        # Subset/Superset
        is_subset = {1, 2}.issubset(set_a)
        is_superset = set_a.issuperset({1, 2})
        
        return {
            'number_set': number_set,
            'even_set': even_set,
            'union': union,
            'intersection': intersection,
            'difference': difference,
            'symmetric_diff': symmetric_diff,
            'is_subset': is_subset,
            'is_superset': is_superset
        }


# ============================================
# 3. STRING OPERATIONS
# ============================================

class StringOperations:
    """Python string operations cheat sheet"""
    
    @staticmethod
    def string_methods():
        """Common string methods"""
        text = "  Hello, World!  "
        
        # Case conversion
        upper = text.upper()
        lower = text.lower()
        title = text.title()
        capitalize = text.capitalize()
        swapcase = text.swapcase()
        
        # Whitespace
        stripped = text.strip()
        lstrip = text.lstrip()
        rstrip = text.rstrip()
        
        # Search and replace
        replaced = text.replace("World", "Python")
        contains = "World" in text
        position = text.find("World")
        rposition = text.rfind("World")
        index = text.index("World")     # Raises ValueError if not found
        
        # Split and join
        words = text.split()
        split_by_comma = "a,b,c".split(",")
        joined = ", ".join(["a", "b", "c"])
        partition = text.partition("World")
        
        # Validation
        is_alpha = "Hello".isalpha()
        is_digit = "123".isdigit()
        is_alnum = "Hello123".isalnum()
        is_space = "   ".isspace()
        is_lower = "hello".islower()
        is_upper = "HELLO".isupper()
        
        # Formatting
        formatted1 = "Hello, {}".format("World")
        formatted2 = "Hello, {name}".format(name="World")
        formatted3 = f"Hello, {'World'}"  # f-string
        
        # Padding
        centered = "Hello".center(11, "-")  # '---Hello---'
        left_just = "Hello".ljust(10, "*")
        right_just = "Hello".rjust(10, "*")
        zfilled = "42".zfill(5)          # '00042'
        
        return {
            'text': text,
            'upper': upper,
            'lower': lower,
            'stripped': stripped,
            'replaced': replaced,
            'words': words,
            'joined': joined,
            'formatted1': formatted1,
            'formatted2': formatted2,
            'formatted3': formatted3,
            'centered': centered,
            'is_alpha': is_alpha,
            'is_digit': is_digit
        }
    
    @staticmethod
    def advanced_string():
        """Advanced string operations"""
        # F-strings formatting
        name = "Alice"
        age = 30
        height = 5.6789
        
        f_strings = {
            'basic': f"Name: {name}, Age: {age}",
            'expressions': f"Double age: {age * 2}",
            'formatting': f"Height: {height:.2f}",
            'padding': f"{name:>10}",
            'alignment': f"{name:^20}",
            'dictionary': f"Name: {person['name']}" if 'person' in locals() else "N/A"
        }
        
        # String multiplication
        repeated = "-" * 20
        
        # Raw strings
        raw = r"Path: C:\Users\Name\Documents"
        
        # Unicode
        unicode_char = "\u03A9"  # Omega
        
        return {
            'f_strings': f_strings,
            'repeated': repeated,
            'raw': raw,
            'unicode_char': unicode_char
        }


# ============================================
# 4. CONTROL FLOW
# ============================================

class ControlFlow:
    """Python control flow cheat sheet"""
    
    @staticmethod
    def if_else():
        """If-else statements"""
        x = 10
        y = 20
        
        # Basic if-else
        if x > y:
            result = "x is greater"
        elif x < y:
            result = "x is smaller"
        else:
            result = "x equals y"
        
        # Ternary operator
        max_val = x if x > y else y
        min_val = x if x < y else y
        
        # Multiple conditions
        if x > 0 and y > 0:
            positive = True
        else:
            positive = False
        
        if x > 0 or y < 0:
            condition = True
        else:
            condition = False
        
        return {
            'result': result,
            'max_val': max_val,
            'min_val': min_val,
            'positive': positive,
            'condition': condition
        }
    
    @staticmethod
    def loops():
        """Loop operations"""
        # For loop
        numbers = [1, 2, 3, 4, 5]
        squares = []
        for num in numbers:
            squares.append(num ** 2)
        
        # For loop with enumerate
        indexed = []
        for i, value in enumerate(numbers):
            indexed.append((i, value))
        
        # For loop with zip
        names = ['Alice', 'Bob', 'Charlie']
        ages = [25, 30, 35]
        for name, age in zip(names, ages):
            person = f"{name} is {age} years old"
        
        # While loop
        count = 0
        while count < 5:
            count += 1
        
        # Loop control
        for i in range(10):
            if i == 3:
                continue        # Skip this iteration
            if i == 7:
                break           # Exit loop
            if i == 5:
                pass            # Do nothing
        
        # For-else (executes if loop completes without break)
        found = False
        for i in range(5):
            if i == 10:
                break
        else:
            found = True        # This executes because no break
        
        return {
            'squares': squares,
            'indexed': indexed,
            'count': count,
            'found': found
        }


# ============================================
# 5. FUNCTIONS
# ============================================

class Functions:
    """Python functions cheat sheet"""
    
    @staticmethod
    def basic_functions():
        """Basic function definitions"""
        # Simple function
        def greet(name):
            return f"Hello, {name}!"
        
        # Default arguments
        def greet_with_title(name, title="Mr."):
            return f"Hello, {title} {name}"
        
        # Positional arguments
        def add(a, b):
            return a + b
        
        # Keyword arguments
        def person_info(name, age, city="Unknown"):
            return f"{name} is {age} years old from {city}"
        
        # Variable arguments
        def sum_all(*args):
            return sum(args)
        
        def keyword_args(**kwargs):
            return kwargs
        
        # Return multiple values
        def min_max(numbers):
            return min(numbers), max(numbers)
        
        min_val, max_val = min_max([1, 2, 3, 4, 5])
        
        return {
            'greet': greet,
            'greet_with_title': greet_with_title,
            'add': add,
            'person_info': person_info,
            'sum_all': sum_all,
            'keyword_args': keyword_args,
            'min_val': min_val,
            'max_val': max_val
        }
    
    @staticmethod
    def advanced_functions():
        """Advanced function concepts"""
        # Lambda functions
        square = lambda x: x ** 2
        multiply = lambda x, y: x * y
        
        # Map
        numbers = [1, 2, 3, 4, 5]
        squared = list(map(lambda x: x**2, numbers))
        
        # Filter
        even = list(filter(lambda x: x % 2 == 0, numbers))
        
        # Reduce
        from functools import reduce
        product = reduce(lambda x, y: x * y, numbers)
        
        # Decorators
        def timer_decorator(func):
            import time
            def wrapper(*args, **kwargs):
                start = time.time()
                result = func(*args, **kwargs)
                end = time.time()
                print(f"{func.__name__} took {end - start:.4f} seconds")
                return result
            return wrapper
        
        @timer_decorator
        def slow_function():
            import time
            time.sleep(0.1)
            return "Done"
        
        # Function annotations
        def annotated_function(x: int, y: str) -> bool:
            return len(y) > x
        
        # Default mutable arguments (be careful!)
        def add_to_list(value, my_list=[]):
            my_list.append(value)
            return my_list
        
        # Better approach
        def add_to_list_safe(value, my_list=None):
            if my_list is None:
                my_list = []
            my_list.append(value)
            return my_list
        
        return {
            'square': square,
            'multiply': multiply,
            'squared': squared,
            'even': even,
            'product': product,
            'slow_function': slow_function,
            'annotated_function': annotated_function,
            'add_to_list': add_to_list,
            'add_to_list_safe': add_to_list_safe
        }


# ============================================
# 6. CLASSES AND OOP
# ============================================

class OOP:
    """Object-Oriented Programming cheat sheet"""
    
    @staticmethod
    def classes_basics():
        """Basic class concepts"""
        
        class Person:
            # Class variable
            species = "Homo sapiens"
            
            # Constructor
            def __init__(self, name, age):
                self.name = name        # Instance variable
                self.age = age
                self._private = "Private"   # Convention for private
                self.__mangled = "Mangled"  # Name mangling
            
            # Instance method
            def greet(self):
                return f"Hello, I'm {self.name}"
            
            # Class method
            @classmethod
            def create_anonymous(cls):
                return cls("Anonymous", 0)
            
            # Static method
            @staticmethod
            def is_adult(age):
                return age >= 18
            
            # Property (getter)
            @property
            def age_in_months(self):
                return self.age * 12
            
            # Setter
            @age_in_months.setter
            def age_in_months(self, months):
                self.age = months // 12
            
            # String representation
            def __str__(self):
                return f"Person(name={self.name}, age={self.age})"
            
            def __repr__(self):
                return f"Person('{self.name}', {self.age})"
        
        # Inheritance
        class Student(Person):
            def __init__(self, name, age, student_id):
                super().__init__(name, age)  # Call parent constructor
                self.student_id = student_id
                self.grades = []
            
            def add_grade(self, grade):
                self.grades.append(grade)
            
            def average_grade(self):
                return sum(self.grades) / len(self.grades) if self.grades else 0
            
            # Override method
            def greet(self):
                return f"Hello, I'm {self.name}, student ID: {self.student_id}"
        
        # Multiple inheritance
        class Mixin:
            def extra_method(self):
                return "Extra functionality"
        
        class AdvancedStudent(Student, Mixin):
            pass
        
        return {
            'Person': Person,
            'Student': Student,
            'AdvancedStudent': AdvancedStudent
        }
    
    @staticmethod
    class MagicMethods:
        """Magic (dunder) methods"""
        
        class Vector:
            def __init__(self, x, y):
                self.x = x
                self.y = y
            
            def __add__(self, other):
                return Vector(self.x + other.x, self.y + other.y)
            
            def __sub__(self, other):
                return Vector(self.x - other.x, self.y - other.y)
            
            def __mul__(self, scalar):
                return Vector(self.x * scalar, self.y * scalar)
            
            def __eq__(self, other):
                return self.x == other.x and self.y == other.y
            
            def __lt__(self, other):
                return (self.x**2 + self.y**2) < (other.x**2 + other.y**2)
            
            def __len__(self):
                return 2
            
            def __getitem__(self, index):
                if index == 0:
                    return self.x
                elif index == 1:
                    return self.y
                raise IndexError("Index out of range")
            
            def __setitem__(self, index, value):
                if index == 0:
                    self.x = value
                elif index == 1:
                    self.y = value
                else:
                    raise IndexError("Index out of range")
            
            def __iter__(self):
                yield self.x
                yield self.y
            
            def __str__(self):
                return f"Vector({self.x}, {self.y})"
            
            def __repr__(self):
                return f"Vector({self.x}, {self.y})"
            
            def __call__(self):
                return f"Vector called with ({self.x}, {self.y})"
        
        return {'Vector': Vector}


# ============================================
# 7. FILE OPERATIONS
# ============================================

class FileOperations:
    """File operations cheat sheet"""
    
    @staticmethod
    def file_reading_writing():
        """Reading and writing files"""
        import os
        
        # Writing to file
        with open('example.txt', 'w') as file:
            file.write('Hello, World!\n')
            file.write('Second line\n')
            file.writelines(['Third line\n', 'Fourth line\n'])
        
        # Reading from file
        with open('example.txt', 'r') as file:
            content = file.read()           # Read entire file
            content_lines = content.splitlines()
        
        with open('example.txt', 'r') as file:
            line1 = file.readline()         # Read one line
            remaining = file.readlines()    # Read remaining lines
        
        # Appending to file
        with open('example.txt', 'a') as file:
            file.write('Appended line\n')
        
        # Reading line by line (memory efficient)
        lines_processed = []
        with open('example.txt', 'r') as file:
            for line in file:
                lines_processed.append(line.strip())
        
        # Binary files
        with open('example.bin', 'wb') as file:
            file.write(b'Binary data')
        
        with open('example.bin', 'rb') as file:
            binary_data = file.read()
        
        # File operations
        file_exists = os.path.exists('example.txt')
        file_size = os.path.getsize('example.txt')
        
        return {
            'content': content,
            'line1': line1,
            'remaining': remaining,
            'lines_processed': lines_processed,
            'binary_data': binary_data,
            'file_exists': file_exists,
            'file_size': file_size
        }
    
    @staticmethod
    def file_context_manager():
        """File context managers"""
        import os
        
        # Custom context manager
        class FileManager:
            def __init__(self, filename, mode):
                self.filename = filename
                self.mode = mode
                self.file = None
            
            def __enter__(self):
                self.file = open(self.filename, self.mode)
                return self.file
            
            def __exit__(self, exc_type, exc_val, exc_tb):
                if self.file:
                    self.file.close()
                # Return True to suppress exceptions
                return False
        
        # Using custom context manager
        with FileManager('example2.txt', 'w') as file:
            file.write('Using custom context manager\n')
        
        # Contextlib
        from contextlib import contextmanager
        
        @contextmanager
        def open_file(filename, mode):
            file = open(filename, mode)
            try:
                yield file
            finally:
                file.close()
        
        with open_file('example3.txt', 'w') as file:
            file.write('Using contextlib\n')
        
        return {}


# ============================================
# 8. EXCEPTION HANDLING
# ============================================

class ExceptionHandling:
    """Exception handling cheat sheet"""
    
    @staticmethod
    def exceptions():
        """Try-except blocks"""
        
        # Basic try-except
        try:
            result = 10 / 0
        except ZeroDivisionError:
            result = "Division by zero handled"
        
        # Multiple exceptions
        try:
            value = int("abc")
        except (ValueError, TypeError):
            value = "Conversion failed"
        
        # Multiple except blocks
        try:
            data = [1, 2, 3]
            value = data[5]
        except IndexError:
            value = "Index out of range"
        except TypeError:
            value = "Type error"
        except Exception as e:
            value = f"Unknown error: {e}"
        
        # Try-except-else-finally
        try:
            num = int("123")
        except ValueError:
            num = 0
        else:
            print("Conversion successful")
        finally:
            print("This always executes")
        
        # Raising exceptions
        def validate_age(age):
            if age < 0:
                raise ValueError("Age cannot be negative")
            if age > 150:
                raise ValueError("Age too high")
            return age
        
        # Custom exceptions
        class CustomError(Exception):
            def __init__(self, message):
                self.message = message
                super().__init__(self.message)
        
        try:
            raise CustomError("This is a custom error")
        except CustomError as e:
            error_message = e.message
        
        return {
            'result': result,
            'value': value,
            'num': num,
            'error_message': error_message
        }


# ============================================
# 9. MODULES AND PACKAGES
# ============================================

class ModulesPackages:
    """Modules and packages cheat sheet"""
    
    @staticmethod
    def modules():
        """Module operations"""
        import sys
        import math
        import random
        from datetime import datetime, timedelta
        import json
        
        # Getting module info
        module_path = sys.path
        current_module = __name__
        
        # Mathematical functions
        sqrt = math.sqrt(25)
        sin = math.sin(math.pi / 2)
        
        # Random functions
        rand_int = random.randint(1, 10)
        rand_float = random.random()
        rand_choice = random.choice(['a', 'b', 'c'])
        random.shuffle(['a', 'b', 'c'])
        
        # Date time
        now = datetime.now()
        future = now + timedelta(days=5)
        formatted_date = now.strftime("%Y-%m-%d %H:%M:%S")
        
        # JSON
        data = {'name': 'Alice', 'age': 30}
        json_string = json.dumps(data)
        parsed_data = json.loads(json_string)
        
        # Creating dynamic modules
        import importlib
        # math = importlib.import_module('math')
        
        return {
            'module_path': module_path,
            'sqrt': sqrt,
            'sin': sin,
            'rand_int': rand_int,
            'rand_float': rand_float,
            'rand_choice': rand_choice,
            'now': now,
            'future': future,
            'formatted_date': formatted_date,
            'json_string': json_string,
            'parsed_data': parsed_data
        }


# ============================================
# 10. ITERATORS AND GENERATORS
# ============================================

class IteratorsGenerators:
    """Iterators and generators cheat sheet"""
    
    @staticmethod
    def iterators():
        """Iterator patterns"""
        
        # Iterator protocol
        class Counter:
            def __init__(self, start, end):
                self.current = start
                self.end = end
            
            def __iter__(self):
                return self
            
            def __next__(self):
                if self.current >= self.end:
                    raise StopIteration
                self.current += 1
                return self.current - 1
        
        counter = Counter(1, 5)
        counter_values = list(counter)
        
        # Built-in iterators
        my_list = [1, 2, 3, 4, 5]
        list_iterator = iter(my_list)
        next_value = next(list_iterator)
        
        # Generators
        def count_up_to(n):
            i = 0
            while i < n:
                yield i
                i += 1
        
        gen = count_up_to(5)
        gen_values = list(gen)
        
        # Generator expressions
        squares = (x**2 for x in range(10))
        squares_list = list(squares)
        
        # Infinite generator
        def infinite_counter():
            i = 0
            while True:
                yield i
                i += 1
        
        # Using itertools
        from itertools import count, cycle, repeat, product, permutations
        
        count_iter = count(0, 2)  # 0, 2, 4, 6, ...
        cycle_iter = cycle('ABC')  # A, B, C, A, B, C, ...
        repeat_iter = repeat(10, 3)  # 10, 10, 10
        
        # Chain
        from itertools import chain
        chain_iter = chain([1, 2, 3], [4, 5, 6])
        chain_list = list(chain_iter)
        
        return {
            'counter_values': counter_values,
            'next_value': next_value,
            'gen_values': gen_values,
            'squares_list': squares_list,
            'chain_list': chain_list
        }


# ============================================
# 11. DECORATORS
# ============================================

class Decorators:
    """Decorator cheat sheet"""
    
    @staticmethod
    def decorator_examples():
        """Decorator examples"""
        import time
        from functools import wraps
        
        # Basic decorator
        def timer(func):
            @wraps(func)
            def wrapper(*args, **kwargs):
                start = time.time()
                result = func(*args, **kwargs)
                end = time.time()
                print(f"{func.__name__} took {end - start:.4f} seconds")
                return result
            return wrapper
        
        @timer
        def slow_function():
            time.sleep(0.1)
            return "Done"
        
        # Decorator with arguments
        def repeat(times):
            def decorator(func):
                @wraps(func)
                def wrapper(*args, **kwargs):
                    results = []
                    for _ in range(times):
                        results.append(func(*args, **kwargs))
                    return results
                return wrapper
            return decorator
        
        @repeat(3)
        def greet(name):
            return f"Hello, {name}!"
        
        # Class decorator
        def add_method(cls):
            def new_method(self):
                return "Added method"
            cls.new_method = new_method
            return cls
        
        @add_method
        class MyClass:
            pass
        
        # Property decorators
        class Temperature:
            def __init__(self, celsius):
                self._celsius = celsius
            
            @property
            def celsius(self):
                return self._celsius
            
            @celsius.setter
            def celsius(self, value):
                self._celsius = value
            
            @property
            def fahrenheit(self):
                return self._celsius * 9/5 + 32
            
            @fahrenheit.setter
            def fahrenheit(self, value):
                self._celsius = (value - 32) * 5/9
        
        temp = Temperature(25)
        f_temp = temp.fahrenheit
        temp.fahrenheit = 77
        
        return {
            'slow_function': slow_function,
            'greet': greet,
            'MyClass': MyClass,
            'Temperature': Temperature,
            'temp': temp,
            'f_temp': f_temp
        }


# ============================================
# 12. CONTEXT MANAGERS
# ============================================

class ContextManagers:
    """Context managers cheat sheet"""
    
    @staticmethod
    def context_examples():
        """Context manager examples"""
        import contextlib
        
        # Class-based context manager
        class Timer:
            def __init__(self, name="Timer"):
                self.name = name
                self.start = None
                self.end = None
            
            def __enter__(self):
                import time
                self.start = time.time()
                return self
            
            def __exit__(self, exc_type, exc_val, exc_tb):
                import time
                self.end = time.time()
                print(f"{self.name}: {self.end - self.start:.4f} seconds")
                # Return False to propagate exceptions
                return False
        
        with Timer("Operation") as timer:
            import time
            time.sleep(0.1)
        
        # Contextlib-based context manager
        @contextlib.contextmanager
        def managed_resource(*args, **kwargs):
            # Setup
            resource = open(*args, **kwargs)
            try:
                yield resource
            finally:
                # Cleanup
                resource.close()
        
        with managed_resource('example.txt', 'w') as file:
            file.write('Context manager example\n')
        
        # Multiple context managers
        with open('file1.txt', 'w') as f1, open('file2.txt', 'w') as f2:
            f1.write('File 1')
            f2.write('File 2')
        
        # Contextlib utilities
        @contextlib.contextmanager
        def ignored(*exceptions):
            try:
                yield
            except exceptions:
                pass
        
        with ignored(ValueError):
            int('abc')  # This will be ignored
        
        return {}


# ============================================
# 13. REGULAR EXPRESSIONS
# ============================================

class RegularExpressions:
    """Regular expressions cheat sheet"""
    
    @staticmethod
    def regex_examples():
        """Regex operations"""
        import re
        
        text = "The quick brown fox jumps over the lazy dog. The dog was lazy."
        
        # Pattern matching
        pattern = r'\bfox\b'
        match = re.search(pattern, text)
        if match:
            matched_text = match.group()
            match_position = match.span()
        
        # Find all matches
        pattern = r'\blazy\b'
        matches = re.findall(pattern, text)
        matches_iter = re.finditer(pattern, text)
        matches_info = [(m.group(), m.span()) for m in matches_iter]
        
        # Substitute
        pattern = r'dog'
        replaced = re.sub(pattern, 'cat', text)
        replaced_count = re.subn(pattern, 'cat', text)
        
        # Split
        pattern = r'\s+'
        words = re.split(pattern, text)
        
        # Compile pattern
        compiled = re.compile(r'\b\w{3}\b')  # Words of length 3
        three_letter_words = compiled.findall(text)
        
        # Groups
        pattern = r'(\w+) (\w+) (\w+)'  # Three words
        match = re.search(pattern, text)
        if match:
            groups = match.groups()
            group0 = match.group(0)  # Full match
            group1 = match.group(1)  # First group
            group2 = match.group(2)  # Second group
        
        # Named groups
        pattern = r'(?P<word1>\w+) (?P<word2>\w+)'
        match = re.search(pattern, text)
        if match:
            named_groups = match.groupdict()
        
        # Flags
        pattern = r'THE'
        case_insensitive = re.findall(pattern, text, re.IGNORECASE)
        
        # Common patterns
        email_pattern = r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}'
        email = 'test@example.com'
        is_email = bool(re.match(email_pattern, email))
        
        return {
            'matched_text': matched_text if 'matched_text' in locals() else None,
            'matches': matches if 'matches' in locals() else [],
            'matches_info': matches_info if 'matches_info' in locals() else [],
            'replaced': replaced if 'replaced' in locals() else text,
            'words': words if 'words' in locals() else [],
            'three_letter_words': three_letter_words if 'three_letter_words' in locals() else [],
            'groups': groups if 'groups' in locals() else (),
            'named_groups': named_groups if 'named_groups' in locals() else {},
            'case_insensitive': case_insensitive if 'case_insensitive' in locals() else [],
            'is_email': is_email if 'is_email' in locals() else False
        }


# ============================================
# 14. THREADING AND MULTIPROCESSING
# ============================================

class Concurrency:
    """Threading and multiprocessing cheat sheet"""
    
    @staticmethod
    def threading_examples():
        """Threading operations"""
        import threading
        import time
        
        # Basic thread
        def worker(name, delay):
            time.sleep(delay)
            return f"Worker {name} completed"
        
        thread1 = threading.Thread(target=worker, args=("A", 0.1))
        thread2 = threading.Thread(target=worker, args=("B", 0.2))
        
        thread1.start()
        thread2.start()
        thread1.join()
        thread2.join()
        
        # Thread with shared state (use locks!)
        counter = 0
        lock = threading.Lock()
        
        def increment():
            global counter
            for _ in range(1000):
                with lock:
                    counter += 1
        
        threads = []
        for _ in range(5):
            t = threading.Thread(target=increment)
            threads.append(t)
            t.start()
        
        for t in threads:
            t.join()
        
        # Thread-safe queue
        import queue
        q = queue.Queue()
        
        def producer():
            for i in range(5):
                q.put(i)
                time.sleep(0.01)
            q.put(None)  # Sentinel
        
        def consumer():
            while True:
                item = q.get()
                if item is None:
                    break
                process_item = item * 2
        
        # ThreadLocal
        local_data = threading.local()
        local_data.value = "Thread-specific data"
        
        return {
            'counter': counter,
            'local_data': local_data
        }
    
    @staticmethod
    def multiprocessing_examples():
        """Multiprocessing operations"""
        import multiprocessing
        import time
        
        # Basic process
        def worker(name, delay):
            time.sleep(delay)
            return f"Process {name} completed"
        
        pool = multiprocessing.Pool(processes=4)
        results = pool.map(worker, [("A", 0.1), ("B", 0.2), ("C", 0.3)])
        pool.close()
        pool.join()
        
        # Process pool with async
        async_results = []
        with multiprocessing.Pool(processes=2) as pool:
            for i in range(4):
                result = pool.apply_async(worker, (f"P{i}", 0.1))
                async_results.append(result)
            
            for result in async_results:
                result.get()
        
        # Shared memory
        shared_value = multiprocessing.Value('i', 0)
        shared_array = multiprocessing.Array('d', [0.0] * 10)
        
        def increment_shared(shared):
            with shared.get_lock():
                shared.value += 1
        
        return {
            'results': results,
            'shared_value': shared_value
        }


# ============================================
# 15. COMMON UTILITIES
# ============================================

class CommonUtilities:
    """Common utility functions and patterns"""
    
    @staticmethod
    def utilities():
        """Common utilities"""
        import os
        import sys
        import json
        import hashlib
        from datetime import datetime, timedelta
        
        # Working directory operations
        current_dir = os.getcwd()
        files = os.listdir('.')
        path_exists = os.path.exists('example.txt')
        is_file = os.path.isfile('example.txt')
        is_dir = os.path.isdir('examples')
        
        # Path operations
        import pathlib
        path = pathlib.Path('example.txt')
        path_stem = path.stem
        path_suffix = path.suffix
        path_parent = path.parent
        
        # Hash functions
        data = b"Hello, World!"
        md5_hash = hashlib.md5(data).hexdigest()
        sha256_hash = hashlib.sha256(data).hexdigest()
        
        # Command line arguments
        sys_argv = sys.argv
        
        # Environment variables
        import os
        env_path = os.environ.get('PATH', '')
        
        # Memory usage
        import sys
        list_size = sys.getsizeof([1, 2, 3, 4, 5])
        
        # Performance timing
        import time
        start_time = time.time()
        time.sleep(0.1)
        elapsed = time.time() - start_time
        
        return {
            'current_dir': current_dir,
            'files': files[:5],  # First 5 files
            'path_exists': path_exists,
            'is_file': is_file,
            'is_dir': is_dir,
            'path_stem': path_stem,
            'path_suffix': path_suffix,
            'path_parent': path_parent,
            'md5_hash': md5_hash,
            'sha256_hash': sha256_hash,
            'list_size': list_size,
            'elapsed': elapsed
        }


# ============================================
# MAIN MODULE EXPORTS
# ============================================

# Export all classes for easy access
__all__ = [
    'BasicSyntax',
    'Collections',
    'StringOperations',
    'ControlFlow',
    'Functions',
    'OOP',
    'FileOperations',
    'ExceptionHandling',
    'ModulesPackages',
    'IteratorsGenerators',
    'Decorators',
    'ContextManagers',
    'RegularExpressions',
    'Concurrency',
    'CommonUtilities'
]

# Module-level helper function
def run_demo():
    """Run a comprehensive demonstration of all features"""
    print("=" * 60)
    print("PYTHON CHEAT SHEET DEMONSTRATION")
    print("=" * 60)
    
    # Basic Syntax
    print("\n1. BASIC SYNTAX")
    print("-" * 40)
    basics = BasicSyntax()
    print("Data Types:", basics.data_types())
    print("Variables:", basics.variables_and_naming())
    
    # Collections
    print("\n2. COLLECTIONS")
    print("-" * 40)
    collections = Collections()
    print("List Example:", collections.lists())
    print("Tuple Example:", collections.tuples())
    print("Dictionary Example:", collections.dictionaries())
    print("Set Example:", collections.sets())
    
    # String Operations
    print("\n3. STRING OPERATIONS")
    print("-" * 40)
    strings = StringOperations()
    print("String Methods:", strings.string_methods())
    
    # Control Flow
    print("\n4. CONTROL FLOW")
    print("-" * 40)
    control = ControlFlow()
    print("If-Else Example:", control.if_else())
    print("Loop Example:", control.loops())
    
    # Functions
    print("\n5. FUNCTIONS")
    print("-" * 40)
    functions = Functions()
    basic_funcs = functions.basic_functions()
    print("Basic Functions:", list(basic_funcs.keys()))
    advanced_funcs = functions.advanced_functions()
    print("Advanced Functions:", list(advanced_funcs.keys()))
    
    # OOP
    print("\n6. OOP")
    print("-" * 40)
    oop = OOP()
    classes = oop.classes_basics()
    print("Classes Created:", list(classes.keys()))
    print("Magic Methods:", oop.MagicMethods.__name__)
    
    print("\n" + "=" * 60)
    print("DEMONSTRATION COMPLETE")
    print("=" * 60)

# Module initialization
if __name__ == "__main__":
    run_demo()
```

## File 2: `showcase.py` - Comprehensive Showcase Script

```python
"""
Showcase Script for Python Cheat Sheet Module
Demonstrates all features with practical examples
"""

import sys
import os
import time
from cheat_sheet import *

def showcase_basic_syntax():
    """Showcase basic syntax and data types"""
    print("\n" + "="*60)
    print("SHOWCASE: BASIC SYNTAX")
    print("="*60)
    
    basics = BasicSyntax()
    
    # Data types demonstration
    data_types = basics.data_types()
    print("\nData Types:")
    for key, value in data_types.items():
        print(f"  {key}: {value} (type: {type(value).__name__})")
    
    # Variables demonstration
    variables = basics.variables_and_naming()
    print("\nVariables:")
    for key, value in variables.items():
        print(f"  {key}: {value} (type: {type(value).__name__})")


def showcase_collections():
    """Showcase collections"""
    print("\n" + "="*60)
    print("SHOWCASE: COLLECTIONS")
    print("="*60)
    
    collections = Collections()
    
    # Lists
    print("\nLists:")
    list_data = collections.lists()
    print(f"  Mixed list: {list_data['mixed_list']}")
    print(f"  Squares: {list_data['squares']}")
    print(f"  Even numbers: {list_data['even_numbers']}")
    print(f"  First three: {list_data['first_three']}")
    print(f"  Last two: {list_data['last_two']}")
    
    # Tuples
    print("\nTuples:")
    tuple_data = collections.tuples()
    print(f"  Tuple: {tuple_data['tuple_data']}")
    print(f"  Unpacked: {tuple_data['a']}, {tuple_data['b']}, {tuple_data['c']}, {tuple_data['d']}")
    
    # Dictionaries
    print("\nDictionaries:")
    dict_data = collections.dictionaries()
    print(f"  Person: {dict_data['person']}")
    print(f"  Squares dict: {dict_data['squares_dict']}")
    
    # Sets
    print("\nSets:")
    set_data = collections.sets()
    print(f"  Number set: {set_data['number_set']}")
    print(f"  Union: {set_data['union']}")
    print(f"  Intersection: {set_data['intersection']}")


def showcase_strings():
    """Showcase string operations"""
    print("\n" + "="*60)
    print("SHOWCASE: STRING OPERATIONS")
    print("="*60)
    
    strings = StringOperations()
    
    print("\nString Methods:")
    string_data = strings.string_methods()
    for key, value in string_data.items():
        if isinstance(value, str) and len(str(value)) < 50:
            print(f"  {key}: '{value}'")
        elif isinstance(value, list) and len(value) < 10:
            print(f"  {key}: {value}")
    
    print("\nF-strings:")
    fstring_data = strings.advanced_string()['f_strings']
    for key, value in fstring_data.items():
        print(f"  {key}: {value}")


def showcase_control_flow():
    """Showcase control flow"""
    print("\n" + "="*60)
    print("SHOWCASE: CONTROL FLOW")
    print("="*60)
    
    control = ControlFlow()
    
    print("\nIf-Else:")
    if_data = control.if_else()
    for key, value in if_data.items():
        print(f"  {key}: {value}")
    
    print("\nLoops:")
    loop_data = control.loops()
    for key, value in loop_data.items():
        print(f"  {key}: {value}")


def showcase_functions():
    """Showcase functions"""
    print("\n" + "="*60)
    print("SHOWCASE: FUNCTIONS")
    print("="*60)
    
    functions = Functions()
    
    print("\nBasic Functions:")
    basic_data = functions.basic_functions()
    for key, value in basic_data.items():
        if callable(value):
            print(f"  {key}: {value.__name__}")
        else:
            print(f"  {key}: {value}")
    
    print("\nAdvanced Functions:")
    advanced_data = functions.advanced_functions()
    for key, value in advanced_data.items():
        if callable(value):
            print(f"  {key}: {value.__name__}")
        elif isinstance(value, list):
            print(f"  {key}: {value}")
        else:
            print(f"  {key}: {value}")


def showcase_oop():
    """Showcase object-oriented programming"""
    print("\n" + "="*60)
    print("SHOWCASE: OOP")
    print("="*60)
    
    oop = OOP()
    
    print("\nClass Creation:")
    classes = oop.classes_basics()
    for class_name, class_obj in classes.items():
        print(f"  {class_name}: {class_obj.__name__}")
    
    # Create instances and demonstrate
    Person = classes['Person']
    Student = classes['Student']
    
    person = Person("Alice", 30)
    student = Student("Bob", 20, "S123")
    student.add_grade(85)
    student.add_grade(90)
    
    print(f"\nPerson: {person}")
    print(f"Student: {student}")
    print(f"Student greet: {student.greet()}")
    print(f"Student average: {student.average_grade():.2f}")
    
    print("\nMagic Methods:")
    Vector = oop.MagicMethods.Vector
    v1 = Vector(1, 2)
    v2 = Vector(3, 4)
    
    print(f"  v1: {v1}")
    print(f"  v2: {v2}")
    print(f"  v1 + v2: {v1 + v2}")
    print(f"  v1 * 3: {v1 * 3}")
    print(f"  v1 == v2: {v1 == v2}")
    print(f"  v1 < v2: {v1 < v2}")
    print(f"  len(v1): {len(v1)}")
    print(f"  v1[0]: {v1[0]}")
    print(f"  list(v1): {list(v1)}")


def showcase_exceptions():
    """Showcase exception handling"""
    print("\n" + "="*60)
    print("SHOWCASE: EXCEPTION HANDLING")
    print("="*60)
    
    exceptions = ExceptionHandling()
    
    print("\nException Examples:")
    exception_data = exceptions.exceptions()
    for key, value in exception_data.items():
        print(f"  {key}: {value}")


def showcase_iterators_generators():
    """Showcase iterators and generators"""
    print("\n" + "="*60)
    print("SHOWCASE: ITERATORS AND GENERATORS")
    print("="*60)
    
    iter_gen = IteratorsGenerators()
    
    print("\nIterator and Generator Examples:")
    data = iter_gen.iterators()
    for key, value in data.items():
        if isinstance(value, list):
            print(f"  {key}: {value}")
        else:
            print(f"  {key}: {value}")


def showcase_file_operations():
    """Showcase file operations"""
    print("\n" + "="*60)
    print("SHOWCASE: FILE OPERATIONS")
    print("="*60)
    
    files = FileOperations()
    
    print("\nFile Operations:")
    try:
        file_data = files.file_reading_writing()
        print("  File written and read successfully")
        print(f"  File exists: {file_data['file_exists']}")
        print(f"  File size: {file_data['file_size']} bytes")
        print(f"  First line: {file_data.get('line1', 'N/A')}")
    except Exception as e:
        print(f"  Error in file operations: {e}")
    
    print("\nContext Managers:")
    files.file_context_manager()
    print("  Custom context manager used successfully")


def showcase_regex():
    """Showcase regular expressions"""
    print("\n" + "="*60)
    print("SHOWCASE: REGULAR EXPRESSIONS")
    print("="*60)
    
    regex = RegularExpressions()
    
    print("\nRegex Examples:")
    data = regex.regex_examples()
    for key, value in data.items():
        if isinstance(value, list) and len(value) > 5:
            print(f"  {key}: {value[:5]}...")
        elif isinstance(value, dict):
            print(f"  {key}: {value}")
        elif value:
            print(f"  {key}: {value}")


def showcase_utilities():
    """Showcase common utilities"""
    print("\n" + "="*60)
    print("SHOWCASE: COMMON UTILITIES")
    print("="*60)
    
    utils = CommonUtilities()
    
    print("\nUtilities:")
    data = utils.utilities()
    for key, value in data.items():
        if isinstance(value, str) and len(value) > 50:
            print(f"  {key}: {value[:50]}...")
        elif isinstance(value, list):
            print(f"  {key}: {value}")
        else:
            print(f"  {key}: {value}")


def showcase_decorators():
    """Showcase decorators"""
    print("\n" + "="*60)
    print("SHOWCASE: DECORATORS")
    print("="*60)
    
    decorators = Decorators()
    
    print("\nDecorator Examples:")
    data = decorators.decorator_examples()
    for key, value in data.items():
        if callable(value):
            print(f"  {key}: {value.__name__}")
        elif isinstance(value, list):
            print(f"  {key}: {value}")
        else:
            print(f"  {key}: {value}")


def main():
    """Main showcase function"""
    print("\n" + "="*60)
    print("PYTHON CHEAT SHEET - COMPREHENSIVE SHOWCASE")
    print("="*60)
    
    # Run all showcases
    showcase_basic_syntax()
    showcase_collections()
    showcase_strings()
    showcase_control_flow()
    showcase_functions()
    showcase_oop()
    showcase_exceptions()
    showcase_iterators_generators()
    showcase_file_operations()
    showcase_regex()
    showcase_utilities()
    showcase_decorators()
    
    print("\n" + "="*60)
    print("SHOWCASE COMPLETE")
    print("="*60)
    print("\nExplore the 'cheat_sheet.py' module for more details!")


if __name__ == "__main__":
    main()
```

## File 3: `__init__.py` - Package Initialization

```python
"""
Python Cheat Sheet Package
A comprehensive reference for Python programming
"""

from cheat_sheet import *

__version__ = "1.0.0"
__author__ = "Python Developer"

# Package metadata
__all__ = [
    'BasicSyntax',
    'Collections',
    'StringOperations',
    'ControlFlow',
    'Functions',
    'OOP',
    'FileOperations',
    'ExceptionHandling',
    'ModulesPackages',
    'IteratorsGenerators',
    'Decorators',
    'ContextManagers',
    'RegularExpressions',
    'Concurrency',
    'CommonUtilities'
]

# Convenience function to get cheat sheet info
def get_cheat_sheet_info():
    """Get information about the cheat sheet"""
    return {
        'version': __version__,
        'author': __author__,
        'modules': __all__,
        'total_classes': len(__all__)
    }

# Auto-run demo if run as script
if __name__ == "__main__":
    from cheat_sheet import run_demo
    run_demo()
```

## How to Use:

1. **Save all files** in the same directory:
   - `cheat_sheet.py` (main module)
   - `showcase.py` (showcase script)
   - `__init__.py` (package initialization)

2. **Run the showcase**:
```bash
python showcase.py
```

3. **Use as a module**:
```python
from cheat_sheet import *
# Access any class or functionality directly
```

## Key Features Covered:

1. **Basic Syntax**: Data types, variables, naming conventions
2. **Collections**: Lists, tuples, dictionaries, sets
3. **String Operations**: All common string methods and f-strings
4. **Control Flow**: If-else, loops, ternary operators
5. **Functions**: Basics, decorators, lambda, map/filter/reduce
6. **OOP**: Classes, inheritance, magic methods, properties
7. **File Operations**: Reading, writing, context managers
8. **Exception Handling**: Try-except, custom exceptions
9. **Modules/Packages**: Import system, common modules
10. **Iterators/Generators**: Custom iterators, generators, itertools
11. **Decorators**: Function decorators, class decorators
12. **Context Managers**: Class-based and contextlib-based
13. **Regular Expressions**: Pattern matching, groups, flags
14. **Concurrency**: Threading, multiprocessing, queues
15. **Common Utilities**: Path operations, hashing, timing

This cheat sheet provides a comprehensive reference that you can expand or modify as needed!
