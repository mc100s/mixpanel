# Mixpanel

## Goal

The goal of this tutorial is to track how much users you have on your website and how much time they spend on it.

Here, you will use Mixpanel and you will have an example to track them on their click or keydown events.

## Steps to track users and the time they spend

- Log in to your [Mixpanel](https://mixpanel.com) account
- Create a new project
- You should see a JS code (`<!-- start Mixpanel -->...`). Include it just before the `</head>` tag of your HTML files
- Include the following code in one of your JS file or in a new file `mixpanel.js` (that you will need to include in your HTML file). It will track identify the user and track the duration on every click.

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
mixpanel.time_event("Event"); // Start a chronometer for "Event"
function mixpanelStopAndStart() {
  mixpanel.track("Event"); // Track "Event"
  mixpanel.time_event("Event"); // Start a new chronometer for "Event"
}
document.addEventListener('click', mixpanelStopAndStart);
document.addEventListener('keydown', mixpanelStopAndStart);
// End Mixpanel tracking
```

- Go to Mixpanel and set up your dashboard like described below. Don't forget to click on "Show" button to refresh the data:
    
    - 1: In the first navbar, go to "Activity"
    
    - 2: In the second navbar, go to "Segmentation"
    
    - 3: Set the event `Event` 
    
    - 4: Filter on `Duration` that is `less than` `60` 
    
    - 5: `SUM` on `Duration` 
    
    - 6: Group `by` `mixpanelId` 
    
    - 7: Change the display to "Chart > Bar"
    
    - 8+: Click on the "Show" button every time you want to refresh the data!

![](https://i.imgur.com/SCdSDfU.png).

<!-- https://i.imgur.com/C4bgyqP.png -->


## Other tracking

Feel free to track other events to understand better how people use your website. For example you can track the number of game played by adding `mixpanel.track("Play");` every time a user click on "Play".
