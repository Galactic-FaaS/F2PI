# Getting Started with F2PI

Welcome to F2PI (Fortran² Package Index)! This guide will help you get started with using and contributing to the Fortran² package ecosystem.

## What is F2PI?

F2PI is a GitHub-based package registry and management system for the Fortran² ecosystem. It provides:

- 🔍 **Package Discovery**: Find and explore Fortran² packages
- 📦 **Package Management**: Install and manage dependencies
- 🔄 **Automated CI/CD**: Built-in validation and testing
- 📊 **Analytics**: Package statistics and community metrics
- 🛡️ **Security**: Automated security scanning
- 📚 **Documentation**: Integrated documentation system

## For Package Users

### Installing F2PI CLI

```bash
# Install via npm (recommended)
npm install -g @f2pi/cli

# Or install from source
git clone https://github.com/Fortransquared/F2PI.git
cd F2PI/tools
make install
```

### Basic Usage

```bash
# Search for packages
f2pi search "linear algebra"
f2pi search --category "Mathematics & Statistics"
f2pi search --author "john-doe"

# Install a package
f2pi install package-name
f2pi install package-name@1.2.0

# List installed packages
f2pi list

# Update packages
f2pi update
f2pi update package-name

# Remove a package
f2pi remove package-name
```

### Using Packages in Your Code

```fortran
program my_program
    use package_name
    
    implicit none
    
    ! Use the package functionality
    call some_function()
    
end program my_program
```

## For Package Authors

### Creating Your First Package

1. **Use the Template**:
   ```bash
   # Copy the basic package template
   cp -r templates/basic-package my-awesome-package
   cd my-awesome-package
   ```

2. **Customize the Package**:
   - Edit `f2pi.json` with your package information
   - Add your source code to `src/`
   - Write tests in `tests/`
   - Update `README.md` with documentation

3. **Validate Your Package**:
   ```bash
   # Validate package structure
   f2pi validate .
   
   # Run tests
   make test
   ```

4. **Submit for Review**:
   - Create a pull request to `packages/pending/`
   - Fill out the package submission form
   - Wait for community review

### Package Structure

```
my-package/
├── f2pi.json          # Package metadata
├── README.md          # Documentation
├── LICENSE            # License file
├── src/               # Source code (.f2 files)
│   └── my_package.f2
├── tests/             # Test files
│   └── test_my_package.f2
├── examples/          # Usage examples
│   └── basic_usage.f2
└── Makefile           # Build configuration
```

### Package Metadata (f2pi.json)

```json
{
  "name": "my-awesome-package",
  "version": "1.0.0",
  "description": "A brief description of your package",
  "category": "Mathematics & Statistics",
  "author": "Your Name <your.email@example.com>",
  "license": "MIT",
  "repository_url": "https://github.com/yourusername/my-awesome-package",
  "keywords": ["math", "statistics", "numerical"],
  "dependencies": [
    {
      "name": "stdlib",
      "version": ">=1.0.0"
    }
  ]
}
```

## Package Categories

Choose the most appropriate category for your package:

- **Mathematics & Statistics**: Mathematical functions, statistical analysis
- **Data Processing**: Data manipulation, parsing, formatting
- **Scientific Computing**: Scientific simulations, physics, chemistry
- **Cryptography & Security**: Encryption, hashing, security protocols
- **Database & Storage**: Database connectivity, data persistence
- **Networking & Communication**: Network protocols, HTTP clients
- **Graphics & Visualization**: Graphics rendering, plotting
- **Utilities & Tools**: General utilities, helper functions
- **Testing & Development**: Testing frameworks, development tools
- **Other**: Packages that don't fit other categories

## Development Workflow

### 1. Package Development

```bash
# Create your package directory
mkdir my-package
cd my-package

# Initialize with template
f2pi init

# Develop your package
# Edit src/, tests/, etc.

# Test locally
make test
f2pi validate .
```

### 2. Submission Process

```bash
# Submit for review
f2pi submit

# Or create pull request manually
git add .
git commit -m "Add my-awesome-package"
git push origin main
# Create PR to packages/pending/
```

### 3. Review and Approval

- Automated validation runs on all submissions
- Community members review packages
- Approved packages move to `packages/approved/`
- Package becomes available in registry

## Best Practices

### Code Quality
- Follow Fortran² coding standards
- Use meaningful variable and function names
- Include comprehensive comments
- Write thorough tests

### Documentation
- Clear README with examples
- Document all public APIs
- Include installation instructions
- Provide usage examples

### Testing
- Aim for high test coverage (>80%)
- Test edge cases and error conditions
- Use consistent testing framework
- Include integration tests

### Versioning
- Use semantic versioning (MAJOR.MINOR.PATCH)
- Document breaking changes
- Maintain backward compatibility when possible
- Tag releases properly

## Community Guidelines

### Contributing
- Be respectful and constructive
- Follow the code of conduct
- Help others learn and improve
- Share knowledge and best practices

### Reviewing Packages
- Provide constructive feedback
- Check for security issues
- Verify functionality and tests
- Ensure documentation quality

### Getting Help
- Check existing documentation
- Ask questions in GitHub Discussions
- Review example packages
- Contact maintainers

## Advanced Features

### CI/CD Integration

F2PI automatically provides:
- Package validation
- Security scanning
- Test execution
- Documentation generation
- Registry updates

### Dependency Management

```json
{
  "dependencies": [
    {
      "name": "package-name",
      "version": ">=1.0.0",
      "optional": false
    }
  ]
}
```

### Custom Build Systems

Support for various build systems:
- Make
- CMake
- Meson
- Custom scripts

## Troubleshooting

### Common Issues

**Package validation fails**:
- Check file structure and naming
- Verify f2pi.json format
- Ensure all required files exist

**Tests fail**:
- Check test framework setup
- Verify test dependencies
- Review test logic

**Build errors**:
- Check compiler compatibility
- Verify dependencies
- Review build configuration

### Getting Support

- 📖 [Documentation](docs/)
- 🐛 [Report Issues](https://github.com/Fortransquared/F2PI/issues)
- 💬 [Discussions](https://github.com/Fortransquared/F2PI/discussions)
- 📧 [Contact](mailto:support@fortransquared.org)

## Next Steps

1. **Explore**: Browse existing packages in the registry
2. **Learn**: Study example packages and documentation
3. **Contribute**: Submit your first package
4. **Engage**: Join the community discussions
5. **Improve**: Help make F2PI better for everyone

Welcome to the Fortran² package ecosystem! 🚀
