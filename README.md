**Clean Code**
===

Clean Code concepts adapted for the Enonic projects.

## **Table of Contents**

1. [Introduction](#introduction)
2. [Git](#git)
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
* [Clean Code TypeScript][6] adaptation by [Labs42][7].

## **Git**

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
 [base-license-url]: http://creativecommons.org/licenses/by-nc-nd/4.0/
[base-license-image]: http://mirrors.creativecommons.org/presskit/buttons/80x15/svg/by-nc-sa.svg
