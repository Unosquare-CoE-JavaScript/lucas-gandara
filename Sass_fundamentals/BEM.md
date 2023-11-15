# Sass Fundamentals
## BEM Architecture
**BEM** is a convention or methodology for naming your CSS classes. By the acronym, BEM means B **Block**, E **element** and M **Modifier**.

### ¿How does BEM work?
Bem works by identifying the block, element and modifier of a component.

- **Block** is the main container of the component
- **Element** are the internal parts that make up the component.
- **Modifying** are the variations of the block element.

### How to use BEM in CSS
Class names with BEM convention may have the following syntax:

- [block]
- [block]__[element]
- [block]--[modifier]
- [element]--[modifier]
- [block]__[element]--[modifier]

Consider:
```html
<div class="textfield">
  <label for="first-name" class="textfield__label">
    First name
  </label>
  <input name="first-name" type="email" class="textfield__input" />
  <span class="textfield__validation-error">
    Must be two characters or longer
  </span>
</div>
```
In SCSS this is achieved leveraging the nesting like so:
```scss
.textfield {
  &__label {
    background-color: red;
    &--error {
      border: solid 1px blue;
    } 
  }
}
```