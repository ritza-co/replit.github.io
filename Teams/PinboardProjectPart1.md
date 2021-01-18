<!-- omit in toc -->
# Pinboard Project: Part 1

The goal of this project is to create a pinboard for users to save, categorise and collected images from across the internet. In addition to adding images to the board, users will also be able to assign specific tag values to images for filtering purposes. Lastly, once a user clicks the "Add New Image" button they will be presented with a form in which they can enter the several tag values and the URL of the image to be added.

You can have a look at the final code that we will have at the end of this project by going to [https://repl.it/@ritza/Pinboard-Project](https://repl.it/@ritza/Pinboard-Project). In addition, you can view it as a standalone page by pressing the "Open in a new tab" button (at the top-right of the REPL) or by going straight to the following URL: [https://pinboard-project.ritza.repl.co](https://pinboard-project.ritza.repl.co/)

Will will walk through the creation of the final pinboard by means of two parts. You are currently looking at part 1, where we will build out the basic HTML and CSS structure of our pinboard. However, if you are not interested in this you can jump straight to [part 2](./PinboardProjectPart2.md), where we will be adding interactivity to our pinboard by means of JavaScript.

We will be working through the first part below as follows:

- [Creating your own project on Repl.it](#creating-your-own-project-on-replit)
- [Basic Structure and Styling](#basic-structure-and-styling)
- [Markup](#markup)
  - [Head](#head)
  - [Datalist](#datalist)
  - [Header](#header)
  - [Sections](#sections)
  - [Dialog](#dialog)
- [Styling](#styling)
  - [Universal Selector](#universal-selector)
  - [Scrolling](#scrolling)
  - [Positioning](#positioning)
  - [Pseudo-classes](#pseudo-classes)
  - [Media Queries](#media-queries)
  - [Transition](#transition)
  - [Object-fit](#object-fit)
  - [Fixed Overlay](#fixed-overlay)
- [Next Steps](#next-steps)


## Creating your own project on Repl.it

If you haven't already, head to the [sign up page](https://repl.it/signup) and create a Repl.it account. Once created do the following to set up a new project:

1. Click on the "+ New repl" button.
2. Choose the "HTML, CSS, JS" language: 
3. Give your repl a name: In our case "pinboard-project"
4. For free accounts you can only set your repl to public.
5. Click the "Create repl" button.

![/images/teamsForEducation/pinboard-project/image-1.png](../static/images/teamsForEducation/pinboard-project/image-1.png)

Because we selected "HTML, CSS, JS" as our repl language, Repl.it has created the basic files needed for our front-end project, which should be as follows:

- `index.html`
- `style.css`
- `script.js`

## Basic Structure and Styling

We'll start off with a basic skeleton with some hard-coded examples in it. First, we need to open our  `style.css` file and add the following styling to it. If you are unsure what it does then don't worry we'll discuss it in depth further below.

```css
* {
  box-sizing: border-box;
}

body {
  padding: 0;
  margin: 0;
  background-color: #f4b0b0;
  font-family: "Helvetica neue", Helvetica, Arial, sans-serif;
  overflow-y: scroll;
  overflow-x: hidden;
}

.title {
  font-size: 4rem;
  text-align: center;
  font-family: "Bungee Shade", cursive;
  color: purple;
	display: none;
}

@media (min-width: 40rem) {
  .title {
    display: block; 
  }
}

.field {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  font-weight: bold;
  letter-spacing: 0.5px;
  position: relative;
  cursor: pointer;
  max-width: 40rem;
}

.label {
  position: absolute;
  font-size: 0.75rem;
  left: 1rem;
  top: 1rem;
  opacity: 0.5;
  text-transform: uppercase;
  font-weight: bold;
}

.input {
  border-radius: 6px;
  font-weight: bold;
  padding: 2rem 0.75rem 0.75rem;
  width: 100%;
  font-size: 1.5rem;
  box-shadow: 0 0 5px #fc47bb;
}

.controls {
  display: flex;
  justify-content: space-between;
  padding: 2rem;
  flex-wrap: wrap;
}

.button {
  border-radius: 6px;
  padding: 1rem;
  font-size: 2rem;
  font-family: "Montserrat", sans-serif;
  font-weight: bold;
  white-space: nowrap;
  cursor: pointer;
	margin: 0.5rem 0;
}

.button:disabled {
  cursor: not-allowed;
}

.button:not(:disabled):hover {
  background: #CCC;
}

.list {
  margin: -1rem;
  display: flex;
  flex-wrap: wrap;
  padding: 0 1rem 4rem;
}

.pin {
  position: relative;
  padding: 1rem;
	width: 100%;
}

@media (min-width: 40rem) {
  .pin { 
    width: 50%; 
  }
}

@media (min-width: 65rem) {
  .pin { 
    width: 33.333333333333%;
  }
}

@media (min-width: 100rem) {
  .pin { 
    width: 25%;
  }
}

.info {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  opacity: 0;
  transition: opacity 0.3s, transform 0.3s;
  list-style: none;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  transform: translateY(1rem);
}

.pin:hover .info {
  opacity: 1;
  transform: translateY(-1rem);
}

.remove {
  position: absolute;
  right: 2rem;
  top: 2rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 2.5rem;
  width: 2.5rem;
  font-size: 1.5rem;
  font-weight: bold;
  font-family: "Montserrat", sans-serif;
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.3s, transform 0.3s;
  transform: translateY(-1rem);
}

.pin:hover .remove {
  transform: translateY(0);
  opacity: 1;
}

.remove:hover {
  background: #CCC;
}

.image {
  width: 100%;
  height: 20rem;
  object-fit: cover;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  border-radius: 6px;
  background-color: #d18c8c;
}

.tag {
  margin: 0.5rem;
  border-radius: 15px;
  padding: 1rem;
  font-size: 1rem;
  font-family: "Montserrat", sans-serif;
  font-weight: bold;
  cursor: pointer;
  text-transform: capitalize;
}

.tag:hover {
  background: #CCC;
}

.overlay {
  position: fixed;
  background: rgba(0, 0, 0, 0.7);
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 
    0px 11px 15px -7px rgba(0,0,0,0.2),
    0px 24px 38px 3px rgba(0,0,0,0.14),
    0px 9px 46px 8px rgba(0,0,0,0.12);
}

.form {
  background: white;
  width: 100%;
  max-width: 40rem;
  border-radius: 16px;
}

.dialog-list {
  list-style: none;
  padding: 1rem;
}

.dialog-item {
  padding: 1rem;
  text-align: center;
}

.helper {
  display: block;
  padding: 0.75rem 0;
  opacity: 0.6;
}

.hidden {
  display: none;
}
```

After adding the above code to `style.css` then proceed by opening your `index.html` file and replacing all of the existing code with the following snippet. Once again, we'll explain what it does further down.

```html
<!DOCTYPE html>

<html>
  <head>
    <meta charset="utf-8" />
    <title>My Moodboard</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <link rel="stylesheet" href="./style.css" />
    <script src="./script.js" defer></script>

    <link rel="preconnect" href="https://fonts.gstatic.com" />

    <link
      href="https://fonts.googleapis.com/css2?family=Bungee+Shade&family=Montserrat:wght@400;700&display=swap"
      rel="stylesheet"
    />
  </head>

  <body id="app">
    <datalist id="existing-tags">
      <option>Engineering</option>
      <option>Headphones</option>
      <option>Wellness</option>
      <option>Ocean</option>
      <option>Office</option>
      <option>Coding</option>
      <option>Desk</option>
      <option>Boxing</option>
      <option>Lab</option>
    </datalist>

    <header>
      <h1 class="title">My Moodboard</h1>

      <div class="controls">
        <label class="field" for="filter-input">
          <span class="label">Filter</span>
          <input
            type="search"
            id="filter-input"
            class="input"
            list="existing-tags"
            placeholder="None"
          />
        </label>

        <button class="button" id="dialog-start">Add New Image</button>
      </div>
    </header>

    <main>
      <div class="list" id="pins-list">
        <section class="pin">
          <img
            class="image"
            src="https://images.unsplash.com/photo-1580983218765-f663bec07b37?w=600"
          />

          <ul class="info">
            <li class="tag-wrap">
              <button class="tag">engineering</button>
            </li>
          </ul>

          <button
            class="remove"
            aria-label="remove"
            value="122203215486581930752615279550"
          >
            &#10005;
          </button>
        </section>

        <section class="pin">
          <img
            class="image"
            src="https://images.unsplash.com/photo-1572932491814-4833690788ad?w=600"
          />

          <ul class="info">
            <li class="tag-wrap">
              <button class="tag">headphones</button>
            </li>

            <li class="tag-wrap">
              <button class="tag">ocean</button>
            </li>

            <li class="tag-wrap">
              <button class="tag">wellness</button>
            </li>
          </ul>

          <button
            class="remove"
            aria-label="remove"
            value="144685389103194178251333634000"
          >
            &#10005;
          </button>
        </section>

        <section class="pin">
          <img
            class="image"
            src="https://images.unsplash.com/photo-1580894908361-967195033215?w=600"
          />

          <ul class="info">
            <li class="tag-wrap">
              <button class="tag">office</button>
            </li>

            <li class="tag-wrap">
              <button class="tag">coding</button>
            </li>

            <li class="tag-wrap">
              <button class="tag">desk</button>
            </li>
          </ul>

          <button
            class="remove"
            aria-label="remove"
            value="159279541173033634211014623228"
          >
            &#10005;
          </button>
        </section>

        <section class="pin">
          <img
            class="image"
            src="https://images.unsplash.com/photo-1584464491033-06628f3a6b7b?w=600"
          />

          <ul class="info">
            <li class="tag-wrap">
              <button class="tag">boxing</button>
            </li>

            <li class="tag-wrap">
              <button class="tag">wellness</button>
            </li>
          </ul>

          <button
            class="remove"
            aria-label="remove"
            value="75261220651273643680893699100"
          >
            &#10005;
          </button>
        </section>

        <section class="pin">
          <img
            class="image"
            src="https://images.unsplash.com/photo-1581094271901-8022df4466f9?w=600"
          />

          <ul class="info">
            <li class="tag-wrap">
              <button class="tag">lab</button>
            </li>

            <li class="tag-wrap">
              <button class="tag">engineering</button>
            </li>
          </ul>

          <button
            class="remove"
            aria-label="remove"
            value="161051747537834597427464147310"
          >
            &#10005;
          </button>
        </section>
      </div>
    </main>

    <dialog id="dialog" class="overlay hidden">
      <form id="dialog-form" class="form">
        <div class="dialog-item">
          <label class="field" for="dialog-image">
            <span class="label">Image URL</span>
            <input class="input" type="url" id="dialog-image" />
          </label>

          <em class="helper">For example: https://images.unsplash.com/photo-1584464491033-06628f3a6b7b</em>
        </div>

        <div class="dialog-item">
          <label class="field" for="dialog-tags">
            <span class="label">Tags</span>
            <input class="input" type="text" id="dialog-tags" />
          </label>

          <em class="helper">Separate multiple tags with commas. For example: engineering, coding</em>
        </div>

        <div class="dialog-item">
          <button type="submit" class="button" id="dialog-submit" disabled>
            Save Image
          </button>
        </div>
      </form>
    </dialog>
  </body>
</html>
```

Yikes! That is quite a lot of HTML and CSS. Regardless, if you run your reply (with the big `Run` button at the top) you should something as follows:

![../static/images/teamsForEducation/pinboard-project/image-2.png](../static/images/teamsForEducation/pinboard-project/image-2.png)

You can click the "Open in new tab" button at the far top-right to open your project in a separate browser tab as follows:

![../static/images/teamsForEducation/pinboard-project/image-3.png](../static/images/teamsForEducation/pinboard-project/image-3.png)

## Markup

As promised, let's walk through the above code step-by-step, starting with the HTML.

### Head

Our HTML starts off with a `<!DOCTYPE html>` and a `<html>` element. At this point you don't need to understand what these do, but only that they are required in all modern-day `.html` files.

Inside the `<html>` element we see another element titled `<head>`. This element is used to communicate meta information to the browser. The elements inside it won't be shown to the user but provide the browser with useful commands to run before the user-facing HTML content is created. Our `<head>` element has the following nested elements:

```html
<head>
  <meta charset="utf-8" />
  <title>My Moodboard</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <link rel="stylesheet" href="./style.css" />
  <script src="./script.js" defer></script>

  <link rel="preconnect" href="https://fonts.gstatic.com" />

  <link
    href="https://fonts.googleapis.com/css2?family=Bungee+Shade&family=Montserrat:wght@400;700&display=swap"
    rel="stylesheet"
  />
</head>
```

- The first `<meta>` element determines the character types that should be used by the browser, this is required in all HTML documents, and is almost always set to "utf-8".
- The `<title>` element determines the name that is shown on in a user's browser tab. It is also used by search engines and accessibility devices as the name of the page.
- The second `<meta>` element tells the browser to not automatically scale the size of our content. This is required for styling to look the same across several screen sizes such as a desktop computer and mobile phone (called [responsive web design](https://en.wikipedia.org/wiki/Responsive_web_design)).
- The first `<link>` element loads our CSS file (`style.css`) we populated above.
- The `<script>` element loads the (still empty) JavaScript file (`script.js`). In addition, the `defer` attribute tells the browser to only execute our JavaScript once all HTML has been created. Otherwise, the HTML tags that we look for in our JavaScript will not exist yet (since the `<script>` element is created before our HTML content (inside the `<body>` element.
- The remaining `<link>` elements are [Google Fonts](https://fonts.google.com) specific code that we receive when selecting fonts to from the [Google Fonts website](https://fonts.google.com/). These are merely copied and pasted from the Google Fonts website, and allow us to use the fonts in question.

### Datalist

Next is our `<body>` element. The `<body>` element contains the actual HTML that should be shown to a user. The first element in our body is an `<datalist>` element. The `<datalist>` element will (ironically) not be displayed to users but will be used by `<input>` elements within our HTML recommend existing tag values as users types. Note that despite the `<datalist>` not rendering anything to users it is required to be in the `<body>` element and not the `<head>` element.

```html
<datalist id="existing-tags">
  <option>Engineering</option>
  <option>Headphones</option>
  <option>Wellness</option>
  <option>Ocean</option>
  <option>Office</option>
  <option>Coding </option>
  <option>Desk</option>
  <option>Boxing</option>
  <option>Lab</option>
</datalist>
```

### Header

Next is `<header>` element. The `<header>` element is meant to group a content (shown to the user) at the top of the page. Be careful to not confuse the `<head>` element and the `<header>` element. Despite them sounding similar, they are very different. Inside our `<header>` element we have the following:

```html
<header>
  <h1 class="title">My Moodboard</h1>

  <div class="controls">
    <label class="field" for="filter-input">
      <span class="label">Filter</span>
      <input type="search" id="filter-input" class="input" list="existing-tags" placeholder="None" >
    </label>
    
    <button class="button" id="dialog-start">Add New Image</button>
  </div>
</header>
```

- An `<h1>` element that serves as the title of our page. The `<h1>` element will be used by search engines and accessibility devices to determine what page a user is currently on. Given that we only have one page this can be the same as our `<title>` (defined in the above section).
- By default `<div>` elements do not have any inherent meaning and are often used to group and position content. The `<div>` element that we are using here is meant to wrap and style both the filter field and "Add New Image" button. The `controls` CSS `class` attribute is used to add styling that aligns the filter and button side by side.
- The `<label>` element wraps the entire filter field and tells search engines and accessibility devices that the tags inside are grouped together. The `field` CSS `class` is used to style the field itself, whereas the `for` attribute points to the `id` attribute the `input` element that is used by this `<label>` element.
- By default `<span>` elements indicate a piece of short text used on our page. In our case it adds a description in the top of the field. We are using the `label` CSS `class` attribute to add the styling required to overlay the `<span>` element on top of the `<input>` element.
- The `<input>` element has a `type` attribute that is set to `search`. This tells the browser to make use of a special search input (this has several enhancements, such as a button to clear the current search phrase). Furthermore, we have the standard `id` attribute and `class` attributes. Lastly, we add the `id` value of our `datalist` (from the previous code snippet) the `list` attribute (this links this input to our `datalist`). Finally, we add a `placeholder` attribute that tells the browser to display "None" when the `input` is empty.
- Lastly, similar to the above our button has a `class` attribute for CSS styling and an `id` attribute to be used by our JavaScript.

### Sections

Then we have an `<main>` element (signifying the main content of our `<body>` element). Inside the `<main>` element we have a `<div>` with several `<section>` elements inside it. Each `<section>` element displays an image (and associated controls) pinned by the user. Let us look at a single pinned image:

```html
<section class="pin">
  <img
    class="image"
    src="https://images.unsplash.com/photo-1580894908361-967195033215?w=600"
  />

  <ul class="info">
    <li class="tag-wrap">
      <button class="tag">office</button>
    </li>

    <li class="tag-wrap">
      <button class="tag">coding</button>
    </li>

    <li class="tag-wrap">
      <button class="tag">desk</button>
    </li>
  </ul>

  <button
    class="remove"
    aria-label="remove"
    value="159279541173033634211014623228"
  >
    &#10005;
  </button>
</section>
```

- The wrapping `<section>` element indicates to search engines and accessibility devices that the content inside should be treated as a grouped, standalone piece of information.
- The `<img>` element is used to show the pinned image (by supplying the URL). Note that the behaviour of this image is a bit different from regular `<img>` element behaviour. By means of the CSS styling applied to it, the relevant image will scale up or down until it covers the entire `<section>` element.
- The `<ul>` element is used to indicate to search engines and accessibility devices that the content that follows is part of a list. When using an `<ul>` element the order of the items don't matter, whereas if you an `<ol>` element they do.
- Each `<li>` inside the `<ul>` element indicates a separate item inside the list.
- Inside each `<li>` is a `<button>` element that can be pressed to show all pins that have the same tag.
- The last `<button>` element creates a way for users to remove an image from the pinboard. We are using the multiplication sign (`×`) as the text label of the button. It can be added to HTML by using the following special [HTML entity](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references) code: `&#10005;`. While this visually appears similar to a crossed-out icon, usually associated with removing something, semantically it will be read differently by search engines and accessibility devices. It will be read as a multiplication sign, which as you can probably understand will create a lot of confusion. Therefore we use the `aria-label` attribute to override the semantic value associated with the button to `"remove"`. Lastly, you will see that the `<button>` element also has a `value` attribute with a unique number. The reason for this will be explained in part 2 of this project, so don't worry about it too much for now.

### Dialog

Lastly, and perhaps most importantly is a `<dialog>` element. While the `<dialog>` element is currently hidden from users by means of a `hidden` CSS class that is applied to it, it will be shown once the `hidden` class is removed. Once when visible users can provide values in order to pin a new image to the board. The `<dialog>` element consists of the following:

```html
<dialog id="dialog" class="overlay hidden">
  <form id="dialog-form" class="form">
    <div class="dialog-item">
      <label class="field" for="dialog-image">
        <span class="label">Image URL</span>
        <input class="input" type="url" id="dialog-image" />
      </label>

      <em class="helper">For example: https://images.unsplash.com/photo-1584464491033-06628f3a6b7b</em>
    </div>

    <div class="dialog-item">
      <label class="field" for="dialog-tags">
        <span class="label">Tags</span>
        <input class="input" type="text" id="dialog-tags" />
      </label>

      <em class="helper">Separate multiple tags with commas. For example: engineering, coding</em>
    </div>

    <div class="dialog-item">
      <button type="submit" class="button" id="dialog-submit" disabled>
        Save Image
      </button>
    </div>
  </form>
</dialog>
```

- The wrapping `<dialog>` element forms the transparent black overlay that sits behind the `<form>` element. It has both an `overlay` CSS class (for this behaviour) and a dynamic `hidden` CSS class that can be toggled on and off in order to show/hide the dialog (and nested elements).
- The `<form>` element indicates to search engines and accessibility devices that the next section functions as a traditional web form that should be submitted button (as opposed to our filtering which happens real-time as you type). Note that a `<form>` element can also be submitted with the "enter" key on the required data has been provided.
- Within the `<form>` element are three repeating `<div>` elements. As mentioned before, these have no semantic meaning, but can be used to group and position elements. In this case, we are using the `<div>` elements to add some spacing between the different elements in the form (by means of the `dialog-item` CSS class).
- Inside the first two `<div>` tags, we are reusing the first input field HTML structure we created (from the above `<header>` snippet), albeit with different `id` and `type` attributes on each `<input>` element.
- We are also adding `<em>` elements after each. The `<em>` element is short for "emphasis" and is similar in function to `<span>`, however, it indicates that the piece of text has a specific importance. In our snippet above, we use them for helper text provide users with context regarding what is expected in the fields.

In order to see how the dialog would look, you might want to temporarily remove the `hidden` CSS class. The dialog should look similar to the screenshot below. However, please remember to read the `hidden` class back again - otherwise, your pinboard will start with the `dialog` open.

![../static/images/teamsForEducation/pinboard-project/image-4.png](../static/images/teamsForEducation/pinboard-project/image-4.png)

## Styling

Now that we've covered the basic HTML structure let us dive into our CSS (`style.css`). Most of the code should be self-explanatory even if you know a little bit of CSS. If not you can use the phenomenal [CSS-Tricks maintained Almanac](https://css-tricks.com/almanac/) to understand exactly what specific properties do. However, there are some broader aspects of the CSS that I want to briefly touch on:

### Universal Selector

The `*` selector is named the [universal CSS selector](https://css-tricks.com/almanac/selectors/u/universal). It applies the designated styling rules to every single HTML element on the page. In our case, we want to override the way that size is calculated on our page. By default, all elements have a `box-sizing` of `content-box`, however, we want to override the default behaviour for all tags to `border-box`. This snippet of CSS is so common in modern-day web development that the 1st of February is actually designated as an annual [International Box-sizing Awareness Day](https://css-tricks.com/international-box-sizing-awareness-day/) by the front-end community.

```css
* {
  box-sizing: border-box;
}
```

However, what exactly does this do? 

By default, `content-box` adds all borders and padding on top of the designated size of an element. For example, if we have an element that has a `width: 10rem` with `padding: 1rem` and `border: 1px` the actual size of the element will be the total value of `10rem + 1rem + 1px`. Alternatively, when an element used `border-box` then all the above is added as part of an element's designated width. For example, instead of the total width being `10rem + 1rem + 1px`, it will be the original `10rem` with the space needed for padding and borders being factored into this amount.

### Scrolling

Secondly is the styling of our `<body>` element. You will notice that we set a couple of straight-forward rules in order to override the default (often different) values of the `<body>` element in different browsers. 

```css
body {
  padding: 0;
  margin: 0;
  background-color: #f4b0b0;
  font-family: "Helvetica neue", Helvetica, Arial, sans-serif;
  overflow-y: scroll;
  overflow-x: hidden;
}
```

However, more specifically, you will see that we set `overflow-x: hidden` and `overflow-y: scroll`. This is done merely to prevent users from accidentally scrolling horizontally, and it also forces a vertical scroll bar (even if the content does exceed the height of your window). The latter is to ensure that the content doesn't jump around when a vertical scroll bar automatically gets added (or removed) as our number of pins exceed the height of the browser viewport.

### Positioning

Next, you'll notice that we are using `position: relative` and `position: absolute` respectively between our `field` and `label` CSS classes. This allows us to overlay the field label on top of the input (overlaying it). The `position: absolute` rule tells the element to exit the [regular content flow](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout) and instead resort to being manually placed by the CSS (by means of `top` and `left`). Furthermore,  `position: relative` tells the absolute positioned content what it should use as a reference. This means that our label will be set `1rem` from the top and bottom of the field parent. Furthermore, `flex`, `justify-content` and `align-items` are used to position elements using the regular content flow inside an element. If you want to learn more about these properties you can have a look at [Chris Coyier](https://chriscoyier.net)'s super useful [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox).

```css
.field {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  font-weight: bold;
  letter-spacing: 0.5px;
  position: relative;
  cursor: pointer;
  max-width: 40rem;
}

.label {
  position: absolute;
  font-size: 0.75rem;
  left: 1rem;
  top: 1rem;
  opacity: 0.5;
  text-transform: uppercase;
  font-weight: bold;
}
```

### Pseudo-classes

You will notice that there is an independant `button` class and selectors with [pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) associated with it. The base class merely defines the styling of our button class in it's resting state, whereas the `:hover` pseudo-class indicates that the styling should only be applied when users hover over a button. Furthermore, you'll notice that we are adding the `font-family` again property once again (despite us already setting it on the `<body>` element. This is due to the fact that the HTML rules do are not automatically applied `<button>` elements, meaning that we need to manually set it once again (this is one of the strange quirks of HTML and CSS). Lastly, you'll see that we are using a special mouse cursor for buttons when they are disabled. Furthermore we are not applying the hover effect when the button is disabled.

```css
.button {
  border-radius: 6px;
  padding: 1rem;
  font-size: 2rem;
  font-family: "Montserrat", sans-serif;
  font-weight: bold;
  white-space: nowrap;
  cursor: pointer;
}

.button:disabled {
  cursor: not-allowed;
}

.button:not(:disabled):hover {
  background: #CCC;
}
```

### Media Queries

Furthermore, you'll notice that we are using several media queries on our `pin` CSS class. If you are not familiar with media queries, they essentially allow us to set the styling rules to be applied to different browser sizes. Media Queries are the heart of the modern-day [responsive web design](https://en.wikipedia.org/wiki/Responsive_web_design) methodology.

In the snippet below, if a user's browser screen is wider than `40rem` that two pins should be shown on a row (each pin should take up `50%` of available space). However, if the browser width is wider `65rem` then we should show three pins on a row instead, and so forth. Try resizing your browser window when viewing the pinboard to see this in action.

```css
.pin {
  position: relative;
  padding: 1rem;
	width: 100%;
}

@media (min-width: 40rem) {
  .pin { 
    width: 50%; 
  }
}

@media (min-width: 65rem) {
  .pin { 
    width: 33.333333333333%;
  }
}

@media (min-width: 100rem) {
  .pin { 
    width: 25%;
  }
}
```

You notice we are using the cascading nature of CSS here to override each width if the browser is wider than the previous value. This approach, named [mobile first](https://en.wikipedia.org/wiki/Responsive_web_design#Mobile_first,_unobtrusive_JavaScript,_and_progressive_enhancement), was pioneered by [Luke Wroblewski](https://www.lukew.com/) in [a book with the same title](https://abookapart.com/products/mobile-first). The reasoning being that it is easier to scale our design up than it is to scale them down, therefore we start by assuming the smallest browser size and then incrementally work our way upwards.

This is also closely related to the computer science principle of [progressive enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement).

### Transition

Further down you will see use the `opacity`, `transform` and `transition` properties being used on a CSS class called `info`. We can use the `transition` property to tell CSS to animate the change in specific CSS values. In our case, we are telling it to animate changes in `opacity` and `transform`. This is used to create the sliding effect of the tags when you hover over an image.

You will see that we are using `.pin:hover .info` and `pin:hover .remove` to change the styling of the `info` and `remove` CSS classes. The blank space between each of these two classes indicates a parent-child relationship. In other words, when users hover over the parent (`pin`) then the following should be applied to the children (`info` and `remove` respectively). Note that, likewise, if a user no longer hovers over an image the styling is animated back to its original resting state.

It is important to keep in mind that a blank space in our CSS selectors do no imply a direct parent-child relation. It merely indicates that class can be nested at any level within the parent element. In order to use a direct parent-child relation you need to use a greater-than sign (`>`). For example with `.pin > .info` it needs to be nest only a single level below the parent.

```css
.info {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  opacity: 0;
  transition: opacity 0.3s, transform 0.3s;
  list-style: none;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  transform: translateY(1rem);
}

.pin:hover .info {
  opacity: 1;
  transform: translateY(-1rem);
}

.remove {
  position: absolute;
  right: 2rem;
  top: 2rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 2.5rem;
  width: 2.5rem;
  font-size: 1.5rem;
  font-weight: bold;
  font-family: "Montserrat", sans-serif;
  cursor: pointer;
  opacity: 0;
  transition: opacity 0.3s, transform 0.3s;
  transform: translateY(-1rem);
}

.pin:hover .remove {
  transform: translateY(0);
  opacity: 1;
}

.remove:hover {
  background: #CCC;
}
```

Our hover effect will display the `info` and `remove` classes as follows over our image:

![../static/images/teamsForEducation/pinboard-project/image-5.png](../static/images/teamsForEducation/pinboard-project/image-5.png)

### Object-fit

We mentioned in our HTML examples that our `<img>` elements's behaviour is a bit different from the default `<img>` element behaviour. We accomplish this as follows:

- The `width: 100%` and `height: 20rem` values tell the image to fill its entire parent width (the pin itself), but to force a height of `20rem`.
- By default the above will cause the image to stretch and distort (since it will be forced to that size without crop).
- However, `object-fit: cover` tells the image to scale up or down according to (keeping its original aspect ratio) while cropping the overflowing parts of the image as needed until the entire `<img>` space if filled.

```css
.image {
  width: 100%;
  height: 20rem;
  object-fit: cover;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  border-radius: 6px;
  background-color: #d18c8c;
}
```

If we leave out the `object-fit` property then our images will get stretched as follows:

![../static/images/teamsForEducation/pinboard-project/image-6.png](../static/images/teamsForEducation/pinboard-project/image-6.png)

### Fixed Overlay

Similar to our `position: absolute` example above, the `position: fixed` rule on our `overlay` CSS class ejects the HTML out of the regular page flow. However, while `position: absolute` positions a tag in relation to any parent that has `position: relative` rule, the `position: fixed` property positions an element in relation to the browser viewport itself. Therefore since we are setting `left` and `top` to `0`, as well as the size of the tag to a `width` and `height` of `100%` our overlay, will fill the entire screen. Note the element is overlaid in the restricted sense of the word, meaning that even if we scroll down it will still cover the viewport.

```css
.overlay {
  position: fixed;
  background: rgba(0, 0, 0, 0.7);
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 
    0px 11px 15px -7px rgba(0,0,0,0.2),
    0px 24px 38px 3px rgba(0,0,0,0.14),
    0px 9px 46px 8px rgba(0,0,0,0.12);
}
```

## Next Steps

While the above creates all of the structural parts needed for our pinboard, it is completely static. This means that nothing happens when users press buttons or enter text into inputs. Luckily all browsers come with a scripting language, called JavaScript, that allows us to programmatically add interactivity to our pages. We will be doing this in [part 2 of our project](./PinboardProjectPart2.md).