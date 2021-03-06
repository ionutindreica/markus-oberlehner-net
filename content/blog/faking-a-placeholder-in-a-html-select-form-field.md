+++
date = "2017-07-16T07:55:22+02:00"
title = "Faking a Placeholder in a HTML Select Form Field"
description = "Style a select form field using a placeholder as default value. Make a HTML form element look like an input field with placeholder attribute."
intro = "Styling native HTML form fields – especially select fields – with CSS has always been a little tricky. Recently I was confronted with the task of creating a select field with a placeholder value so that the select field blends in nicely with other form fields on the page. The problem of custom styled select elements is a hard one..."
draft = false
categories = ["Development"]
tags = ["Pure CSS", "CSS", "Forms"]
+++

Styling native HTML form fields – especially select fields – with CSS has always been a little tricky. Recently I was confronted with the task of creating a select field with a placeholder value so that the select field blends in nicely with other form fields on the page.

The problem of custom styled select elements is a hard one. Styling a select form field in a very specific way is often times impossible. For that reason, a lot of websites are replacing select elements with a custom built solution powered by HTML, CSS and JavaScript.

Most of the time this is a pretty bad idea. It is very hard to get accessibility right when building a custom form element. Many of those custom built select form fields do not work with screen readers at all or are very hard to use on mobile devices.

I'd recommend you to avoid building custom form elements at all cost. If you absolutely have to use a custom styled solution, use a battle tested library instead of rolling your own.

## Fiddling around
In my case it was not necessary to swap the native HTML select field with a fake select field. The problem at hand is, how to display a placeholder inside a select field.

At first I didn’t realise that the HTML select element does not support the placeholder attribute, I just assumed it does. The next thing I tried was using a disabled but default selected option element and setting the font color to the same grey as the input placeholder element. And this works in Firefox (and maybe even in Internet Explorer) but in WebKit and Blink based browsers, this does not work either.

## The solution
After playing around and noticing that you can change the color of the select element itself, I worked on the idea of setting the select elements color to placeholder grey as long as a disabled option is selected and changing the color to the default color as soon as the value changes.

After coming up with a simple JavaScript powered solution my “somehow this has to work without JavaScript” sense tingled again. After some research I found out I could use native browser form validation with the `required` attribute and the `:invalid` pseudo class to achieve the effect I was looking for.

<p data-height="265" data-theme-id="0" data-slug-hash="WOWrqO" data-default-tab="html,result" data-user="maoberlehner" data-embed-version="2" data-pen-title="Fake Select Placeholder with Pure CSS" class="codepen">See the Pen <a href="https://codepen.io/maoberlehner/pen/WOWrqO/">Fake Select Placeholder with Pure CSS</a> by Markus Oberlehner (<a href="https://codepen.io/maoberlehner">@maoberlehner</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

### Avoiding JavaScript at all costs
The problem with this solution is, that it only works for required form fields. To circumvent the need for JavaScript we can avoid using a placeholder in optional select fields altogether by providing a neutral default option like you can see with the second select field in the CodePen above.

### Sprinkles of JavaScript
Assuming that select fields are either always required or we are able to provide a default value for optional select fields is an assumption which might not hold true all of the time.

Although usually one of my pet peeves is to build functionality which requires (or seems to require) JavaScript, with pure CSS, in this case just some sprinkles of JavaScript could solve this problem once and for all.

<p data-height="265" data-theme-id="0" data-slug-hash="YQBQNj" data-default-tab="css,result" data-user="maoberlehner" data-embed-version="2" data-pen-title="Fake Select Placeholder with (CSS + JavaScript Fallback)" class="codepen">See the Pen <a href="https://codepen.io/maoberlehner/pen/YQBQNj/">Fake Select Placeholder with (CSS + JavaScript Fallback)</a> by Markus Oberlehner (<a href="https://codepen.io/maoberlehner">@maoberlehner</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

By setting the initial placeholder grey color of the element with JavaScript, we are save in case the user has disabled JavaScript, JavaScript didn’t load, the Browser couldn’t execute our JavaScript code or any other reason why JavaScript can be not available.
