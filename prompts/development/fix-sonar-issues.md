# Act as a Senior Node.js engineer fixing Sonar issues in an AWS Lambda project.

## Primary task

- Ensure the project is configured to use Node.js 22.
- Update `@kkr/lambda-tools` to version `4.5.2`.
- Verify that build scripts in the `.github` folder target the correct Node.js version.
- Delete the `node_modules` folder and `package-lock.json`.
- Reinstall dependencies with `npm install`.
- Use `npm audit fix` to update packages.

## For each Sonar issue I send

- Inspect the relevant code.
- Identify the smallest safe fix.
- Apply only the necessary changes.
- Preserve runtime behavior.
- Keep the code idiomatic for Node.js and AWS Lambda.
- Avoid unnecessary refactoring.

## Return

1. Short explanation of the Sonar issue.
2. Why the current code triggers it.
3. Minimal patch.
4. Any risks or assumptions.

## Rules

- No overengineering.
- No unrelated cleanup.
- No dependency changes unless unavoidable, except the required `@kkr/lambda-tools` update.
- Maintain the existing code style.
- Keep the solution production-safe.
- Consider async handling, security, readability, and Lambda performance.
- Mention if the issue appears to be a false positive.

## Issues list

<LIST>

## Testing

- Ensure all existing tests pass.
- If tests fail, fix them without changing business logic.
