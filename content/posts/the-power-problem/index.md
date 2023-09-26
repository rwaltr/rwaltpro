---
title: "HomeCompute - The Power Problem"
descripton: "What is the maximum dosage"
date: 2023-09-19
tags: [Diary, HomeCompute]
draft: true
topics: [Homelab]
series: ["HomeCompute"]
series_order: 2
---
![XKCD Power converter](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimgs.xkcd.com%2Fcomics%2Funiversal_converter_box_2x.png&f=1&nofb=1&ipt=3981cfac1012b8c442d36956a82c3edbbe0ecfceed63fae9baf4cae5c80fa4b1&ipo=images) 
## Power, it is already in the wall?

If there is anything I ever learned, it is that someone else has **already** solved your problem, the tricky part is finding and applying it.

## What can we do before my house goes on 🔥

Go look at you panel, find the breaker that connects to your homelab, and do this `math`.

```
(120 x <number on your breaker>) x .8
```

Boom, that is your max wattage you homelab should be rated for.

> For the record, it technically isn't. But your electrician will get very sad. 🙁

Mine is `20`, so my max wattage is `(120 x 20) x .8 = 1920`

### I like your funny words magic man

Alright, you just calculated your maximum `Running Watts`, this defines what you can run your homelab at indefinitely before burning the wires in your walls.

> If you had 15 on the breaker. It would have been `1440` watts, but you already calculated that. right?

## What does my homelab use?

Now, go into your homelab, google, stare at your power bricks, you need to find the following information.

- If your computer only accepts an AC input
  - What is its max `Watt` rating
- If your computer/device has an external power brick.
  - What is its `Volts` and `Amps`

Sort all this together

| Device    | Volts    | Amps    | Watts    |
|---------------- | --------------- | --------------- | --------------- |
| Router | 12   | 5    |  60   |
| 6 port Switch    | 12   | 5   | 60   |
| 24 port edgemax switch    |  16-25  |    |  25  |
| NAS   |    |    | 600   |
| minipc x5   | 19   | 6   |   114 / 570 |

