**Clean Code**
===

Clean Code concepts adapted for the Enonic projects.

## **Table of Contents**

1. [Introduction](#introduction)
2. [Git](#git)
   * [Commits](#commits)
   * [Pull Requests](#pull-requests)
3. [TypeScript](#typescript)
   * [Variables](#variables)
   * [Functions](#functions)
   * [Classes](#classes)
3. [CSS](#css)
<br/> [License](#license)

## **Introduction**

While the original Robert C. Martin's book [_Clean Code_][3] represents a guide to producing readable, reusable, and refactorable code, this document will also describe the principles of creating compatible applications for the [Enonic][1] [XP][2]. Some parts of this document can be used as a style guide since it touches not only the TypeScript, but also a CSS, application structure, and even Git commits.

It's recommended to read the following first:

* [Clean Code][3] by Robert C. Martin;
* [Clean Code JavaScript][4] adaptation by [Ryan McDermott][5];
* [Clean Code TypeScript][6] adaptation by [Labs42][7];
* [Pro Git][8] Book;
* [Git Commit][9] article by [Chris Beams][10].

## **Git**

This part describes the rules of the Enonic workflow while working with Git. For the detailed overview of the basic commit principles see the separate [article][9].

## Commits

### Use issue title as commit subject

**Bad:**

```bash
git commit -m "Changes to confirmation dialog"
```

**Good:**

```bash
git commit -m "Confirmation not working #77"
```

### Non-task commit subject must be short, descriptive, and neutral

:warning: Avoid non-task commits.

The sentence "*Applying this commit will* \*commit subject\*" must make sense.

**Bad:**

```bash
git commit -m "fixed console errors."
```

**Good:**

```bash
git commit -m "Fix exception on dialog initial load"
```

## Pull Requests

### Add the same person to Reviewers and Assignees lists

When you create a Pull Request and know exactly who should review it, add this person both to the Reviewers and Assignees lists.

**Bad:**

```
Reviewers:
  - John Smith

Assignees:
```

**Good:**

```
Reviewers:
  - John Smith

Assignees:
  - John Smith
```

### Add at least two reviewers

When you create a Pull Request consider adding at least two reviewers to it, and avait both to complete a review. It is not always possible but desireable for team knowlage sharing.

**Bad:**

```
Reviewers:
  - John Smith
```

**Good:**

```
Reviewers:
  - John Smith
  - Jaine Doe
```

### Pool request for a bugfix

First bugfix pool request should always be issued for the master branch (bugfix branch should have a name `issue-{issue#}` ex. `issue-1234`).
After Pool Request was approved and merged into master branch create separate pool request for all version branches this fix should be applied to (branches should have a name `issue-{issue#}-{version#}` ex. `issue-1234-7.3`)
Bugfix pool request must be one-commit. Sqash miltiplie commits into one before and after Pool request review adjustments.

Example: Bug #8225 has to be fixed in supported versions 6.15, 7.2 and 7.3

- Create a branch issue-8225 based on master
- Create a PR from issue-8225 branch
- Assign reviewers
- Wait for reviewes to approve PR
- Rebase and merge PR into master. Delete branch if not deleted automatically.
- Create a backprot branch `issue-8225-6.15` based on 6.15 version branch and PR with a fix
- Create a backprot branch `issue-8225-7.2` based on 7.2 version branch and PR with a fix
- Create a backprot branch `issue-8225-7.3` based on 7.3 version branch and PR with a fix
- Assign repository owner (administrator) for review on each PR
- Owners rebase merge and delete individual PRs into corresponding version branches.

## **TypeScript**

## Variables

### Use verbs at the beginning of the boolean variable names

This rule works exactly the opposite for class or object properties.

**Bad:**

```typescript
const enabled = this.hasClass('enabled');
const updatable = input != null && !input.disabled;
```

**Good:**

```typescript
const isEnabled = this.hasClass('enabled');
const canBeUpdated = input != null && !input.disabled;
```

## Functions

--

## Classes

### Use Object to pass several parameters to the constructor

When passing more than 3 parameters to the `constructor` (more than 2, if there are at least one optional parameter), use the configuration object.

**Bad:**

```typescript
class ModalDialog {
  constructor(title: string, className?: string, closeCallback?: () => void) {
    // ...
  }
}

const closeCallback = () => { /* do something */ };
const dialog = new ModalDialog(title, null, closeCallback);
```

**Good:**

```typescript
interface ModalDialogConfig {
  title: string;
  className?: string;
  closeCallback?: () => void;
}

class ModalDialog {
  constructor(config: ModalDialogConfig) {
    // ...
  }
}

const title = 'My Dialog';
const closeCallback = () => { /* do something */ };

const dialog = new ModalDialog({title, closeCallback});
```

## **CSS**

## **License**

[MIT](LICENSE) © [Enonic][1]

<!-- Links -->

[1]: https://enonic.com/
[2]: https://enonic.com/products/enonic-xp
[3]: https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882
[4]: https://github.com/ryanmcdermott/clean-code-javascript
[5]: https://github.com/ryanmcdermott
[6]: https://github.com/labs42io/clean-code-typescript
[7]: https://github.com/labs42io
[8]: https://git-scm.com/book/
[9]: https://chris.beams.io/posts/git-commit/
[10]: https://github.com/cbeams
 [base-license-url]: http://creativecommons.org/licenses/by-nc-nd/4.0/
[base-license-image]: http://mirrors.creativecommons.org/presskit/buttons/80x15/svg/by-nc-sa.svg
