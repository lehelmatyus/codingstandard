# I. Front-End Standards and Best Practices at Urban Insight 

_Maintained by Lehel Mátyus - Director, Front-End Engineering at Urban Insight, inc._  

Edit: https://bitbucket.org/urban-insight/front-end-standards/src/master/I.%20Front%20End%20Standards%20-%20Best%20Practices.md

This document to be revised every 3 months and updated to accommodate to ever changing requirements of the web.   
Last Updated: **5/1/2018**  
Next Update: **8/1/2018**

## The 5 Pillars of UI's Front-End Standards

1. **The way of the code** 
    - 1.1 HTML 
        - 1.1.1 HTML Syntax
        - 1.1.2 HTML HTML General Rules
    - 1.2 CSS
    - 1.3 SASS/LESS Rules
        - 1.3.1 SASS/LESS General Rules     
        - 1.3.2 BEM General Rules     
        - 1.3.3 UTILITY Classes General Rules     
        - 1.3.4 MIXINS General Rules     
        - 1.3.5 SASS/LESS File Structure and task runner   
    - 1.4 Javascript Rules (ES5 version)   
    - 1.5 Performance, Optimize for Speed as You Develop        
2. **Design systems, component based design**
3. **Leveraging front-end frameworks**
4. **Accessibility, 508 Compliance and WCAG 2.0**
5. **Front-end StarterKits**



This document describes the front-end standards and best practices used at Urban Insight by developers and engineers. In other words rules for stuff that we don't think about because we are too busy writing code. By following the rules consistently we ensure we write code that is:

- Fun to write
- Reusable
- DRY (dont repeat yourself)
- Easy to understand and easy to support
- Easier to take over by a different developer
- Easy to train a new developer
- Upholds industry standards and best practices
- Increases our productivity
- Compliant with gov. regulations


Other documents in the UI Front-End standards series:

- II. Drupal 8 Front-End Standards
- III. WordPress Front-End Standards
- IV. Decoupled JS Framework Standards
- V. Front-End Onboarding Training Program    


## 1. The Way of the Code

### 1.1 HTML 

#### 1.1.1 HTML Syntax
- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment
- Nested elements should be indented once (two spaces)
- Always use double quotes, never single quotes, on attributes
- Don’t omit optional closing tags (e.g. `</li>` or `</body>`)
- Enforce standards mode and more consistent rendering in every browser possible with this simple doctype at the beginning of every HTML page
~~~~html   
<!--  Enforce standards mode -->
<!DOCTYPE html>
<html>
<head>
</head>
</html>
~~~~

- Practicality over purity - strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible.

#### 1.1.2 HTML General Rules
- Never use inline styles - don’t mix CSS with HTML
- Never use inline JavaScript - don’t mix Javascript with HTML
- Include external CSS inside the HEAD tag
- Use lowercase in your tags
- Structure your HTML using all the tags trying to make it easier to read
    - se the new HTML 5 elements like `<header>, <footer>, <article>` and others
    - use semantics elements
- Base your styles in the HTML structure, not the other way around. 
    - Creating the HTML first allows you to visualize the entire page as a whole, and to think of your CSS in a more holistic, top-down manner.

- Avoid using `<br>` tags to separate paragraphs or lines of text. Use `<p></p>` instead with proper opening and closing elements.    

- Attribute order - HTML attributes should come in this particular order for easier reading of code. Classes make for great reusable components, so they come first. Ids are more specific and should be used sparingly (e.g., for in-page bookmarks), so they come second.

~~~~html

    class
    id, name
    data-*
    src, for, type, href, value
    title, alt
    role, aria-*

    <!-- IDEALLY -->
    <a class="..." id="..." data-toggle="modal" href="#">
    Example link
    </a>

    <input class="form-control" type="text">
    <img src="..." alt="...">
~~~~
- Reduce markup
    
~~~~html
    <!-- Not so great -->
    <span class="avatar">
        <img src="...">
    </span>

    <!-- Better -->
    <img class="avatar" src="...">
~~~~

- When writing template files for major sections describe your closing tags

~~~~html
    <div id="sidebar">
        <div id="sub" class="first left">
        ...
        </div><!-- #sub.first.left -->
    </div><!-- #sidebar -->
~~~~
- Don't do `@import` in CSS this is not `import something.less` which is fine inside a preprocessor

~~~~css
    <!-- DONT! -->
    <style type="text/css">
        @import url('a.css');
        @import url('b.css');
    </style>
    
    <!-- the @import directive is much slower than the other way  -->

    <!-- DO THIS INSTEAD -->
    <link rel='stylesheet' type='text/css' href='a.css'>
    <link rel='stylesheet' type='text/css' href='b.css'>
~~~~

- IE Hacks are OK as long as they are separated in files and used in conditionals
    
~~~~~~~~css
    // DONT DO THIS!
    height: 200px; /* normal browsers */
    _height: 300px; /* IE6 */
    .height: 250px; /* IE7 */
    *height: 350px; /* All IEs */
~~~~~~~~
   
~~~~~~~~html
    <!-- DO THIS INSTEAD -->

    <link href="style.css" rel="stylesheet" type="text/css" />
    <!--[if lte IE 6]>
    <link href="ie.css" rel="stylesheet" type="text/css" />
    <![endif]-->
~~~~~~~~

- If possible place Javascript file at the bottom,   
    - by placing Javascript files at the bottom of your documents, you’ll ensure that JS files will be loaded only when the content has been properly displayed
    
~~~~~~~~html
        ...
            <script type='text/javascript' src='jquery.js?ver=1.3.2'></script>
        </body>
    </html>
~~~~~~~~    
    
### 1.2 CSS

- CSS Should:
    - Be easy to maintain.
    - Follow clear enough patterns to understand.
    - Offer a clear place for new styles going forwards.
    - Not be a drag on page loading performance.
    - Not include unused style rules.
    - Address different devices, browser versions, and do as much as it can with as little code as possible.

- If not using a framework like Bootstrap that does a css rest be sure to use Normalize.css http://necolas.github.io/normalize.css/
- Organize your code with comments
- Write code using multiple lines and spaces
- Build proficient selectors
    - avoid location specific selectors
    - don't use ID's in your selectors or overly specific selectors

- Use the minimum specificity required to achieve the desired style.    
    
~~~~~~~~css
    /* BAD */
    .button#back-button { ... }
    .popular ul li a { ... }
    .popular > ul > li > a { ... }

    /* GOOD */
    .back-button { ... }
    .popular-link { ... }
    .unpopular-link { ... }
~~~~~~~~

- Avoid using the `!important` keyword. Treat it like the nuclear option, only to be used in the most extreme of cases. This fundamentally destroys the specificity feature and can even break accessibility for some users.

- Vendor Prefixes
    - When using vendor prefixed features, put the standardized rule at the end to ensure browsers optimize and use the standard if they recognize it. 
    
~~~~~~~~css
    .thing {
        -webkit-transition: all 100ms;
        transition: all 100ms;
    }
~~~~~~~~

- When Using a preprocessor LESS/SASS add Grunt or Gulp packages to your task runner to do the vendor prefixing for you see "autoprefixer" grunt script or similar.

- ID selectors `#something` should be minimized, as noted above, use the lowest level of specificity necessary to get the desired results.

- Components should not be responsible for their positioning or layout within the site. Never apply widths or heights except to elements that natively have these properties (e.g. images have these properties, so it's okay to use CSS to modify their width and height). Within components, separate structural rules from stylistic rules.

### 1.3 SASS/LESS Rules

#### 1.3.1 SASS/LESS General Rules

- SASS/LESS Compiler and task runner
    - Default LESS and SASS Compiler and task runner of UI is **gulp.js** `https://gulpjs.com/`
    - If a specific framework insists on a different one, feel free to use a different one

- When writing LESS/SASS try to not nest more than 3 levels Deep
~~~~~~~~less
    .class1 {
        .class2 {
            .class3 {
            }
        }
    }
~~~~~~~~

#### 1.3.2 BEM General Rules

- When naming visual components use the **BEM** methodology to create reusable elements
    - BEM - block, element, modifier - is a CSS naming methodology that aims to organize and modularize code in a way that is transparent and informative to developers.
    - BEM — Block Element Modifier http://getbem.com/

- Naming convention
    - Block naming convention : simply make up a name for the block
    - Element naming convention: give the element a name and prepend it with block name plus 2 underscores
        - formula:  `block_class` +  `__` + `element_class`
    - Inner elements don't get the outer elements name only the block name just like outer elements
        - same formula:  `block_class` +  `__` + `element_class`

~~~~~~~~~~~~html
    <!-- EXAMPLE 1 -->
    <!-- Generic Example -->
    <div class="block-name">
        ...
        <div class="block-name__element-name">
            ...
            <span class="block-name__another-element">
            </span>
        </div>
        ...
    </div>

    <!-- EXAMPLE 2 -->
    <div class="hero-slider">
        ...
        <span class="hero-slider__headline"></span>
        <span class="hero-slider__main-text"></span>
    </div>

    <!-- EXAMPLE 3 -->

    <div class="article-preview">
    <img class="article-preview__image" src="https://i.vimeocdn.com/video/4848asd2_1280x720.webp" alt="">
    <div class="article-preview__content">
        <h2 class="article-preview__title">Stubbing Eloquent Relations for Faster Tests</h2>
        <p class="article-preview__body">
        In this quick blog post and screencast, I share a trick I use to speed up tests that use Eloquent relationships but don't really depend on database functionality.
        </p>
    </div>
    </div>

~~~~~~~~~~~~

- Modifier naming convention
    - Flags on blocks or elements. Use them to change appearance, behavior or state.
    - Flags are named as the `element_class or block_class` + `--` + `modifier_class` 
    
~~~~~~~~~~~~html
    <!-- EXAMPLE 1 -->
    <!-- Element + Modifier -->
    <button class="button">	Normal button </button>
    <button class="button button--state-success"> Success button </button>
    <button class="button button--state-danger">Danger button</button>

    <!-- EXAMPLE 2 --> 
    <!-- Block, Element, Modifier -->
    <form class="form form--theme-xmas form--simple">
        <input class="form__input" type="text" />
        <input class="form__submit form__submit--disabled" type="submit" />
    </form>
    
~~~~~~~~~~~~

- BEM will enable you to write comprehensive SASS/LESS code
    
~~~~~~~~~~~~less
    // BLOCK, ELEMENTS FLAGS
    block{
        //...
        &__elem{
            //...
            &--flag1{
                //...
            }
            &--flag2{
                //...
            }
        }
    }

    // LESS EXAMPLE 1
    .button{
        display: inline-block;
        border-radius: 3px;
        font-size:13px;
        color: #333;
        &--state-success{
            color: green;
        }
        &--state-danger{
            color: red;
        }
    }
~~~~~~~~~~~~

#### 1.3.3 UTILITY Classes General Rules    

- Use **UTILITY** classes in order to write lite-framework like themes that are easy to manage and modify
    - Utility classes should be used inside your LESS/SASS files not in markup always have one extra layer between them

**Bad Example**
~~~~~~~~~~~~css
    // BAD Example

    .font_12{
        font-size: 12px;
    }
    
    <p class="font_12">Hello World<p>
        
~~~~~~~~~~~~

**Good Example**
    
~~~~~~~~~~~~css

    // GOOD Example
    .font_12{
        font-size: 12px;
    }
    .small_text{
        color:gray;
        .font_12;
    }

    <!-- file1.html -->
    <p class="small_text">Hello World</p>

    <!-- file2.html ... file_n.html --> 
    <p class="small_text">Hello World Again</p>

~~~~~~~~~~~~

#### 1.3.4 MIXINS  General Rules   

- **MIXINS**: Write short mixins for LESS and use @extend for SASS
    - only ever do it for 2 levels, overdoing it will complicate things in the long run
    
~~~~~~~~~~~~css
        // LESS
        .message {
            padding: .5em;
            font-size:12px
            border: 1px solid green;
        }

        .message-important {
            .message;
            font-weight: bold;
        }

        .message-error {
            .message-important;
            border: 1px solid red;
        }
    
~~~~~~~~~~~~
    
~~~~~~~~~~~~css
        // SASS

        .message {
            padding: .5em;
            font-size:12px
            border: 1px solid green;
        }

        .message-important {
            @extend .message;
            font-weight: bold;
        }

        .message-error {
            @extend .message-important;
            border: 1px solid red;
        }
    
~~~~~~~~~~~~
    
~~~~~~~~~~~~css
        // OUTPUT

        .message, .message-important, .message-error {
        padding: .5em;
        font-size:12px;
        border: 1px solid green;
        }

        .message-important, message-error {
            font-weight: bold;
        }

        .message-error {
            border: 1px solid red;
        }
    
~~~~~~~~~~~~

#### 1.3.5 SASS/LESS File Structure

- Use the two tier organization pattern, comment out each section inside the file
    - use `general.less` - sections:
        - framework specific overrides
        - utility classes
        - utility mixins
        - default layout
        - default and fallback styles for elements
        - component styles (*component styles may life withing component files if framework like Angular etc requires it.)
    - use `page.less` - sections:
        - page specific styles
        - page specific layout
        - page specific derivates of components


### 1.4 Javascript Rules (ES5 version)

- Embrace Progressive Enhancement, do your best to compensate for when JavaScript is disabled. 

- Comment Your Code, be kind to your future self and others. 


- When possible, using Gulp (or Grunt) task runner addd JSLint tool to identify common JavaScript Issues

- Raw JavaScript can always be quicker than using a library,however if necessary use a library but load only for the pages that use it.

- Include All Necessary Semicolons;

- Use `camelCase` for identifier names (variables and functions).

~~~JavaScript
firstName = "John";
lastName = "Doe";

price = 19.90;
tax = 0.20;

fullPrice = price + (price * tax); 
~~~
 
- Always put spaces around operators ( = + - * / ), and after commas:

~~~ JavaScript
var x = y + z;
var values = ["Volvo", "Saab", "Fiat"]; 
~~~

- Strictly ‘use strict’ 

~~~~Javascript
//myGreatApp.js
"use strict"; // could have unforeseen effects

(function (){
    "use strict";
    // do incredible things
})();
~~~~

- Use Explicit Blocks

~~~Javascript
// DONT
if (i > 3)
   doSomething();

// DO THIS INSTEAD
if (i > 3) {
   doSomething();
}   
~~~

- Start Blocks on the Same Line
~~~Javascript
if(myState === 'testing') {
   console.log('You are in testing');
} else {
   console.log('You are in production');
}
~~~

- Use === to Test Equality
~~~Javascript
if(1 === '1') //Returns false
if(1 == '1') //Returns true

if(0 === '') //Returns false
if(0 == '') //Returns true
~~~

- Use a Namespace, not using it makes your code extremely vulnerable to being affected by other code

~~~Javascript
var MyNamespace = {};
MyNamespace.cost = 5;
//...time goes by...
console.log(MyNamespace.cost);
~~~

- Do Not Use "With"

~~~Javascript
//DONT
with (myNamespace.parent.child.person) {
   firstName = 'Jon';
   lastName = 'Smyth';
}

// DO THIS INSTEAD
var p = myNamespace.parent.child.person;
p.firstName = 'Jon';
p.lastName = 'Smyth';
~~~

- Use Var to Declare Variables, use the scope in a smart way.

~~~JavaScript
function carDemo() {
   var carMake = 'Dodge';
   carModel = 'Charger';
}
~~~
- For Same type of variables use var only once

~~~JavaScript
var someItem = 'some string';
var anotherItem = 'another string';
var oneMoreItem = 'one more string';

// BETTER

var someItem = 'some string',
    anotherItem = 'another string',
    oneMoreItem = 'one more string';
~~~

- Use Decimals Cautiously

~~~Javascript
var hamburger = 8.20;
var fries = 2.10;
var total = hamburger + fries;
console.log(total); //Outputs 10.299999999999999

hamburger = hamburger * 100;
fries = fries * 100;
total = hamburger + fries;
total = total / 100;
console.log(total); //Outputs 10.3
~~~

- Declare All Variables First, JavaScript utilizes function-level scoping of variables and functions. When a variable is declared, the declaration statement gets hoisted to the top of the function. 

~~~Javascript
function complexExample() {
   var testOne;
   function testTwo(){ return 'Hi from test two'; }
   var i;
   i = 7;

   console.log(i);         //The message says 7
   console.log(testOne()); //This gives a type error saying testOne is not a function
   console.log(testTwo()); //The message says "Hi from test two"

   testOne = function(){ return 'Hi from test one'; }
   i = 2;
}
~~~

- Avoid use of switch fall through
~~~Javascript

// DONT
switch(i) {
   case 1:
      console.log('One');
      break;
   case 2:
      console.log('Two');
   case 3:
      console.log('Three');
      break;
   default:
      console.log('Unknown');
      break;
}

// DO THIS INSTEAD

switch(i) {
   case 1:
      console.log('One');
      break;
   case 2:
      console.log('Two');
      break;
   case 3:
      console.log('Three');
      break;
   default:
      console.log('Unknown');
      break;
}
~~~

### 1.5 Performance, Optimize for Speed as You Develop 

* Using minimum DOM elements in web pages
* Limit HTTP Requests, very important
* Optimize Image Size, images are taking at least 80% of the total page load time. 
    - when possible we optimize image size and using lazy loading concepts (on demand loading) for images so that will not block required content. We are reducing number of DOM elements in pages.
* Load JS after CSS  
    * Every Request fetched Inside of HEAD, will Postpone the rendering of the page
* Avoid inline JavaScript code    
* Clean Frameworks before use, get rid of bloat
* Avoiding `@import` tag for CSS anywhere in website


## 2. Design systems, component based design

### 2.1 Breaking down the component based design

Component Based Design is based on Atomic Design which is methodology for creating design systems.
Atomic design provides a clear methodology for crafting design systems. 
Component Based Design gives us the ability to traverse from abstract to concrete. Because of this, we can create systems that promote consistency and scalability while simultaneously showing things in their final context. And by assembling rather than deconstructing, we’re crafting a system right out of the gate instead of cherry picking patterns after the fact.

- The 5 Levels of the Component based Designs are   
    - Elements
    - Components
    - Compositions
    - Layout
    - Pages

- **Element**: is a visual structure that can not be further broken down without loosing its purpose of existing.  example: (Buttons), (knobs), (input fields and labels)
  - properties: Element may act and react based on it's state, component and environment placed in or user interaction.

- **Component**: is a visual structure that made of at least 4-5 elements logically placed together that form a pattern that is repeated in compositions OR throughout the system.
    - properties: may rearrange itself based on : the elements in it, environment placed in.

- **Compositions** are assemblies of components functioning together as a unit to serve a purpose.
    - properties: it can change the behavior of components inside. It can change it's own mode of behavior based on media queries.

-  **Layout** is a more abstract collection of design principles. Herein the amounts of whitespace, grids and wrappers are defined..

- **Pages**: Each Page consists of an arrangement of Compositions and Components.
    - properties: pages are able to handle exceptions and overrides

    
### 2.2 Converting a Component Based Design into code

- Start with the most simple elements that can not be broken down any further without losing it's purpose and   is repeated trough-out the design
    - set up LESS/SASS Classes for them and create the element styles
    - set up variables as you go, for font size, color etc.
    - as you go set up any necessary utility classes that makes your development easier
~~~~~~~~LESS
        //EXAMPLE UTILITY CLASS
        .font_12{
            font-size: 12px;
        }
        .small_text{
            .font_12;
        }

        // EXAMPLE USE UTILITY CLASS IN ELEMENT
        .description_text{
            .small_text;
            color:@gray;
        }
~~~~~~~~
- Move on to Components that have simple display logic in them, these may have elements appearing/dis-appearing changing order or even change shape based on the context they are placed in but have a uniquely identifiable visual structure and repeat through-out the design
    - Set up BEM Structures for them
    - modify existing or add extra utility classes if the design requires it.
    - if using `Drupal 8` or a `WordPress` theme that allows it consider moving the HTML markup of the components into their separate files under `/components` folder

~~~~~~~~LESS
        // Following the BEM Structure
        .block
        .block__element
        .block__element--modifier
        .block--modifier
        .block--modifier__element

        // Example
        .hero-slider
        .hero-slider__headline
        .hero-slider__main-text
        .hero-slider__main-text--orange
~~~~~~~~  

- Identify **compositions** of the Components that you identified
    - create collector classes and container classes for these
    - set up the necessary MediaQueries and styles

- Identify the overall **layout**, and sections on pages (header, footer, sidebar etc.)
    - Create the **most generic page** template or fall back page template and add the individual sections to the HTML markup
    - Set up MediaQueries and additional needed styles

- Move on to other specific **pages** create their template files, identify new sections or removal of sections.
    - Identify overrides to specific: layouts, compositions and components
    - Add the specific new wrappers if needed to the newly created HTML templates
    - Add the necessary new SASS/LESS CSS rules to `page.less` file, creating a commented out special section for each page in the less file.

Every Time a component is done, or a page is themed hand it off to Quality Assurance to review it.

## 3. Leveraging Front-End Frameworks 

- Preferred Front-End Framework of Ui is Twitter's Bootstrap front-end component library   
    web: `https://getbootstrap.com/`  
    git: `https://github.com/twbs/bootstrap`

- Compiling the framework
    - Always compile from source files
    - Compile only what you need, to get rid of bloat

- LESS/SASS Compiler and task runner
    - Default LESS and SASS Compiler and task runner of UI is **gulp.js** `https://gulpjs.com/`
    - If a specific framework insists on a different one, feel free to use a different one

- Compress JavaScript and CSS files with a task runner
    - Exception is for Drupal which will compress CSS and JavaScript files anyway

- When using a StarterKit follow the rules of the StarterKit to set up the files of the framework is uses in order to leverage the StarterKit.


### 3.1 The Structure 

- The Component Based Design works well with the two file structure
    - `general.less` - to hold utility classes, element, component and composition styles because they all build upon each-other
    - `page.less` - to hold page specific overrides of compositions and layouts 

- Both of these files needs to have thoroughly commented out sections for each level, each component and override, example:
    - general.less
~~~~~~~~LESS
        // general.less 

        // --- Table of contents ---- [LM 1.0 marking standard]
        // Variables
        // Utility_styles
        // Element_Styles
        // Component_styles
        // Layout_styles


        // --------------- Variables
        @white: white;
        @gray: #ccc;

        // --------------- Utility_styles
        .small_text{}
                ...
        // --------------- Element_Styles
        .navigation_styles{}
        .form_elements_styles{}
                ...
        // --------------- Component_styles
        .login_block{}
        .hero_slider{}
                ...
        // --------------- Layout_styles
        .header{}
        .sidebar{}
        .footer{}
~~~~~~~~

- page.less

~~~~~~~~LESS
        //page.less

        // --- Table of contents ---- [LM 1.0 marking standard]
        // Home_page_styles
        // Browse_Page


        //------------------------------------------- Home_page_styles 
        ...

        //------------------------------------------- Browse_Page
        ...
~~~~~~~~

- Each of these pages need to be included into the end of the `styles.less` file that will also compile the framework that the theme is leveraging. Example:

~~~~~~~~LESS
    // Bootstrap library.
    @import 'bootstrap';

    // Base-theme overrides.
    @import 'overrides';

    // Fonts
    @import 'font-awesome/less/fontawesome-all.less';

    // Theme Specific
    @import "general.less"; 
    @import "page.less"; 
~~~~~~~~

- This way we can leverage the whole force of the framework (bootstrap variables, mixins, mediaqueries) in the files we work with and end up with only one `styles.css` file 


----

## 4. Accessibility, 508 Compliance and WCAG 2.0

- Provide "Skip Navigation" and/or "Skip to Content". It should be present and linking to the correct anchor or heading.

- Semantic Structure: When Building Components be sure to follow a semantic structure for headings. There should be no missing headings in the hierarchy.
  - **Test**: "Firefox Developer Tools –> Information –> Document Outline". 

- Always provide alternative Text for Images and Icons: 
    - **Test**:  for missing Alternate Text for images using Chrome WAVE extension.

- Alternative text for Fonticons and Image buttons. Buttons with no text in it should provide a text for screen readers. This is achievable in the bootstrap framework by adding a span with the class "sr-only".  
    
~~~~~~~~~~~~html
    // for instance a close button for a modal with character "X" is enough when visually placed 
    // but for screen-readers extra textual information is needed

    // INSTEAD OF THIS
    <button aria-label="Close" onclick="myDialog.close()">X</button>

    // DO THIS
    <button onclick="myDialog.close()"><span class="sr-only">Close</span>X</button>
~~~~~~~~~~~~

**Test** :  for linked font- icons that do not have alternate text using Chrome WAVE extension.


- Forms and Form Labels. All input fields should be associated with a `<label>` element. The for attribute of the `<label>` element should contain the ID of the corresponding input field.
    - **Test**: Check for form fields that do not have appropriate labels or labels that do not have form fields using WAVE.
    
~~~~~~~~~~~~html
    <label for="home-address">Home Address</label>
    <input id="home-address" type="text">
~~~~~~~~~~~~

- Tables can cause many issues the most prevalent one is empty headers
    - Tables carry visual information in the way the TD elements are organized, if this information is not carried over be sure to provide a short description below the table what the data shows.
    - The `<caption>` element is the recommended way to describe a table for both sighted and sight-impaired users
        - **Test**: Check for any issues with TABLES using WAVE.
    
~~~~~~~~~~~~html
    <table>
        <caption>First two U.S. presidents</caption>  <!--Add This -->
        <thead> 
            <tr>
                <th scope="col">Name</th>
                <th scope="col">Took office</th>
                <th scope="col">Party</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>George Washington</td>
                <td>April 30, 1789</td>
                <td>n/a</td>
            </tr>
            <tr>
                <td>John Adams</td>
                <td>March 4, 1797</td>
                <td>Federalist</td>
            </tr>
        </tbody>
    </table>
~~~~~~~~~~~~

- Identify any other issues such as DOCTYPE, ARIA Elements 
    - **Test**: using WAVE tool.

- Color Contrasts: If WAVE reports any contrast errors use Chrome Developer Tools:
    -    Select failed element and "Inspect" element.
    -    Then select "Accessibility Properties"
    -    Review contrast ratio and recommended replacement colors
    -    Repeat for all elements identified by WAVE.

- Keyboard Interactivity and Focus
    - Tab through all elements of the web page using only your keyboard.
    - Are all elements accessible via keyboard only? (Examples: pulldown menus, popup dialogs, etc.)
    - Is the tab order logical? (Particularly for forms)

- Screen Reader Test: Use MacOSX Voiceover (or equivalent) to review the page.
    - Is the order logical?
    - Is all information on a page read out aloud?
    - Do all elements make sense when read out aloud?

- Disable Javascript and test if the information on the page is readable and all information is accessible.
- Disable CSS and review if the information on the page is still readable and all information is accessible.

## 5. Front-end StarterKits

### Front End Starterkits
| Starterkit| For | Description | Status | Link | Maintainer |
|-----------|-----|-------------|--------|------|------------|
| d8-gulp-starter-theme | Drupal 8 | Bootstrap 3.7 Childtheme for D8 | ready for use | [ d8-gulp-starter-theme ](https://bitbucket.org/urban-insight/d8-gulp-starter-theme/src/master/)     |Evan & Lehel|
| <del>startertheme-d8-b3</del> | <del>Drupal 8</del> | <del>Bootstrap 3.7 Childtheme for D8</del> | Deprecated | <del>[ startertheme-d8-b3 ](https://bitbucket.org/urban-insight/startertheme-d8-b3)</del>     |Lehel|
| startertheme-d7 | Drupal 7 | Bootstrap 3.7 Childtheme for D7 | ready for use | [ startertheme-d7 ](https://bitbucket.org/urban-insight/starter-static)     |Lehel|
| starter-wp-child-theme |WP| WordPress Child Theme Skeleton | ready for use | [ starter-wp-child-theme ](https://bitbucket.org/urban-insight/starter-wp-child-theme)     |Lehel|
| ui-wireframes |Static Wireframes | Bootstrap 3.x elements and pages for wireframing | ready for use | [      ui-wireframes ](https://bitbucket.org/urban-insight/ui-wireframes)     |Mark E.|


### Front End Code Snippet Library

| Starterkit| For | Description | Status | Link | Maintainer |
|-----------|-----|-------------|--------|------|------------|
| wp_salient_snippets |WP Salient| WordPress Code Snippets for Salient| ready for use | [ wp_salient_snippets ](https://bitbucket.org/urban-insight/wp_salient_snippets)     |Lehel|

## Bibliography

https://www.slideshare.net/foobartel/front-end-best-practices       
https://www.quora.com/What-are-front-end-development-guidelines-and-best-practices    
https://www.catswhocode.com/blog/top-10-best-practices-for-front-end-web-developers    
https://github.com/grab/front-end-guide    
https://www.belatrixsf.com/blog/best-practices-for-front-end-coding/    
https://code.tutsplus.com/tutorials/24-javascript-best-practices-for-beginners--net-5399    
https://www.codeproject.com/Articles/580165/JavaScript-Best-Practices    
