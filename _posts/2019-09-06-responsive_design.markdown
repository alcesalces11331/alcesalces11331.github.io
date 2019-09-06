---
layout: post
title:      "RESPONSIVE DESIGN"
date:       2019-09-06 04:41:07 +0000
permalink:  responsive_design
---


## Why the basics go a long way

### What is responsive design?

When we're examining a webpage, what do we see? Containers, divs, images, all in a tidy arrangement. However, it is often a user visits a webpage on devices other than their desktop computers. It is because of this variation produced in viewer-height the designers need to reliably consider smaller viewing windows. It is also more and more common for the typical desktop user to utilize more than one monitor *or* to split their viewing window into more than one screen. Personally, I do this all the time if I need to reference two or more webpages or applications. It saves me time from alt-tabbing back and forth, especially when the number of referenced applications becomes numerous. 

Responsive design is the methodology of designing web applications to seamlessly adapt to a smaller or larger window size. This needs to happen on-the-fly as well as already be incorporated in. This is doable in a multitude of ways. Many frameworks have developed their own systems for handling responsive design, but it all comes back to the basics: modifying the HTML with CSS.

### HTML & CSS

The Hypertext Markdown Language is the architecture and skeleton of the web. It tells browsers *what* to display. Under the hood (even under the hood of this blog post), a myriad number of tags exist. What is really seen is containers within containers within containers. We have headers, body, divs, p... the list continues. All this builds the webpage, but without any styling (besides the basic styling inherent in HTML), it looks like a vacant structure. What's required is a way to style the *what*. 

With Cascading Style Sheets, we can tell the browser to apply a certain style to any of the containers. This is where building the web becomes a beast all its own. This is where a programmer can choose a font for the text, design and format the header, place a container on the bottom of the page which sticks to it. Cascading Style Sheets (better known as CSS) is the meat of the web -- and what makes it look pretty. However, before the web had natively built in responsive elements, i.e., Flexbox, Bootstrap, and CSS Grid, the sculpting was ugly. It was building with floats, inline-blocks and the ancestors of CSS Grid: tables. It left a lot to be desired and the elegant websites had to be executed using lines of Javascript. This is not to say those ancient elements do not have their uses. It means more efficient means to style websites exists and any wise programmer would be wise to pick them up. I'll touch upon the merits upon each of the three listed above, and, moreover, I'll discuss how they relate to media queries. I've found no one method is the best over all, but each have their strengths. To further elaborate on the elegance provided by the three methods I've listed above, I'll demonstrate each with an example.

For instance, to center a div on a page with normal CSS there are a few ways to do it:

#### Text-Align Method

Here's an example showing how to utilize text-align:
```
.arbitrary-div-container {
    text-align: center;
}

.arbitrary-div {
    height: 100px;
		width: 100px;
		display: inline-block;
}
```
You will notice it takes *two* CSS styles on elements to center our arbitrary-div. Furthermore, if we want to style the text within arbitrary-div-container, we have to specify it in another styling. The line `display: inline-block;` is necessary otherwise the arbitrary-div default to `display: block;` and will span the whole width of the page other than the 100px specified. 

#### Margin-Auto Method

Here's an example showing how to utilize margin auto:
```
.arbitrary-div {
    width: 100px;
    height: 100px;
    margin: 0 auto;
```
This method works because we've specified a width. If we don't specify a width the arbitrary-div will span outwards indiscriminantly. When we specify `margin: 0 auto;` what we're doing is telling the browser to render this div with 0px margin on each of its sides. This method has ramifications when the window is scaled down to a smaller size. This is because the margin will *always* be 0 on each side but because we have to specify definitive pixel width, the div will be hard to work around. However, it is an improvement on the previous text-align method as it only requires a single element's styling. 

#### Absolute Positioning

This method is incredibly effective, but has glaring weaknesses when scaled down. Here's the code for the absolute positioning method:
```
.arbitrary-div {
    height: 100px;
    width: 100px;
    position: absolute;
    left: 50%;
    margin-left: -50px;
}
```
The centering of this div is down with three lines: `position: absolute`, `left: 50%`, and `margin-left: -50px`. The styling created by `position: absolute` is maximum. It places the element forever at its position, which is defined by the other lines listed. We set `left: 50%;` to move the div 50% from the edge of the page, but this creates an issue which has to be fixed by setting the left margin of the arbitrary-div to -50px, exactly half the width declared. 

However, setting an elements position to absolute means when the display is scaled down to support smaller devices, it will be at that position *with* the width and the further positioning required to center it. This means support for keeping it in the center requires styling from other elements to prevent weird overlap, but also it will take up more of the page, which may lead to undesired results. 

### Flexbox

The beauty of Flexbox is underestimated. While CSS by itself allowed websites to be organized in a clunky, somewhat difficult way, Flexbox allows containers to fill and fit *within* parent containers. It's far simpler to utilize *and* it's responsive, which is exactly what we're looking for. It means we have to write less code and the code we do write goes the distance when we need to view the page on a smaller device. Looking at the same example but written with Flexbox styling:
```
.arbitrary-div-container {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.arbitrary-div {
    width: 300px;
    height: 300px;
}
```
Notice here, to make use of Flexbox styling to center the arbitrary-div, it is required to style the parent container as well. What is not specified is that all HTML, Body, and the parent div all need to be set at 100%. Doing this tells the browser this container is Flexbox styled. Two other lines are required to center the div: `align-items: center;` and `justify-content: center;`. This tells the browser to place the div center. Another huge bonus for using Flexbox instead of hard CSS is Flexbox is responsive. When we scale the page down to smaller sizes, no matter how large or small it gets, Flexbox will maintain the centering of the div. This means overall we can write less code to do more. 

This does bring up another leg of the expedition to understanding responsive design methodology, that of making use of CSS Grid

### CSS Grid

CSS Grid has some benefits over Flexbox. Namely, whereas Flexbox is primarily content-based, CSS Grid is layout based. This means it's better to blindly begin with CSS Grid rather than Flexbox, but only if you've no idea what the content is you're going to be programming with. Furthermore, CSS Grid can be useful when scaling down styles to meet size restrictions. Per [w3schools](https://www.w3schools.com/css/css_rwd_mediaqueries.asp):
```
.col-1 {width: 8.33%;}
.col-2 {width: 16.66%;}
.col-3 {width: 25%;}
.col-4 {width: 33.33%;}
.col-5 {width: 41.66%;}
.col-6 {width: 50%;}
.col-7 {width: 58.33%;}
.col-8 {width: 66.66%;}
.col-9 {width: 75%;}
.col-10 {width: 83.33%;}
.col-11 {width: 91.66%;}
.col-12 {width: 100%;}
```
the grid format separates vertical segmentation into 12 different sizes. I've found this useful when explicitly scaling from desktop to mobile, as it requires writing code for a definitive break point, usually max-width: 768px. When the screen size gets below 768px, it is useful to code only using `[class*="col-"] { width: 100%; }`. The scaling simply becomes a single column, vastly narrowing the scope for what requires to be coded. Another benefit of using Grid over Flexbox is the usefulness of detailing large-scale layouts. The level of complexity accomodated by CSS Grid exceeds that of Flexbox. Depending on the requirements of the project, either or both, are useful tools at the programmer's disposal. 

Comparing Flexbox and CSS Grid favors both, but each have their strengths and weaknesses. Whereas it is useful to scale headers and footers (this is due to them having a unilateral layout) using Flexbox, it is better -- for more complex bodies -- to make use of Grid (due to it have multiple dimensions scaled). 

### Media Queries

With all which we have covered so far, it is a small step to discuss media queries. Essentially, with a media query, the browser is waiting until a condition is filled. These conditions are usually from screen sizes. This is how a programmer is going to tell the browser which CSS styling to use when a screen is enlarged or shrunk from its current size. Following mobile-first layout strategies, here is what a sample media query looks like using the CSS Grid scaling from the example immediately above:
```
/* For mobile phones: */
[class*="col-"] {
    width: 100%;
}

@media only screen and (min-width: 768px) {
    /* For desktop: */
    .col-1 {width: 8.33%;}
    .col-2 {width: 16.66%;}
    .col-3 {width: 25%;}
    .col-4 {width: 33.33%;}
    .col-5 {width: 41.66%;}
    .col-6 {width: 50%;}
    .col-7 {width: 58.33%;}
    .col-8 {width: 66.66%;}
    .col-9 {width: 75%;}
    .col-10 {width: 83.33%;}
    .col-11 {width: 91.66%;}
    .col-12 {width: 100%;}
}
```
Using media queries allows divs to be hidden as well. This is incredibly useful for an image which may be centered and taking up a large space on the desktop level of screen size. When the screen size is shrunk to the condition set by the media query, the div/image will be hidden. 

### Bootstrap

This is a unique category all its own. Bootstrap is a framework providing a bunch of styling options built in. What Bootstrap does (I'm primarily trained in React Bootstrap) is provide custom styling using, in this case using React JSX. This allows the programmer to develop, build, and maintain code with only using code which builds the HTML and the CSS for you. Bootstrap has a built in default styling which can be quickly used to develop mock drafts of layouts for the programmer to provide to project leads or clients. It allows the use of CSS Grid and Flexbox, along with regular ol' CSS, but without the hard programming required to architect the hard layout. 

What I've learned is Bootstrap is best utilized with other methods of styling. It allows for the ease of creating HTML and frees the programmer up for more abstract or mentally intensive crunch. 

## The Treasure

And there we have it. Styling a webpage and ensuring it is responsive is a matter of following the basics then building upon it. Whether you use one, two, or a combination of all listed, designing and building a webpage is a walk in the park.


