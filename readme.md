# How to write your own effective modules for Python applications using rust

## Usage:

1. You need to install python library called maturin:
```
$ pip install maturin
```
2. Next, you need to init your maturin project:
```
$ maturin init
```
3. After that you need to check your source folder. There should be a file called ***lib.rs***
4. There you can find a simple example of usage. There is a simple rust function to make a summ of to digits, like this:

```rust
#[pyfunction]
fn sum_as_string(a: usize, b: usize) -> PyResult<String> {
    Ok((a + b).to_string())
}
``` 
Actuallay you can update it or write your own functions.

5. And after that you should add it in ***module***:

```rust
#[pymodule]
fn rust_with_python(_py: Python, m: &PyModule) -> PyResult<()> {
    m.add_function(wrap_pyfunction!(sum_as_string, m)?)?;
    Ok(())
}
```
6. Then, compile this module with command:

```
$ maturin develop
```

************************

Now you can call this new function from your python code. In *examples* folder you can test it.

```python

import rust_with_python

result = rust_with_python.sum_as_string(1, 2)

print("Your result is:", result)
```

