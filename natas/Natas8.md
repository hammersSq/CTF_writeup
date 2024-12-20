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