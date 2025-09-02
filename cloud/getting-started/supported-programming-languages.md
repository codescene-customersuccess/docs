# Supported Programming Languages

CodeScene supports different programming languages at different levels:

1\. **Basic**: All text-based content can be analysed on the file level. This enables hotspot analyses, change coupling, and knowledge metrics.

2\. **X-Ray with method level hotspots**: The second level of support is CodeScene’s language aware X-Ray analysis that calculates hotspots and change coupling on a function/method level.

3\. **Full support**: Full language support means that CodeScene calculates Code Health metrics, enables the virtual code reviewer, and supports the goal-oriented workflow concept to manage technical debt and code quality.

### Language Specific Features[¶](broken-reference)

CodeScene has dedicated language support for the following programming languages:

| Language                                 | Full support | X-Ray (method level hotspots) |
| ---------------------------------------- | ------------ | ----------------------------- |
| C                                        | Yes          | Yes                           |
| C++                                      | Yes          | Yes                           |
| C#                                       | Yes          | Yes                           |
| Java                                     | Yes          | Yes                           |
| Groovy                                   | Yes          | Yes                           |
| JavaScript                               | Yes          | Yes                           |
| TypeScript                               | Yes          | Yes                           |
| React (jsx, tsx)                         | Yes          | Yes                           |
| ECMAScript Modules                       | Yes          | Yes                           |
| Vue.js                                   | Yes          | Yes                           |
| Objective-C 2.0                          | Yes          | Yes                           |
| Scala                                    | Yes          | Yes                           |
| Python                                   | Yes          | Yes                           |
| Swift                                    | Yes          | Yes                           |
| Go                                       | Yes          | Yes                           |
| Dart2                                    | Yes          | Yes                           |
| Visual Basic .Net                        | Yes          | Yes                           |
| PHP                                      | Yes          | Yes                           |
| Rust                                     | Yes          | Yes                           |
| Ruby                                     | Yes          | Yes                           |
| Rational Software Architect models (C++) | Yes          | Yes                           |
| Kotlin                                   | Yes          | Yes                           |
| Perl 5                                   | Yes          | Yes                           |
| Erlang                                   | Yes          | Yes                           |
| Elixir                                   | Yes          | Yes                           |
| Clojure                                  | Yes          | Yes                           |
| PowerShell                               | Yes          | Yes                           |
| TCL                                      | Yes          | Yes                           |
| Apex (Salesforce)                        | Yes          | Yes                           |
| BrightScript                             | Yes          | Yes                           |
| BrighterScript                           | Yes          | Yes                           |
| Terraform                                | No           | Yes                           |

### Programming Language Details[¶](broken-reference)

The code health metric represents a general concept which applies across all supported languages. However, some details might vary. This section highlights any language specific analysis details.

#### C# Analysis Details[¶](broken-reference)

**Local Functions**: Local functions are a fairly recent addition to the C# language. A local function is simply a method defined inside another method:

```
private void Process(string?[] lines, string mark)
{
    foreach (var line in lines) // Here's some logic in the enclosing function...
    {
        if (IsValid(line))      // ...and we encapsulate details in a local function.
        {
            // Processing logic...
        }
    }

    bool IsValid([NotNullWhen(true)] string? line) // <-- local function.
    {
        return !string.IsNullOrEmpty(line) && line.Length >= mark.Length;
    }
}
```

CodeScene treats local functions as first-class analysis elements. This means that a code smell inside a local function is reported there (e.g. _IsValid_ in the example above); not on the enclosing method (e.g. _Process_). Similiarly, this also allows you to view local functions as separate priorities in the X-Ray analysis. Here’s an example:

#### C++ Analysis Details[¶](broken-reference)

**Unit Test Frameworks**: CodeScene supports two formal C++ Unit Test frameworks:

1. Microsoft Unit Testing Framework
2. GoogleTest

This means that CodeScene will recognize the test methods as well as analyze the assertion patterns in the test methods. The purpose of the assertion analysis is to identify test-specific smells like large assertion blocks and duplicated assertion blocks. These findings are included in the Code Health calculation and accessible via the virtual code review and X-Ray for each test file.

#### Rust Analysis Details[¶](broken-reference)

**Analyzing Tests embedded in the Application Code Module**: CodeScene lets you apply custom rules to tests, even when embedded in a file with application code. (Rust only).

Some CodeScene users prefer to relax the Code Health rules for test code. A common example is to allow more Code Duplication across tests, but be strict on duplication in the application code. Since idiomatic Rust code can contain unit tests embedded in the same file as the application code, CodeScene has extended its custom Code Health configuration support for Rust.

In Rust, we let you specify an optional “content\_filter” element. That element is used to indicate “test\_code”. Using this mechanism, you can define separate rules for the unit tests. Here’s an example on how it could look:

In the preceding example, the configuration disables the “Code Duplication” rule for unit tests, but keeps the check for any application code. These rules are applied in the CodeScene analysis as well as any PR checks or via the CodeScene CLI.

### Lack Support for a specific Programming Language?[¶](broken-reference)

We continue to add support for more programming languages over time. As always: if you lack support for a language, let us know and we will make it happen.
