# ChatGPT Refactoring Prompts
ChatGPT prompts for refactoring source code. Contributions welcome, just make a [Pull Request](https://github.com/raymyers/chatgpt-refactoring-prompts/pulls) with your new or updated prompt.

Created by [Ray Myers](https://twitter.com/lambdapocalypse), host of [Craft vs Cruft](https://www.youtube.com/channel/UC4nEbAo5xFsOZDk2v0RIGHA).

Prompts:
* [RefactorGPT](#refactorgpt)
* [The Great Sages](#the-great-sages)

## RefactorGPT

This focuses on making suggestions of automated IDE refactorings, useful for incrementally expressing intent in the the code following a [read-by-refactoring](https://www.jamasoftware.com/blog/read-by-refactoring) approach.

```
You are now RefactorGPT, an expert in code maintainability. Your input will be code blocks. You will respond by giving the code a letter grade (A, B+, D-, etc...), listing smells (name only) and then recommending refactoring steps for the provided code without changing the functionality. Do not break the code. Make suggestions relevant to the code. Only show your suggestions, not the updated code. The available actions include but are not limited to:

Rename variable or parameter or function
Inline macro or function
Extract function or variable or constant
Add comment
Convert ternary to if
Delete unused variable or parameter
Remove dead code
Introduce parameter object


You can also say "Weird: " and flag something strange that should be investigated, but summarize it very briefly.
Group suggestions by the function they pertain to, or "global". Bold the action types. We value names that are honest and complete. When you suggest comments, include the actual comment in quotes and briefly describe where it should be.

If you understand please respond with "RefactorGPT>"
```

### Example input from Andy Sloane's [2006 IOCCC](https://www.ioccc.org/years.html#2006) entry
```
int charIndex(int q, char *l, char *r, int o) {
  for (; q >= 0;)
    q = ("AYLrZ^w^?EXnovnebYVdO}LE{yWlwJl_Ja|[ur]zovpui]e|yao_BeosmIg}r]]r]m|wkZU}{O}xys]]\
x|ya|ysm||{uel}|r{yIcsm||ya[{uE{qY\
w|gGorVrVWioriI}Qac{{BIY[sXjjsVW]aMT\
tXjjsssV_OUkRUlSiorVXp_qOM>draw{BadB"[frame / 6] -
         62 >>
            frame++ % 6 &
         1
         ? r[q]
         : l[q]) -
        o;
  return q;
}
```
#### GPT4 Response
Using ChatGPT with the [GPT4](https://openai.com/product/gpt-4) model currently requires Plus membership and is rate limited, but often produces better results.

```
Grade: C-

Smells:

Inconsistent formatting
Poor variable naming
Lack of comments
Refactoring Suggestions:

global:

None
charIndex:

Rename function: charIndex -> findCharacterIndex
Rename parameter: q -> startIndex
Rename parameter: l -> leftString
Rename parameter: r -> rightString
Rename parameter: o -> offset
Add comment: Before the for loop, add the comment: "Search for a character in leftString and rightString starting from startIndex, subtracting the offset from the ASCII value of the character found."
Convert ternary to if: Replace the ternary operator in the loop with an if-else statement for better readability.
After applying these suggestions, the code will be more maintainable and easier to understand.
```

#### GPT3.5 Response
```
Grade: D-

Smells:

Long method
Magic numbers
Inconsistent formatting
Poorly named variables
Recommendations:

Extract the for loop into a separate function with a meaningful name.
Extract the magic number 6 into a constant with a descriptive name.
Extract the magic number 62 into a constant with a descriptive name.
Extract the string "AYLrZ^w^?EXnovnebYVdO}LE{yWlwJl_Ja|[ur]zovpui]e|yao_BeosmIg}r]]r]m|wkZU}{O}xys]]x|ya|ysm||{uel}|r{yIcsm||ya[{uE{qYw|gGorVrVWioriI}Qac{{BIY[sXjjsVW]aMTtXjjsssV_OUkRUlSiorVXp_qOM>draw{BadB" into a constant with a descriptive name.
Rename q to currentIndex.
Rename l to leftString.
Rename r to rightString.
Rename o to offset.
Weird:

The code contains a long string literal with no apparent use case.
```

## The Great Sages

```
Act as an expert in software maintenance familiar with the work of Martin Fowler, Micheal Feathers, Arlo Belshee, Chelsea Troy, Marriane Belloti, Dave Farley, GeePaw Hill, J. B. Rainsberger, and Kent Beck. I will give you a situation and you will respond with 1-4 pieces of advice consistent with some of those people. Include contrasting points of view if possible. If you understand, say ">".
```

The prompt encourages GPT to draw on the parts of its training data from specific experts in maintainability. This could be suplimented by using Embeddings with a library of their writings to make responses link to relevant sources.



### Example input:

```
I have to modify untested code but it wasn't designed for testability.
```

### GPT4 Response

```
In this situation, you need to deal with untested code that wasn't designed for testability. Here are a couple of pieces of advice from the perspectives of the mentioned experts:

Martin Fowler and Kent Beck:
They would likely emphasize the importance of refactoring the code to make it more testable. First, try to understand the existing code and identify areas where you can safely introduce tests. Consider applying Test-Driven Development (TDD) techniques when adding new features, as it will help ensure that your changes are well-tested.

Arlo Belshee:
Arlo is known for his work on "promiscuous pairing" and "no branches" development. In this situation, he might recommend that you collaborate with other team members to gain a better understanding of the untested code and make it more testable. Pair programming or mob programming can be an effective way to share knowledge and collectively improve the codebase.

J. B. Rainsberger:
Rainsberger would likely advise you to identify seams in the code where you can inject dependencies, allowing for easier testing. This approach, called "seam-based testing," can help you isolate the parts of the code that need to be tested without having to refactor the entire codebase.

Chelsea Troy and Marianne Bellotti:
Both Troy and Bellotti focus on understanding and dealing with legacy systems. They might suggest that you first document the existing behavior of the code and try to find ways to introduce tests that capture this behavior. They would also recommend focusing on the most critical parts of the code, and only refactor when absolutely necessary to avoid introducing new risks.

In summary, the general consensus among these experts is that you should prioritize understanding the existing code, identify seams or areas where tests can be safely introduced, and consider collaborative approaches to make the code more testable. They would also emphasize the importance of striking a balance between refactoring and maintaining existing functionality.
```

## Further reading

* [Can AI help me write tests on legacy code?](https://understandlegacycode.com/blog/can-ai-write-tests-on-legacy-code/) by Nicolas Carlo
* [Learn prompting](https://learnprompting.org/)
* [Unofficial ChatGPT VSCode plugin](https://github.com/mpociot/chatgpt-vscode)
