# Introduction to Next.js
:zap: :bulb: 🟢 :warning: 🟠 

The main differences between an app created by create-react-app and a React app created by Next.js is that it vastly improves SEO performance and load times since the content is rendered server-side before it loads in the browser.

Here's a list of other advantages to take not of:

🟢 **Hot Code Reloading**—Next relaods the page when it detects any changes saved.

🟢 **Automatic Routing**—Any URL is mapped to the filesystem, to files put in the pages folder, and you don't need any configuration.

🟢 **Single File Components**— Using styled-jsx, completely integraged as built by the same team, it's trivial to add styles scoped to the component.

🟢 **Server Rendering**—You can render React components on the server side, before sending the HTML to the client.

🟢 **Ecosystem Compatability**—Next.js plays well with the rest of the JavaScript, Node, and React ecosystem.

🟢 **Automatic Code Splitting**—Pages are rendered with just the libraries and JavaScript they need. Instead of generating one single JavaScript file containing all the app code. 

By analyzing page imports Next.js only loads the JS necessary for that particular page. For example if only one page uses Axios, only that page will include the library in its bundle. This ensures quick page loads.

:warning: However, frequently used JS imports are moved into the main JS file if they're used by at least half of the site pages. 

🟢 **Prefetching** — The Link component, used to link together different pages, supports a prefetch prop which automatically prefetches page resourses (including code missing due to code splitting) in the background.

🟢 **Dynamic Components**— You can import JavaScript modules and React Components dynamically.

🟢 **Static Exports**— Using the **next export** command, Next.js allows you to export a fully static site from your app.

🟢 **TypeScript Support** Next.js is written in TypeScript and as such comes with excellent TypeScript support.

## How to install Next.js
If your familiar with the create-react-app command, create-next-app is the same thing - except it creates a Next App instead of a React App.

The command asks the application name (and creates a new folder for you with that name), then downloads all the packages it needs (react, react-dom, next),sets the package.json to:
```json=
{"name": "my-app",
"version": "0.10",
"private": true,
"scripts":{
"dev": "next-dev",
"build": "next build",
"start": "next start",
},
"deependencies":{
"next": "9.1.3",
"react": "16.11.0",
"react-dom": "16.11.0"
    }
}
```
After this, you can immediately "run dev" and this is what you should see on local host:

![](https://i.imgur.com/lQCxcc7.png)


