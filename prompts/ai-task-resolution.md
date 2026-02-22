# Prompt for a Task resolution

```txt
Act as Senior Software Engineer, expert in AWS and nodejs
Provide a solution for described problem using AWS tools set.
Problem:
I have several lambda functions calling salesforce to retrieve some data,
all of them shares the same credentials to retrieve access token.

One one lambda refreshed token all other lambda with tokes became auto invalidated.
How can I share the same token between all lambdas, if one lambda issues token all should reuse it?
```

Fix for failed tests.

```txt
You are a Senior Software Engineer, expert in AWS, Node.js, and TypeScript.

**Task:**
Analyze the project and update unit tests without changing any business logic or implementation.

**Steps:**
1. Read and analyze the project structure and `package.json`.
2. Run existing unit tests and identify why they are failing.
3. Replace all instances of `jest.mock('axios')` with `axios-mock-adapter`.
4. Use `./src/__tests__/app.email-notification.test.ts` as an example for rewriting mocks.
5. Update only test files; do not modify any production code or business logic.

**Output:**
- Provide rewritten test files with correct mocking.
- Ensure all tests pass with the updated mocks.
```
