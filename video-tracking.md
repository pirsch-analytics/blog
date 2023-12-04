slug = "tracking-youtube-vimeo-videos"
title = "How to Track the Playback Time of YouTube and Vimeo Videos Using Custom Events"
date = 2023-12-02
summary = "Learn how you can track the playback time of YouTube and Vimeo videos on your website using custom events."
image = "video.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

We've talked about it and been asked about it many times, but we've never really shown how to track the playback time of a YouTube or Vimeo video using Pirsch and custom events. I'm going to change that in this article.

## What Will We Track and How Will It Be Useful?

Showing rather than telling what your product, service or company does in a video can be very effective. It's more personal and saves time when the visitor can watch a short video instead of reading an entire web page. But how many people actually watch a video on your website? For how long? Do they finish it?

These questions can be answered using custom events in Pirsch. Combined with conversion goals, you can get a nice graph of how long visitors watch your videos on average. We track:

* When a visitor has started playback
* The percentage of time a video has been watched
* When a visitor has finished watching a video
* A graph of the average play time (also in percent)

First, I'll show you how to use the YouTube and Vimeo APIs to query playback time. Then I will show you what the results look like on the dashboard and how to set up conversion goals. The full source code can be found as part of our demo repository on [GitHub](https://github.com/pirsch-analytics/demo/blob/master/web/static/video.html).

## Setting Up Video Tracking for YouTube

First, we need some data. To track the playback time of a video, we'll send a custom event with three metrics: the playback time in percent, whether the video has started, and whether it has finished.

For tracking, you should embed the Pirsch extended snippet (or `pirsch.js` + `pirsch-events.js`) in the `head` section of your website. This will automatically track a page view and provide the `pirsch` event function.

```html
<script defer src="https://api.pirsch.io/pirsch-extended.js"
    id="pirschextendedjs"
    data-code="YOUR_IDENTIFICATION_CODE"></script>
```

Next, we need to add the YouTube API script. This is used to set up the player and attach events to it so we can track its progress. Add it to the `head` section of your page.

```html
<script src="https://www.youtube.com/iframe_api"></script>
```

Alright, now that we have these in place, we can start embedding the video into your website. Normally, you would just add an iframe to your site that looks something like this.

```html
<iframe width="560"
    height="315"
    src="https://www.youtube.com/embed/dQw4w9WgXcQ?si=EEO27bqXDcymifbj"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen></iframe>
```

In our case, we need to set it up through JavaScript so that we can attach the necessary events. Replace the `iframe` on your page with a simple `div`.

```html
<div id="youtube"></div>
```

The id can be anything, but you need to set it in the code below. Now add a `<script>` tag right after that. We'll use this to set up the player.

```html
<script>
    let player;
    let progress = 0;
    let started = 0;
    let completed = 0;

    function onYouTubeIframeAPIReady() {
        // ...
    }

    window.addEventListener("beforeunload", () => {
        // ...
    });
</script>
```

The `player` variable will hold the player instance. The `progress`, `started`, and `completed` variables are used for tracking.

The `onYouTubeIframeAPIReady` will be triggered by the YouTube iframe API script we've embedded in the `head` section. It must match this name exactly. If you have multiple players on your site, you will need to set them all up in this single function.

The `beforeunload` event listener is triggered when the tab or window is closed or the page is navigated away. We'll use it to send the data to Pirsch.

Let's start by setting up the player. Add the following code to your `onYouTubeIframeAPIReady` function.

```JavaScript
player = new YT.Player("youtube", {
    height: "360",
    width: "640",
    videoId: "dQw4w9WgXcQ",
    events: {
        "onStateChange": (event) => {
            if (event.data === YT.PlayerState.PLAYING) {
                started = 1;
            } else if (event.data === YT.PlayerState.PAUSED) {
                const p = Math.round(player.getCurrentTime() / player.getDuration() * 100);

                if (p > progress) {
                    progress = p;
                }
            } else if (event.data === YT.PlayerState.ENDED) {
                progress = 100;
                completed = 1;
            }
        }
    }
});
```

As you can see, the video ID is the same as in the regular iframe (`dQw4w9WgXcQ`). The size can be adjusted as needed. Important for tracking is the `events` section.

We have added a listener for state changes. In our case we only care about the `PLAYING`, `PAUSED` and `ENDED` events. When the video starts, we set `started` to `1`. When the video is finished, we set the progress to `100` (percent) and `completed` to `1`. They are tracked as `0` and `1` so that we can calculate graphs from them.

Progress is tracked by dividing the current playtime by the duration of the video. We round this number to ensure that it can be grouped properly on the dashboard later. Otherwise we would have unique playtimes for basically every visitor, like `56.92842` instead of `56`.

That's all there is to it. Now we just need to send an event to Pirsch when the page is navigated away or the window or tab is closed. Add the following code to the `beforeunload` event listener.

```JavaScript
if (started) {
    pirsch("YouTube Playback", {
        meta: {
            progress,
            started,
            completed
        }
    });
}
```

The event is only tracked if the video has been started.

## Setting Up Video Tracking for Vimeo

The setup for vimeo is very similar to YouTube. For simplicity, I'll just show the differences here.

Instead of adding the YouTube iframe API script, add the Vimeo script to the `head` section.

```html
<script src="https://player.vimeo.com/api/player.js"></script>
```

It also requires a `div` on the page, which is later replaced by the player.

```html
<div id="vimeo"></div>
```

To initialize the player, replace the `onYouTubeIframeAPIReady` with the following code.

```JavaScript
document.addEventListener("DOMContentLoaded", () => {
    const iframe = document.querySelector("#vimeo");
    player = new Vimeo.Player(iframe, {
        id: 76979871, // video ID
        width: 640
    });

    player.on("timeupdate", data => {
        const p = Math.round(data.percent * 100);

        if (p > progress) {
            progress = p;

            if (p >= 100) {
                progress = 100;
                completed = 1;
            }
        }
    });

    player.on("play", () => {
        started = 1;
    });
});
```

The logic is almost identical to that for YouTube, but instead of attaching an `ended` event, we simply set it to completed when the video progress reaches 100%. The Pirsch event trigger also stays the same, but you may want to change the event name.

## Analyzing Video Statistics

Now that we have collected the progress as custom events, we can take a look at the dashboard. For the demo, there is a YouTube video and a Vimeo video on the page. Both will appear in the events panel.

![Video Playback Events](/blog/static/videotracking/events.png)

If you open the details view (top right corner of the panel), you can see the metadata attached to each event.

![Video Playback Meta Data](/blog/static/videotracking/video-progress.png)

The metadata statistics tell you how many times a video has been watched and for how long. The progress is grouped in one percent increments. If you prefer larger steps, you can change the calculation in the JavaScript snippets.

`started` is always set to one in the demo because we don't collect events if the video hasn't been started. Of course, you could change this to see how many visitors didn't watch the video. The alternative would be to filter for the event and metadata and exclude them from the results.

To see a graph of the number of people who have watched a video over time, click on the `progress` metadata entry you want to see.

![Playback Progress](/blog/static/videotracking/event-filter.png)

This will show all visitors who watched 48% of the video. You can adjust the number directly in the filter. For example, setting it to 99% won't show any results.

![Playback Progress](/blog/static/videotracking/event-filter-no-data.png)

## Setting up a Conversion Goal

To get a better understanding of the progress of the playback, you can create a conversion goal. Here is an example.

![Playback Conversion Goal](/blog/static/videotracking/goal.png)

In this case, it's called *Playback Progress* and only applies to the `/video.html` page. The conversion goal will filter for the `YouTube Playback` event and create a graph from the `progress` metadata field, which we interpret as integers.

Clicking on the conversion goal in the dashboard will display the following graph.

![Playback Conversion Goal](/blog/static/videotracking/progress-graph.png)

In this case, the average progress was 58% for two visitors. You can add additional conversion goals for the `started` and `completed` fields. Since we set them to `0` or `1`, they can again be interpreted as integers.

## Conclusion

I hope you enjoyed reading this little tutorial. Again, the full source code for the demo can be found on [GitHub](https://github.com/pirsch-analytics/demo/blob/master/web/static/video.html). Please reach out if you have any questions.
