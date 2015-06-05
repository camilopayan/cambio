## Harp.js and Cascade CMS: A modern workflow

I've always been frustrated by how hard it is to work simultaneously on code 
once it's in Cascade. Constantly, the same thing would happen: templates would 
be made, a development site raised, and then the constant back and forth.

"Are you editing the CSS? Yea? Okay let me know when you're done."

Cascade doesn't have one of the most important features for working 
collaboratively on code: **code merging**. 

The answer to this problem is to have a step where development takes place
before going into Cascade. The ideas goes: we'd experiment with the look and 
feel of pages, then freeze them before putting them into Cascade. It seems 
simple enough.

This solution quickly raised another issue. As a developer, I'm already used to 
creating my own development environments and developing locally. Others can't 
do the same thing and honestly shouldn't be expected to.

### Enter HarpJS

At this point, I'll introduce [HarpJS](http://harpjs.com/), a static web server.
When HarpJS first came to my attention, I was thrilled. 

HarpJS gives a very similar feel to Cascade. Both create static sites, both use 
some preprocessing to that effect (Cascade uses XSLT, HarpJS uses... everything
else). Most importantly, HarpJS was simple enough that everyone on the team 
use it right away. Just run `harp server` and you've got a site running.

What's more, with HarpJS you have access to many modern tools that we were 
previously unable to incorporate, like Sass. EJS partials map very well to 
Cascade's `<system-region>` template tags. Javascript stays Javascript, though 
you could use Coffeescript in HarpJS and upload the finished JS files after the 
freeze.

The next step would be making scripts that could quickly take the assets in 
HarpJS, convert them to the most similar assets in Cascade, and uploading them 
via Cascade's SOAP API.
