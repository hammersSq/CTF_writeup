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
[Refer security problem](https://developer.mozilla.org/en-US/docs/Web/Security/Referer_header:_privacy_and_security_concerns) 

The referer contains the addres of a request, meaning the address from which a resource is requested with http (eg. the web page url where i clicked the current link i'm using in http).

interesting example of security problem cited in the article:
*Consider a "reset password" page with a social media link in a footer. If the link was followed, depending on how information was shared the social media site may receive the reset password URL and may still be able to use the shared information, potentially compromising a user's security.*
