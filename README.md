# [Translation.io](https://translation.io/lingui) client for React & JavaScript (using [Lingui](https://github.com/lingui/js-lingui))

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)

Add this package to localize your **React**, **React Native** or **JavaScript** application.

Use this <a href="#react-jsx-syntax">`<Trans>React syntax</Trans>`</a>
 or this <a href="#javascript-syntax">``t`JavaScript syntax` ``</a>.

Write only the source text, and keep it synchronized with your translators on
[Translation.io](https://translation.io/lingui).

<a href="https://translation.io/lingui">
  <img width="720px" alt="Translation.io interface" src="https://translation.io/gifs/translation.gif">
</a>

----------

**Important Information:**

 * The [Translation.io](https://translation.io/lingui) client is directly integrated into
the great [Lingui](https://github.com/lingui/js-lingui) internationalization
framework.

 * This repository only provides additional documentation and a useful
meta-package to simplify the [Lingui](https://github.com/lingui/js-lingui)
installation. You can also refer to the [Lingui documentation](https://lingui.js.org/)
for more advanced features.

----------

Need help? [contact@translation.io](mailto:contact@translation.io)

## Table of contents

 * [Localization syntaxes](#localization-syntaxes)
   * [React JSX Syntax](#react-jsx-syntax)
   * [JavaScript Syntax](#javascript-syntax)
 * [Installation](#installation)
 * [Usage](#usage)
   * [Sync](#sync)
   * [Sync and Purge](#sync-and-purge)
 * [Manage Languages](#manage-languages)
   * [Add or Remove Language](#add-or-remove-language)
   * [Edit Language](#edit-language)
   * [Custom Languages](#custom-languages)
   * [Fallbacks](#fallbacks)
 * [Change the current locale](#change-the-current-locale)
 * [Dynamic loading of .JS translation catalogs](#dynamic-loading-of-js-translation-catalogs)
 * [List of clients for Translation.io](#list-of-clients-for-translationio)
   * [Ruby on Rails (Ruby)](#ruby-on-rails-ruby)
   * [Laravel (PHP)](#laravel-php)
   * [React, React Native and JavaScript](#react-react-native-and-javascript)
   * [Angular](#angular)
   * [Others](#others)
 * [Contributing](#contributing)
 * [License](#license)

## Localization syntaxes

### React JSX Syntax

#### Singular

~~~javascript
import { Trans } from "@lingui/macro"
~~~

~~~jsx
{/* Regular */}
<Trans>
  Text to be translated
</Trans>

{/* Variable Interpolation */}
<Trans>
  Hello {name}
</Trans>

{/* Simple HTML Tags 
   -> Translators will see "Text with <0>HTML</0> tags" */}
<Trans>
  Text with <em>HTML</em> tags
</Trans>

{/* Complex HTML Tags 
   -> Translators will see "Text with a <0>link</0>" */}
<Trans>
  Text with a
  <a href="https://google.com" target="_blank">link</a>
</Trans>

{/* Context 
   -> Helps translators differentiate translations for the same source text (IDs should be unique) */}
<div>
  <Trans id="meeting someone">
    Date
  </Trans>

  <Trans id="moment in time">
    Date
  </Trans>
</div>
~~~

#### Plural

~~~javascript
import { Plural } from "@lingui/macro"
~~~

~~~jsx
{/* Regular */}
<Plural
  value={count}
  one="You've got 1 message"
  other="You've got # messages"
/>

{/* Custom plural forms */}
<Plural
  value={count}
  _0="Your inbox is empty!"
  _42="You've found the ultimate answer"
  one="You've got 1 message"
  other="You've got # messages"
/>

{/* Variable interpolation */}
<Plural
  value={count}
  one={`Hello ${name}, you've got 1 message`}
  other={`Hello ${name}, you've got # messages`}
/>

{/* HTML tags */}
<Plural
  value={count}
  one={<Trans>You've got <strong>1</strong> message</Trans>}
  other={<Trans>You've got <strong>#</strong> messages</Trans>}
/>
~~~

**Note:** English has only 2 plural forms (`one` and `other`), but other languages
have more of them, from this list: `zero`, `one`, `two`, `few`, `many`,
`other`.

Translators will have the correct list of plural forms proposed directly
in the interface, with examples in their target language:

<a href="https://translation.io/lingui">
  <img width="500px" alt="Translation.io plural management" src="https://translation.io/gifs/lingui/translation-plural-forms.png">
</a>

You can find the complete list of plural forms and plural rules here:
[available languages and plural forms](https://translation.io/docs/languages_with_plural_cases)

### JavaScript Syntax

#### Singular

~~~javascript
import { t } from "@lingui/macro"
~~~

~~~javascript
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
~~~

#### Plural

~~~javascript
import { plural } from "@lingui/macro"
~~~

~~~javascript
// Regular
plural(count, {
  one: "You've got 1 message",
  other: "You've got # messages"
})

// Custom plural forms
plural(count, {
  _0: "Your inbox is empty!",
  _42: "You've found the ultimate answer",
  one: "You've got 1 message",
  other: "You've got # messages"
})

// Variable interpolation
plural(count, {
  one: `Hello ${name}, you've got 1 message`,
  other: `Hello ${name}, you've got # messages`
})
~~~

**Note:** English has only 2 plural forms (`one` and `other`) but other languages
have more of them, from this list: `zero`, `one`, `two`, `few`, `many`,
`other`.

Translators will have the correct list of plural forms proposed directly
in the interface, with examples in their target language:

<a href="https://translation.io/lingui">
  <img width="500px" alt="Translation.io plural management" src="https://translation.io/gifs/lingui/translation-plural-forms.png">
</a>

You can find the complete list of plural forms and plural rules here:
https://translation.io/docs/languages_with_plural_cases

## Installation

### 1. Install the package

#### Solution 1: Meta-package

Quick way to install Lingui with the correct dependencies.

~~~bash
# NPM
npm install @translation/lingui

# Yarn
yarn add @translation/lingui
~~~

#### Solution 2: Fine-Grained Install

More complex but cleaner install, with some packages in development only.

~~~bash
# NPM
npm install --save-dev @lingui/cli @lingui/macro
npm install --save-dev @babel/core babel-plugin-macros
npm install @lingui/react
~~~

~~~bash
# Yarn
yarn add --dev @lingui/cli @lingui/macro
yarn add --dev @babel/core babel-plugin-macros
yarn add @lingui/react
~~~

### 2. Add the following scripts (optional)

Add these lines to your `package.json` to make your life easier.

~~~json
{
  "scripts": {
    "sync": "lingui extract --overwrite && lingui compile",
    "sync_and_purge": "lingui extract --overwrite --clean && lingui compile"
  }
}
~~~

### 3. Create a new translation project

Create your new project [from the UI](https://translation.io/lingui) and select
the correct source and target languages.

### 4. Configure your project

Copy the `.linguirc` configuration file that was generated for you to the
root of your application.

The configuration file looks like this:

~~~json
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
~~~

### 5. Setup your application

For React (cf. [React Documentation](https://lingui.js.org/tutorials/react.html) or [React Native documentation](https://lingui.js.org/tutorials/react-native.html)):

~~~jsx
import { i18n } from '@lingui/core'
import { I18nProvider } from '@lingui/react'
import { en } from 'make-plural/plurals'         // Plural rules for English
import { messages } from './locales/en/messages' // English catalog of translations
import Inbox from './Inbox'

i18n.loadLocaleData('en', { plurals: en })
i18n.load('en', messages)
i18n.activate('en')

const App = () => (
  <I18nProvider i18n={i18n}>
    <Inbox />
  </I18nProvider>
)
~~~

For JavaScript (cf. [documentation](https://lingui.js.org/tutorials/javascript.html)):

~~~javascript
import { i18n } from '@lingui/core'
import { en } from 'make-plural/plurals'         // Plural rules for English
import { messages } from './locales/en/messages' // English catalog of translations

i18n.loadLocaleData('en', { plurals: en })
i18n.load('en', messages)
i18n.activate('en')
~~~

### 6. Localize your code

Localize your app using the <a href="#react-jsx-syntax">`<Trans>React syntax</Trans>`</a>
or the <a href="#javascript-syntax">``t`JavaScript syntax` ``</a>.

### 7. Initialize your project

Run the following commands to push your source keys and 
existing translations to Translation.io:

~~~bash
# NPM
npm run sync

# Yarn
yarn sync
~~~

If you need to add or remove languages in the future, please read
[this section](#add-or-remove-language) about that.

## Usage

### Sync

To send new translatable strings and get new translations from Translation.io,
and at the same time generate the minified Javascript catalog files, simply run:

~~~bash
# NPM
npm run sync   # alias of `npm run extract --overwrite && npm run compile`

# Yarn
yarn sync      # alias of `yarn extract --overwrite && yarn compile`
~~~

### Sync and Purge

If you need to remove unused strings from Translation.io, using
the current branch as reference, use the `--clean` option.

~~~bash
# NPM
npm run sync_and_purge   # alias of `npm run extract --overwrite --clean && npm run compile`

# Yarn
yarn sync_and_purge      # alias of `yarn extract --overwrite --clean && yarn compile`
~~~

As the name says, this operation will also perform a sync at the same time.

**Warning:** all strings that are not present in the current local branch will be
**permanently deleted from Translation.io**.

## Manage Languages

### Add or Remove Language

You can add or remove a language by updating `"locales": []` in your
`.linguirc` file, and syncing your project again.

If you want to add a new language with existing translations (ex. if you already have
a translated PO file in your project), you will need to create a
new empty project on Translation.io and init it for the first time again.

### Edit Language

To edit existing languages while keeping their translations (e.g. changing from `en` to `en-US`).

 1. Create a new project on Translation.io with the correct languages.
 2. Adapt `.linguirc` (new API key and languages)
 3. Adapt the language code in the PO directory structure, and also the language header in PO files.
 4. Sync your project for the first time and check that everything went fine.
 5. Invite your collaborators in the new project.
 6. Remove the old project.

Since you created a new project, the translation history and tags will unfortunately be lost.

### Custom Languages

Custom languages are convenient if you want to customize translations for a specific customer
or another instance of your application.

A custom language is always be derived from an [existing language](https://translation.io/docs/languages).
Its structure should be like:

~~~javascript
`${existingLanguageCode}-${customText}`
~~~

where `customText` can only contain alphabetic characters and `-`.

Examples: `en-microsoft` or `fr-BE-custom`.

### Fallbacks

Language fallbacks will work as expected for any regional or custom
language. It means that if the `en-GB` translation is missing,
then it will fallback to `en`. So you only need to translate keys that
are different from the main language when you specialize a language.

Note that fallbacks are chained, so `en-US-custom` will fallback to `en-US` that will
fallback to `en`.

You can find more information about Lingui fallback configuration
[here](https://lingui.js.org/ref/conf.html#fallbacklocales).

## Change the current locale

You can change the current locale by using:

~~~javascript
import { i18n } from '@lingui/core'
import { en } from 'make-plural/plurals'
import { messages } from './locales/en/messages.js'

// [...]

i18n.loadLocaleData('en', { plurals: en })
i18n.load('en', messages)
i18n.activate('en')
~~~

You may be able to detect the default locale of the user, based on many things
like navigator meta tags, HTML language tag, subdomain, path, cookie, etc.

The easiest way to do that would be to use the small
[`@lingui/detect-locale`](https://lingui.js.org/ref/locale-detector.html) package.

~~~javascript
import { detect, fromUrl, fromStorage, fromNavigator } from "@lingui/detect-locale"

// can be a function with custom logic or just a string, `detect` method will handle it
const DEFAULT_FALLBACK = () => "en"

const result = detect(
  fromUrl("lang"),
  fromStorage("lang"),
  fromNavigator(),
  DEFAULT_FALLBACK
)

console.log(result) // "en"
~~~

You will find more information about this package
[here](https://lingui.js.org/ref/locale-detector.html)

## Dynamic loading of .JS translation catalogs

It’s your responsibility to load the correct translation catalog based on the active locale.

There is a clean [dynamic loader helper](https://lingui.js.org/guides/dynamic-loading-catalogs.html)
that will assist you with this task.

~~~typescript
// i18n.ts

import { i18n } from '@lingui/core';
import { en, cs } from 'make-plural/plurals'

export const locales = {
  en: "English",
  cs: "Česky",
};
export const defaultLocale = "en";

i18n.loadLocaleData({
  en: { plurals: en },
  cs: { plurals: cs },
})

/**
* We do a dynamic import of just the catalog that we need
* @param locale any locale string
*/
export async function dynamicActivate(locale: string) {
  const { messages } = await import(`./locales/${locale}/messages`)
  i18n.load(locale, messages)
  i18n.activate(locale)
}
~~~

Please read more about this loader [here](https://lingui.js.org/guides/dynamic-loading-catalogs.html).

## List of clients for Translation.io

The following clients are officially supported by [Translation.io](https://translation.io)
and are well documented.

Some of these implementations (and other non-officially supported ones)
were started by contributors for their own translation projects.
We are thankful to all contributors for their hard work!

### Ruby on Rails (Ruby)

Officially supported on [https://translation.io/rails](https://translation.io/rails)

 * GitHub: https://github.com/translation/rails
 * RubyGems: https://rubygems.org/gems/translation/

Credits: [@aurels](https://github.com/aurels), [@michaelhoste](https://github.com/michaelhoste)

### Laravel (PHP)

Officially supported on [https://translation.io/laravel](https://translation.io/laravel)

 * GitHub: https://github.com/translation/laravel
 * Packagist: https://packagist.org/packages/tio/laravel

Credits: [@armandsar](https://github.com/armandsar), [@michaelhoste](https://github.com/michaelhoste)

### React, React Native and JavaScript

Officially supported on [https://translation.io/lingui](https://translation.io/lingui)

Translation.io is directly integrated in the great
[Lingui](https://lingui.js.org/) internationalization project.

 * GitHub: https://github.com/translation/lingui
 * NPM: https://www.npmjs.com/package/@translation/lingui

### Angular

Officially supported on [https://translation.io/angular](https://translation.io/angular)

 * GitHub: https://github.com/translation/angular
 * NPM: https://www.npmjs.com/package/@translation/angular
 
Credits: [@SimonCorellia](https://github.com/SimonCorellia), [@didier-84](hthttps://github.com/didier-84), [@michaelhoste](https://github.com/michaelhoste)

### Others

If you want to create a new client for your favorite language or framework, please read our
[Create a Translation.io Library](https://translation.io/docs/create-library)
guide and use the special
[init](https://translation.io/docs/create-library#initialization) and
[sync](https://translation.io/docs/create-library#synchronization) endpoints.

You can also use the more [traditional API](https://translation.io/docs/api).

Feel free to contact us on [contact@translation.io](mailto:contact@translation.io)
if you need some help or if you want to share your library.

## Contributing

This is a dumb meta-package that doesn't need any contribution.

If you want to contribute, please refer to
[the official Lingui CONTRIBUTING.md](https://github.com/lingui/js-lingui/blob/main/CONTRIBUTING.md)
file.

## License

This meta-package is released under MIT license.

The Lingui MIT License is located here [here](https://github.com/lingui/js-lingui/blob/main/LICENSE)

(c) [https://translation.io](https://translation.io) / [contact@translation.io](mailto:contact@translation.io)
