# Introduction

> Pick My Solar works with a plug and play javascript snippet installed on your website. A standalone JS snippet and an HTML markup tag `<pms-injectable>` will integrate your website with Pick My Solar marketplace application.


<br/>

<br/>

<br/>

<br/>


# Requirements

-   Your PMS token.

-   Access to your website's code base.
    
-   Basic knowledge of Javascript and HTML.

<br/>

<br/>

<br/>

<br/>

# Implementation
It's an easy, convenient and effortless implementation of PMS Injectable App. Pick My Solar application can only be delivered to `<pms-injectable>` HTML tag. To get the Pick My Solar application, add `<pms-injectable>` tag inside `<body>` wherever you want the application to appear. This tag will automatically adjust the `height` and `width` based on the container’s `height` and `width`. So it’s recommended to use this inside a `<div>` with specific `height` and `width`.

## Basic Code

To get started with PMS Injectable App, you need to first add the base code. The base code snippet has your PMS token/pid as displayed below: 
```
<html>
  <head>
    . . .
    <script src="https://codebase.pickmysolar.com/pms.js" pid="YOUR_PMS_TOKEN"></script>
    . . .
  </head>
  <body>
    . . . 
    <pms-injectable><pms-injectable>
    . . .
  </body>
</html>
```
You need to replace `YOUR_PMS_TOKEN` with your token/key provided by Pick My Solar. 
>Note: If the given token/key is invalid then you will see an error in the browser's javascript console.

## Basic Integration Test
For Testing & validation, open your browser javascript console. You will see the following in the console:

- On successful integration :

![success](https://s3.amazonaws.com/solarassets/partner_assets/inject-sucess.png)

- In case of wrong integration :

![warning](https://s3.amazonaws.com/solarassets/partner_assets/inject-warning.png)

- In case of error within the scripts :

![error](https://s3.amazonaws.com/solarassets/partner_assets/inject-error.png)
