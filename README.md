# Introduction

> Pick My Solar works with a plug and play JavaScript snippet. A standalone JavaScript snippet and an HTML markup tag `<pms-injectable>` will integrate your website with Pick My Solar marketplace application.


<br/>

<br/>

<br/>

<br/>


# Requirements

-   Your PMS token

-   Access to your website's codebase
    
-   Basic knowledge of Javascript and HTML

<br/>

<br/>

<br/>

<br/>

# Implementation
It's an easy, convenient and effortless implementation. Pick My Solar Application can only deliver to `<pms-injectable>` HTML tag. You need to add `<pms-injectable>` tag inside `<body>` wherever you want the application to appear. This tag will automatically adjust the `height` and `width` based on the container’s `height` and `width`. So it’s recommended to use this inside a `<div>` with specific `height` and `width`.
>Note: Anything placed inside the `<pms-injectable></pms-injectable>` tag, will be ignored.

## PMS Injectable Script URL

This script can render the entire PMS Injectable application to your website/app.

> Script URL : https://codebase.pickmysolar.com/v2/pms.js

### Usage

```html
    <script src="https://codebase.pickmysolar.com/v2/pms.js" pid="YOUR_PMS_TOKEN"></script>
```

## Basic Code

To get started with PMS Injectable Application, you need to add the base code first. The base code snippet has your PMS token/pid as shown below: 
```
<html>
  <head>
    . . .
    <script src="https://codebase.pickmysolar.com/v2/pms.js" pid="YOUR_PMS_TOKEN"></script>
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
>Note: If the given token/key is invalid, you will see an error in the browser's JavaScript console.

## Basic Integration Test
For testing & validation, open your browser's JavaScript console. You will see the following messages:

- On successful integration :

![success](https://s3.amazonaws.com/solarassets/partner_assets/inject-sucess.png)

- In case of wrong integration :

![warning](https://s3.amazonaws.com/solarassets/partner_assets/inject-warning.png)

- In case of error within the scripts :

![error](https://s3.amazonaws.com/solarassets/partner_assets/inject-error.png)


<br/>

<br/>

<br/>

<br/>

# User Authentication
## Login Function
To initiate the ‘logged-in user’ into Pick My Solar application, you need to set PMS parameters using `window._PMS.setParams()` function. You can call this function inside your native website's login function/method.
### Example:
```js
yourLoginFunction() {
 ...
 // end-line of the function
 window._PMS.setParams({
    userData: {
      fullname: "------",       //user's full name
      email: "--@--",           //user's email
      password: "-----"         //user's password
    }
  });
}
```
>`yourLoginFunction()` is supposed to be login method/function in your native website/app.
>If a user is logged by already active session (cookie) at Client/Partner application then PMS Injectable application will be expecting the parameters to be sent each time on CTA click. For all the logged in users, we strongly recommend to set the parameters every time when PMS Injectable Application accesses/triggers point or CTA buttons get clicked in your website/application. 
### Login Parameters
The function `window._PMS.setParams()` needs the user data in a JSON format consisting of the user’s name, email, and password. The data model for the user’s information is given below:
```js
{
     fullname: string,          //user's full name
     email: string,             //user's email
     password: string           //user's password
}
```
> Name, Email and Password are required elements.

## Logout Function
To logout or wipe-out from PMS Injectable Application active session, call `window._PMS.flush()` function. You can call this function anywhere as per the requirement.

<br/>

<br/>

<br/>

<br/>

# Callback Functions
PMS Injectable application has callback functions. You can attach your own functions with our PMS Injectable Application callback mechanism in order to get the data from the Pick My Solar application. This is the only communication channel for your base code to communicate with Pick My Solar application. Any changes or updates to the params have to be triggered through callbacks only. All callback functions need to be registered on the initialization of Pick My Solar application.
```js
window._PMS.cbFunctions = {
      signUp: yourSignUpCatchFn,
      projectType: functionToSetProjectType
   };
```
## Available Callbacks
### signUp
This callback function can be used to get the information of the user while signing up on PMS Injectable Application. 
>The attached function will be called with certain parameters, parallel to the PMS signup process.
#### Parameters
```js
{
     fullname: string,          //user's full name
     email: string,             //user's email
     password: string           //user's password
}
```
### projectType
This callback function can be used to set the project type on PMS Injectable Application. 
>The attached function is supposed to return an array of strings of required keywords. This function will always be used by PMS Injectable Application to decide the project type.
#### Function Example 
```js
    function functionToSetProjectType() {
        return ['solar', 'battery'];
    }
    // PMS callbacks initialization.
    window._PMS.cbFunctions = {
        signUp: yourSignUpCatchFn,
        projectType: functionToSetProjectType
    };
```

#### Input Parameters

```js
['solar', 'battery']
```

##### Available keywords
  - 'solar'
  - 'battery'
  >Note: Single project type should also be sent in array format.


## How to attach callback functions
You need to attach your callback functions on window._PMS.cbFunctions wherever you declare them to catch the required data. 
### Example:
#### Javascript:
```
<script>
   function yourSignUpCatchFn(params) {
       ...
   }
   function functionToSetProjectType() {
       return ['solar', 'battery'];
   }
   // PMS callbacks initialization.
   window._PMS.cbFunctions = {
      signUp: yourSignUpCatchFn,
      projectType: functionToSetProjectType
   };
</script>
```

#### Angular 2+ component:

```js
ngOnInit() {
  (window as any)._PMS.cbFunctions = {
      signUp: this.yourSignUpCatchFn,
      projectType: this.functionToSetProjectType
   };
}
yourSignUpCatchFn(params) {
       ...
}
functionToSetProjectType() {
       return ['solar', 'battery'];
}
```

#### React component:

```js
componentWillMount() {
  window._PMS.cbFunctions = {
      signUp: this.yourSignUpCatchFn,
      projectType: this.functionToSetProjectType
   };
}
yourSignUpCatchFn(params) {
       ...
}
functionToSetProjectType() {
       return ['solar', 'battery'];
}
```





<br/>

<br/>

<br/>

<br/>


# UTM Tracking
To track UTM with injection, you need to attach UTM default params in the url where injection is initializing.
Example URL - 
```js
https://example.com/?utm_source=dev&utm_medium=testing&utm_campaign=testing%201&utm_term=freee&utm_content=testing%20analytics%20update
```
> utm_source, utm_medium, utm_campaign, utm_term and utm_content are default params. 




<br/>

<br/>

<br/>

<br/>


# GTM Tracking
To add GTM tracking using Google Analytics with injection, please follow the below document.

> https://docs.google.com/document/d/1MwSQrQ-MnASRrb2F8Dac6HfBCWSipJWxE98ET29iMwY/edit?usp=sharing 





<br/>

<br/>

<br/>

<br/>


# Change logs

### v2.1.0 - 03/13/2020
- New callback function added for project type selection. [See Docs](/#projectType)


### v2.0.9 - 02/15/2020
- Stability improvements and various bug fixes.
- Internet Explorer 11 compatibility fix.

### v2.0.8 - 02/01/2020
- Partner specific disclaimer added.
- Various bug fixes.



# Credits
Designed & Developed by 
[Jitendra Singh Chauhan](https://jitendra.info)

