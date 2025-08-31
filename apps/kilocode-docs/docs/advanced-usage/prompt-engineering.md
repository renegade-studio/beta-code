# A Guide to Prompt Engineering with Kilo Code

Prompt engineering is the art and science of crafting effective instructions for AI models like Kilo Code. By mastering this skill, you can unlock the full potential of Kilo Code, leading to better results, fewer errors, and a more efficient workflow.

This guide will walk you through the fundamentals of prompt engineering and introduce you to a range of techniques that will help you get the most out of Kilo Code.

## Core Principles

These are the fundamental principles that underpin all effective prompts.

*   **Be Clear and Specific:** The more specific you are in your instructions, the better Kilo Code can understand and execute your request. Avoid vague language and provide concrete details about what you want to achieve.
    *   **Bad:** `Fix the code.` (Too vague. What code? What's wrong with it?)
    *   **Good:** `In @/src/components/Calculator.js, the calculateTotal function is throwing a NaN error when the input is a string. Please add validation to ensure that only numbers are processed.`

*   **Provide Context:** Kilo Code is a powerful tool, but it doesn't have the same level of context as a human developer. Use [@context mentions](/basic-usage/context-mentions) to provide relevant files, folders, or error messages. The more context you provide, the more accurate the results will be.
    *   **Bad:** `Refactor this function to be more efficient.` (Which function? What does "more efficient" mean?)
    *   **Good:** `The bubbleSort function in @/src/lib/sorting.ts is too slow for large datasets. Please refactor it to implement the quicksort algorithm instead.`

*   **Break Down Tasks:** Complex tasks can be overwhelming for an AI. Instead of asking Kilo Code to do everything at once, break down the task into smaller, manageable steps. This allows you to guide the AI and review its work at each stage.
    *   **Bad:** `Build a new authentication system.`
    *   **Good:**
        1.  `Create a new file for the authentication service.`
        2.  `Add a function to handle user registration.`
        3.  `Implement password hashing using bcrypt.`
        4.  `Add a function for user login.`

*   **Give Examples (Few-Shot Prompting):** If you have a specific coding style, pattern, or output format in mind, provide examples in your prompt. This is a powerful technique known as "few-shot prompting."
    *   **Good:** `I'm converting my project to use TypeScript. Please convert the following JavaScript function to TypeScript:
        \`\`\`javascript
        function addUser(user) {
          return { ...user, id: Date.now() };
        }
        \`\`\`
        Here's an example of another converted function:
        \`\`\`typescript
        type Product = { name: string; price: number; };
        function addProduct(product: Product): Product & { id: number } {
          return { ...product, id: Date.now() };
        }
        \`\`\``

*   **Specify Output Format:** If you need the output in a particular format (e.g., JSON, Markdown, a specific code style), explicitly state it in your prompt.
    *   **Good:** `Please generate a list of all the functions in @/src/api/index.ts and format the output as a JSON array of strings.`

*   **Iterate and Refine:** Don't expect to get the perfect result on the first try. Prompt engineering is an iterative process. If the initial results aren't what you expect, analyze the output, refine your prompt, and try again. Use the feedback mechanisms in Kilo Code to guide the AI toward the desired outcome.

## Beginner Techniques

If you're new to prompt engineering, these techniques are a great place to start.

### Thinking vs. Doing

It's often helpful to guide Kilo Code through a "think-then-do" process:

1.  **Analyze:** Ask Kilo Code to analyze the current code, identify problems, or plan the approach.
2.  **Plan:**  Have Kilo Code outline the steps it will take to complete the task.
3.  **Execute:**  Instruct Kilo Code to implement the plan, one step at a time.
4.  **Review:**  Carefully review the results of each step before proceeding.

### Using Custom Instructions

You can provide [custom instructions](/advanced-usage/custom-instructions) to further tailor Kilo Code's behavior. There are two types of custom instructions:

*   **Global Custom Instructions:** Apply to all modes.
*   **Mode-Specific Custom Instructions:** Apply only to a specific mode (e.g., Code, Architect, Ask, Debug, or a [custom mode](/features/custom-modes)).

Custom instructions are added to the system prompt, providing persistent guidance to the AI model. You can use these to:

*   Enforce coding style guidelines.
*   Specify preferred libraries or frameworks.
*   Define project-specific conventions.
*   Adjust Kilo Code's tone or personality.

### Handling Ambiguity

If your request is ambiguous or lacks sufficient detail, Kilo Code might:

*   **Make Assumptions:**  It might proceed based on its best guess, which may not be what you intended.
*   **Ask Follow-Up Questions:** It might use the [`ask_followup_question`](/docs/features/tools/ask-followup-question.md) tool to clarify your request.

It's generally better to provide clear and specific instructions from the start to avoid unnecessary back-and-forth.

### Providing Feedback

If Kilo Code doesn't produce the desired results, you can provide feedback by:

*   **Rejecting Actions:** Click the "Reject" button when Kilo Code proposes an action you don't want.
*   **Providing Explanations:** When rejecting, explain *why* you're rejecting the action.  This helps Kilo Code learn from its mistakes.
*   **Rewording Your Request:** Try rephrasing your initial task or providing more specific instructions.
*   **Manually Correcting:** If there are a few small issues, you can also directly modify the code before accepting the changes.

## Intermediate Techniques

Once you've mastered the basics, you can start using more advanced techniques to further improve your results.

### Zero-Shot, One-Shot, and Few-Shot Prompting

These techniques refer to the number of examples you provide in your prompt.

*   **Zero-Shot:** You don't provide any examples. This works well for simple tasks where the AI already has enough information to understand your request.
    *   **Example:** `Create a function that takes a string as input and returns the reversed string.`

*   **One-Shot:** You provide a single example to guide the AI. This is useful when you want the output to follow a specific pattern.
    *   **Example:** `Convert the following comment to JSDoc format:
        // Takes a user object and returns the full name.

        Example:
        // Input: const user = { firstName: 'John', lastName: 'Doe' };
        // Output: /**
        //  * Takes a user object and returns the full name.
        //  * @param {object} user - The user object.
        //  * @returns {string} The user's full name.
        //  */`

*   **Few-Shot:** You provide multiple examples. This is the most powerful technique for complex tasks or when you need to enforce a specific coding style. I've already shown an example of this in the Core Principles section.

### Chain-of-Thought Prompting

This technique involves breaking down a complex task into a series of smaller, logical steps. It's similar to the "Thinking vs. Doing" approach, but it focuses more on guiding the AI's reasoning process.

*   **Example:**
    1.  `First, analyze the @/src/api/auth.ts file and identify all the dependencies that are not being used.`
    2.  `Next, create a list of the unused dependencies.`
    3.  `Finally, remove the unused dependencies from the file.`

By guiding the AI through a chain of thought, you can help it tackle more complex problems and reduce the likelihood of errors.

### Role-Playing

You can instruct Kilo Code to act as a specific persona, such as a senior developer, a security expert, or a database administrator. This can help you get more targeted and relevant responses.

*   **Example:** `Act as a senior security engineer and review the @/src/controllers/userController.ts file for any potential security vulnerabilities. Pay close attention to input validation and SQL injection risks.`

### Using Delimiters

Delimiters are special characters or strings that you can use to separate different parts of your prompt. This can help the AI better understand the structure of your request. Common delimiters include backticks (```), quotes ("""), and XML tags (<example></example>).

*   **Example:** `Here is a function that I want to refactor:
    \`\`\`javascript
    function factorial(n) {
      if (n === 0) {
        return 1;
      } else {
        return n * factorial(n - 1);
      }
    }
    \`\`\`
    Please refactor this function to use a loop instead of recursion.`

## Advanced Techniques

*(Coming soon...)*

## Real-World Examples

Let's take a look at some real-world scenarios to see how you can apply these principles and techniques.

### Scenario 1: Refactoring a Complex Function

**Goal:** Refactor a complex function to improve its readability and performance.

**Bad Prompt:** `Refactor this function.`

**Good Prompt:**
> Act as a senior software engineer. The `processData` function in `@/src/services/dataProcessor.js` is becoming difficult to maintain and is a performance bottleneck.
>
> Here is the function:
> ```javascript
> function processData(data) {
>   // ... complex logic ...
> }
> ```
>
> Please refactor this function by:
> 1.  Breaking it down into smaller, more manageable helper functions.
> 2.  Adding comments to explain the logic of each helper function.
> 3.  Replacing the nested loops with more efficient array methods like `map` and `filter`.
> 4.  Ensuring that the refactored code produces the same output as the original function.

### Scenario 2: Generating Unit Tests

**Goal:** Generate unit tests for a specific function to ensure it works as expected.

**Bad Prompt:** `Write some tests.`

**Good Prompt:**
> I need to write unit tests for the `calculateDiscount` function in `@/src/utils/pricing.js`.
>
> Here is the function:
> ```javascript
> function calculateDiscount(price, percentage) {
>   return price * (percentage / 100);
> }
> ```
>
> Please generate a new file at `@/src/utils/pricing.test.js` with unit tests for this function using the Jest testing framework. The tests should cover the following cases:
> - A positive price and a positive percentage.
> - A price of zero.
> - A percentage of zero.
> - A percentage of 100.

### Scenario 3: Debugging a Tricky Issue

**Goal:** Debug an issue where an API call is failing silently.

**Bad Prompt:** `My code is not working.`

**Good Prompt:**
> I'm having trouble with an API call in my React component. The `fetchData` function in `@/src/components/DataFetcher.jsx` is not updating the state with the fetched data, and there are no errors in the console.
>
> Here is the component:
> ```jsx
> function DataFetcher() {
>   const [data, setData] = useState(null);
>
>   useEffect(() => {
>     async function fetchData() {
>       const response = await fetch('/api/data');
>       const json = await response.json();
>       setData(json);
>     }
>     fetchData();
>   }, []);
>
>   return (
>     // ...
>   );
> }
> ```
>
> Please help me debug this issue by:
> 1.  Adding `console.log` statements to trace the execution of the `fetchData` function.
> 2.  Adding error handling to the `try...catch` block to catch any potential errors.
> 3.  Checking the network tab in the browser's developer tools to see if the API call is being made correctly.

### Scenario 4: Automating a Multi-Step Task

**Goal:** Automate the process of creating a new React component.

**Bad Prompt:** `Create a new component.`

**Good Prompt:**
> I want to automate the creation of new React components. Please perform the following steps using the [`write_to_file`](/docs/features/tools/write-to-file.md) tool:
> 1.  Create a new directory for the component at `src/components/NewComponent`.
> 2.  Inside this directory, create a new file named `NewComponent.jsx` with a basic functional component template.
> 3.  Create a new file named `NewComponent.css` with some basic styles.
> 4.  Create a new file named `index.js` that exports the `NewComponent`.

## Anti-Patterns

Just as important as knowing what to do is knowing what *not* to do. Here are some common anti-patterns to avoid when writing prompts.

### Vague or Ambiguous Prompts

As mentioned in the Core Principles, vague prompts are the most common source of errors. Always be as specific as possible.

*   **Anti-Pattern:** `Improve this code.`
*   **Better:** `Please refactor the @/src/utils/helpers.js file to improve its performance. Specifically, I'm concerned about the `processLargeArray` function.`

### Providing Too Much Irrelevant Context

While context is important, providing too much *irrelevant* context can confuse the AI. Only include the files and information that are directly relevant to the task at hand.

*   **Anti-Pattern:** Including the entire codebase in the context for a small change.
*   **Better:** Only including the specific file or function that needs to be modified.

### Asking the AI to Perform Unsafe Operations

Kilo Code has safeguards to prevent it from performing dangerous operations, but you should still be cautious about what you ask it to do. Avoid prompts that could have unintended consequences, such as deleting files or modifying system settings.

*   **Anti-Pattern:** `Delete all the files in the /tmp directory.`
*   **Better:** `Please list all the files in the /tmp directory so I can decide which ones to delete.`

### Expecting Perfect Code Every Time

AI models are powerful tools, but they are not perfect. Always review the code that Kilo Code generates and be prepared to make manual corrections. Think of Kilo Code as a junior developer that can help you with the heavy lifting, but still needs your guidance and supervision.
