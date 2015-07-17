# manageability
A brief clean up of the website project to make markup and css more manageable

### Separate CSS

0. Make sure your web server is running, and you have your website open in another browser tab.
1. In the root directory of your website workspace, create a directory called css.
2. In the css directory, create a file called `custom.css`, and open that file.
3. Open the index.html file that resides in the root directory of your website workspace.
4. Within the `<head>` tag, find the `<style>` tag, and copy/cut all of the CSS selectors and styling rules from between the `<style></style>` tag.
5. Delete the leftover opening and closing `<style></style>` tag.
6. Save the `index.html` file, and, for kicks, switch back to your website, and refresh - no style!
7. Switch back to the `custom.css` file, and paste in all of the css on your clipboard.
8. Google "How to link a CSS file": Answer => Create a `<link>` tag in the `<head>` of the index.html file, and link the path to the `custom.css` file.
9. Save, switch back to your website, refresh, voila, we got style!

### Modularize Markup

1. Google "jquery cdn".
2. Paste `<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>` at the very bottom of the body tag, just above the closing `</body>`. We are now using jquery, a third party API for manipulating web pages, or the DOM. We're making use of a cdn to do so.
3. On the line directly below the jquery script tag, but still inside the body tag, create a blank `<script></script>` tag. (Explain that we can open scripts within an HTML page.)
4. Add as the very first line of code, a listener to the jquery:
        $(document).ready(initialize);
5. Within the same `<script>` tag, create an initialize function and use jquery to load "nav.html":

````javascript
// other code ...
        <script>
            $(document).ready(initialize);
            
            function initialize() {
                $("nav").load("nav.html");
            }
        </script>
    </body>
</html>
````

6. Within the `index.html` file, cut and paste all of markup between the opening and closing `<nav></nav>` tags, BUT LEAVE the `<nav></nav>` in place.
7. Save your `index.html`, switch back to your website, refresh: No nav!
8. From the file explorer, in the root directory of your website, create file called `nav.html`, and paste in all of the markup on your clipboard. Format it appropriately by doing, in Cloud9, **Edit > Code Formatting > Auto Selected Formatter**, or `Ctrl + alt + f`.
9. Save your `index.html`, switch back to your website, refresh: We got nav!
10. Open the debugger and break within the `initialize()` function.

### Fragmenting with Hash

    See:
    0. https://blog.httpwatch.com/2011/03/01/6-things-you-should-know-about-fragment-urls/
    1. https://en.wikipedia.org/wiki/Fragment_identifier
    2. http://blog.mgm-tp.com/2011/10/must-know-url-hashtechniques-for-ajax-applications/

1. In the `nav.html` file, replace the href of both `<li>` to use a location hash inside of referencing a file, so, your nav items should look like this:

````HTML
<li><a href="#home">Home</a></li>
<li><a href="#portfolio">Portfolio</a></li>
````

2. From the file explorer, create a new file called `home.html`, and open it in the text editor.
3. From within the `index.html` file, cut and paste all of the markup between the opening and closing `<main></main>` tags, BUT LEAVE the `<main></main>` tags in place.
4. Switch back to the `home.html` and paste in the markup on your clipboard, then format it: **Edit > Code Formatting > Auto Selected Formatter**, or `Ctrl + alt + f`.
5. Google "JavaScript get location hash", and within the `index.html` file, create a variable called `hash` and assign it using the knowledge you've just gained.  
6. Save, and switch to your website, debug and break to see what the hash equals when clicking on the **Home** nav item.
7. We need to edit the `hash` var so we remove the `#`! Google "JavaScript String slice".
8. Still within the `initialize()` function, clean up our code to include a new variable called `template`.
9. Using the turnary operator, if we have a `hash` at all, assign the result of our `hash` slice to `template`, othewise, assign the value `home`
9. Finally, call the method `loadTemplate(template);`, your full `initialize()` function should look like this:

````javascript
// other code...
            
            function initialize() {
                var hash, template;
                
                $("nav").load("nav.html");
                
                hash = window.location.hash;
                template = hash ? hash.slice(1) : 'home';
                loadTemplate(template);
            }
            
// other code...
````

10.  Within the same `<script>` tag, define a function called `loadTemplate()`, like so:

````javascript
// other code...
            function loadTemplate(template) {
                $("main").load(template + '.html');
            }
// other code...
````

11. Save, switch back to your website, reload, notice by default or `home.html` template loads, and clicking on the **Home** nav item does the same.
12. Repeat this pattern for `portfolio.html`!