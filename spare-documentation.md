# Matthew Brewer's thebrewergame.com Spare Code Documentation

Howdy! This file is the official documentation of the spare bits of code written and developed for thebrewergame.com that normally go unused. Before jumping in, please take a mental note of the following that will appear regularly throughout this document:

- "Stylesheet" / "CSS file" --> /src/styles/styles.css
- "Main page" / "Main code" / "Main page code" --> /index.html

The list below is organized in descending order of development.

### Colored Social Links

In thebrewergame.com v1.8, actuallyaridan added code to color the background of each social link in the site's footer. This coloring was achieved with HTML classes that defined the primary color for each platform the footer displayed at the time in the stylesheet that the links in the main page then called upon. While the colors were removed in the subsequent release, thebrewergame.com v1.9, all of the original HTML classes remain near the bottom of the stylesheet and can be reattached to their respective links by adding back the corresponding `class` values. For example, take this link to my Twitter profile:

```
<a href="https://x.com/thebrewergame" target="_blank" rel="noopener">X (formerly Twitter)</a>
```

The link tag above creates a link to my Twitter profile, thebrewergame, which appears as "X (formerly Twitter)" and opens in a new tab in the browser. This link would appear visually consistent with what the stylesheet has defined for links on the website. However, if you wanted to add back the Twitter blue brand color background to the link, the link would need to appear like this:

```
<a href="https://x.com/thebrewergame" target="_blank" rel="noopener" class="twitter">X (formerly Twitter)</a>
```

This link tag creates a link to my Twitter profile, thebrewergame, which appears as "X (formerly Twitter)", opens in a new tab in the browser, and uses Twitter's signature blue as the link background, which is defined in the stylesheet. For reference and archiving purposes, these are all of the original HTML classes:

```
.twitter{
    background-color: #008AD8;
    color: white;
}

.instagram{
    background-color: #F56040;
    color: white;
}

.substack{
    background-color: #FF6719;
    color: white;
}

.airchat{
    background-color: #3170e7;
    color: white;
}

.youtube{
    background-color: #FF0000;
    color: white;
}

.twitch{
    background-color: #6441a5;
    color: white;
}
```

### Announcement Banner

thebrewergame.com v1.18 introduced the announcement banner, a handy tool that can be used to promote something specific underneath the social links in the website's footer. It offers space for a header, additional tagline, content, and a few actions, like a link to another website. The banner's code can be identified in the main page code and the stylesheet by the HTML class "announcementBanner" as of thebrewergame.com v1.49. In versions of thebrewergame.com before 1.49, the HTML class was "announcement-banner". Since version 1.49 and onward, each individual element of the announcement banner has its own HTML ID that allows them to be called upon in other parts of the code. In descending order of appearance, these IDs are:

```
announcementTagline
announcementHeader
announcementContent
announcementActions
```

To take the banner live once the content has been appropriately filled in the main page and the sizing adequately adjusted in the stylesheet, remove the comment tags surrounding the `<br>` just above the banner's container, and remove or comment out the `display: none;` at the bottom of the announcement banner class' entry in the stylesheet. This will reveal the banner, and add a little extra spacing in between it and the social links above it.

### Countdown

thebrewergame.com v1.49 also brought in code for a countdown ahead of Matthew's birthday on December 4, 2024. To use it, copy the block of JavaScript code below from when it was first used into the `<script>` section of the main page, and go through the list of steps underneath to set it up.

```
var countdownDate = new Date("Dec 4, 2024 00:00:00").getTime();
var countdownElement = document.getElementById("announcementContent")
var countdownUpdater = setInterval(function() {
    var countdownCurrentTime = new Date().getTime();
    var countdownDifference = countdownDate - countdownCurrentTime;

    var countdownDays = Math.floor(countdownDifference / (1000 * 60 * 60 * 24));
    var countdownHours = Math.floor((countdownDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    var countdownMinutes = Math.floor((countdownDifference % (1000 * 60 * 60)) / (1000 * 60));
    var countdownSeconds = Math.floor((countdownDifference % (1000 * 60)) / 1000);

    var countdown = countdownDays + "d " + countdownHours + "h " + countdownMinutes + "m " + countdownSeconds + "s"
    var countdownCompletionMessage = "TODAY! HAPPY BIRTHDAY, MATTHEW!"

    countdownElement.innerHTML = countdown;

    if (countdownDifference < 0) {
        clearInterval(countdownCurrentTime);
        countdownElement.innerHTML = countdownCompletionMessage;
    }
}, 1000);
```

First, define the date the countdown will be ticking down to with the variable `countdownDate`. In the code above, this date is Dec 4, 2024. Once the date is defined, specify the element of the website the countdown is supposed to appear in with the variable `countdownElement`. Once you've done that, make sure to configure a relevant message to be displayed when the countdown is completed with the variable `countdownCompletionMessage`, and you're all set! Now, you have a countdown that includes days, hours, minutes, and seconds. If you want to customize what the countdown actually shows, such as by only displaying days and hours, you can do so with the `countdown` variable.

### Mobile Determiner Function

The mobile determiner function detects what user client a visitor is using, and can adjust elements of the website accordingly based on whether or not they are on mobile or desktop with the `if` statement located just below the check. The full code of the mobile determiner function from when it was first introduced is located below:

```
function MobileDeterminer() {
    const userClient = navigator.userAgent;
    return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(userClient);
}

if (MobileDeterminer()) {
    document.getElementById("announcementHeader").textContent = "MATTHEW'S BDAY IS IN:"
}
```

To adjust an element of the website based on if they're on mobile, put the changes inside the `if` statement. In the code above, it's set to adjust the content of the `announcementHeader` to "MATTHEW'S BDAY IS IN:".

### Additional Unstyled Social Link/Fediverse Button

An additional, unstyled social link was developed to sit just below the primary social links' `<div>` originally for the fediverse. When pressed, the button (which is styled to appear as an unstyled link) triggers a browser `alert()`. There are three components to it. First, the actual button, which sits right below the social links' `<div>`, above the announcement banner's `<br>`. When it was originally developed, this is what the button looked like:

```
<button type=button class="fediverseButton" onclick="fediverseAlert()">Looking for the fediverse?</button>
```

Then, the scripting was located in the `<script>` section of `index.html`:

```
function fediverseAlert() {
    var alertMessage = "While I don't frequent the fediverse myself, my Bluesky account is streamed over the rainbow protocol bridge at @thebrewergame.com@bsky.brid.gy. Follow me there on your fediverse platform of choice, and consider enabling the bridge back to Bluesky by following @bsky.brid.gy@bsky.brid.gy yourself so I can see and interact with you!"
    
    alert(alertMessage)
}
```

Finally, to style the button to appear as an unstyled link, the following CSS was included in `/src/styles/styles.css` just above the announcement banner's CSS:

```
.fediverseButton {
    background: none;
    border: none;
    padding: 0;
    margin-top: 10px;
    margin-bottom: 0;
    color: #069;
    text-decoration: underline;
    cursor: pointer;
    display: none;
}
```