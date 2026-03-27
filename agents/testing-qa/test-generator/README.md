# Test Generator Agent

## Overview

The Test Generator agent automatically creates comprehensive test suites for code, including unit tests, integration tests, and end-to-end tests.

## Core Concept

Test generation workflow:
1. **Code Analysis** - Understand code structure and logic
2. **Test Planning** - Identify test cases needed
3. **Test Generation** - Generate test code
4. **Edge Case Discovery** - Find edge cases
5. **Coverage Analysis** - Ensure comprehensive coverage

## Skills

### Primary Skills
1. **Unit Test Generation** - Generate unit tests
2. **Integration Test Design** - Design integration tests
3. **Edge Case Detection** - Find edge cases
4. **Mock Generation** - Create mocks and stubs
5. **Assertion Design** - Create meaningful assertions

### Secondary Skills
- Property-based testing
- Mutation testing
- Performance test generation
- Security test generation
- Accessibility testing

## Use Cases

1. **New Code Testing** - Test newly written code
2. **Legacy Code Coverage** - Add tests to legacy code
3. **Regression Prevention** - Create regression tests
4. **Documentation** - Tests as documentation
5. **CI/CD Integration** - Automated test generation

## Example Test Output

### Unit Tests
```python
# Generated tests for user_service.py

import pytest
from unittest.mock import Mock, patch
from user_service import UserService, UserNotFoundError

class TestUserService:
    """Test suite for UserService"""
    
    @pytest.fixture
    def user_service(self):
        return UserService(db=Mock())
    
    @pytest.fixture
    def sample_user(self):
        return {"id": 1, "name": "John Doe", "email": "john@example.com"}
    
    # Happy path tests
    def test_get_user_by_id_success(self, user_service, sample_user):
        """Test successful user retrieval"""
        user_service.db.get.return_value = sample_user
        result = user_service.get_user(1)
        assert result == sample_user
        user_service.db.get.assert_called_once_with(1)
    
    def test_create_user_success(self, user_service, sample_user):
        """Test successful user creation"""
        user_service.db.insert.return_value = sample_user
        result = user_service.create_user(sample_user)
        assert result == sample_user
    
    # Error cases
    def test_get_user_not_found(self, user_service):
        """Test user not found raises error"""
        user_service.db.get.return_value = None
        with pytest.raises(UserNotFoundError):
            user_service.get_user(999)
    
    # Edge cases
    def test_create_user_with_empty_name(self, user_service):
        """Test creating user with empty name"""
        with pytest.raises(ValueError):
            user_service.create_user({"name": "", "email": "test@example.com"})
    
    def test_create_user_with_invalid_email(self, user_service):
        """Test creating user with invalid email"""
        with pytest.raises(ValueError):
            user_service.create_user({"name": "Test", "email": "invalid"})
    
    # Boundary tests
    def test_user_name_max_length(self, user_service):
        """Test user name at maximum length"""
        long_name = "a" * 255
        user = {"name": long_name, "email": "test@example.com"}
        user_service.db.insert.return_value = user
        result = user_service.create_user(user)
        assert result["name"] == long_name
```

## Configuration

```json
{
  "agent_type": "test-generator",
  "test_framework": "pytest",
  "coverage_target": 80,
  "test_types": ["unit", "integration", "edge_case"],
  "mock_strategy": "auto",
  "include_performance": false,
  "include_security": true,
  "output_format": "python"
}
```

## Test Types Generated

| Type | Purpose | Coverage |
|------|---------|----------|
| Unit | Test individual functions | 70% |
| Integration | Test component interactions | 20% |
| Edge Case | Test boundary conditions | 10% |

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Tests per minute | 50-100 |
| Coverage improvement | +40% |
| False positive rate | <5% |
| Best for | Python, JavaScript, Java |

## Monetization Strategy

### Pricing Tiers
- **Basic**: $0.05/function tested
- **Pro**: $0.15/function (all test types)
- **Enterprise**: $0.30/function (with coverage report)

### Target Markets
1. Development teams
2. QA teams
3. DevOps teams
4. Enterprise software

## Related Agents

- `bug-reproducer/` - Create tests from bugs
- `qa-orchestrator/` - Test orchestration
- `code-reviewer/` - Review code quality
