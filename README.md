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
>Note: Anything placed inside `<pms-injectable></pms-injectable>` will be ignored.

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


<br/>

<br/>

<br/>

<br/>

# User Authentication
## Login Function
In order to initiate the ‘logged-in user’ into Pick My Solar application, you need to set PMS parameters using `window._PMS.setParams()` function. You can call this function inside your native website's login function/method.
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
>If user is logged by already active session (cookie) at Client/Partner application then PMS Injectable app will be expecting the parameters to be sent each time on CTA click. For all logged in user, We strongly recommend to set the parameters every time when injectable app access/trigger point or CTA get clicked in your website/app. 
### Login Parameters
The function `window._PMS.setParams()` needs the user data in a JSON format consisting of the user’s name, email, and password. The data model for the user’s information is given below:
```js
{
     fullname: string,          //user's full name
     email: string,             //user's email
     password: string           //user's password
}
```
> Name, Email and Password are required elements, absence of any of them will throw an error.

## Logout Function
In order to logout or wipe-out PMS Injectable app active session, call `window._PMS.flush()` function. You can call this function anywhere as per the requirement.

<br/>

<br/>

<br/>

<br/>

# Callback Functions
PMS Injectable application has callbacks functions. You can attach your own functions with our callback mechanism in order to get data from Pick My Solar application. This is the only communication channel for your base code to communicate with Pick My Solar application. Any changes or updates to the params have to be triggered through callbacks only. All callback functions need to be registered on initialization of Pick My Solar application.
```js
window._PMS.cbFunctions = {
      signUp: yourSignUpCatchFn,
      projectType: functionToSetProjectType
   };
```
## Available Callbacks
### signUp
This callback function can be used to get the information of user while signing up on PMS Injectable App. 
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
This callback function can be used to set the project type on PMS Injectable App. 
>The attached function is supposed to return array of strings of required keywords. This function will always be used by PMS Injectable App to decide the project type.
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
  - 'ev charger'
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
