# Front end code convention

The wordings “must”, “must not”, “should”, “should not” is to be interpreted as <http://www.ietf.org/rfc/rfc2119.txt>

## General

* All files must be delivered as UTF-8 with unix line endings.
* Code must use four spaces for indentation.
* No whitespace at end of lines.
* All function names, variables, classes etc. must be in English.

## HTML

### General

* We use the HTML5 doctype, and all markup must comply with this.
* You must make sure that newer HTML5 structures work in all browsers we support - polyfills may be used after careful consideration of gain vs. performance.
* You must quote attributes using `""` and must always use lowercase tags and attributes.
* You must not have spaces between attribute and value.
* No `<br />` but `<br>` and no `<img />` but `<img>`
* There must not be any inline styling. Move it to css files no matter how small.
* There must not be any inline scripting. Move it to js files no matter how small.
* Block level  elements that are “row-like” (bootstrap: class=”row”) should be seperated by empty lines for readability.

### Naming

* Multi-word class names and data names must be spinal-cased instead of camelCased.
* CSS and JS must not be bound to the same class. Create separate classes that you bind javascript to, and prefix javascript hooks with `js-`, eg. `<input type=”submit” class=”btn js-submit-btn” … >`.

### Indentation

* Child nodes must be indented with four spaces.
* In case of much indentation, you should put a comment after a closing div tags stating what div it is closing.

### Semantics

* Element use must correspond with the intention. A div is not a link. A paragraph of text is within `<p>` and not separated by `<br><br>`
* Class names should reflect what they are rather than what their styling look like.
* Labels must be associated to their corresponding form fields using for and id attributes
* Tables must not be used for layout. Tables are for tabular data.
* Tables should have thead and tbody.
* All images must have an alt attribute. Use `alt=””` for presentational images.

## CSS and SCSS

* CSS ruleset anatomy: Selector(s) must be followed by one space and a curly open brace. Property and value pairs are on seperate lines, indented with four spaces and with one space between : and value. You must always end property and value pairs with a semicolon.<br>
`[selector(s)] {`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`[property]: [value];`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`[property]: [value];`
* Related selectors should be on the same line (seperated with space after comma), and unrelated on separate lines:<br>
`.some-selector, .some-selector--foo,`<br>
`.another-selector {`<br>
&nbsp;&nbsp;&nbsp;&nbsp;`...`<br>
`}`
* You should think in reusability and objects whenever writing your styles.
* You should use BEM notation whenever possible.<br>
BEM - meaning _block, element, modifier_ - is a class naming pattern that encourages you to think in reusable objects.
  * Block: Standalone entity that is meaningful on its own. Think this like: person.<br>Written as `class=”person”`
  * Element: Parts of a block that have no standalone meaning. Think this like: hand on a person. <br>Written as `class=”person__hand”`
  * Modifier: Flags on block. Use them to change appearance or behavior. Think this like: person that is female.<br>Written as `class=”person--female”`<br>
  * If you are unfamilar with the pattern, read <http://bit.ly/1qvURwR>
* You should not use id’s in selectors as it reduces reusability and complicates specificity. Doesn’t matter if there is already an id and you want to style the element. The id is probably there as a javascript hook. Add a class and style that.
* You should scope reasonably and think about the specificity, performance and reach of selectors. `.widget-title` is a more maintainable selector than `.widget h2`, which is too broad. And `.article-meta` is much, much better than `html > body > section.content > article span.meta`. Be extra careful of this when writing your SCSS.
* You should avoid deep nesting of your style rules, as it minimizes reusability. Be extra careful of this when writing your SCSS.
* You should not qualify selectors with tag name, eg. do not write table.something
* You must only use `!important` proactively. This means that it must not be used to override a selector problem (fix that instead), but only to ensure that a rule always wins. Eg. if you always want error messages to be red.
* You must use px or rem for font size.
* Styling must be “mobile first”: baseline is always smallest displays; then add styling for larger displays in media queries: `@media (min-width: $screen-sm-min)` etc. Not the other way around (`@media (max-width: $screen-xs-max`). We should demand mobile first material from our designers.
* You should not worry about displays with a width of less than 320 pixels.
* You must place browser specific styles in includes/_shame.scss.<br>
* All SCSS files which should be imported, should be prefixed with `_`, ex. `_included_file.scss`.<br>
* Included files needs to be imported in correct order depending on when it's needed.
* Hex colors must be lowercased.
* Code must be able to pass through our stylelint setup without errors.

## Javascript

* Javascript files must be lowercase and use underscore as word separator. View specific files must follow the name of the view.
* You must always declare your variables with var to avoid placing variables in the global context.
* You should declare variables using one var statement in the top of your function.
* You must use `NAMES_LIKE_THIS` for faux constant vars (pre ES2015)
* Variable names must be `camelCased`.
* Class names must be in `BumpyCaps`.
* You should use `'` over `"`
* You should use `===` and `!==` instead of `==` and `!=`.
* Each line should contain at most one statement.
* You must always use semicolons. Also at the end of function expressions (but not at the end of function declarations).
* You must not write function declarations within blocks (eg. inside an if statement).
* Opening braces must not be on its own line. Closing braces must be on its own line.
* Control structure keywords (`if`, `while` etc.) must have one space after them. Method and function calls must not.
* Parentheses in control structures must never have space after the opening or a space before the closing.
* Parameters and arguments must have a space after comma. `(foo, bar)`
* There must be spaces between `?` and `:` in a ternary operator statement.
* There must be spaces between operators `+ - * /` etc.
* Deletion should be executed using `something.foo = null` instead of `delete something.foo`.
* `eval()` is dangerous and should not be used unless you have a really, really good reason.
* For long strings, you should concatenate lines and not use multiline string literals (“\”).
* Define arrays and objects using `[]` and `{}` instead of `new Array()` and `new Object(`).
* You must never override built in prototypes, eg. `Array.prototype`.
* Code must be able to pass through ESLint: <http://eslint.org/>. For JustCasino, we lint through webpack.
* You should group logically related pieces of code using newlines.
* You should not use for-in-loop to iterate over arrays. It may break if there is something unexpected in the prototype. Use classic for loop.
* You should strive not to rely on the user agent string, but feature detection.
* You should not apply or modify css from javascript, but add and remove classes.
* All functions should be documented.
* You should save DOM elements in variables instead of making a query in the DOM every time you need them.

## Image files

* For image sets with multiple resolutions, annotate the higher resolutions in the filename with `@Nx`, eg. `logo@2x.png`
