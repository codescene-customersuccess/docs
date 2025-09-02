# Auto-Refactor Code

CodeScene has always been great at identifying code smells and prioritizing them. With our AI-based Auto-Refactor capability – CodeScene ACE – we make those insights actionable, too. Better: we also fact-check the AI code to ensure it makes the right thing, saving you a lot of time and guaranteeing that your refactorings are both correct and impactful.

Check out the [full video demo ](https://www.youtube.com/watch?v=AilrTeEiRuo)to see CodeScene ACE in action.

### Integrate Auto-Refactor in your development flow[¶](broken-reference)

1. Enable Auto-Refactor in [CodeScene’s VS Code extension ](https://marketplace.visualstudio.com/items?itemName=CodeScene.codescene-vscode). The VS Code extension will identify the code smells that can be automatically refactored, and indicate them in the IDE. Click on the Auto-Refactor action to inspect and apply a refactoring.
2. Make sure you have installed the local code review tool, [CodeScene CLI tool](broken-reference). When making a commit, CodeScene CLI checks for any new Code Health issues, and offers to Auto-Refactor when applicable/doable. The CLI is the obvious default in case you’re not using VS Code as your editor.

Please note that we have additional IDEs like IntelliJ and Visual Studio on our roadmap, and Auto-Refactor will come to those IDEs too.

**NOTE**: The Auto-Refactor capability is available as a preview release by invitation for all paid CodeScene subscriptions. Sign-up [here ](https://codescene.com/ai)to enable CodeScene ACE for your code.

### Supported Programming languages[¶](broken-reference)

CodeScene’s Auto-Refactor capability is available for the following programming languages:

* JavaScript
* TypeScript

We’ll continue to expand the Auto-Refactor capabilities to languages such as Java, C#, Golang, etc. Missing your favorite language? Feel free to [Contact us ](https://codescene.com/contact-us)with a feature request.

#### Refactoring Scope[¶](broken-reference)

Currently, ACE can Auto-Refactor the following code smells: Large Method, Deep Nested Logic, Bumpy Road, Complex Conditional, and Complex Method. Support for auto-refactoring more code smells will come in subsequent releases. The vision is to support automated fixes of all Code Health issues, so that you can – safely – clean-up any code.

### How is CodeScene ACE different from Copilot and other AI-assistants?[¶](broken-reference)

The first generation of AI-coding tools focused on writing new code. However, the big win is in simplifying software maintenance which accounts for over 90% of a product’s life cycle cost. Specifically, 70% of developers’ time is spent on program understanding, meaning that any improvements which make code easier to grasp will have a high return on investment. This is the purpose of CodeScene ACE.

CodeScene ACE differs from other AI-assistants in two important ways:

1. _Optimize for software maintenance_: ACE lets you improve existing code to make it easier to understand. ACE can also be used on top of other tools like Copilot or CodeWhisperer as a guardrail: that way, new AI-generated code can be checked and – if needed – automatically cleaned-up.
2. _Improve AI to the level of a human expert_: Our benchmarking study, [Refactoring vs Refuctoring ](https://codescene.com/hubfs/whitepapers/Refactoring-vs-Refuctoring-Advancing-the-state-of-AI-automated-code-improvements.pdf), shows that existing AI solutions only deliver correct refactorings in 37% of the cases. That’s unacceptable for software. CodeScene’s fact-checking model is able to validate the proposed code changes, sorting out the good from the bad refactorings.

Simply puy, ACE adds a safety net on top of the AI. That way, you reap the benefits of automation while still giving us – as software people – sane guarantees that we are refactoring, not refuctoring, our code.

#### The Technical Solution: How is this even Possible?[¶](broken-reference)

Using multiple AI-services in only part of the solution. A much more important component is data – to make ACE happen, the CodeScene team relied on high-quality data as the secret sauce:

1. _Better data quality_: The fact-checking model is based on our data lake consisting of +100,000 real-world JavaScript refactoring samples with a known ground truth (i.e. semantically equivalent or not). This enables our algorithms to observe and learn patterns in successfully refactored code.
2. _A gold standard for code quality_: All training data comes from the automated code review capabilities of the CodeScene tool based on the Code Health metric. This is crucial as improvements are objectively measurable. Without this metric, it’s simply not possible to implement a reliable AI refactoring as you cannot tell whether the code improves or just looks different. (See the details in [our research paper ](https://codescene.com/hubfs/whitepapers/Refactoring-vs-Refuctoring-Advancing-the-state-of-AI-automated-code-improvements.pdf)).
3. _Semantic Fact-Checking of the AI_: CodeScene doesn’t attempt to solve semantic equivalence in general. (Doing so would be futile at best). Instead, the fact-checking is tailored to the set of code smells identified via the Code Health metric. That way, we can safely constrain the fact-checking model to a finite number of structural changes that can be learned by our in-house models

At CodeScene, we have always been open and public about the performance of our metrics. Software is important, so we want to make sure you know what you get. We hope you enjoy CodeScene ACE for many years to come!

#### Data Privacy and Security Principles[¶](broken-reference)

Your code is your company’s intellectual property. As such, CodeScene ACE will never use your code as training data for the AI, nor will we persist it to any storage device. Further, only the minimal code snippets necessary for processing are fed to the automatic refactoring service – we never share your complete codebase with an AI.

We also apply industry-standard security measures, including encryption and secure protocols, to protect your code during the analysis process.

Check out our full Privacy Principles for more information.
