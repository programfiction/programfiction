## C# coding and review guidelines
A code review can provide value towards your `design, techniques, patterns, approach` etc. There are numerous guidelines and best practices software development 
teams follow. However, I want to assure you that all the guidelines mentioned below will help any individual to practice and apply good coding principles and perform
a quality code review. Feel free to add any specific guidelines that you think is necessary. 

# Let's begin with `C#`  code review guidelines.
I have worked in various teams settings and work environments. Many times I have been invited to perform a code review for a friend who is not part of my team or rather
I am not part of their team. But what I admire and appreciate here is the fact that someone reached out to another dev/architect in case their team's developers is
either not available or busy with critical production issues. Such a mindset empowers the team to deliver the best written code. 
- Use of `SonarLint` (is an IDE extension) that helps you detect and fix quality issues as you write code. Lke a spell checker, SonalLint squiggles  flaws so that
  they can be fixed before committing code
  - Read more: [Sonar Lint addon Vs2019 ](https://marketplace.visualstudio.com/items?itemName=SonarSource.SonarLintforVisualStudio2019)
  - Sonar Analyzer: `C#` nuget package manager
- Try to code & review in terms of `Code Reusability, Code Consistency & Code Readability`.
- Write comments on top of all methods to describe their usage and expected input types and return type information.
- Avoid straight forward copy paste of code from other sources. 
- Mange sure there should not be any project warnings, treat warning as error. It will be much better if `Code Analysis(style cop & fx cop)` is performed on a project.
- Try to code & review in terms of `Code Reusability, Code Consistency & Code Readability`.
- Write comments on top of all methods to describe their usage and expected inpt types and return type information.
- Avoid straight forward copy paste of code from other sources. 
- Mange sure there should not be any project warnings, treat warning as error. It will be much better if `Code Analysis (style cop & fx cop)` is performed on a project.
- Its not enough to deliver well written functional code. A well defined project and file name is equally important and brings a lot  of clarity. 
  	- Generally variables/parameters follow `camel casing` and methods /class names use `pascal casing`
-Unit testing: 



