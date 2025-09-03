# Example Package Makefile
# This is a template Makefile for F2PI packages

# Compiler and flags
FC = f2direct
FFLAGS = -O2 -Wall -Wextra
DEBUG_FLAGS = -g -O0 -Wall -Wextra -fcheck=all

# Directories
SRCDIR = src
TESTDIR = tests
BUILDDIR = build
LIBDIR = lib

# Source files
SOURCES = $(wildcard $(SRCDIR)/*.f2)
TEST_SOURCES = $(wildcard $(TESTDIR)/*.f2)
OBJECTS = $(SOURCES:$(SRCDIR)/%.f2=$(BUILDDIR)/%.o)
TEST_OBJECTS = $(TEST_SOURCES:$(TESTDIR)/%.f2=$(BUILDDIR)/%.o)

# Library name
LIBRARY = $(LIBDIR)/libexample_package.a

# Test executable
TEST_EXECUTABLE = test_runner

# Default target
.PHONY: all
all: build

# Build the library
.PHONY: build
build: $(LIBRARY)

$(LIBRARY): $(OBJECTS) | $(LIBDIR)
	ar rcs $@ $^
	@echo "Library built: $@"

# Compile source files
$(BUILDDIR)/%.o: $(SRCDIR)/%.f2 | $(BUILDDIR)
	$(FC) $(FFLAGS) -c $< -o $@

# Build tests
.PHONY: test
test: $(TEST_EXECUTABLE)
	@echo "Running tests..."
	./$(TEST_EXECUTABLE)

$(TEST_EXECUTABLE): $(OBJECTS) $(TEST_OBJECTS) | $(BUILDDIR)
	$(FC) $(FFLAGS) -I$(SRCDIR) $^ -o $@

# Compile test files
$(BUILDDIR)/%.o: $(TESTDIR)/%.f2 | $(BUILDDIR)
	$(FC) $(FFLAGS) -I$(SRCDIR) -c $< -o $@

# Debug build
.PHONY: debug
debug: FFLAGS = $(DEBUG_FLAGS)
debug: clean build test

# Install the package
.PHONY: install
install: $(LIBRARY)
	@echo "Installing package..."
	@mkdir -p /usr/local/lib
	@mkdir -p /usr/local/include
	cp $(LIBRARY) /usr/local/lib/
	cp $(SRCDIR)/*.f2 /usr/local/include/
	@echo "Package installed successfully"

# Uninstall the package
.PHONY: uninstall
uninstall:
	@echo "Uninstalling package..."
	rm -f /usr/local/lib/libexample_package.a
	rm -f /usr/local/include/example_package.f2
	@echo "Package uninstalled successfully"

# Create directories
$(BUILDDIR):
	mkdir -p $(BUILDDIR)

$(LIBDIR):
	mkdir -p $(LIBDIR)

# Clean build artifacts
.PHONY: clean
clean:
	rm -rf $(BUILDDIR) $(LIBDIR) $(TEST_EXECUTABLE)
	@echo "Build artifacts cleaned"

# Format code
.PHONY: format
format:
	@echo "Formatting source code..."
	# Add code formatting commands here if available

# Lint code
.PHONY: lint
lint:
	@echo "Linting source code..."
	# Add linting commands here if available

# Generate documentation
.PHONY: docs
docs:
	@echo "Generating documentation..."
	# Add documentation generation commands here if available

# Package for distribution
.PHONY: package
package: clean build test
	@echo "Creating package archive..."
	tar -czf example-package-1.0.0.tar.gz \
		--exclude='.git' \
		--exclude='$(BUILDDIR)' \
		--exclude='$(LIBDIR)' \
		--exclude='$(TEST_EXECUTABLE)' \
		.
	@echo "Package created: example-package-1.0.0.tar.gz"

# Show help
.PHONY: help
help:
	@echo "Available targets:"
	@echo "  build     - Build the library"
	@echo "  test      - Build and run tests"
	@echo "  debug     - Build with debug flags"
	@echo "  install   - Install the package system-wide"
	@echo "  uninstall - Remove the package from system"
	@echo "  clean     - Remove build artifacts"
	@echo "  format    - Format source code"
	@echo "  lint      - Lint source code"
	@echo "  docs      - Generate documentation"
	@echo "  package   - Create distribution package"
	@echo "  help      - Show this help message"

# Dependencies
$(OBJECTS): | $(BUILDDIR)
$(TEST_OBJECTS): | $(BUILDDIR)
