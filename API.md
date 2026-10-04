# Yield Editor Pro — local API

Other programs can run the same clean as the page. There is no hosted API. A yield file is not sent to a server. The call runs in the browser on the machine that has the file.

Dan Breckon wrote the flow-delay search this call uses. The method is PCDI, from Lee, Sudduth, Drummond, and Chung, 2012.

## Call it

Open `index.html`, then from the page console or from a script on that page:

```js
YieldEditor.load(points, {
  lon: "Longitude",
  lat: "Latitude",
  yieldDry: "Yield_bu_ac",
  timestamp: "Timestamp",
  velocity: "Speed_mph",
  swath: "Swath_ft",
  moisture: "Moisture"
});
const result = await YieldEditor.clean();
```

`points` is an array of objects. Longitude, latitude, a yield column, and a timestamp are required. Speed and swath let the other cuts run. Heading is used when the file has it, and is derived when it does not.

`result` is:

- `delay` — seconds, half-second steps. `0` when the direction blocks disagree by more than 6 seconds.
- `kept` — points remaining
- `total` — points loaded
- `average` — mean of the yield column on the kept points
- `unit` — the yield unit, when known
- `note` — the same sentence the page shows
- `rows` — the kept points

The clean is the same pass as Clean this field: the delay search, start and end of pass, then yield, speed, half-header swath, speed jumps, overlap, and local scatter. Moisture delay is not set. Start or end stays at 0 when the passes disagree by more than 6 seconds.

## What this is not

A planting or sprayer file is not accepted yet. A raw John Deere card is not accepted. A program that cannot open the page cannot call this yet. A local HTTP wrapper can be added later, still on that computer, if a desktop tool needs to post a file. A hosted endpoint is not the plan.
