# Interviewer Coding Exercise Template

<details>
<summary><h2>#[Number] [Problem Title] [Difficulty Level]</h2></summary>

## Problem Statement

[Clear problem description including constraints, input/output formats, and any special considerations]

## Template Code

```[language]
// [Language] Solution Template
// Provide a skeleton for the candidate to fill in

function solutionFunction(param1, param2) {
    // TODO: Implement solution here
    
    return result;
}

// Test cases
function runTests() {
    const testCases = [
        {
            input: [param1, param2],
            expected: expectedOutput,
            description: "Test case description"
        },
        // Additional test cases
    ];
    
    for (const test of testCases) {
        const result = solutionFunction(...test.input);
        const passed = deepEqual(result, test.expected);
        console.log(`${test.description}: ${passed ? "PASSED" : "FAILED"}`);
        if (!passed) {
            console.log(`  Expected: ${JSON.stringify(test.expected)}`);
            console.log(`  Received: ${JSON.stringify(result)}`);
        }
    }
}

// Helper function for comparing results
function deepEqual(a, b) {
    // Implement comparison logic as needed
}

// Run tests
runTests();
```

## Expected Solution

```[language]
// Solution code that the interviewer can reference
// Include comments explaining the approach and time/space complexity

function solutionFunction(param1, param2) {
    // Solution implementation
    
    return result;
}

// Time Complexity: O(?)
// Space Complexity: O(?)
```

## Test Cases

| Input | Expected Output | Notes |
|-------|----------------|-------|
| Input1 | Output1 | Explanation for this test case |
| Input2 | Output2 | Edge case handling |
| Input3 | Output3 | Corner case |
| Input4 | Output4 | Performance consideration |

## Evaluation Criteria

- **Correctness**: Does the solution work for all test cases?
- **Efficiency**: Is the time and space complexity optimal?
- **Code Quality**: Is the code clean, readable, and well-structured?
- **Edge Cases**: Did the candidate handle all edge cases?
- **Problem Solving**: How did the candidate approach the problem?

## Interview Prompts

If the candidate is stuck, consider these prompts:
- "Have you considered using [data structure/algorithm]?"
- "What happens if the input is [edge case]?"
- "Can you think of a way to optimize your current approach?"
- "Let's analyze the time complexity of your solution."

## Problem Variations

- Harder version: [Description of how to make the problem more challenging]
- Easier version: [Description of how to simplify the problem]
- Follow-up question: [Related question to ask if time permits]

</details>
