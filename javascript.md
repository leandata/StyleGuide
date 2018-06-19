# Introduction

This document serves as a guide for LeanData's coding standards in the Javascript programming language.

A chunk or diff of code is described as style-compliant if and only if it adheres to the rules outlined here.

Like other programming style guides, the issues covered span not only aesthetic issues of formatting, but other types of conventions or coding standards as well. However, this document focuses primarily on the hard-and-fast rules that we can follow universally, and avoids giving advice that isn't clearly enforceable (whether by human or tool).

## Context

As LeanData's codebase and engineering team grow, minor variances between styles, even when equally valid, generate minor-to-major inefficiencies. The code velocity of an engineering team depends not only on each individual's skills in writing new code but also on their abilities to understand, review, debug and refactor existing code, all of which are predicated on the readability of the codebase.

As Google's style guide points out, "Every major open-source project has its own style guide: a set of conventions (sometimes arbitrary) about how to write code for that project. It is much easier to understand a large codebase when all the code in it is in a consistent style."

## Scope

The LeanData style guide was created organically, and does not seek to be comprehensively prescriptive. Rather, it is added to and edited as inconsistent styles are discovered and brought up. If an inconsistency in existing code is found, proper responses include adding a new issue or upvoting an existing issue, creating a pull requests with an edit onto the style guide, bringing up the issue in Slack.

The style guide does not seek to be prescriptive towards *existing* code. Instead, the expectation is that any *new* code added into the LeanData codebase is style-compliant. Likewise, editing existing lines of code should **only** make style-compliant the lines **directly** modified.

# General

## Follow [LIFT](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#application-structure-lift-principle):

Create code so that:

**Locate** - others can quickly and intuitively debug and locate related codes

**Identify** - file and variable names should clearly represent the content (don't be afraid of long names, but don't go crazy)

**Flat** - Keep a flat folder structure (7-10 files per folder as a rule of thumb). When exceeding 7-10, consider separation into subfolder, with subfolders representing a well-decoupled sub-feature or functionality.

**Try to stick to DRY** - keep it simple and avoid redundancy when it's obvious. (i.e. intNumberOfEmployees vs. numberOfEmployees, funcProcessData vs. processData) Don't sacrifice readability.

## DRY - Don't Repeat Yourself

For the libraries used by LeanData - LoDash, JQuery - avoid repeating existing functionality.

### Extend Code when Needed
When libraries, UI components or code can be consolidated, shared or extended to accomplish a task, brand new standalone code should not be created.

### Centralize Code when Needed
If code needed exists in a particular component, consider centralizing (floating up) the functionality into a centralized scope. Example areas for possible centralization:
- Validation
- Events handling at window/document/wrapper level
- URL manipulation
- Date/Time handling
- Ajax/Remote calls
- Global settings, configurations and caching

# Formatting

## Braces are used for all control structures

Braces are required for all control structures (i.e. `if`, `else`, `for`, `do`, `while`, as well as any others), even if the body contains only a single statement. The first statement of a non-empty block must begin on its own line.

**Exception**: A simple if statement that can fit entirely on a single line with no wrapping (and that doesn’t have an `else`) may be kept on a single line with no braces when it improves readability. This is the only case in which a control structure may omit braces and newlines.

**Example**: `if (shortCondition()) return;`

## Block indentation: +2 spaces

Each time a new block or block-like construct is opened, the indent increases by two spaces. When the block ends, the indent returns to the previous indent level. The indent level applies to both code and comments throughout the block.

## Statements

Each statement belongs in its own line and should be followed by a semicolon and a line-break.

## Line-Wrapping and Column limit
JavaScript code has a column limit of `80` characters. Any line that would exceed this limit must be line-wrapped. The only exception involves existing code making line-wrapping to the 80-character limit impossible; at that point, the code should line-wrap based on discretion of those involved in the development/review process.

When line-wrapping, each line after the first (each continuation line) is indented at least +4 from the original line, unless it falls under the rules of block indentation.

When there are multiple continuation lines, indentation may be varied beyond +4 as appropriate. In general, continuation lines at a deeper syntactic level are indented by larger multiples of 4, and two lines use the same indentation level if and only if they begin with syntactically parallel elements.

**Note:** While the typical reason for line-wrapping is to avoid overflowing the column limit, even code that would in fact fit within the column limit may be line-wrapped at the author's discretion.

**Tip:** Extracting a method or local variable may solve the problem without the need to line-wrap.

## Horizontal Whitespace
Use of horizontal whitespace depends on location, and falls into three broad categories: *leading* (at the start of a line), *trailing* (at the end of a line), and *internal*. Leading whitespace (i.e., indentation) is addressed elsewhere. Trailing whitespace is **forbidden**.

Beyond where required by the language or other style rules, and apart from literals, comments, and JSDoc, a single internal ASCII space also appears in the following places only.

- Separating any reserved word (such as `if`, `for`, or `catch`) from an open parenthesis (`(`) that follows it on that line.
- Separating any reserved word (such as `else` or `catch`) from a closing curly brace (`}`) that precedes it on that line.
- Before any open curly brace (`{`), with two exceptions:
  - Before an object literal that is the first argument of a function or the first element in an array literal (e.g. `foo({a: [{c: d}]})`).
  - In a template expansion, as it is forbidden by the language (e.g. `abc{%= 1 + 2 %}def`).
- On both sides of any binary or ternary operator.
- After a comma (`,`) or semicolon (`;`). Note that spaces are never allowed before these characters.
- After the colon (`:`) in an object literal.
- On both sides of the double slash (`//`) that begins an end-of-line comment. Here, multiple spaces are allowed, but not required.
- After an open-JSDoc comment character and on both sides of close characters (e.g. for short-form type declarations or casts: t`his.foo = /** @type {number} */ (bar);` or `function(/** string */ foo) {`).

# Language Features

## Local variable declarations

### Use `const` and `let`
Declare all local variables with either `const` or `let`. Use `const` by default, unless a variable needs to be reassigned. The `var` keyword must not be used.

### Use trailing commas
Include a trailing comma whenever there is a line break between the final element and the closing bracket for both array literals and object literals.

Example:
```
const values = [
  'first value',
  'second value',
];
```

### Use `===`
Use type strict checks with `===` as opposed to `==` whenever possible.

### Use single quotes for strings
Quoted values should be in `'single quotes'` so that double quotes may easily exist inside them.

### Do Not Modify `prototype`
Do not modify javascript core functionalities via `prototype`. Necessary changes need to be discussed with the team.

# Best Practices

## Naming

Identifiers use only ASCII letters and digits, and, in a small number of cases noted below, underscores and very rarely (when required by frameworks like jQuery) dollar signs.

Give as descriptive a name as possible, within reason. Do not worry about saving horizontal space as it is far more important to make your code immediately understandable by a new reader. Do not use abbreviations that are ambiguous or unfamiliar to readers outside your project, and do not abbreviate by deleting letters within a word.

```
priceCountReader      // No abbreviation.
numErrors             // "num" is a widespread convention.
numDnsConnections     // Most people know what "DNS" stands for.
```

Illegal:
```
n                     // Meaningless.
nErr                  // Ambiguous abbreviation.
nCompConns            // Ambiguous abbreviation.
wgcConnections        // Only your group knows what this stands for.
pcReader              // Lots of things can be abbreviated "pc".
cstmrId               // Deletes internal letters.
kSecondsPerDay        // Do not use Hungarian notation.
```

## Minimize number of global variables
If absolutely needed for a near-global scope, use `window.foo` or declare variable (`const`/`let`) at the top level without closure. When creating a global variable, it's best to include a a namespace in front of the variable. i.e. `LeanData__globalVariable1`.

## Use JQuery for DOM manipulation
Use JQuery instead of plain Javascript for DOM manipulation.

## Avoid global selectors
Avoid globally selecting elements, especially by classes or attributes, even with JQuery.

Instead of $('.some-class'), do this if you can this.$el.find('.some-class') or `$('#my-wrapper .some-class')

## Avoid browser reflow
Avoid broswer reflow. When possible, toggle classes and show/hide elements instead of adding and removing elements.

## Events Delegation
Use JQuery Event Delegation appropriately to avoid memory leaks.

## Templating
When use lodash and backbone for templating, avoid putting too much logic and looping into the HTML. Try to minimize it toward string output and markup rendering only. Logic should go in the `Backbone.View` or the controller.

# Credits
https://google.github.io/styleguide/jsguide.html
https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md
https://isobar-us.github.io/code-standards/
