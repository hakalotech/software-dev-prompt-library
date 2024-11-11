# Aider Looping Strategies for Continuous Improvement

## Overview

This guide explores methods to create automated loops for using Aider to continuously improve code through architectural refinement and testing.

## Approach 1: Shell Script Looping

A basic shell script can create a loop to run Aider in architect mode, execute tests, and potentially generate reports:

```bash
#!/bin/bash
while true; do
    # Run aider architect mode
    aider --message "Improve architecture" 

    # Run tests
    aider --test-cmd "your_test_command"

    # Optional: generate a report
    # You might need a custom script here depending on your specific needs
    
    # Break condition (optional)
    # Add logic to break the loop if tests pass or after N iterations
done
```

### Key Considerations
- Specify your exact test command with `--test-cmd`
- Use `--auto-test` for automatic testing after each edit
- Implement break conditions to prevent infinite loops

## Approach 2: Python Scripting

For more programmatic control, use Python with the Aider library:

```python
from aider.coders import Coder
from aider.models import Model

model = Model("claude-3-5-sonnet")
fnames = ["your_files_here"]

coder = Coder.create(main_model=model, fnames=fnames)

while True:
    # Architect mode
    coder.run("Improve system architecture")
    
    # Run tests
    test_result = coder.run("/test")
    
    # Add break condition based on test results
    if test_result.success:
        break
```

### Advantages
- More fine-grained control over the improvement process
- Ability to add complex logic and break conditions
- Easier integration with existing Python workflows

## Recommended Options

- `--test-cmd`: Specify your exact test command
- `--auto-test`: Automatically run tests after each edit
- `--test`: Run tests and fix problems found

## Best Practices

1. Start with a clear, well-defined test suite
2. Use meaningful, incremental improvement messages
3. Monitor and adjust the loop to prevent unproductive iterations
4. Consider adding logging or reporting mechanisms

## References

- [Aider Scripting Documentation](https://aider.chat/docs/scripting.html)
- [Lint and Test Documentation](https://aider.chat/docs/usage/lint-test.html)
- [Aider Configuration Options](https://aider.chat/docs/config/options.html)
```
