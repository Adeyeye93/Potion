---
layout: post
title: "How to connect React With liveView"
description: "How to connect React With liveView, and Use react frontend component in liveView/Phoenix"
date: 2024-07-02
feature_image: images/how-to-connect-react-with-liveview.png
tags: [tips, how-to's, liveView, Phoenix]
---

### Why Use React Components in LiveView/Phoenix?

As most Phoenix and LiveView developers come from a backend background, writing frontend code can sometimes feel tedious and time-consuming. For backend-focused developers, managing the complexities of frontend JavaScript frameworks or building dynamic, interactive components from scratch isn't always appealing. Luckily, many beautifully designed, ready-to-use components already exist—particularly in the React ecosystem. React components offer a wide variety of features and functionality that can be integrated with minimal effort.

That’s why in this post, I’m going to walk you through how to seamlessly connect and use React components in your Phoenix LiveView projects. By doing this, you can leverage the best of both worlds: LiveView's powerful real-time capabilities and React's highly customizable components.

<!--more-->

## Step 1: Create a Phoenix Project
Start by creating a new Phoenix project. If you don’t already have one, you can run the following command:
```bash
 mix phx.new my_liveview_project
```
Once the project is created, navigate into your project directory:

```bash
cd my_liveview_project
```

## Step 2: Install the React Component
Next, you'll need to install the React component that you want to use. For this example, we'll use the `sonner` library as an example, which provides a Toaster component.
Navigate to your Phoenix project's `assets` directory and install the React component:


```bash
cd assets
npm install sonner react react-dom
```

## Step 3: Recompile Static Assets
Once the React component is installed, you'll want to recompile your Phoenix assets:

```bash
cd ..
mix phx.digest
```
This ensures that Phoenix includes your newly added dependencie

## Step 4: Create the React Component
Now, let's create a directory to store your React components. In your `assets` directory, create a components folder and add a file named `Toaster.jsx` you can give it any name but this is will be better to follow the code in this post.:

In the `Toaster.jsx` file, add the following code

```javascript
import React from "react";
import { Toaster } from "sonner";

function ToasterComponent() {
  return (
    <Toaster position="bottom-right" expand={true} richColors />
  );
}

export default ToasterComponent;
```

This React component will display a toaster notification at the bottom-right corner of the screen with rich colors and expansion enabled, to know more about `toaster` please visit [Sooner Doc](https://sonner.emilkowal.ski/getting-started "Sooner Documentation")

## Step 5: Modify `app.js` to Use the React Component
Next, update your `app.js` file to integrate the Toaster component. You’ll listen for Phoenix LiveView’s page loading events to trigger the React component. In `assets/js/app.js`, add the following code:

``` javascript
import React from "react";
import ReactDOM from "react-dom/client";
import ToasterComponent from "../components/Toaster";
import { toast } from "sonner";

const rootElement = document.getElementById("react-root");

window.addEventListener("phx:page-loading-start", (info) => {
  console.log("LiveView loading started", info);
  toast.loading("Page is loading");
});

window.addEventListener("phx:page-loading-stop", (info) => {
  const root = ReactDOM.createRoot(rootElement);
  root.render(<ToasterComponent />);
});

```
### Note:
> If the request is handled by traditional Phoenix controller ignore EventListener

## Step 6: Add the React Root Element to HTML
Now, you need to add a root element for React in your LiveView HTML template. Open your template file (e.g., lib/my_liveview_project_web/templates/layout/root.html.heex) and add the following line inside the body tag:

```html
<div id="react-root"></div>
```
his `<div>` element acts as the mount point for your React component.

## Conclusion
By following these simple steps, you've successfully integrated a React component into your Phoenix LiveView application! You've used a pre-built React component (the Toaster from the sonner library) and hooked it into LiveView’s lifecycle events, adding interactive client-side functionality with minimal frontend coding effort.

# Need Help?
If you run into any issues or have any questions while integrating React components into your Phoenix LiveView project, feel free to reach out to me! I'm always happy to help.

You can connect with me on [LinkedIn](www.linkedin.com/in/adeyeye-seyi-269226213 "LinkedIn") or reach out via X (link below).
Don't forget to drop your Comment bellow

<!-- Put this code anywhere in the body of your page where you want the badge to show up. -->

