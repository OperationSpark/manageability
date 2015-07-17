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