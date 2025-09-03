# Example Package

A basic example package demonstrating F2PI structure and conventions for Fortran² packages.

## Description

This package provides simple mathematical and utility functions to demonstrate the proper structure and conventions for F2PI packages. It includes basic arithmetic operations, string utilities, and mathematical functions.

## Features

- Basic arithmetic operations (addition, multiplication)
- String utilities (greeting generation)
- Mathematical functions (factorial, even number checking)
- Comprehensive test suite
- Well-documented API

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/example-package.git
cd example-package

# Build the package
make build

# Run tests
make test
```

## Usage

```fortran
program example_usage
    use example_package
    
    implicit none
    
    integer :: sum_result, product_result
    character(len=:), allocatable :: greeting
    logical :: is_even_number
    
    ! Basic arithmetic
    sum_result = add_numbers(5, 3)
    print *, "5 + 3 =", sum_result
    
    product_result = multiply_numbers(4, 7)
    print *, "4 * 7 =", product_result
    
    ! String utilities
    greeting = greet_user("World")
    print *, greeting
    
    ! Mathematical functions
    is_even_number = is_even(8)
    print *, "Is 8 even?", is_even_number
    
    print *, "5! =", factorial(5)
    
end program example_usage
```

## API Reference

### Functions

#### `add_numbers(a, b)`
Adds two integers together.

**Parameters:**
- `a` (integer): First number
- `b` (integer): Second number

**Returns:**
- `result` (integer): Sum of a and b

**Example:**
```fortran
integer :: result
result = add_numbers(2, 3)  ! result = 5
```

#### `multiply_numbers(a, b)`
Multiplies two integers together.

**Parameters:**
- `a` (integer): First number
- `b` (integer): Second number

**Returns:**
- `result` (integer): Product of a and b

**Example:**
```fortran
integer :: result
result = multiply_numbers(3, 4)  ! result = 12
```

#### `greet_user(name)`
Generates a greeting message for a user.

**Parameters:**
- `name` (character): User's name

**Returns:**
- `greeting` (character): Greeting message

**Example:**
```fortran
character(len=:), allocatable :: greeting
greeting = greet_user("Alice")
! greeting = "Hello, Alice! Welcome to the example package."
```

#### `is_even(n)`
Checks if a number is even.

**Parameters:**
- `n` (integer): Number to check

**Returns:**
- `result` (logical): True if number is even, false otherwise

**Example:**
```fortran
logical :: result
result = is_even(4)  ! result = .true.
```

#### `factorial(n)`
Calculates the factorial of a number.

**Parameters:**
- `n` (integer): Non-negative integer

**Returns:**
- `result` (integer): Factorial of n

**Example:**
```fortran
integer :: result
result = factorial(5)  ! result = 120
```

**Note:** Raises an error if n is negative.

## Testing

The package includes comprehensive tests using the funit testing framework:

```bash
# Run all tests
make test

# Run specific test
./test_runner --test test_add_numbers
```

## Dependencies

- **stdlib**: Fortran Standard Library (>=1.0.0)
- **funit**: Fortran Unit Testing Framework (for tests)

## Build System

The package uses a simple Makefile for building:

```makefile
# Build the package
make build

# Run tests
make test

# Clean build artifacts
make clean
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Changelog

### Version 1.0.0
- Initial release
- Basic arithmetic functions
- String utilities
- Mathematical functions
- Comprehensive test suite

## Support

- 📖 [Documentation](https://yourusername.github.io/example-package)
- 🐛 [Report Issues](https://github.com/yourusername/example-package/issues)
- 💬 [Discussions](https://github.com/yourusername/example-package/discussions)
