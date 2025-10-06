# Contributing to Uvicorn

Thank you for considering contributing to Uvicorn! 💚

This document provides guidelines and instructions for contributing to the project.

## About Uvicorn

Uvicorn is a lightning-fast ASGI (Asynchronous Server Gateway Interface) web server implementation for Python.
It is designed to be a minimal, low-level server/application interface for async frameworks.

**Key Features:**
- HTTP/1.1 and WebSockets support
- High performance with optional Cython-based dependencies (uvloop, httptools)
- Compatible with ASGI frameworks like FastAPI, Starlette, Django Channels, and more
- Production-ready with Gunicorn integration
- Auto-reload for development

## Getting Started

### Prerequisites

- Python 3.8 or higher
- Git
- (Optional) A virtual environment manager

### Setting Up Your Development Environment

1. **Fork and clone the repository:**

   ```bash
   git clone https://github.com/<your-username>/uvicorn.git
   cd uvicorn
   ```

2. **Install dependencies:**

   Uvicorn provides a convenient installation script that sets up a virtual environment and installs all required dependencies:

   ```bash
   ./scripts/install
   ```

   If you want to use a specific Python version:

   ```bash
   ./scripts/install -p python3.11
   ```

   This script will:
   - Create a virtual environment in the `venv` directory
   - Install all dependencies from `requirements.txt`
   - Install uvicorn in editable mode with the `[standard]` extras

3. **Activate the virtual environment:**

   ```bash
   source venv/bin/activate  # On Unix/macOS
   # or
   venv\Scripts\activate  # On Windows
   ```

### Running Uvicorn Locally

After installation, you can test Uvicorn with a simple application:

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

2. **Run the server:**

   ```bash
   uvicorn example:app
   ```

   Or with auto-reload for development:

   ```bash
   uvicorn example:app --reload
   ```

## Development Workflow

### Code Quality and Linting

Uvicorn uses several tools to maintain code quality:

- **ruff**: For code formatting and linting
- **mypy**: For type checking

**Run all checks:**

```bash
./scripts/check
```

This script will:
- Synchronize version information across files
- Check code formatting with ruff
- Run type checking with mypy
- Verify linting rules
- Validate CLI usage documentation

**Auto-fix formatting and linting issues:**

```bash
./scripts/lint
```

This will automatically format code and fix linting issues where possible.

### Running Tests

Uvicorn uses pytest for testing with extensive coverage requirements (>98%).

**Run all tests:**

```bash
./scripts/test
```

**Run specific tests:**

```bash
./scripts/test tests/test_config.py
./scripts/test tests/test_config.py::test_bind_unix_socket
```

**Run tests with coverage report:**

```bash
./scripts/test
./scripts/coverage
```

The test script will:
- Run the full test suite
- Generate a coverage report
- Fail if coverage is below the threshold (98.35%)

### Building Documentation

Uvicorn uses MkDocs for documentation.

**Serve documentation locally:**

```bash
./scripts/docs serve
```

This will start a local documentation server at `http://127.0.0.1:8000`.

**Build documentation:**

```bash
./scripts/docs build
```

### Building the Package

To build the distribution packages:

```bash
./scripts/build
```

This creates both source distribution and wheel files in the `dist/` directory.

## Making Changes

### Before You Start

- **Check existing issues:** Search for existing issues or discussions related to your change.
- **Discuss significant changes:** For major features or changes, please open an issue first to discuss your proposal.
- **One change per PR:** Try to keep pull requests focused on a single change or feature.

### Development Process

1. **Create a new branch:**

   ```bash
   git checkout -b feature/my-new-feature
   # or
   git checkout -b fix/my-bug-fix
   ```

2. **Make your changes:**
   - Write code following the existing style
   - Add or update tests as needed
   - Update documentation if applicable

3. **Run checks locally:**

   ```bash
   ./scripts/check
   ./scripts/test
   ```

4. **Commit your changes:**

   ```bash
   git add .
   git commit -m "Description of your changes"
   ```

   Use clear, descriptive commit messages.

5. **Push to your fork:**

   ```bash
   git push origin feature/my-new-feature
   ```

6. **Open a Pull Request:**
   - Go to the [Uvicorn repository](https://github.com/encode/uvicorn)
   - Click "New Pull Request"
   - Select your fork and branch
   - Fill in the PR template with details about your changes

### Pull Request Guidelines

When submitting a pull request:

- [ ] I understand that this PR may be closed in case there was no previous discussion. (This doesn't apply to typos!)
- [ ] I've added a test for each change that was introduced, and I tried as much as possible to make a single atomic change.
- [ ] I've updated the documentation accordingly.
- [ ] All tests pass locally (`./scripts/test`)
- [ ] Code passes linting checks (`./scripts/check`)
- [ ] Coverage remains above the threshold

## Code Style Guidelines

### Python Code Style

- Follow PEP 8 with a line length of 120 characters
- Use type hints for function signatures
- Write descriptive variable and function names
- Add docstrings for public APIs

### Testing Guidelines

- Write tests for all new features and bug fixes
- Aim for high test coverage (>98%)
- Use descriptive test names that explain what is being tested
- Group related tests in classes when appropriate

### Documentation Guidelines

- Update documentation for user-facing changes
- Use clear, concise language
- Include code examples where appropriate
- Keep the README and docs in sync

## Project Structure

```
uvicorn/
├── uvicorn/              # Main package source code
│   ├── __init__.py      # Package initialization and version
│   ├── main.py          # CLI entry point
│   ├── config.py        # Configuration handling
│   ├── server.py        # Server implementation
│   ├── protocols/       # HTTP and WebSocket protocol implementations
│   ├── loops/           # Event loop implementations (asyncio, uvloop)
│   ├── lifespan/        # ASGI lifespan handling
│   ├── middleware/      # Built-in middleware
│   └── supervisors/     # Process supervision (multiprocessing)
├── tests/               # Test suite
├── docs/                # Documentation source files
├── scripts/             # Development and build scripts
└── pyproject.toml       # Project metadata and configuration
```

## Getting Help

- **Documentation:** [https://www.uvicorn.org](https://www.uvicorn.org)
- **Issues:** [GitHub Issues](https://github.com/encode/uvicorn/issues)
- **Discussions:** [GitHub Discussions](https://github.com/encode/uvicorn/discussions)

## Code of Conduct

Please be respectful and considerate in all interactions. This project follows the general principles
of open source collaboration and expects contributors to maintain a welcoming and inclusive environment.

## License

By contributing to Uvicorn, you agree that your contributions will be licensed under the [BSD 3-Clause License](LICENSE.md).

---

Thank you for contributing to Uvicorn! Your efforts help make this project better for everyone. 🦄
