# Nginr Style Guide

nginr is a lightweight preprocessor for Python that offers an alternative syntax style and is still under active development.

## Key Features

- **Concise & Modern Syntax**: Use `fn` to declare functions easily
- **Type Hints**: Our style is full support for Python type hints
- **Pythonic**: Compatible with all existing Python libraries
- **Easy to Learn**: Of course, because it is based on Python

## Installation

```bash
pip install nginr
```

## Quick Start

### Simple Program
Create a file `example.xr`:

```python
# example.xr

fn greet(name: str) -> str:
    return f"Hello, {name}!"

fn main() -> None:
    name = input("What is your name? ")
    print(greet(name))

if __name__ == "__main__":
    main()
```

Run with:
```bash
nginr example.xr
```

## Documentation

See [STYLE_GUIDE_EN.md](STYLE_GUIDE_EN.md) for a comprehensive Nginr code style guide.

## Example Programs

Find various example programs in the [examples/](examples/) directory:

- `hello.xr` - Hello World program
- `calculator.xr` - Simple calculator
- `advanced_types.xr` - Advanced type hints examples
- `error_handling.xr` - Error handling examples
- `list_generator.xr` - List comprehension and generator examples

## Contributing

Contributions are welcome! Please create an issue or pull request for:
- Bug fixes
- New features
- Documentation improvements

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
