# Domparty - Component library

A while-labeled component library, ready for you to style. Unbiased on how styling should look on your
website, while giving you the handles to kick-start you application with some helpful functional components.

## Instructions

Install the component library using `npm i @domparty/fe`. This will make the library available for your project.
Because @domparty/fe uses Goober internally to provide all neat CSS tricks, first implement our provider into your application.

### Default React apps

For default React apps, the following snippet can be used.

```
import React from "react";
import { Provider } from "@domparty/fe/core";

export default () => (
  <Provider value={{}}>
    <App />
  </Provider>
);

```

### Next.js apps

To implement @domparty/fe into Next.js make sure the \_app.js file implements the <Provider /> component.

```
import React from "react";
import { Provider } from "@domparty/fe/core";

export default ({ Component, pageProps }) => (
  <Provider value={{}}>
    <Component {...pageProps} />
  </Provider>
);
```

## SSR (server-side rendering)

To make sure all styles are rendered correctly on the server. The component library exports Goobers' `extractCss` function for you to implement.

To use this feature in Next.js apps, make sure the `getInitialProps` in your \_document file uses this function.

```
import Document, { Head, Main, NextScript } from "next/document";
import { extractCss } from "@domparty/fe/core";

export default class MyDocument extends Document {
  static getInitialProps({ renderPage }) {
    const page = renderPage();

    // Extrach the css for each page render
    const css = extractCss();
    return { ...page, css };
  }

  render() {
    return (
      <html>
        <Head>
          <style
            id={"_goober"}
            // And defined it in here
            dangerouslySetInnerHTML={{ __html: this.props.css }}
          />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </html>
    );
  }
}
```

# License

[MIT](https://oss.ninja/mit/domparty/)
