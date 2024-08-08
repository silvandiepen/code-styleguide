# Styling

- **Always use [BEM](#bem) style classes**: Adopting BEM (Block Element Modifier) naming conventions ensures consistency and clarity in your codebase, making it easier to maintain and scale. BEM divides your CSS into blocks, elements, and modifiers, which helps in understanding the relationship between components and their states.

- **[Avoid styling HTML elements](#styling-on-elements) directly**: Instead of styling elements like `<p>` or `<div>` directly, encapsulate styles within classes. This reduces specificity issues and makes your CSS more modular.

- **Do not use [utility classes](#utility-classes) in HTML**: Keep your HTML clean by avoiding utility classes. Instead, define these styles within the CSS of the specific component. This approach leads to better readability and maintainability of your code.

- **[Prefer custom properties](#custom-properties-over-sass-variables) over Sass variables**: Use CSS custom properties (`--my-variable`) whenever possible. Custom properties can be dynamically updated, inherited, and are more flexible than Sass variables, which are static after compilation.

- **Avoid [scoping](#scoping) styles unnecessarily**: Properly structured HTML and CSS should eliminate the need for complex scoping. Over-scoping can make stylesheets harder to maintain and debug.

- **[Base all sizes on a logical system](#base-all-sizes-on-a-logical-system)**: Use a consistent grid, modular scale, or other logical systems for sizing. This approach maintains consistency across your design.

- **[Avoid setting sizes on containers](#avoid-container-sizes)**: Containers should adapt to their content, not the other way around. This ensures your design is responsive and fluid.

- **Use [custom properties over Sass variables](#custom-properties--sass-variables) where possible** Custom properties (CSS variables) offer several advantages over Sass variables.

- **Never use ['margin-bottom'](#the-case-of-the-forbidden-margin-bottom)**: Instead of relying on `margin-bottom`, control spacing with adjacent sibling selectors or layout methods like flexbox and grid. This approach prevents spacing issues when elements are reordered or when new elements are added to the layout.








## **BEM**

Using BEM helps structure your classes in a meaningful way, allowing for easier comprehension of the relationship between different parts of your UI. BEM naming convention uses a block name, followed by an element name and modifier, separated by double underscores (`__`) and double hyphens (`--`), respectively.

```
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










## **Styling on Elements**

Avoid styling HTML elements directly. This can lead to conflicts and make your styles harder to manage. For example:

```
button {
    background-color: blue;
}
```

Instead, apply a class to the button and style that class:

```
.button {
    background-color: blue;
}
```

This way, your styles are more modular, and the risk of unintended side effects is reduced. Even when writing scoped CSS, act as though it’s global—this mindset will help you avoid issues later on when styles are combined.

Directly styling elements can lead to specificity conflicts, as other styles might override them unexpectedly. By using classes, you ensure that styles are encapsulated, predictable, and easier to manage as your project grows.










## **Utility Classes**

While utility classes have their place, they can clutter your HTML. If you must use them, define and manage them in the stylesheet rather than in the HTML. This approach encapsulates your styles and keeps your HTML clean and semantic.

```
.utility-padding-top {
    padding-top: 1rem;
}
```
[BEM](/#bem)'s structured approach to naming classes minimizes specificity conflicts, encourages reusability, and makes it easier to maintain large codebases. It is especially beneficial in projects with multiple developers or when working on complex UIs.

## **Custom Properties > Sass Variables**

Custom properties (CSS variables) offer several advantages over Sass variables. For example:

```
:root {
    --font-size: 16px;
}

h1 {
    font-size: var(--font-size);
}
```

Custom properties also enable theming and responsive design patterns that are difficult to achieve with Sass variables alone.

Unlike Sass variables, which are compiled at build time, custom properties are live in the browser, meaning they can be altered based on user interactions or environmental factors like screen size. This dynamic behavior makes them much more powerful for modern web development.










## **Scoping**

Good HTML and CSS structure eliminates the need for excessive scoping. Instead of deeply nested selectors:

```
.container .container__header .container__title {
    color: #000;
}
```

Use a flat, more maintainable structure:

```
.container__title {
    color: #000;
}
```

This approach keeps your styles simple and easier to manage.

Excessive scoping can lead to overly specific selectors, which are hard to override and can cause conflicts. By keeping your selectors shallow, you reduce the likelihood of these issues, making your CSS more robust and easier to work with.




## Base All Sizes on a Logical System

When designing and developing a website, it's crucial to base all sizes—whether it's spacing, typography, or element dimensions—on a logical system like a grid or a modular scale. This approach creates consistency and ensures that your design is visually harmonious. By sticking to a defined system, you avoid the pitfalls of arbitrary sizing, which can lead to a disjointed and unprofessional appearance.

For example, instead of randomly choosing font sizes like `15px`, `18px`, and `24px`, you might use a modular scale based on a ratio, such as 1.25. This would produce sizes like `16px`, `20px`, and `25px`, which maintain a consistent rhythm and proportion throughout your design. Similarly, you can use a grid system for layout, where all spacing and dimensions are multiples of a base unit, like `8px`, to create a cohesive structure.

Logical systems also simplify responsive design. By using relative units like `em` or `rem` based on a modular scale, you can easily adjust your design for different screen sizes without breaking the visual hierarchy. This approach makes your design more adaptable and ensures a consistent user experience across devices.

In summary, basing sizes on a logical system not only enhances the visual consistency of your design but also streamlines the development process, making it easier to maintain and scale your project over time.





## **Avoid Container Sizes**

Specifying fixed widths or heights on containers is outdated and often problematic. Modern layouts should be flexible, using CSS grid, flexbox, or other responsive techniques to allow containers to adapt to their content. For example:

```
.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

This approach ensures your design is responsive and adapts to different screen sizes without breaking.

By avoiding fixed sizes on containers, you embrace a responsive design approach, ensuring your website or application works well across various devices and screen sizes. This leads to a better user experience and reduces the need for extensive media queries.








## **The Case of the Forbidden 'Margin-Bottom'**

Relying on `margin-bottom` can create unpredictable spacing issues, especially when elements are reordered or new elements are added. For example:

```
p + .container {
    margin-top: 10px;
}
```

This approach ensures that spacing is consistent regardless of the order of elements. Additionally, modern CSS layout tools like flexbox and grid offer the `gap` property, which is a more reliable way to manage spacing between items:

```
.container {
    display: flex;
    gap: 20px;
}
```

This eliminates the need for individual margins and provides a more predictable layout.

By avoiding `margin-bottom`, you simplify your layout and avoid issues when elements change order or new components are introduced. Using tools like `gap` in flexbox or grid makes your layout more consistent and easier to manage, leading to fewer layout bugs and a more maintainable codebase.
