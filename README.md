# This is Repo for CSS Session

# New CSS Features

- Nesting
- Container Queries
- `:has()`
- View Transition API
- animation-timline:scroll()

Most of these features have specific use cases, you might think we are already using something better but it’s best to know your technology more

## NESTING

### Why would we use nesting

We use nesting in CSS for pure developer experience, end-user has nothing to do with how CSS is written

There are 2 syntaxes to do nesting in CSS directly

1. Direct Nesting

```css
.single-listing-item__heading {
  /* Directly selecting the child elements */
  h2 {
    font-size: 26px;
  }
}
```

1. Using the nested selector

```css
.single-listing-item__content {
  padding-top: 20px;
  /* Using the nesting selector */
  & p {
    font-weight: 300;
    font-size: 18px;
    line-height: 1.5;
  }
}
```

The second syntax is preferred because when using the pseudo-classes or pseudo-elements, you will have to use the nesting selector

Selecting the pseudo classes and pseudo elements

```css
.single-listing-item {
  background-color: #161616c2;
  padding: 20px;
  border-radius: 12px;
  position: relative;
  overflow: hidden;

  &:after {
    position: absolute;
    content: "";
    width: 100%;
    height: 0%;
    background-color: #f1d4e5;
    top: 0;
    left: 0;
    z-index: -1;
    transition: all 0.2s ease-in;
  }

  &:hover:after {
    height: 100%;
  }
}
```

### Parent Selection with specific class

```css
.single-listing-item__content {
  background-color: aqua;

  .single-listing-item & {
    /* select the parent with this class */
    background-color: aliceblue;
  }
}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a1b7ae2a-e34a-4a83-98e5-f7077a7d581a/3953a5b9-222e-4935-bac1-f61482945fad/Untitled.png)

### Let’s make it a little complex

```css
.single-listing-item__heading {
  & h2 {
    text-decoration: underline;

    .red__text & {
      color: tomato;
    }
  }
}
```

In this code, we are applying underline to all the `h2` in div with `.single-listing-item__heading` class then we are selecting a parent of h2 which has `.red__text` class which results in

`.single-listing-item__heading.red__text`

## Using @media-rule in Nesting

We can use nested media queries in nesting as well

```css
.listing-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 35px;
  padding-top: 40px;

  /* NESTED MEDIA QUERIES */
  @media (max-width: 1440px) {
    & {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  /* NESTED MEDIA QUERIES */
  @media (max-width: 1080px) {
    & {
      grid-template-columns: repeat(1, 1fr);
    }
  }
}
```

## Container Queries

Alternate way of writing Responsive Components

It handles responsive design based on the size of the container rather than basing the responsive design on the screen size.

It is helpful when making reusable components, you can create one component with multiple variants based on where it is being used.

### Using Container Queries

the `container-type` property is used to declare a container/wrapper for a container query.

There are 3 values you can pass to this container query

- size (Not Implemented properly) - The query will be based on the inline and block dimensions of the container
- inline-size - The query will be based on the inline dimensions of the container
- normal - The element is not a query container for any container size queries but remains a query container for container-style queries.

### @rule ()
