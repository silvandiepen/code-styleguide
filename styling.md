# Styling

- **Always use [BEM](#bem) style classes**: Adopting BEM (Block Element Modifier) naming conventions ensures consistency and clarity in your codebase, making it easier to maintain and scale. BEM divides your CSS into blocks, elements, and modifiers, which helps in understanding the relationship between components and their states.

- **Avoid styling HTML elements directly**: Instead of styling elements like `<p>` or `<div>` directly, encapsulate styles within classes. For example, instead of:

  ```css
  p {
      color: #333;
      padding-top: 20px;
  }
  ```

  Use:

  ```css
  .text-paragraph {
      color: #333;
      padding-top: 20px;
  }
  ```

  This reduces specificity issues and makes your CSS more modular.

- **Do not use [utility classes](#utility-classes) in HTML**: Keep your HTML clean by avoiding utility classes. For example, avoid using classes like `text-center` or `pt-4` directly in HTML. Instead, define these styles within the CSS of the specific component:

  ```css
  .card {
      text-align: center;
      padding-top: 1rem;
  }
  ```

  This approach leads to better readability and maintainability of your code.

- **[Prefer custom properties](#custom-properties-over-sass-variables) over Sass variables**: Use CSS custom properties (`--my-variable`) whenever possible. Custom properties can be dynamically updated, inherited, and are more flexible than Sass variables, which are static after compilation. For example:

  ```css
  :root {
      --primary-color: #3498db;
  }

  .button {
      background-color: var(--primary-color);
  }
  ```

  This allows you to change `--primary-color` at runtime if needed.

- **Avoid scoping styles unnecessarily**: Properly structured HTML and CSS should eliminate the need for complex scoping. For example, avoid over-nesting selectors:

  ```css
  .component .component__header .component__title {
      color: #000;
  }
  ```

  Instead, keep it simple:

  ```css
  .component__title {
      color: #000;
  }
  ```

  Over-scoping can make stylesheets harder to maintain and debug.

- **Base all sizes on a logical system**: Use a consistent grid, modular scale, or other logical systems for sizing. For instance, instead of random pixel values like `22px` or `37px`, base sizes on a scale such as:

  ```css
  :root {
      --base-size: 16px;
  }

  .layout-container {
      padding: calc(var(--base-size) * 2);
  }
  ```

  This approach maintains consistency across your design.

- **Avoid setting sizes on containers**: Containers should adapt to their content, not the other way around. For example, avoid setting fixed widths like `width: 300px` on containers. Instead, use flexible layouts like flexbox or grid:

  ```css
  .container {
      display: flex;
      justify-content: space-between;
  }
  ```

  This ensures your design is responsive and fluid.

- **Never use ['margin-bottom'](#the-case-of-the-forbidden-margin-bottom)**: Instead of relying on `margin-bottom`, control spacing with adjacent sibling selectors or layout methods like flexbox and grid. For example:

  ```css
  p + .container {
      margin-top: 20px;
  }
  ```

  This approach prevents spacing issues when elements are reordered or when new elements are added to the layout.

# **Utility Classes**

While utility classes have their place, they can clutter your HTML. If you must use them, define and manage them in the stylesheet rather than in the HTML. For example, instead of using a class like `pt-4` in your HTML, define this in your CSS:

```css
.utility-padding-top {
    padding-top: 1rem;
}
```

Then, apply this class in your CSS where needed. This approach encapsulates your styles and keeps your HTML clean and semantic.

## **BEM**

Using BEM helps structure your classes in a meaningful way, allowing for easier comprehension of the relationship between different parts of your UI. BEM naming convention uses a block name, followed by an element name and modifier, separated by double underscores (`__`) and double hyphens (`--`), respectively. For example:

```css
.card {
    /* Block */
}

.card__title {
    /* Element */
}

.card__title--large {
    /* Modifier */
}
```

This structure not only improves readability but also enhances collaboration among developers by creating a common understanding of how styles are applied.

### **More about BEM and why to use it**

BEM's structured approach to naming classes minimizes specificity conflicts, encourages reusability, and makes it easier to maintain large codebases. It is especially beneficial in projects with multiple developers or when working on complex UIs.

## **Styling on Elements**

Avoid styling HTML elements directly. This can lead to conflicts and make your styles harder to manage. For example, styling a `<button>` element directly:

```css
button {
    background-color: blue;
}
```

Instead, apply a class to the button and style that class:

```css
.button {
    background-color: blue;
}
```

This way, your styles are more modular, and the risk of unintended side effects is reduced. Even when writing scoped CSS, act as though it’s global—this mindset will help you avoid issues later on when styles are combined.

### **Reasons why**

Directly styling elements can lead to specificity conflicts, as other styles might override them unexpectedly. By using classes, you ensure that styles are encapsulated, predictable, and easier to manage as your project grows.

## **Custom Properties > Sass Variables**

Custom properties (CSS variables) offer several advantages over Sass variables. For example, they can be updated dynamically in JavaScript and provide better inheritance and fallback mechanisms:

```css
:root {
    --font-size: 16px;
}

h1 {
    font-size: var(--font-size);
}
```

Custom properties also enable theming and responsive design patterns that are difficult to achieve with Sass variables alone.

### **Reasons why**

Unlike Sass variables, which are compiled at build time, custom properties are live in the browser, meaning they can be altered based on user interactions or environmental factors like screen size. This dynamic behavior makes them much more powerful for modern web development.

## **Scoping**

Good HTML and CSS structure eliminates the need for excessive scoping. Instead of deeply nested selectors:

```css
.container .container__header .container__title {
    color: #000;
}
```

Use a flat, more maintainable structure:

```css
.container__title {
    color: #000;
}
```

This approach keeps your styles simple and easier to manage.

### **More on why**

Excessive scoping can lead to overly specific selectors, which are hard to override and can cause conflicts. By keeping your selectors shallow, you reduce the likelihood of these issues, making your CSS more robust and easier to work with.

## **Avoid Container Sizes**

Specifying fixed widths or heights on containers is outdated and often problematic. Modern layouts should be flexible, using CSS grid, flexbox, or other responsive techniques to allow containers to adapt to their content. For example:

```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

This approach ensures your design is responsive and adapts to different screen sizes without breaking.

### **More**

By avoiding fixed sizes on containers, you embrace a responsive design approach, ensuring your website or application works well across various devices and screen sizes. This leads to a better user experience and reduces the need for extensive media queries.

## **The Case of the Forbidden 'Margin-Bottom'**

Relying on `margin-bottom` can create unpredictable spacing issues, especially when elements are reordered or new elements are added. For example:

```css
p + .container {
    margin-top: 10px;
}
```

This approach ensures that spacing is consistent regardless of the order of elements. Additionally, modern CSS layout tools like flexbox and grid offer the `gap` property, which is a more reliable way to manage spacing between items:

```css
.container {
    display: flex;
    gap: 20px;
}
```

This eliminates the need for individual margins and provides a more predictable layout.

### **More**

By avoiding `margin-bottom`, you simplify your layout and avoid issues when elements change order or new components are introduced. Using tools like `gap` in flexbox or grid makes your layout more consistent and easier to manage, leading to fewer layout bugs and a more maintainable codebase.
