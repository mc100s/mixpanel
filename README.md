# Mixpanel

## Goal

The goal of this tutorial is to track how much users you have on your website and how much time they spend on it.

Here, you will use Mixpanel and you will have an example to track them on their click. 

## Steps to track users and the time they spend

- Log in to your [Mixpanel](https://mixpanel.com) account
- Create a new project
- You should see a JS code (`<!-- start Mixpanel -->...`). Include it just before the `</head>` tag of your HTML files
- Include the following code in one of your JS file. It will track identify the user and track the duration on every click.

```js
// Start Mixpanel tracking
try {
  if (!localStorage.mixpanelId) { // First time to connect with the current browser
    localStorage.mixpanelId = Math.floor(Math.random() * Number.MAX_SAFE_INTEGER);
    mixpanel.identify(localStorage.mixpanelId);
    mixpanel.people.set({
      "$created": new Date(),
      "$last_login": new Date(),
      "mixpanelId": localStorage.mixpanelId,
    });
  }
  else {
    mixpanel.identify(localStorage.mixpanelId);
    mixpanel.people.set({
      "$last_login": new Date(),
    });
  }
}
catch (e) {
  console.log("CATCH", e);
}
mixpanel.time_event("Click"); // Start a chronometer for "Click"
document.addEventListener('click', function() {
  mixpanel.track("Click"); // Track "Click"
  mixpanel.time_event("Click"); // Start a new chronometer for "Click"
});
// End Mixpanel tracking
```

- Go to Mixpanel > Activity Analysis (First navbar) > Segmentation (Second navbar). You should set the event `Click`, `SUM: Duration`, `BY mixpanelId`. Then you will see the total duration by each user. 
![](https://i.imgur.com/2nS2kNf.png).


## Other tracking

Feel free to track other events to understand better how people use your website. For example you can track the number of game played by adding `mixpanel.track("Play");` every time a user click on "Play".
