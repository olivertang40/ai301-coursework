I contributed a code-style configuration to AUCTOR, an open-source Python project, and the maintainer merged it. I found the issue using a search assistant I built and then improved after it made two mistakes.

The project had no shared linter, which is a tool that automatically flags style problems and common bugs. Before writing anything, I asked the maintainer which linter they preferred. When my first run found 34 existing problems in the code, I kept my change small and said so plainly instead of rewriting files nobody had asked about. The maintainer tested it and suggested one improvement. I added it the same day, and they merged the pull request.

What I learned about how I work:
🔹 Ask the maintainer before building. One question saved a wrong guess.
🔹 Say what your change doesn't do as well as what it does.
🔹 Fix your tools when they fail. My search assistant once recommended spam and once recommended an issue that was already closed. Each mistake became a new check.

Pull request: https://github.com/bleedZzzz/auctor/pull/33

#OpenSource #Python #SoftwareEngineering #LearningInPublic
