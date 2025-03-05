# Unit Test Failure Analysis Guide

## Table of Contents
- [Initial Analysis](#initial-analysis)
- [Common Failure Patterns](#common-failure-patterns)
- [Environment Issues](#environment-issues)
- [Test Code Analysis](#test-code-analysis)
- [Implementation Analysis](#implementation-analysis)
- [Debugging Techniques](#debugging-techniques)
- [Solutions Checklist](#solutions-checklist)

## Initial Analysis

### 1. Understanding the Error Message
- Read the full error message carefully
- Note the specific expectation that failed
- Check the line number and file location
- Look for any stack trace information
- Identify any related test setup code

### 2. Quick Checks
```typescript
// Check test environment
beforeEach(() => {
  // Verify environment variables
  console.log('Node ENV:', process.env.NODE_ENV);
  // Check mock implementations
  console.log('Mock status:', jest.isMockFunction(myFunction));
});
```

### 3. Test Context
- Is this a new test or did it recently break?
- Are other related tests failing?
- Did the test pass previously?
- Recent code changes in the area?

## Common Failure Patterns

### 1. Type Mismatches
```typescript
// ❌ Common type mismatch
test('user data processing', () => {
  const userData = {
    id: '123', // String
    age: 25    // Number
  };
  
  expect(processUser(userData)).toEqual({
    id: 123,   // Expected as number
    age: 25
  });
});

// ✅ Fix: Align types
test('user data processing', () => {
  const userData = {
    id: '123',
    age: 25
  };
  
  expect(processUser(userData)).toEqual({
    id: '123', // Match the input type
    age: 25
  });
});
```

### 2. Async Issues
```typescript
// ❌ Missing await
test('async operation', () => {
  const result = fetchData(); // Promise not resolved
  expect(result).toBeDefined();
});

// ✅ Fix: Add async/await
test('async operation', async () => {
  const result = await fetchData();
  expect(result).toBeDefined();
});
```

### 3. Mock Implementation Mismatches
```typescript
// ❌ Incorrect mock implementation
const mockService = {
  getData: jest.fn().mockReturnValue({ status: 'success' })
};

// ✅ Fix: Match the actual service interface
const mockService = {
  getData: jest.fn().mockReturnValue({
    status: 'success',
    data: {
      id: 1,
      type: 'user'
    }
  })
};
```

## Environment Issues

### 1. Configuration Checks
- Verify Jest configuration
- Check TypeScript configuration
- Confirm environment variables
- Review test setup files

```typescript
// jest.config.js validation
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  setupFilesAfterEnv: ['./jest.setup.ts'],
  moduleNameMapper: {
    '^@/(.*)$': '<rootDir>/src/$1'
  }
};
```

### 2. Dependencies
- Check package versions
- Verify peer dependencies
- Review recent dependency updates
- Check for conflicting packages

## Test Code Analysis

### 1. Test Structure Review
```typescript
// Check the test structure
describe('UserService', () => {
  let service: UserService;
  let mockDb: jest.Mocked<Database>;

  beforeEach(() => {
    // Verify setup code
    mockDb = {
      query: jest.fn(),
      connect: jest.fn()
    };
    service = new UserService(mockDb);
  });

  // Verify tear down
  afterEach(() => {
    jest.clearAllMocks();
  });
});
```

### 2. Assertion Analysis
- Check assertion types
- Verify expected values
- Review matcher usage
- Check for partial matches

### 3. Mock Verification
```typescript
// Verify mock calls
test('service calls database', () => {
  service.getUser(1);
  
  // Check mock was called correctly
  expect(mockDb.query).toHaveBeenCalledWith(
    expect.stringContaining('SELECT'),
    expect.arrayContaining([1])
  );
});
```

## Implementation Analysis

### 1. Code Changes
- Review recent commits
- Check for refactoring
- Verify interface changes
- Review dependency updates

### 2. Interface Consistency
```typescript
// Check interface implementation
interface UserService {
  getUser(id: number): Promise<User>;
}

// Verify implementation matches
class UserServiceImpl implements UserService {
  async getUser(id: number): Promise<User> {
    // Implementation
  }
}
```

### 3. Side Effects
- Check for unintended side effects
- Review state modifications
- Check cleanup procedures
- Verify resource handling

## Debugging Techniques

### 1. Console Debugging
```typescript
test('debug with console', () => {
  console.log('Test started');
  
  const result = processData();
  console.log('Process result:', result);
  
  expect(result).toBeDefined();
});
```

### 2. Jest Debug Config
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Jest Current File",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": ["${fileBasename}", "--config", "jest.config.js"],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
  ]
}
```

### 3. Breakpoint Usage
- Set strategic breakpoints
- Use conditional breakpoints
- Check variable values
- Step through execution

## Solutions Checklist

### 1. Test Environment
- [ ] Jest configuration is correct
- [ ] TypeScript configuration is valid
- [ ] Environment variables are set
- [ ] Dependencies are up to date
- [ ] No conflicting packages

### 2. Test Code
- [ ] Test structure is correct
- [ ] Assertions are appropriate
- [ ] Mocks are properly configured
- [ ] Async operations are handled
- [ ] Cleanup is performed

### 3. Implementation
- [ ] Interface matches specification
- [ ] Types are consistent
- [ ] Side effects are handled
- [ ] Resources are managed
- [ ] Error handling is proper

### 4. Common Fixes
- [ ] Update type definitions
- [ ] Fix async/await usage
- [ ] Correct mock implementations
- [ ] Update assertions
- [ ] Fix environment setup

## Best Practices for Preventing Failures

### 1. Write Clear Tests
```typescript
// ✅ Clear test structure
describe('UserService', () => {
  describe('getUser', () => {
    test('returns user when found', async () => {
      // Clear arrangement
      const userId = 1;
      const expectedUser = { id: 1, name: 'Test' };
      mockDb.query.mockResolvedValue([expectedUser]);

      // Clear action
      const result = await service.getUser(userId);

      // Clear assertion
      expect(result).toEqual(expectedUser);
    });
  });
});
```

### 2. Maintain Test Isolation
```typescript
// ✅ Isolated tests
beforeEach(() => {
  // Reset all mocks
  jest.clearAllMocks();
  // Reset any global state
  global.localStorage.clear();
});

test('isolated test', () => {
  // Test-specific setup
  const testData = { ... };
  
  // Test logic
});
```

### 3. Regular Maintenance
- Review and update tests regularly
- Keep dependencies current
- Monitor test coverage
- Document known issues
- Maintain test documentation

## Additional Resources
- [Jest Debugging Guide](https://jestjs.io/docs/troubleshooting)
- [TypeScript Testing Handbook](https://www.typescriptlang.org/docs/handbook/testing.html)
- [VS Code Jest Extension](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest)
