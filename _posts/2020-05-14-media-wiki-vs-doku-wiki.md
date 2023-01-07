---
layout: page
title: Web Technologies - Media Wiki vs Doku Wiki
permalink: /wiki/media-wiki-vs-doku-wiki
tag: misc
---

## Media Wiki vs Doku Wiki
Wiki's are great for making it quick and easy for virtually anyone to add content to a website.  However, there are many choices in setting up a wiki for a web site and picking the correct one can seem like a daunting task.  

### Media Wiki
One of the first questions in picking a wiki is what languages does your web server support.  If you are like me, then you will find PHP-based wiki's as the first solutions to filter on.  Next, I find it important to filter on popularity.  More popular wiki software packages will have a greater range of support options and documentation available not to mention more regular security updates.  

All of these lead me down the path of choosing to first try out MediaWiki.  MediaWiki is a mature wiki software application and has a large community of supporters.  I was able to build a custom theme based off of the previously installed velocity theme.  I had to also update the Resources.php file to add the additional skin modeled off of the configuration that I found there for the velocity theme.  I found it helpful that anonymous public guest users would see the default theme and that I could configure my editing user accounts with a more feature rich theme.  It did take me some time to modify the rewrite module's .htaccess file to work on my website providers system as it was different then the XAMPP server (beta version) that I used for testing.

Unfortunately, I soon found that my hosting provider did not provide me as much speed as I needed.  Some of my wait times were approaching 90 seconds!  If you have the best wiki software in the world, but users leave your site before they see the content then it is not adding the best value.  This helped me to see that I needed to try a different wiki software product.

### DokuWiki
To cope with slower website speed availability without changing providers yet, I did some research on smaller, popular wikis.  I soon found both DokuWiki and WackoWiki to be among the top on the list.  I ended up choosing DokuWiki with its smaller codebase (~90k vs MediaWiki's 2.5Mb) and due to it being based off of files instead of a database.  Removing the database from the equation removed a possible bottleneck and allows for easier backups.  Dokuwiki pages are stored in their original wiki annotated text and can be copied readily for backup.  

For a small wiki, Dokuwiki has both unicode and multi-language support.  I would have enjoyed seeing a comprehensive list of performance comparisons across wiki implementations, but a lot of this may be complicated by the implications of unique site themes used for each wiki implementation.  

### Wiki Setup Steps
Both DokuWiki and MediaWiki had pretty nice setup scripts.  To setup DokuWiki, I wanted a very limited list of users who could make changes and for the public to be able to read the contributed content.  To do this, I chose a public wiki in the setup.  After creating the desired login/administrator accounts, I went into the configuration and removed the ability for new users to register by unchecking a box in account management.  To clean up some unneeded functionality and increase potential performance, I also removed the ability to set new passwords, subscribe/unsubscribe, view RAW page content, send better looking emails, old revisions, recent changes, and updates to profiles.  It was also helpful to remove the original install.php and any unneeded language files (depending on the languages of those who will be adding content).  

Finally, I went to work on seo optimizations for my wiki page names justified by information at [[http://www.seomoz.org/learn-seo/url]].  I changed the separator from a underscore to a dash and turned on .htaccess nice URL's since the internal nice URL setting shows the same doku.php URL for all pages.  
```
<Files ~ "^([\._]ht|README$|VERSION$|COPYING$)">
    Order allow,deny
    Deny from all
</Files>
RewriteEngine on
RewriteRule ^_media/(.*)              lib/exe/fetch.php?media=$1  [QSA,L]
RewriteRule ^_detail/(.*)             lib/exe/detail.php?media=$1  [QSA,L]
RewriteRule ^_export/([^/]+)/(.*)     doku.php?do=export_$1&id=$2  [QSA,L]
RewriteRule ^_detail/(.*)             lib/exe/detail.php?media=$1  [QSA,L]
RewriteRule ^_export/([^/]+)/(.*)     doku.php?do=export_$1&id=$2  [QSA,L]
RewriteRule ^$                        doku.php  [L]
RewriteCond %{REQUEST_FILENAME}       !-f
RewriteCond %{REQUEST_FILENAME}       !-d
RewriteRule (.*)                      doku.php?id=$1  [QSA,L]
RewriteRule ^index.php$               doku.php
RewriteBase /wiki
```
Overall, DokuWiki has proved itself to be a good wiki and is much, much faster in my environment than MediaWiki ever was.  If you need to run speed tests, I would recommend using [[http://www.webpagetest.org]].
