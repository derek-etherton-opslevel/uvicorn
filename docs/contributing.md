# Contributing

For detailed information about contributing to Uvicorn, please see the [CONTRIBUTING.md](https://github.com/encode/uvicorn/blob/master/CONTRIBUTING.md) file in the repository root.

## Quick Links

- **GitHub Repository**: [https://github.com/encode/uvicorn](https://github.com/encode/uvicorn)
- **Issue Tracker**: [https://github.com/encode/uvicorn/issues](https://github.com/encode/uvicorn/issues)
- **Pull Requests**: [https://github.com/encode/uvicorn/pulls](https://github.com/encode/uvicorn/pulls)

## Getting Started

To contribute to Uvicorn:

1. Fork the repository on GitHub
2. Clone your fork locally
3. Install development dependencies with `./scripts/install`
4. Make your changes
5. Run tests with `./scripts/test`
6. Run linting checks with `./scripts/check`
7. Submit a pull request

## Development Commands

### Setup

```bash
# Clone the repository
git clone https://github.com/YOUR-USERNAME/uvicorn.git
cd uvicorn

# Install dependencies
./scripts/install
```

### Testing

```bash
# Run all tests
./scripts/test

# Run specific tests
./scripts/test tests/test_config.py
```

### Code Quality

```bash
# Check code quality
./scripts/check

# Auto-fix formatting and linting
./scripts/lint
```

### Documentation

```bash
# Serve documentation locally
./scripts/docs serve

# Build documentation
./scripts/docs build
```

## Guidelines

Before submitting a pull request:

- Discuss the change in an issue first (except for typos)
- Add tests for new functionality
- Ensure all tests pass
- Follow the code style guidelines
- Update documentation as needed
- Keep changes focused and atomic

## Code of Conduct

Please be respectful and considerate in all interactions. We aim to maintain a welcoming, inclusive community.

---

For complete contribution guidelines, see [CONTRIBUTING.md](https://github.com/encode/uvicorn/blob/master/CONTRIBUTING.md).
