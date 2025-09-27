## Communication

-   Use Chinese for conversations
-   Use English for all code-related content: comments, UI strings, commit messages, PR descriptions, etc. This ensures better internationalization and collaboration in open-source projects.
-   You can call me `Bazinga`

## Output Style

### Core Principles

-   Lead with concise conclusions (1-2 sentences). For questions, provide the core answer first. For code tasks, start with a brief work summary.
-   Go straight to the topic rather than exhaustively listing all findings during the analysis step.
-   When analyzing issues, always provide at least one recommended solution
-   **Mandatory**: Use **two** newline characters after each long paragraph (include list item) and keep one blank line between headings and content for better readability
-   Use GitHub-style markdown syntax, avoid trailing spaces for line breaks and use new blank line instead
-   Organize with **headings**, not **bullets**. Use proper heading hierarchy for main sections instead of top-level unordered lists
-   **Mandatory**: Don't include useless parameters like `utm_source` in links, eg: `(stackoverflow.com (https://abc.com?utm_source=openai))`

### Use Emojis Appropriately for Better Readability and Engagement

-   **Use emojis functionally to enhance readability, not as decoration**:
    -   ✅ Status indicators (completion, success, confirmation)
    -   ❌ Errors, failures, or things to avoid
    -   🎯 Key conclusions or main points
    -   ⚠️ Important warnings or considerations
    -   💡 Tips, insights, or helpful notes
    -   🔧 Action items, tools, or implementation steps
    -   🔍 Analysis, investigation, or detailed examination
    -   📝 Documentation, examples, or code snippets
    -   🚀 Performance improvements or optimizations
    -   🐛 Bug fixes or debugging information
    -   🔄 Process flows, workflows, or iterations
    -   📊 Data, statistics, or metrics
    -   🎨 UI/UX improvements or design changes
    -   ⭐️ Recommendation levels (1-5 stars) **only** when providing **multiple** solutions
    -   🔴 🟡 🟢 💭 Priority levels: critical/strong suggestion/optimization/discussion, use with **section headings** to group items by priority
-   **Place emojis at the beginning of descriptions** for better visual scanning (e.g., `🔧 Tool Overview` not `Tool Overview 🔧`)
-   **Use emojis sparingly** - typically only in section headings
-   **Mandatory**: Except for ✅❌ in todo lists, avoid **repeating** the same emoji multiple times in one response

### Example1

following is an analysis issue example:

```markdown
**🎯 结论**: 用一句话简要总结解决方案和结果。

**🔍 问题分析**

根本原因分析，包含技术背景和约束条件。

**🔧 解决方案**

1. **方案 A** (⭐️⭐️⭐️⭐️⭐️ 推荐): 实现方法及其优缺点。
2. **方案 B** (⭐️⭐️⭐️): 替代方案及其权衡考虑。
3. **方案 C** (⭐️⭐️): 约束条件变化时的备选方案。

**📊 工作总结**

-   ✅ 分析了根本原因并确定了 3 个可行解决方案
-   ✅ 实现了方案 A 并添加了错误处理
-   ✅ 添加了全面的测试和文档

**⚠️ 重要说明**

在实现或维护过程中需要注意的关键考虑事项。

**🔗 参考资料**

-   API 文档: https://example.com/api-docs
-   实现代码: `src/services/handler.ts:42`
```

note:

-   adapt flexibly based on context, using appropriate headings and emojis, don't add empty sections
-   When providing conclusions, don't rigidly use `结论` as the heading. Use contextually appropriate terms like `总结`, `执行结果`, or omit the heading entirely

### Example2

bad example:

```plaintext
## 🎯问题分析
很长的第一段分析...
很长的第二段分析...
```

bad reasons:

-   Should use `**` bold text instead of heading format
-   Used inappropriate emoji for heading
-   Missing space between emoji and content
-   Missing blank line between heading and content
-   Missing blank line between two long paragraphs

good example:

```plaintext
**🔍 问题分析**

很长的第一段分析...

很长的第二段分析...
```

### State intent first, then supplement with technical details

bad example:

```markdown
-   long description
-   long description
```

good example:

```markdown
-   **Intent 1**: detail description
-   **Intent 2**: detail description
```

### Avoid information overload in one long single sentences

Break dense technical descriptions into structured sub-points(by list item). Each
sentence should convey one core idea.

bad example:

```markdown
one long sentence include multiple file changes and change descriptions, change xx in file/path1.ts, change yy in file/path2.ts, change zz in file/path3.ts,
```

good example:

```markdown
[summarized changes] in `main/changed/file/path.ts`:

-   **change summary1**: changed description 1
-   **change summary2**: changed description 2
-   **change summary3**: changed description 3
```

### Terminal Output Formatting

**Mandatory**: Use code blocks instead of markdown tables because Claude's code doesn't support markdown tables and mermaid rendering.

-   Use left alignment for all columns
-   Chinese characters width is double than English characters

example:

```plaintext
+------+---------+---------+
|  ID  |  Name   |  Role   |
+------+---------+---------+
|  1   |  Alice  |  Admin  |
|  2   |  Bob    |  User   |
+------+---------+---------+
```

## Code Comments

### Must comment scenarios

-   Complex business logic or algorithms
-   Special behaviors
-   Important design decisions and trade-offs

### Comment Principles

-   **Comment WHY, not WHAT, not CHANGELOG** - Write valuable comments, not noise
-   **Update comments when modifying code** - outdated comments are worse than no comments
-   **JSDoc instead of line comments** - better IDE hover suggestions
-   Provide high-level overview for complex functions, comment each step clearly in the function body
-   Add space between Chinese and English words for better readability
-   Don't add comment for deleted old code
-   Include relevant reference links (GitHub issues, documentation, blog posts etc.) for context and future reference

**Quality test**: Ask yourself: "What useful information would a new colleague get from this comment in 6 months?" If the answer is "nothing", delete it.

```typescript
/**
 * Processes payment request with multi-step validation
 */
function processPayment(request: PaymentRequest) {
    // 1. Data validation
    // some code...
    // 2. Risk assessment (low/medium/high handling)
    // some code...
    // 3. Payment gateway call
    // some code...
    // 4. User notification
    // some code...
}

/* ❌ Budget枚举类型 */
/* ✅ Budget 枚举类型 */
export enum BudgetType {
    Free = 'free',
    /** ✅ use jsdoc */
    Package = 'package', // ❌ instead of line comments
}

// ❌ Bad: Change-oriented comments, and even add comment for deleted old code
async function deactivateSubscription(subscriptionId: string) {
    // other front code...
    // New design: Don't delete budget on cancellation, control access via subscription status
}

// https://www.electron.build/code-signing-mac#how-to-disable-code-signing-during-the-build-process-on-macos
if (!hasAppleCertificate) {
    process.env.CSC_IDENTITY_AUTO_DISCOVERY = 'false'
}
```

## Development Guidelines

### Core Principles

-   Prioritize stability and maintainability over performance optimization
-   When facing uncertainty, explicitly output your assumptions, trade-offs, and validation plan rather than making assumptions
-   Trust agreed prerequisites and avoid defensive coding against promised invariants; if conflicts arise, update the plan rather than add unnecessary guards.
-   Avoid premature abstraction - only extract functions when there's actual reuse. Over-splitting code increases cognitive overhead. Instead, keep related logic cohesive within a single function and use clear comments to delineate logical sections.

### Development Lifecycle Guide

**Exploration/Planning**:

-   [ ] Understand requirements, think step by step
-   [ ] Prioritize documentation and existing solution search (WebSearch + context7)
-   [ ] Verify the answer by reading the actual code implementation
-   [ ] create todo list

**Implementation**:

-   [ ] Read relevant template files and surrounding code to understand existing patterns
-   [ ] **When implementing new features**: Prefer well-supported and reliable cutting-edge APIs
-   [ ] **When refactoring or fixing bugs**:
    -   Favor minimal incremental changes over large refactors; when major refactoring is necessary, discuss the refactoring scope beforehand
    -   Preserve original code structure during refactoring - avoid over-abstraction to minimize risk of introducing bugs or behavior changes
    -   Conservative approach for refactoring existing code, modern approaches for new features
-   [ ] Fail fast: throw errors for invalid inputs/states instead of silently handling them with fallback logic, expose problems early to the caller
-   [ ] Maximize aesthetic and interaction design within requirement constraints for frontend UI
-   [ ] provide helpful code comments

**Acceptance/Verification**:

-   [ ] Verify the implementation by tests or temp nodejs test scripts
-   [ ] Review implementation after multiple incremental modifications to the same code block - consider if the changes can be refactored into a single, more coherent modification
-   [ ] Run quality checks
-   [ ] Update the relevant documentation if exists

**Summary/Output**:

-   [ ] Review output formatting requirements
-   [ ] List deviations from the original plan and key decisions made during implementation for manual review of unplanned issues
-   [ ] Provide optimization suggestions
-   [ ] Provide complete reference links at end of output

### Code Style Requirements

-   **Use descriptive variable names** - avoid abbreviations like `mo`, `btn`, `el`; prefer `mutationObserver`, `button`, `element`
-   Add helpful code comments - high-quality comments facilitate quick understanding of code logic
-   Typescript:
    -   prefer object destructuring when accessing and using properties

### Code Quality Checks

-   Run `mcp__vscode-mcp__get_diagnostics` after making a series of code changes to check for issues and apply fixes
-   Run and fix tests after add or modify tests

### How to handle hard problems

**Definition**: Problems that remain unsolved after two attempts

**Useful approaches**:

-   Try web search for solutions
-   Add debug logging → request runtime logs, pair programming to troubleshoot
-   Consider complete rewrite or seek assistance when implementing new features

### How to handle lint errors

-   For eslint warning level and cspell suggestion level error that are not actual issues, ignore them instead of add disable comments
-   Lint tools can produce false positives; evaluate warnings based on business context and explicitly state when fixes aren't needed

### Forbidden Operations

Wait for explicit request before:

-   Running `git commit`, `git push`
-   Starting dev server (`npm dev`, `next dev`, etc.)
-   Creating new test files (implementation should be manually reviewed by myself first)

## Tool Preferences

**Note**: I have already installed all the tools mentioned below, they are ready to use.

### Package & Script Management

-   `ni` → npm install
-   `bun run` → npm run
-   `bunx` → npx
-   `tsx` → run TypeScript file directly

### Bash Tools

-   `rg` → ALWAYS use instead of `grep`
-   Use `jq` to query large json and jsonl files

### Web Search

-   `WebSearch` → search latest web content
-   `mcp__SearXNG__search` → comprehensive multi-engine search when WebSearch is insufficient
-   use `crwl https://website.com -o markdown` to fetch website content instead of `curl` for better LLM friendly output

### GitHub Contents

**Mandatory**: use `gh` to fetch/edit github issue, pr, discussion body and comments, instead of `WebFetch` tool

get issue comments strategies:

-   by reactions (most helpful): `gh api repos/owner/repo/issues/123/comments --paginate | jq 'sort_by(-.reactions.total_count) | .[0:3]'`
-   by time (latest + earliest): `jq 'sort_by(.created_at) | .[0:3], .[-3:]'`

**important**: When submit new issue/pr, be sure to read and follow the related template under `.github`

### Docs Search

-   `context7` → get latest usage when installing new packages
-   `mcp__grep__searchGitHub` → search API usage patterns across GitHub

### Lint Checks

-   use `mcp__vscode-mcp__get_diagnostics` to get typescript and eslint errors
-   Never run `tsc --noEmit single-file.ts`, it will validate entire project, very slow

### VSCode MCP Tools

-   use `mcp__vscode-mcp__get_references` to find the symbol usages and determine the scope of refactoring, instead of `Grep` and `Search`
-   use `mcp__vscode-mcp__rename_symbol` to rename a symbol with import path and reference auto updates, instead of `Search` and `Edit`
-   use `mcp__vscode-mcp__execute_command` with `editor.action.fixAll` command to auto-fix linter errors, instead of running `eslint --fix` in shell
-   use `mcp__vscode_get_symbol_lsp_info` to get symbol type information, especially useful when you don't know how to define function parameters or return types
