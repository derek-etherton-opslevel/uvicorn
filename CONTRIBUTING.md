# Contributing to Uvicorn

Thank you for your interest in contributing to Uvicorn! We welcome contributions from the community.

## About Uvicorn

Uvicorn is a lightning-fast ASGI (Asynchronous Server Gateway Interface) web server implementation for Python. It is built on top of `uvloop` and `httptools`, providing high-performance async capabilities for Python web applications and frameworks.

### Key Features

- **ASGI 3 Support**: Implements the ASGI specification for async Python web applications
- **HTTP/1.1 and WebSockets**: Full support for modern web protocols
- **High Performance**: Built on uvloop and httptools for maximum speed
- **Production Ready**: Used by major Python async frameworks like FastAPI and Starlette
- **Flexible Configuration**: Extensive command-line options and programmatic API
- **Process Management**: Includes Gunicorn worker class for production deployments

## Getting Started

### Prerequisites

- Python 3.8 or higher
- Git
- A Unix-like environment (Linux, macOS, WSL on Windows)

### Setting Up Your Development Environment

1. **Fork and Clone the Repository**

   ```bash
   git clone https://github.com/YOUR-USERNAME/uvicorn.git
   cd uvicorn
   ```

2. **Install Dependencies**

   Run the installation script which will create a virtual environment and install all required dependencies:

   ```bash
   ./scripts/install
   ```

   This script will:
   - Create a `venv` virtual environment in the project directory
   - Install all dependencies from `requirements.txt`
   - Install uvicorn in editable mode with the `[standard]` extras

   If you need to use a specific Python version:

   ```bash
   ./scripts/install -p python3.11
   ```

3. **Activate the Virtual Environment**

   ```bash
   source venv/bin/activate  # On Unix/macOS
   # or
   venv\Scripts\activate  # On Windows
   ```

### Running Uvicorn Locally

After installation, you can test the server with a simple example:

1. **Create a test application** (`example.py`):

   ```python
   async def app(scope, receive, send):
       assert scope['type'] == 'http'

       await send({
           'type': 'http.response.start',
           'status': 200,
           'headers': [
               (b'content-type', b'text/plain'),
           ],
       })
       await send({
           'type': 'http.response.body',
           'body': b'Hello, world!',
       })
   ```

2. **Run the server**:

   ```bash
   uvicorn example:app
   ```

   Or using the development reload mode:

   ```bash
   uvicorn example:app --reload
   ```

3. **Test it**:

   Open your browser to `http://127.0.0.1:8000` or use curl:

   ```bash
   curl http://127.0.0.1:8000
   ```

## Development Workflow

### Code Style and Linting

We use `ruff` for code formatting and linting, and `mypy` for type checking.

**Check code quality** (runs all checks):

```bash
./scripts/check
```

This will:
- Verify version consistency with `./scripts/sync-version`
- Check code formatting with `ruff format`
- Run type checks with `mypy`
- Run linting with `ruff check`
- Verify CLI usage documentation is up to date

**Auto-fix formatting and linting issues**:

```bash
./scripts/lint
```

This will:
- Format code with `ruff format`
- Auto-fix linting issues with `ruff --fix`
- Update CLI usage documentation

### Running Tests

**Run the full test suite**:

```bash
./scripts/test
```

This will:
- Run all tests with `pytest`
- Generate a coverage report
- Enforce minimum coverage requirements (98.35%)

**Run specific tests**:

```bash
./scripts/test tests/test_config.py
./scripts/test tests/test_config.py::test_host_port
./scripts/test -v  # Verbose mode
./scripts/test -k "test_pattern"  # Run tests matching pattern
```

**Check test coverage**:

```bash
./scripts/coverage
```

### Building Documentation

The documentation is built using MkDocs with the Material theme.

**Serve documentation locally**:

```bash
./scripts/docs serve
```

Then open your browser to `http://127.0.0.1:8000` to view the docs.

**Build documentation**:

```bash
./scripts/docs build
```

### Building the Package

To build the distribution packages:

```bash
./scripts/build
```

This creates wheel and source distributions in the `dist/` directory.

## Making Changes

### Creating a Pull Request

1. **Create a new branch** for your feature or bugfix:

   ```bash
   git checkout -b feature/my-new-feature
   # or
   git checkout -b fix/issue-description
   ```

2. **Make your changes** following the code style guidelines

3. **Add tests** for any new functionality:
   - Tests should be added in the `tests/` directory
   - Maintain or improve the test coverage (minimum 98.35%)
   - Run the test suite to ensure everything passes

4. **Update documentation** if needed:
   - Update relevant `.md` files in the `docs/` directory
   - Update docstrings for changed functions/classes
   - If adding CLI options, run `./scripts/lint` to update usage docs

5. **Run all checks**:

   ```bash
   ./scripts/check
   ./scripts/test
   ```

6. **Commit your changes**:

   ```bash
   git add .
   git commit -m "Add feature: brief description"
   ```

   Write clear, descriptive commit messages explaining what changed and why.

7. **Push to your fork**:

   ```bash
   git push origin feature/my-new-feature
   ```

8. **Open a Pull Request** on GitHub:
   - Provide a clear description of the changes
   - Reference any related issues
   - Ensure all CI checks pass

### Pull Request Guidelines

Before submitting a pull request, please ensure:

- [ ] You have discussed the change in an issue first (except for typos)
- [ ] Tests have been added for any new functionality
- [ ] All tests pass locally (`./scripts/test`)
- [ ] Code follows the project's style guidelines (`./scripts/check`)
- [ ] Documentation has been updated if needed
- [ ] The change is atomic (focused on a single concern)
- [ ] Commit messages are clear and descriptive

## Project Structure

```
uvicorn/
├── uvicorn/              # Main package source code
│   ├── __init__.py       # Package initialization and version
│   ├── main.py           # CLI entry point
│   ├── config.py         # Configuration management
│   ├── server.py         # Server implementation
│   ├── protocols/        # HTTP and WebSocket protocol implementations
│   ├── lifespan/         # ASGI lifespan handling
│   ├── loops/            # Event loop implementations (asyncio, uvloop)
│   ├── middleware/       # Built-in middleware
│   └── supervisors/      # Process supervision (reload, multiprocess)
├── tests/                # Test suite
│   ├── test_*.py         # Test modules
│   ├── protocols/        # Protocol-specific tests
│   └── supervisors/      # Supervisor-specific tests
├── docs/                 # Documentation source files
├── scripts/              # Development utility scripts
├── pyproject.toml        # Project configuration and dependencies
├── requirements.txt      # Development dependencies
└── mkdocs.yml            # Documentation configuration
```

## Reporting Issues

If you find a bug or have a feature request:

1. **Check existing issues** to avoid duplicates
2. **Create a new issue** with:
   - Clear, descriptive title
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Environment details (OS, Python version, uvicorn version)
   - Minimal code example if applicable

## Code of Conduct

Please be respectful and considerate in all interactions. We aim to maintain a welcoming, inclusive community.

## Development Tips

### Virtual Environment Management

If you need to recreate your virtual environment:

```bash
rm -rf venv
./scripts/install
```

### Testing Specific Python Versions

To test with a specific Python version:

```bash
./scripts/install -p python3.9
source venv/bin/activate
./scripts/test
```

### Debugging Tests

To drop into a debugger on test failures:

```bash
./scripts/test --pdb
```

To see print statements during tests:

```bash
./scripts/test -s
```

### Working with Protocol Implementations

Uvicorn supports multiple protocol implementations:

- **HTTP**: `h11` (pure Python) or `httptools` (fast C-based)
- **WebSockets**: `websockets` or `wsproto`
- **Event Loop**: `asyncio` (built-in) or `uvloop` (fast C-based)

When making changes to protocol handling, test with different implementations:

```bash
uvicorn example:app --http h11
uvicorn example:app --http httptools
uvicorn example:app --ws websockets
uvicorn example:app --ws wsproto
```

### Understanding ASGI

Uvicorn implements the ASGI specification. Familiarize yourself with:

- [ASGI Specification](https://asgi.readthedocs.io/)
- [ASGI HTTP Protocol](https://asgi.readthedocs.io/en/latest/specs/www.html)
- [ASGI WebSocket Protocol](https://asgi.readthedocs.io/en/latest/specs/www.html#websocket)
- [ASGI Lifespan Protocol](https://asgi.readthedocs.io/en/latest/specs/lifespan.html)

## Release Process

(For maintainers)

Releases are managed through the `./scripts/publish` script and follow semantic versioning.

## Additional Resources

- **Documentation**: https://www.uvicorn.org
- **GitHub Repository**: https://github.com/encode/uvicorn
- **Issue Tracker**: https://github.com/encode/uvicorn/issues
- **PyPI Package**: https://pypi.org/project/uvicorn/
- **ASGI Specification**: https://asgi.readthedocs.io/

## Questions?

If you have questions about contributing, feel free to:

- Open an issue for discussion
- Check existing issues and pull requests
- Review the documentation at https://www.uvicorn.org

---

Thank you for contributing to Uvicorn! Your efforts help make Python's async web ecosystem better for everyone. 🦄
