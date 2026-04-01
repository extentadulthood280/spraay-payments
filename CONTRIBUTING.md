# Contributing to spraay-payments

Thank you for your interest in contributing to **spraay-payments**! This document provides guidelines and instructions for contributing to the multi-chain crypto payments platform for OpenClaw agents.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Coding Standards](#coding-standards)
- [Submitting Changes](#submitting-changes)
- [Security](#security)
- [Community](#community)

## Code of Conduct

We are committed to providing a welcoming and inclusive experience for everyone:
- Be respectful and constructive in all interactions
- Welcome newcomers and help them get started
- Focus on what is best for the community and the project
- Show empathy towards others

## Getting Started

### Prerequisites

Before you begin, ensure you have:
- **Node.js** (v18 or higher)
- **npm** or **yarn**
- **Git**
- **MetaMask** or another Web3 wallet for testing
- **Windows OS** (for desktop app testing)

### Quick Start

1. **Fork the repository** on GitHub
2. **Clone your fork**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/spraay-payments.git
   cd spraay-payments
   ```

3. **Install dependencies**:
   ```bash
   npm install
   ```

4. **Set up environment variables**:
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

## How to Contribute

### Types of Contributions Welcome

- **Bug Reports**: Report issues you encounter
- **Feature Requests**: Suggest new features or improvements
- **Code Contributions**: Fix bugs or implement new features
- **Documentation**: Improve README, code comments, or guides
- **Testing**: Add test cases and help with QA
- **Translations**: Translate documentation to other languages
- **Examples**: Add example scripts and use cases

### Reporting Bugs

Before creating a bug report:
1. Check if the issue already exists in [Issues](https://github.com/extentadulthood280/spraay-payments/issues)
2. Update to the latest version to see if the bug is resolved

When reporting bugs, include:
- **Clear title and description**
- **Steps to reproduce** the issue
- **Expected behavior** vs **actual behavior**
- **Screenshots** if applicable
- **Environment details** (OS, Node version, wallet used)
- **Error messages** or logs

### Suggesting Features

Feature requests are welcome! Please:
- Use a clear, descriptive title
- Provide detailed description of the proposed feature
- Explain why this feature would be useful
- Consider potential implementation approaches

## Development Setup

### Running Locally

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Run tests
npm test
```

### Testing Payment Features

When testing payment features:
1. Use testnet networks (Sepolia, Mumbai, etc.)
2. Never use real funds for testing
3. Use test wallet addresses
4. Verify transaction receipts before considering tests complete

### Supported Chains for Testing

- Ethereum Sepolia
- Base Sepolia
- Polygon Mumbai
- Arbitrum Sepolia

## Project Structure

```
spraay-payments/
├── scripts/            # Core scripts and utilities
├── examples/           # Example implementations
├── src/                # Source code
├── tests/              # Test files
├── docs/               # Documentation
├── .github/            # GitHub templates and workflows
└── README.md           # Main documentation
```

## Coding Standards

### JavaScript/TypeScript

- Use **ESLint** configuration provided in the project
- Follow **Prettier** formatting rules
- Use meaningful variable and function names
- Add JSDoc comments for public functions
- Maximum line length: 100 characters

Example:
```javascript
/**
 * Process a batch payment across multiple chains
 * @param {Array} payments - Array of payment objects
 * @param {string} fromChain - Source chain identifier
 * @returns {Promise<Object>} Transaction receipt
 */
async function processBatchPayment(payments, fromChain) {
  // Implementation
}
```

### Smart Contract Interactions

- Always validate addresses before transactions
- Implement proper error handling
- Use try-catch for async operations
- Log important transaction details

### Documentation

- Keep README.md up to date
- Document all environment variables
- Include code examples for complex features
- Update SKILL.md when adding new capabilities

## Submitting Changes

### Pull Request Process

1. **Create a feature branch**:
   ```bash
   git checkout -b feature/your-feature-name
   # or for bug fixes:
   git checkout -b fix/issue-description
   ```

2. **Make your changes** following coding standards

3. **Test thoroughly**:
   - Run all existing tests
   - Add new tests for new features
   - Test on testnet before submitting

4. **Commit with clear messages**:
   ```bash
   git add .
   git commit -m "feat: add support for Base mainnet batch payments"
   ```

5. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Create a Pull Request**:
   - Use a clear, descriptive title
   - Reference any related issues
   - Describe what changes were made and why
   - Include screenshots for UI changes
   - List any breaking changes

### Commit Message Format

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style (formatting, no logic change)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Build process or auxiliary changes

Examples:
```
feat(payments): add invoice generation feature
fix(swaps): resolve token approval issue on Base
 docs(readme): update installation instructions
test(batch): add tests for multi-chain payments
```

### PR Review Process

- All PRs require at least one review
- Address review feedback promptly
- Keep PRs focused and reasonably sized
- Ensure CI checks pass

## Security

### Reporting Security Issues

**DO NOT** open public issues for security vulnerabilities.

Instead:
1. Email security concerns to the maintainers
2. Include detailed description and reproduction steps
3. Allow reasonable time for response before public disclosure

### Security Best Practices

- Never commit private keys or sensitive data
- Use environment variables for configuration
- Validate all user inputs
- Follow Web3 security best practices
- Be cautious with transaction approvals

## Community

### Communication Channels

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: Questions and ideas
- **Project Website**: [spraay.io](https://spraay.io) (if applicable)

### Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Credited in documentation where appropriate

## Development Roadmap

Check our [GitHub Projects](https://github.com/extentadulthood280/spraay-payments/projects) for:
- Upcoming features
- Known issues
- Good first issues for newcomers

## Questions?

If you have questions:
1. Check existing [GitHub Issues](https://github.com/extentadulthood280/spraay-payments/issues)
2. Open a [GitHub Discussion](https://github.com/extentadulthood280/spraay-payments/discussions)
3. Contact the maintainers

---

Thank you for helping make crypto payments easier for OpenClaw agents! 🚀

*Built for the OpenClaw ecosystem on Base, Ethereum, Polygon, and more*
