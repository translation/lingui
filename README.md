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

**Important Information:**

 * The [Translation.io](https://translation.io) client is directly integrated into
the great [Lingui](https://github.com/lingui/js-lingui) internationalization
framework.

 * This repository only provides additional documentation and a useful
meta-package to simplify the [Lingui](https://github.com/lingui/js-lingui)
installation. You can also refer to the [Lingui documentation](https://lingui.js.org/)
for more advanced features.

----------

Need help? [contact@translation.io](mailto:contact@translation.io)

Table of contents
=================

 * [Translation syntaxes](#translation-syntaxes)
   * [React JSX Syntax](#react-jsx-syntax)
   * [JavaScript Syntax](#javascript-syntax)
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
return <Trans>
  Text to be translated
</Trans>

// Variable Interpolation
return <Trans>
  Hello {name}
</Trans>

// Simple HTML Tags.
// Translators will see "Text with <0>HTML</0> tags"
return <Trans>
  Text with <em>HTML</em> tags
</Trans>

// Complex HTML Tags
// Translators will see "Text with a <0>link</0>"
return <Trans>
  Text with a
  <a href="https://google.com" target="_blank">link</a>
</Trans>

// Context
// Helps translators differentiate translations for the same source text (IDs should be unique)
return <Trans id="meeting someone">
  Date
</Trans>

return <Trans id="moment in time">
  Date
</Trans>
```

#### Plural

```jsx
// Regular
return <Plural
  value={count}
  one="You've got 1 message"
  other="You've got # messages"
/>

// Custom plural forms
return <Plural
  value={count}
  _42="You've got the solution of the universe!"
  one="You've got 1 message"
  other="You've got # messages"
/>

// Variable interpolation
return <Plural
  value={count}
  one={`Hello ${name}, you've got 1 message`}
  other={`Hello ${name}, you've got # messages`}
/>

// HTML tags
return <Plural
  value={count}
  one={<Trans>You've got <strong>1</strong> message</Trans>}
  other={<Trans>You've got <strong>#</strong> messages</Trans>}
/>
```

**Note:** English has only 2 plural forms (`one` and `other`) but other languages
have more of them, from this list: `zero`, `one`, `two`, `few`, `many`,
`other`.

Translators will have the correct list of plural forms proposed directly
in the interface, with examples in their target language.

You can find the complete list of plural forms and plural rules here:
https://translation.io/docs/languages_with_plural_cases

### JavaScript Syntax

#### Singular

```javascript
// Regular
t`Text to be translated`

// Variable Interpolation
t`Hello ${name}`

// Context
// Helps translators differentiate translations for the same source text (IDs should be unique)
t({
   id: "meeting someone",
   message: "Date"
})

t({
   id: "moment in time",
   message: "Date"
})
```

#### Plural

```javascript
// Regular
plural(count, {
  one: "You've got 1 message",
  other: "You've got # messages"
})

// Custom plural forms
plural(count, {
  _42: "You've got the solution of the universe!",
  one: "You've got 1 message",
  other: "You've got # messages"
})

// Variable interpolation
plural(count, {
  one: `Hello ${name}, you've got 1 message`,
  other: `Hello ${name}, you've got # messages`
})
```

**Note:** English has only 2 plural forms (`one` and `other`) but other languages
have more of them, from this list: `zero`, `one`, `two`, `few`, `many`,
`other`.

Translators will have the correct list of plural forms proposed directly
in the interface, with examples in their target language.

You can find the complete list of plural forms and plural rules here:
https://translation.io/docs/languages_with_plural_cases

## Installation

### 1. Install the package

#### Solution 1: Meta-package

Quick way to install Lingui with the correct dependencies.

```bash
# NPM
npm install @translation/lingui

# Yarn
yarn add @translation/lingui
```

#### Solution 2: Fine-Grained Install

More complex but cleaner install, with some packages in development only.

```bash
# NPM
npm install --save-dev @lingui/cli @lingui/macro
npm install --save-dev @babel/core babel-plugin-macros
npm install @lingui/react
```

```bash
# Yarn
yarn add --dev @lingui/cli @lingui/macro
yarn add --dev @babel/core babel-plugin-macros
yarn add @lingui/react
```

### 2. Create a new translation project

Create your new project [from the UI](https://translation.io) and select
the correct source and target languages.

### 3. Configure your project

Copy the `.linguirc` configuration file that was generated for you at the
root of your application.

The configuration file looks like this:

```json
{
  "locales": ["en", "fr", "nl", "de", "es"],
  "sourceLocale": "en",
  "catalogs": [{
    "path": "src/locales/{locale}/messages",
    "include": ["src"]
  }],
  "format": "po",
  "service": {
    "name": "TranslationIO",
    "apiKey": "abcdefghijklmnopqrstuvwxyz012345"
  }
}
```

### 4. Initialize your project and push existing translations to Translation.io with:

```bash
# NPM
npm run extract --overwrite && npm run compile

# Yarn
$ yarn extract --overwrite && yarn compile
```

If you need to add or remove languages in the future, please read our
[documentation](https://translation.io/blog/adding-target-languages) about that.

