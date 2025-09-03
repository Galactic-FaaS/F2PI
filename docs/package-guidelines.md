# F2PI Package Guidelines

This document provides comprehensive guidelines for creating and submitting packages to the F2PI (Fortran² Package Index) registry.

## Package Structure

Every F2PI package must follow this directory structure:

```
package-name/
├── f2pi.json          # Package metadata (required)
├── README.md          # Package documentation (required)
├── LICENSE            # License file (required)
├── src/               # Source code directory (required)
│   ├── package-name.f2
│   └── ...
├── tests/             # Test files (required)
│   ├── test_package-name.f2
│   └── ...
├── examples/          # Usage examples (recommended)
│   ├── basic_usage.f2
│   └── ...
├── docs/              # Additional documentation (optional)
│   ├── api-reference.md
│   └── ...
└── Makefile           # Build configuration (recommended)
```

## Package Metadata (f2pi.json)

The `f2pi.json` file contains essential package information:

```json
{
  "name": "package-name",
  "version": "1.0.0",
  "description": "Brief description of the package functionality",
  "category": "Mathematics & Statistics",
  "author": "Author Name <email@example.com>",
  "license": "MIT",
  "repository_url": "https://github.com/username/package-name",
  "documentation_url": "https://username.github.io/package-name",
  "keywords": ["math", "statistics", "numerical"],
  "dependencies": [
    {
      "name": "dependency-name",
      "version": ">=1.0.0"
    }
  ],
  "fortran_version": ">=2023",
  "platforms": ["linux", "windows", "macos"],
  "build_system": "make",
  "test_framework": "funit"
}
```

### Required Fields

- **name**: Package name (lowercase, hyphens only, unique)
- **version**: Semantic version (e.g., "1.0.0")
- **description**: Brief description (max 200 characters)
- **category**: One of the predefined categories
- **author**: Author name and email
- **license**: License identifier (MIT, Apache-2.0, GPL-3.0, etc.)

### Optional Fields

- **repository_url**: GitHub repository URL
- **documentation_url**: Documentation website
- **keywords**: Array of search keywords
- **dependencies**: Array of dependency objects
- **fortran_version**: Minimum Fortran² version required
- **platforms**: Supported operating systems
- **build_system**: Build system used (make, cmake, etc.)
- **test_framework**: Testing framework used

## Package Categories

Choose the most appropriate category for your package:

- **Mathematics & Statistics**: Mathematical functions, statistical analysis, numerical methods
- **Data Processing**: Data manipulation, parsing, formatting, transformation
- **Scientific Computing**: Scientific simulations, physics, chemistry, engineering
- **Cryptography & Security**: Encryption, hashing, security protocols, authentication
- **Database & Storage**: Database connectivity, data persistence, file I/O
- **Networking & Communication**: Network protocols, HTTP clients, communication libraries
- **Graphics & Visualization**: Graphics rendering, plotting, visualization tools
- **Utilities & Tools**: General utilities, helper functions, development tools
- **Testing & Development**: Testing frameworks, development tools, debugging utilities
- **Other**: Packages that don't fit into other categories

## Naming Conventions

### Package Names
- Use lowercase letters only
- Use hyphens (-) to separate words
- Must be unique across the registry
- Should be descriptive but concise
- Examples: `linear-algebra`, `json-parser`, `http-client`

### Source Files
- Use lowercase with underscores: `package_name.f2`
- Main module file should match package name: `package_name.f2`
- Test files should end with `_test.f2`: `package_name_test.f2`
- Example files should be descriptive: `basic_usage.f2`

### Module Names
- Use PascalCase: `PackageName`
- Should match the package name structure
- Example: package `linear-algebra` → module `LinearAlgebra`

## Source Code Requirements

### File Extensions
- All source files must use `.f2` extension
- No `.f90`, `.f95`, or other Fortran extensions allowed

### Code Style
- Follow Fortran² coding standards
- Use consistent indentation (2 or 4 spaces)
- Include comprehensive comments
- Use meaningful variable and function names

### Module Structure
```fortran
module PackageName
    use stdlib_strings
    use stdlib_io
    ! Other dependencies
    
    implicit none
    
    ! Public interface
    public :: function1, function2, type1
    
    ! Private implementation
    private
    
    contains
    
    function function1() result(result)
        ! Implementation
    end function function1
    
end module PackageName
```

## Testing Requirements

### Test Structure
- All packages must include comprehensive tests
- Test files should be in the `tests/` directory
- Use a consistent testing framework (recommended: funit)
- Aim for high test coverage (>80%)

### Test Naming
- Test files: `package_name_test.f2`
- Test modules: `PackageNameTest`
- Test functions: `test_function_name`

### Example Test
```fortran
module PackageNameTest
    use funit
    use PackageName
    
    implicit none
    
    contains
    
    @test
    subroutine test_basic_functionality()
        integer :: result
        
        result = basic_function(5)
        @assertEqual(10, result)
    end subroutine test_basic_functionality
    
end module PackageNameTest
```

## Documentation Requirements

### README.md
Must include:
- Package description and purpose
- Installation instructions
- Basic usage examples
- API reference (or link to detailed docs)
- Contributing guidelines
- License information

### Code Documentation
- Document all public functions and types
- Include parameter descriptions
- Provide usage examples in comments
- Document any side effects or limitations

## Build System

### Makefile (Recommended)
```makefile
# Package Makefile
FC = f2direct
FFLAGS = -O2 -Wall
SRCDIR = src
TESTDIR = tests
BUILDDIR = build

# Build the package
build: $(BUILDDIR)/libpackage.a

$(BUILDDIR)/libpackage.a: $(SRCDIR)/*.f2
	@mkdir -p $(BUILDDIR)
	$(FC) $(FFLAGS) -c $(SRCDIR)/*.f2 -o $(BUILDDIR)/
	ar rcs $@ $(BUILDDIR)/*.o

# Run tests
test: build
	$(FC) $(FFLAGS) -I$(SRCDIR) $(TESTDIR)/*.f2 -o test_runner
	./test_runner

# Clean build artifacts
clean:
	rm -rf $(BUILDDIR) test_runner

.PHONY: build test clean
```

## License Requirements

- Every package must include a LICENSE file
- Use a standard open-source license (MIT, Apache-2.0, GPL-3.0, etc.)
- License must be compatible with Fortran² ecosystem
- Include license information in f2pi.json

## Versioning

- Use semantic versioning (MAJOR.MINOR.PATCH)
- MAJOR: Breaking changes
- MINOR: New features, backward compatible
- PATCH: Bug fixes, backward compatible
- Examples: 1.0.0, 1.1.0, 1.1.1, 2.0.0

## Dependencies

### Declaring Dependencies
- List all required dependencies in f2pi.json
- Use version constraints (>=, ==, ~>)
- Prefer stable, well-maintained packages
- Minimize dependencies when possible

### Example Dependencies
```json
"dependencies": [
    {
        "name": "stdlib",
        "version": ">=1.0.0"
    },
    {
        "name": "json-fortran",
        "version": "~>8.0.0"
    }
]
```

## Quality Standards

### Code Quality
- No compiler warnings
- Passes all static analysis tools
- Follows Fortran² best practices
- Well-documented and commented

### Performance
- Reasonable performance for intended use case
- No obvious performance bottlenecks
- Memory usage should be appropriate

### Security
- No known security vulnerabilities
- Safe handling of user input
- Proper error handling

## Submission Process

1. **Prepare Package**: Ensure your package meets all requirements
2. **Create Pull Request**: Submit package to `packages/pending/`
3. **Automated Validation**: CI system validates package structure and tests
4. **Community Review**: Community members review the package
5. **Approval**: Package is moved to `packages/approved/`
6. **Publication**: Package appears in registry and becomes available

## Review Criteria

Packages are evaluated on:
- **Functionality**: Does it work as described?
- **Code Quality**: Is the code well-written and documented?
- **Testing**: Are there adequate tests?
- **Documentation**: Is the documentation clear and complete?
- **Usefulness**: Does it provide value to the community?
- **Maintenance**: Is it likely to be maintained?

## Getting Help

- Check existing packages for examples
- Ask questions in GitHub Discussions
- Review rejected packages for common issues
- Contact maintainers for guidance

## Best Practices

1. **Start Small**: Begin with simple, focused functionality
2. **Iterate**: Improve based on feedback and usage
3. **Document**: Comprehensive documentation is crucial
4. **Test**: Thorough testing prevents issues
5. **Maintain**: Keep packages updated and maintained
6. **Community**: Engage with the Fortran² community

Remember: The goal is to create a high-quality, useful package that benefits the entire Fortran² ecosystem!
