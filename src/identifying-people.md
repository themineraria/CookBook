# Identifying People

## Identifying People <a id="identifying-people"></a>

We want to find out how is connected to the target. That can be site administrator, employees, owner, mods. Maybe one of the administrators have posted in a forum with their email, or in a newsgroup or somewhere else. Those posts could contain useful data about the stack or help us devlop a network diagram. We might also need to use social engineering.

In order to find people we might use the following sources:

* The company website
* Social media \(LinkedIn, Facebook, Twitter etc\)
* Forums and newsgroups
* Metadata from documents

#### Company Website <a id="company-website"></a>

This is pretty obvious. Just look around on the website. Or download it. Or spider it with burp and then search the result.

Make sure to check out the blog. There you might have employees writing blogposts under their name.

```text
site:twitter.com companyname
site:linkedin.com companyname
site:facebook.com companyname
```

#### Metadata From Documents <a id="metadata-from-documents"></a>

You find some documents and then run exiftool on them to see if there is any interesting metadata.

```text
site:example.com filetype:pdf
```

### Email Harvesting <a id="email-harvesting"></a>

theharvester - I have not had luck with this

```text
theharvester -d example.com -l 500 -b all
```

### Check if emails have been pwned before <a id="check-if-emails-have-been-pwned-before"></a>

[https://haveibeenpwned.com](https://haveibeenpwned.com/)

## Users <a id="users"></a>

social-searcher.com

Reddit  
Snoopsnoo

