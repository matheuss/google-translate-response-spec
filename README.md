# Google Translate's response specification
## ALSO KNOWN AS "f.txt"

### What is it?
When you're using Google Translate, it sends a request for translation of your phrase and recieves a response. Of course, Translate know how to interpret response, but how about __us__?
That's why we've made this repo. The only purpose is to show you, people, how to interpret this response and, probably, to show you a few examples of using (or even more..?)

### Yeah, but what about official Translate's API..?
Yeah, but how about 60-days trial and 20$ for every million of translated characters? 

Price is pretty low, I must admit. What's the reason then? We're pretty stubborn, I suppose.

### Whom is it for?
__Developers__, I guess. Response's usage is quite easy, so _even a beginner with python and requests lib_ (like me) can use it

### Ok, where's it?
__specification.md__ is what you need.

### Hey, response from google is 403!
..yeeaaaah, I wasn't absolute clear with you. __Google uses tokens ('tk = number1.number2' in request's data) for validating responses. So you should generate this token for sending correct request.__ And this token changes every hour. But the good thing about it is that server accepts old (don't know how old though) tokens. 

The token is client-side calculated, so you actually can rip this code from [desktop_module_main.js](https://translate.google.ru/translate/releases/twsfe_w_20160627_RC01/r/js/desktop_module_main.js) (relevant for 11 July, 2016) of Web Translate. But be aware, that script's _obfuscated_ pretty hard.

It would be much better for you to check @matheuss [google-translate-token](https://github.com/matheuss/google-translate-token) for JS code of calculating this token. [BEGIN-END section.](https://github.com/matheuss/google-translate-token/blob/master/index.js)
 
### Hey, but what about...
I have a lack of imagination, so if you have any questions, then create an issue. We'll add important Q&A to this readme.
