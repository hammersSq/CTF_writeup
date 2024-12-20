# Natas 8
As in challenge 6 we have the source code of the site. 

It ask for a secret, that is encoded but visible in the source code
```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

...

function encodeSecret($secret) {  
    return bin2hex(strrev(base64_encode($secret)));  
}
```

reversing the function is straightforward 

```php
function decode($secret){
	return base64_decode(strrev(hex2bin($secret)))
}
```
this can be ran in every php sandbox and you can obtain the secret:
oubWYf2kBq

put this in the challenge and you obtain the password for the next challenge

ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t