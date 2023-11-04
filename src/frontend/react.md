## React - what and why

React is a library for web and native user interfaces



### What are the advantages of using React?

**Use of Virtual DOM to improve efficiency:** React uses virtual DOM to render the view. As the name suggests, virtual DOM is a virtual representation of the real DOM. Each time the data changes in a react app, a new virtual DOM gets created. Creating a virtual DOM is much faster than rendering the UI inside the browser. Therefore, with the use of virtual DOM, the efficiency of the app improves.

**Gentle learning curve**: React has a gentle learning curve when compared to frameworks like Angular. Anyone with little knowledge of javascript can start building web applications using React.
SEO friendly: React allows developers to develop engaging user interfaces that can be easily navigated in various search engines. It also allows server-side rendering, which boosts the SEO of an app.

**Reusable components**: React uses component-based architecture for developing applications. Components are independent and reusable bits of code. These components can be shared across various applications having similar functionality. The re-use of components increases the pace of development.

**Huge ecosystem of libraries to choose from:** React provides you with the freedom to choose the tools, libraries, and architecture for developing an application based on your requirement.


## React concepts



## What is JSX?

JSX is a syntax extension to JavaScript. It is used with React to describe what the user interface should look like. JSX is similar to a template language, but it has full power of JavaScript. JSX is not a necessity to write React applications. However, it is recommended to use JSX as it makes the code easier to read and write.

#### Can web browsers read JSX directly? 
Web browsers cannot read JSX directly. This is because they are built to only read regular JS objects and JSX is not a regular JavaScript object 
For a web browser to read a JSX file, the file needs to be transformed into a regular JavaScript object. For this, we use Babel

### Virtual DOM

The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called reconciliation.

This approach enables the declarative API of React: You tell React what state you want the UI to be in, and it makes sure the DOM matches that state. This abstracts out the attribute manipulation, event handling, and manual DOM updating that you would otherwise have to use to build your app.

### Creating a React app

- create-react-app
- vite
- webpack
- singlespa

#### frameworks
- Next.js
- Remix