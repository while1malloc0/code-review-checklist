# Code Review Checklist

## What is this?

A checklist to be used during code review. Each of headers is a "pass", or theme with accompanying questions to ask about the code. The passes are divided up into "every time" and "for more depth". "Every time" passes should be completed, as you might guess, every time. If there are any red flags on these items *don't proceed to the* for more depth *section*. The "every time" passes are meant to establish the high level goals and context for the PR, and if one of those items has a red flag, commenting on deeper issues is superfluous information. Put another way, if someone's PR has a fundamental logic flaw, commenting on their indentation isn't helpful. Each of the passes is presented with justification and discussion. Skip to the bottom for a copyable list.

**Note:** This list is meant to be customized and adapted to the user's personal use case and tastes. There's no attempt made at being comprehensive, and several opinions are built into this list. Take what works for you, change what you need to, and drop what you don't need.

## The Passes

## Every time

### Sizing Up

What is the general shape of the PR? i.e. Is it a completely new feature, a refactor, a one line change?

**Justification:** Knowing what kind of PR you're looking at will help you to gather your thoughts and put you in a different mindset in terms of what to look for. For instance, new features might need more scrutiny, and thus require a lot of time to review. Refactors should have a goal state that they are enabling, and should be scrutinized in that light.

Is the PR the right size?

**Justification:** Extremely large PRs are hard to reason about, and can easily overflow the number of items that humans can easily keep in their head. Don't be too picky about the size of the PR, but if it's too large for you to review, it's probably too large for others to review. Ask the author to break it up into more manageable PRs.

### Context

What is this PR trying to accomplish?

**Justification:** We should know what the code is attempting to do. Hopefully this is provided in the PR message.

Why is this PR trying to accomplish that?

**Justification:** Code must be maintained, and should have good reason for existing.

### Relevance

Is the change made to this PR necessary?

**Justification:** Sometimes we write code in a way that is short sighted or we don't have the full context of the problem that we're trying to solve. In these cases, we might write code that seems necessary, but in reality is superfluous. It's the job of the reviewer to call out unnecessary changes as such.

Does this PR duplicate existing functionality?

**Justification:** Sometimes we write code to solve a problem that we believe to be novel, when in reality there is already an existing solution for it. If the reviewer sees functionality duplication, they should ask the author why the existing solution wasn't used. In some cases, the existing solution may not solve 100% of the problem; in that case, encourage the developer to contribute to that code base where possible.

Are there others that should be aware of this PR?

**Justification:** If other developers or teams have a vested interest in the health of the code base that's under review, they should be notified of large or potentially breaking changes that are currently being considered.

## For more depth:

### Readability

Would a person who knows the language but not the codebase be able to read the code?

**Justification:** At some point, a new member of an engineering organization will have to read the code that's being reviewed. Making sure that the code is reasonably readable to newcomers will ease their onboarding process, and improve the overall maintainability of the codebase.

Are any esoteric language features used?

**Justification:** Esoteric language features often make a trade off between expressive syntax and readability. The reviewer should acknowledge that trade off, and ask if the expressive syntax is worth the reduction in readability for the general case.

### Production Readiness

How do we know when this code breaks?

**Justification:** Code breakage should have some means of alerting the people who care about it. If nobody cares about it, the code probably doesn't need to exist in the first place.

Are any documentation changes or additions required by this change?

**Justification:** Documentation often becomes out of date with code because they are not updated at the same time. Asking oneself if a documentation change is warranted by the code being reviewed helps ensure that this drift is minimal.

Is there a method for validating that this program works as expected? (i.e. tests)

**Justification:** In most cases, manual testing is not enough to inspire confidence in code. There should be automatic means of verifying that the code accomplishes what it says that it will. Generally this means unit tests, but may include integration tests, property tests, contract tests, a formal method specification, or other automatic verification methods.

Is this change reasonably secure?

**Justification:** Security is hard, and not everyone can be a security expert. However, knowing how to spot code that introduces common application vulnerability is an invaluable skill. For example, a reviewer for database code should know how to spot a SQL injection vulnerability being introduced.

### Naming

Do names communicate what things do?

**Justification:** Code with confusing or misleading variable names is hard to read. See the justification for Readability above.

Are the names of things idiomatic to the language?

**Justification:** Unidiomatic names significantly impact someone's ability to read code, as it introduces unnecessary cognitive noise.

Do names leak implementation details?

**Justification:** Similar to the above, names that leak implemenation details increase the cognitive overhead required to read code. The most common case of this is including unnecessary type descriptions in names, e.g. `ipArray` instead of `ips`.

### Gotchas

What are the ways in which new or changed code can break?

**Justification:** Asking how code can break while it's being reviewed will help find error cases before the code goes to production.

Is this code subject to any common programming gotchas? (i.e. transposition errors, off by one errors, etc.)

**Justification:** There are programming errors that are generally agnostic of language, such as transposition errors, off by one errors, null pointer dereferences, etc. The reviewer should have a short list of these and make sure that the code isn't accidentally falling into any of the pitfalls.

Is the spelling of variable names, comments, etc. correct and consistent?

**Justification:** Correct and consistent spelling, especially of variable/method/etc names is important for code searchability.

### Language Specific

Is the code idiomatic to the language?

**Justification:** Unidiomatic code is hard to read for regular users of the langauge.

Are there new language usage patterns being introduced?

**Justification:** Patterns (reusable bits of code that solve common problems) in code are often copied. If a new pattern is being introduced, you should assume that it will be copied, and ask if that's ok. Similarly, if a new pattern is being introduced to solve a problem that already has a prescribed pattern, you should point out the prescribed pattern.

Does the code fall into any common pitfalls of the language?

**Justification:** Every language has its unergonomic aspects. Code reviewers who are fluent in a language should have a list of these rough edges, and be able to spot if the author has run into any of these.

## The Copyable Version

Every time:
* Sizing Up
  - What is the general shape of the PR?
  - Is this PR the right size?
* Context
  - What is this PR trying to accomplish?
  - Why is this PR trying to accomplish that?
* Relevance
  - Is the change made to this PR necessary?
  - Does this PR duplicate existing functionality?
  - Are there others that should be aware of this PR?

For more depth:
* Readability
  - Would a person who knows the language but not the codebase be able to read the code?
  - Are any esoteric language features used?
* Production Readiness
  - How do we know when this code breaks?
  - Are any documentation changes or additions required by this change?
  - Is there a method for validating that this program works as expected? (i.e. tests)
  - Is this change reasonably secure?
* Naming
  - Do names communicate what things do?
  - Are the names of things idiomatic to the language?
  - Do names leak implementation details?
* Gotchas
  - What are the ways in which new or changed code can break?
  - Is this code subject to any common programming gotchas? (i.e. transposition errors, off by one errors, etc.)
  - Is the spelling of variable names, comments, etc. correct and consistent?
* Language Specific
  - Is the code idiomatic to the language?
  - Are there new language usage patterns being introduced?
  - Does the code fall into any common pitfalls of the language?
