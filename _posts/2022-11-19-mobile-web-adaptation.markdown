---
layout: post
title:  "Mobile web adapation"
date:   2022-11-19 14:00:00 +0100
categories: web mobile
---

According to [statistics](https://gs.statcounter.com/platform-market-share/desktop-mobile-tablet) approximately 60% of web browsing is done from a mobile:

{% include web-stats.html %}

So it is very important to be able to properly browse your website from a mobile. Having a website working perfectly in all desktop browser (at least major ones) is already a hard task. But doing same for all mobile browser is a nightmare.

In this post, some tricks will be seen to be able to adapt major "bug" on mobile browser.

## Big issue with 100vh
On mobile device, we have a navigation bar. This bar can ba at the top or at the bottom of the screen. The main problem of this bar is that if you use `100vh` it will be behind the bar. Yes, you read it well, behind the bar! Since the bar change its own height on scroll, it will reduce and expend the height during scroll.

Expended            |  Reduced
:-------------------------:|:-------------------------:
![navbar expended](/assets/img/navbar_expend.png)  |  ![navbar reduced](/assets/img/navbar_reduce.png)

So the `100vh` doesn't recaculate istelf. Fortunatley there is a trick that can be done to fix this.

We have to calculate it using Javascript:

```js
window.addEventListener('resize', () => {
    const vh = document.documentElement.clientHeight * 0.01;
    document.documentElement.style.setProperty('--vh', `${vh}px`);
});

```
Note: I directly put it on a resize event listener because on mobile you can rotate it so you have to deal with screen resizing. 
I didn't use `window.innerHeight` because after rotating the mobile, I had some issue on Samsung browser. 

Now let's use the `--vh` in CSS:
```css
.my-full-size-element {
  height: 100vh;
  height: calc(var(--vh, 1vh) * 100);
}
```

Of course you can reuse this logic to position absolute `div` at the bottom (but always upper than the nav bar 😁):

```css
/* Here it will appear 20px upper */
.my-bottom-element {
    position: absolute;
    top: 0;
    left: 0;
    height: 50px;
    width: 100%;
    margin-top: calc(var(--vh, 1vh) * 100 - 20px;
}
```

## Automatic zoom on safari/iOS
On iOS, you can have an issue with the inputs. When you write something in it, you have a zoom on the page.

Form view            |  Form view after input click
:-------------------------:|:-------------------------:
![navbar expended](/assets/img/input.png)  |  ![navbar reduced](/assets/img/input_zoom.png)

As you can see it on the right the scroll bar are there for horizontal and vertical.
This is due to accessibility on iOS/safari that enforce zoom on any input with a font size smaller than `16px`.

There are many ways to fix this issue like disable zoom but I don't like this solution. For me the best one is to enforce the `16px` minimum size on mobile device on inputs:

```css
@media screen and (-webkit-min-device-pixel-ratio:0) { 
    select,
    textarea,
    input {
      font-size: 16px !important;
    }
  }
```
<!-- ## Video autoplay iOS -->

<!-- ## Parallax effect on iOS -->


## Sources
- <https://css-tricks.com/the-trick-to-viewport-units-on-mobile/>
- <https://stackoverflow.com/questions/2989263/disable-auto-zoom-in-input-text-tag-safari-on-iphone>
