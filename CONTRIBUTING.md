# Contributing to spraay-payments 💧

Thank you for your interest in contributing to spraay-payments! This document provides guidelines and instructions for contributing to our multi-chain crypto payment protocol.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Contributing Workflow](#contributing-workflow)
- [Coding Standards](#coding-standards)
- [Testing](#testing)
- [Security](#security)
- [Community](#community)

## Code of Conduct

This project adheres to a code of conduct. By participating, you are expected to uphold this code:

- Be respectful and inclusive
- Welcome newcomers
- Focus on constructive feedback
- Respect different viewpoints and experiences

## Getting Started

### Prerequisites

- **Node.js** (v18 or higher)
- **npm** or **yarn**
- **Git**
- **curl** and **jq** (for testing API endpoints)
- A crypto wallet (for testing x402 payments)
- Familiarity with:
  - x402 payment protocol
  - Multi-chain crypto transactions
  - REST APIs

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
4. **Set up environment**:
   ```bash
   export SPRAAY_GATEWAY_URL="https://gateway.spraay.app"
   ```
5. **Run tests**:
   ```bash
   npm test
   ```

### Understanding x402

spraay-payments uses the x402 protocol for micropayments:

- **HTTP 402**: Payment Required response
- **Automatic retry**: Client pays and retries automatically
- **No API keys**: Payments authenticate requests
- **Per-request pricing**: Each endpoint has its own cost

Learn more: [x402 Protocol Specification](https://github.com/coinbase/x402)

## Development Setup

### Local Development

1. **Install dependencies**:
   ```bash
   npm install
   ```

2. **Set up environment variables**:
   ```bash
   # Required
   export SPRAAY_GATEWAY_URL="https://gateway.spraay.app"
   
   # Optional - for testing with your own wallet
   export PRIVATE_KEY="your_test_wallet_private_key"
   export RPC_URL="https://mainnet.base.org"
   ```

3. **Run the development server**:
   ```bash
   npm run dev
   ```

### Testing x402 Payments

To test paid endpoints:

```bash
# Test a free endpoint (no payment required)
curl "$SPRAAY_GATEWAY_URL/api/health"

# Test a paid endpoint (requires x402 payment)
curl -X POST "$SPRAAY_GATEWAY_URL/api/batch-payment" \
  -H "Content-Type: application/json" \
  -d '{
    "recipients": [
      {"address": "0xABC...123", "amount": "10", "token": "USDC"}
    ],
    "chain": "base"
  }'
```

### Supported Chains for Testing

- **Base** (primary)
- Ethereum
- Arbitrum
- Polygon
- BNB Chain
- Avalanche
- Solana
- Unichain
- Plasma
- BOB
- Bittensor

## Project Structure

```
spraay-payments/
├── README.md              # User documentation
├── SKILL.md               # OpenClaw skill definition
├── package.json           # Dependencies and scripts
├── examples/              # Usage examples
│   ├── batch-payment.js
│   ├── payroll.js
│   ├── swap.js
│   └── invoice.js
├── src/
│   ├── index.js           # Main entry point
│   ├── api/               # API client
│   ├── chains/            # Chain configurations
│   ├── payments/          # Payment utilities
│   └── utils/             # Helper functions
├── tests/                 # Test suite
└── scripts/               # Build and utility scripts
```

### Key Components

- **Gateway Client**: Communicates with `https://gateway.spraay.app`
- **x402 Handler**: Manages payment flows and retries
- **Chain Configs**: Multi-chain support (11 chains)
- **Payment Utils**: Batch payments, payroll, swaps, invoices

## Contributing Workflow

### Branch Naming

- `feature/description` - New features
- `fix/description` - Bug fixes
- `docs/description` - Documentation updates
- `test/description` - Test additions/improvements
- `refactor/description` - Code refactoring

Example: `feature/add-optimism-support`

### Commit Messages

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
- `test`: Test changes
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `chore`: Maintenance tasks

Examples:
```
feat(chains): add Optimism chain support
fix(payments): resolve batch payment calculation error
docs(api): update endpoint documentation
test(x402): add payment retry tests
```

### Pull Request Process

1. **Create a branch** for your changes
2. **Make your changes** following our coding standards
3. **Test thoroughly** including x402 payment flows
4. **Update documentation** if needed
5. **Submit a pull request** with:
   - Clear title and description
   - Reference to any related issues
   - Test results
   - Screenshots (if UI changes)

### PR Review Criteria

- Code follows style guidelines
- Tests pass
- Documentation is updated
- x402 payment flows work correctly
- Multi-chain compatibility maintained

## Coding Standards

### JavaScript/TypeScript Style

- Use **ESLint** for linting
- Follow **Prettier** formatting
- Use **async/await** for asynchronous code
- Add **JSDoc comments** for public APIs

Example:
```javascript
/**
 * Send a batch payment to multiple recipients
 * @param {Array} recipients - Array of recipient objects
 * @param {string} chain - Target chain (base, ethereum, etc.)
 * @returns {Promise<Object>} Transaction result
 */
async function sendBatchPayment(recipients, chain) {
  // Implementation
}
```

### Error Handling

Always handle errors gracefully:

```javascript
try {
  const result = await api.sendBatchPayment(recipients, chain);
  return result;
} catch (error) {
  if (error.code === 'INSUFFICIENT_FUNDS') {
    throw new PaymentError('Insufficient funds for payment', error);
  }
  if (error.code === 'X402_PAYMENT_REQUIRED') {
    // Handle x402 payment flow
    return await handleX402Payment(error);
  }
  throw error;
}
```

### Chain Configuration

When adding new chains:

```javascript
const chains = {
  base: {
    id: 8453,
    name: 'Base',
    rpcUrl: 'https://mainnet.base.org',
    nativeCurrency: 'ETH',
    paymentContract: '0x1646452F98E36A3c9Cfc3eDD8868221E207B5eEC'
  },
  // Add new chain here
};
```

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run specific test file
npm test -- batch-payment.test.js

# Run with coverage
npm run test:coverage
```

### Test Structure

```javascript
describe('Batch Payments', () => {
  test('should send payment to multiple recipients', async () => {
    const recipients = [
      { address: '0x123...', amount: '10', token: 'USDC' },
      { address: '0x456...', amount: '20', token: 'USDC' }
    ];
    
    const result = await sendBatchPayment(recipients, 'base');
    
    expect(result.success).toBe(true);
    expect(result.transactions).toHaveLength(2);
  });
  
  test('should handle x402 payment required', async () => {
    // Test x402 flow
  });
});
```

### Integration Testing

Test against the live gateway:

```bash
# Set test environment
export SPRAAY_GATEWAY_URL="https://gateway.spraay.app"
export TEST_WALLET_KEY="your_test_key"

# Run integration tests
npm run test:integration
```

### Manual Testing Checklist

- [ ] Free endpoints work without payment
- [ ] Paid endpoints trigger x402 flow
- [ ] Batch payments work on all supported chains
- [ ] Payroll functionality works
- [ ] Token swaps execute correctly
- [ ] Invoices can be created and paid
- [ ] Error messages are clear and helpful

## Security

### Reporting Vulnerabilities

If you discover a security vulnerability:

1. **DO NOT** open a public issue
2. Email security@spraay.app with details
3. Include steps to reproduce
4. Allow time for remediation before disclosure

### Security Best Practices

- Never commit private keys
- Use environment variables for sensitive data
- Validate all user inputs
- Use HTTPS for all API calls
- Implement proper error handling
- Follow OWASP guidelines

### Payment Security

- Always verify payment amounts
- Check recipient addresses
- Use test networks for development
- Implement proper retry logic
- Log payment attempts (not keys)

## Community

### Communication Channels

- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and ideas
- **Discord**: [Join our community](https://discord.gg/spraay)
- **Twitter**: [@spraayapp](https://twitter.com/spraayapp)

### Getting Help

- Check existing [issues](https://github.com/extentadulthood280/spraay-payments/issues)
- Read the [documentation](https://docs.spraay.app)
- Ask in GitHub Discussions
- Join our Discord community

### Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Eligible for Spraay contributor rewards

## Resources

### Learning Materials

- [x402 Protocol](https://github.com/coinbase/x402)
- [Base Documentation](https://docs.base.org)
- [EIP-1559](https://eips.ethereum.org/EIPS/eip-1559) - Fee market
- [ERC-20](https://eips.ethereum.org/EIPS/eip-20) - Token standard

### Tools

- [Coinbase CDP](https://docs.cdp.coinbase.com/) - Wallet SDK
- [Viem](https://viem.sh/) - Ethereum library
- [Ethers.js](https://docs.ethers.io/) - Ethereum library
- [Jest](https://jestjs.io/) - Testing framework

---

Thank you for contributing to spraay-payments! Together we're building the future of multi-chain crypto payments. 💧

**Happy coding! 🚀**
