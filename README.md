# [Translation.io](https://translation.io) client for React & JavaScript (using [Lingui](https://github.com/lingui/js-lingui))

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)

Add this package to localize your **React** or **JavaScript** application.

Use this <a href="#react-jsx-syntax">`<Trans>React syntax</Trans>`</a>
 or this <a href="#javascript-syntax">``t`JavaScript syntax` ``</a>.

Write only the source text, and keep it synchronized with your translators on
[Translation.io](https://translation.io).

<a href="https://translation.io">
  <img width="720px" alt="Translation.io interface" src="https://translation.io/gifs/translation.gif">
</a>

----------

**Important Note:**

 * The [Translation.io](https://translation.io) client is directly integrated into
the popular [Lingui](https://github.com/lingui/js-lingui) internationalization
framework.

 * This repository only provides additional documentation and a dumb
meta-package to simplify the [Lingui](https://github.com/lingui/js-lingui)
installation. You can also refer to the [Lingui documentation](https://lingui.js.org/)
for more advanced features.

----------

Need help? [contact@translation.io](mailto:contact@translation.io)

Table of contents
=================

 * [Translation syntaxes](#translation-syntaxes)
   * [React JSX Syntax](#i18n-yaml)
   * [JavaScript Syntax](#gettext)
 * [Installation](#installation)
 * [Usage](#usage)
   * [Sync](#sync)
   * [Sync and Show Purgeable](#sync-and-show-purgeable)
   * [Sync and Purge](#sync-and-purge)
 * [Manage Languages](#manage-languages)
   * [Add or Remove Language](#add-or-remove-language)
   * [Edit Language](#edit-language)
   * [Custom Languages](#custom-languages)
   * [Fallbacks](#fallbacks)
 * [Change the current locale](#change-the-current-locale)
   * [Globally](#globally)
   * [Locally](#locally)
 * [Contributing](#contributing)
 * [List of clients for Translation.io](#list-of-clients-for-translationio)
   * [Ruby on Rails (Ruby)](#ruby-on-rails-ruby)
   * [Laravel (PHP)](#laravel-php)
   * [Others](#others)
 * [License](#license)

## Translation syntaxes

### React JSX Syntax

#### Singular

```jsx
// Regular
<Trans>Text to be translated</Trans>

// Variable Interpolation
<Trans>Hello {name}</Trans>

// Simple HTML Tags
<Trans>One sentence with <em>HTML</em> tags</Trans>

// Complex HTML Tags
<Trans>One sentence with a <a href="https://google.com" target="_blank">link</a></Trans>

// Comment for translators
<Trans comment="comments for translators">One sentence</Trans>

// Context (to allow different translations for the same source text)
<Trans id="my context">One sentence</Trans>
```

#### Plural

=> see forms and rules here: https://translation.io

```jsx
// Pluralization
<Plural
  value={count}
  one="You've got 1 message"
  other="You've got # messages"
/>

// Custom plural forms
<Plural
  value={count}
  _42="You've got the solution of the universe!"
  one="You've got 1 message"
  other="You've got # messages"
/>

// Complex plural forms with interpolation
<Plural
  value={count}
  one={`Hello ${name}, you've got 1 message`}
  other={`Hello ${name}, you've got # messages`}
/>

// Complex plural forms with HTML tags
<Plural
  value={count}
  one={<Trans>You've got <strong>1</strong> message</Trans>}
  other={<Trans>You've got <strong>#</strong> messages</Trans>}
/>

// Add plural with id and comments?
```

### JavaScript Syntax

#### Singular

```javascript
// Regular
t`Text to be translated`

// Variable Interpolation
t`Hello ${name}`

// Comment for translators
t({
   id: "msg.refresh",
   message: "One inline sentence with an id"
})

// Context (to allow different translations for the same source text)
```

#### Plural

```javascript
plural(count, {
  one: "one inline plural sentence without id",
  other: "# inline plural sentences without id"
})
```

