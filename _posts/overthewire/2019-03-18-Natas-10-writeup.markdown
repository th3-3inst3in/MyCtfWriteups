---
layout: post
title: Natas 10 writeup
date: 2019-03-11
author: OutHackThem
comments: true
categories: overthewire
tags: [web,overthewire]
---

## Natas 10

Visit this [link](http://natas10.natas.labs.overthewire.org/) to go to level 10 for which you’ll need the password from the previous level.
You’ll land here 

![login](https://themctfwriteups.files.wordpress.com/2019/03/image.png)

As always our goal is to read the flag which is inside the /etc/ folder as instructed at the start of level 1.

Clicking the view Sourcecode link we see the following code

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
```

main thing to be noted here is the preg_match() function which looks at our input and if it sees & \| ; then it immediately throws an error saying Input contians illegal characters

Since our input is going in the passthru() function and will be a part of the current grep command we can simply get the flag with the following payload.

The main thing to note here is the user of `.*` the rest of the path formation can be understood by reading the instructions on level 1.

```bash
.* /etc/natas_webpass/natas11
```

![flag](https://i.imgur.com/QmC4XyM.png)
