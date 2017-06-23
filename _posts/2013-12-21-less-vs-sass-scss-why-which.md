---
title: "LESS vs SASS - Why to Use Them and Which to Use"
excerpt: "LESS vs SASS: Why we should use them, and which one should you use?"
tags: 
  - LESS
  - SASS
categories:
  - Development
comments: true
header:
  image: /images/sass-less.png
  caption: "Photo Credit: [Bootstrap](http://getbootstrap.com/)"
---

{% include toc title="Overview" icon="file-text" %}

## LESS and SASS Overview

LESS and SASS (or SCSS) are High-level dynamic stylesheet languages created to help create cleaner and more modular stylesheets. SCSS is the predecessor to SASS, providing native CSS support. This means, like LESS, SCSS is a superset of CSS, allowing CSS to be "dropped in" and still be valid at compile time. With this functionality, development integration to pre-existing styles becomes quick and painless.


# Primary Features

Some of the main features that LESS and SASS provide are: variables, nesting (or inheritance), & mixins. These solve a variety of problems that plain CSS creates. In addition, these two languages allow "normal" css to be used withing their language. This means that porting is easy as even if you only modify a few lines, the whole stylesheet is still valid.

## Nesting (Inheritance)

For example, say you wanted to set the property of a child element of a parent element. You would have to define in a single line both the parent element and the child element. If you then wanted to set the property of another child element, you would again have to copy the parent's identity in addition to the child's.

For small CSS projects this may seem acceptable, and in reality it is. What happens, though, for large websites and applications? You have a very large CSS code base with duplicated styles. This easily becomes hard to manage, modify, and extend. In addition, imagine you decide you need to namespace it to allow external CSS stylesheets to work with your current styles. You would have to go through each and every line to add your namespacing scope. If any classes change, again you would have to go through very many lines to change them.

How does this work exactly? Look at the before and example below. You can easily see how, in addition to increasing maintainability, the code is much easier to read and understand.

<div></div>

**CSS:**

{% highlight css %}
/**
 *  Project is namespaced as "my-project"
 */

.my-project.my-project-container { 
    width: 1000px;
}

.my-project.my-project-container h1,
.my-project.my-project-container h2,
.my-project.my-project-container h3,
.my-project.my-project-container h4,
.my-project.my-project-container h5 {
   margin: 20px 5px;
   color: #ff0000;
   font-weight: normal;
}
{% endhighlight %}


**LESS:**

{% highlight scss %}
/**
 *  Project is namespaced as "my-project"
 */

.my-project { 
    &.my-project-container {
        width: 1000px;

        h1, h2, h3, h4, h5 {
            margin: 20px 5px;
            color: #ff0000;
            font-weight: normal;
        }
    }
}
{% endhighlight %}

As you can clearly see, by nesting you can easily create a hierarchy of style rules that becomes easy to modify and extend.

## Variables

Variables are another great feature that both LESS and SASS provide. Simply stated, you can define any CSS property value in a variable and re-use that value across all stylesheets. This makes making changes to things such as colors across an entire site as simple as editing the one variable.

## Mixins

The final of the 3 major features that both LESS and SASS provide are mixins. Mixins allow you to re-use classes within other CSS rules. Mixins also allow for variables to be passed in  to modify the way that mixin outputs CSS, similar to a function. Below are examples from their respective websites of mixins in both LESS and SASS.

<div></div>

**LESS**

{% highlight scss %}
.rounded-corners(@radius: 5px) {  
    border-radius: @radius;  
    -webkit-border-radius: @radius;  
    -moz-border-radius: @radius;  
}  
#header {  
    .rounded-corners;  
}  
#footer {  
    .rounded-corners(10px);  
}
{% endhighlight %}

**SASS**

{% highlight scss %}
@mixin border-radius($radius) {  
    -webkit-border-radius: $radius;  
    -moz-border-radius: $radius;  
    -ms-border-radius: $radius;  
    -o-border-radius: $radius;  
    border-radius: $radius;  
}  
.box {  
    @include border-radius(10px);  
}
{% endhighlight %}

# Differences

LESS and SASS are very powerful languages and are very similar in feature sets. In fact, at this time as far as I can tell, neither has a major benefit over the other. LESS does provide client side compilation, but that feature is limited and not as useful. So what are the differences? Syntax.

LESS is true to it's name when it comes to its syntax. LESS looks almost identical to CSS, therefore the learning curve is very low. With few keywords and the logic language being the familiar JavaScript, it is excellent for quick integration without any history with CSS superset languages. Variables are defined with the "@" symbol, and mixins are just classes with arguments.

SASS on the other hand has a very defined language structure. They have more than a few reserved words and have a specific way of utilizing functions and mixins. They also have their own logic framework, meaning they have their own language spec on how to do loops and conditional statements.

# Which to Use?

In terms of features and power, it's a definitive tie. You might go with LESS if you would like to test using the client-side loading feature of the LESS instead of compiling each time you modify the stylesheets.

The only reason to choose one over the other is really a matter of preference. Each language has very different language syntax. LESS leans toward being more easy to catch on, even for designers. Unless you have a team already familiar with SASS, my recommendation would be to check out LESS.