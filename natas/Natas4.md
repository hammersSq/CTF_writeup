# Natas 4
Also here you have an hint from the challenge: 
" Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/" "

At the beginning i did not understand what he was referring to, but i was positive that it was talking about the HTTP request, so i opened Burp and used the proxy tool to look at it:
![Screenshot](./imgs/natas4_image.png)
We can se that the request for the root directory is made with the Referer "http://natas4.natas.labs.overthewire.org/", so i tried to change it with "http://natas5.natas.labs.overthewire.org/" .
with this modification you have the password for the next challenge:
0n35PkggAPm2zbEpOU802c0x0Msn1ToK

# Close up
Since i've never seen the **Referer** header in http request i did a quick research to understood when it is used and for what.
*The HTTP `Referer`request header contains the absolute or partial address from which a resource has been requested. The `Referer` header allows a server to identify referring pages that people are visiting from or where requested resources are being used. This data can be used for analytics, logging, optimized caching, and more.*
