---
layout: docs
title: Blocking Spam
---

# Blocking Spam with the "Spam Protector" plugin

*  [What is this plugin](#A2)
*  [Configuring the plugin](#A3)
  *  [Emergency comment shutdown](#A4)
  *  [Disable spamblock for Authors](#A5)
  *  [Do not allow duplicate comments](#A6)
  *  [Reject comments which only contain the entry title](#A7)
  *  [IP block interval](#A8)
  *  [Enable captchas](#A9)
  *  [Force captchas after how many days](#A10)
  *  [Background color of the captcha](#A11)
  *  [Force comment moderation after how many days](#A12)
  *  [What to do with comments when being auto-moderated?](#A13)
  *  [Force trackback moderation after how many days](#A14)
  *  [What to do with trackbacks when being auto-moderated](#A15)
  *  [How to treat comments made via APIs](#A16)
  *  [Check Trackback URLs](#A17)
  *  [How many links before a comment gets moderated](#A18)
  *  [How many links before a comment gets rejected](#A19)
  *  [Activate wordfilter](#A20)
  *  [Wordfilter for URLs, author names, comment body](#A21)
  *  [Activate URL filtering by blogg.de Blacklist](#A22)
  *  [Akismet API KEY](#A23)
  *  [How to treat Akismet-reported spam](#A24)
  *  [Hide E-Mail addresses of commenting users](#A25)
  *  [Check e-mail addresses](#A26)
  *  [Required comment fields](#A27)
  *  [Choose logging method](#A28)
  *  [Logfile location](#A29)
*  [Was that all?](#A30)
*  [Adapting spam from the Comment Moderation Panel](#A31)
*  [Questions?](#A32)

## <a name="A2"></a>What is this plugin

Serendipity ships with a default event plugin called "Spam Protector" that is used to fight blog spam.

This plugin is also installed by default in your Serendipity installation. You can find it's configuration by going to the Plugin Configuration menu in your Admin Interface and clicking on the title "Spam Protector" of the listing of event plugins.

The Spam Protector will check each comment and trackback that is made on your blog; either via API (wfwComment, Trackback) or via your using blog interface (extended entry, comment popup).

Each comment will be analyzed through different, configurable facilities. If any configured option qualifies the comment as spam, it will be set to "moderation" or "rejected" state. Moderated comments will show up in your Admin section "Comments", where you can either remove the comment or activate the comment to be seen on your blog. If configured, you will also receive a mail about moderated comments.

To ideally keep your blog free from spam, there are a lot of individual options which you will learn to configure in the next section.

## <a name="A3"></a>Configuring the plugin

### <a name="A4"></a>Emergency comment shutdown

If you enable this option, ALL comments and trackbacks to your blog will be disabled. Nobody can then leave a comment. It is as if you checked the "Do not allow comments to this entry" checkbox for each of your entries.

This option is meant to be used when you might go on holiday and want no spam to appear on your blog.

### <a name="A5"></a>Disable spamblock for Authors

The anti-spam methods can be bypassed for registered and logged-in authors. Here you can choose which author group is allowed to bypass them. "All authors" means that every registered author can bypass it, but you could also specify that bypassing is only allowed for Administrators. "none" means that authors are treated just the same as anonymous comments.

### <a name="A6"></a>Do not allow duplicate comments

If enabled, a comment that already exists in the database with the same body will be rejected. This option is very helpful to disallow mass-spam with the same contents.

### <a name="A7"></a>Reject comments which only contain the entry title

Sometimes comment spam used just the same content than your entry title contained. If you enable this option, spam like this will be rejected.

### <a name="A8"></a>IP block interval

This setting forbids comments from the same IP within a specific timespan. You should be aware that different users might have the same IP if they are using a proxy. AOL users, for instance, often are forced to use the same proxy and then could run into problems if other AOL users comment the same time on your blog. For low-volume comment blogs though, this option is helpful to prevent mass-attacks.

### <a name="A9"></a>Enable captchas

Captchas are currently the most probate action you can take to prevent comment spam. Captchas are tests to check that a real human user is performing an action. In terms of Serendipity, this means that the commenting user will see a crypted image and needs to enter which characters he sees. Until now, spambots are not able to do the same task.

Captchas have three major issues:

1. Sometimes they are even hard to read for "real" humans, and they might annoy people. Captchas are very hard to read for impaired users, and are not accessible to blind people.
2. Captchas will be cracked in a matter of time, forcing either stronger captchas or different approaches to spamfighting. There already exist algorithms that crack available variations of other system's captchas.
3. Captchas can only be enabled for COMMENTS. Since trackbacks are machine generated by definition, they cannot use the captcha image to be verified. This means that even though enabled captchas for your users will block virtually all comment spam, trackbacks still can only be blocked by different means.

The option "scrambled captchas" will use a stronger captcha implementation with varying pixels scattered within the captcha to make them harder to read for automatted bots.

### <a name="A10"></a>Force captchas after how many days

With this option you can enter the amount of days an article of you needs to age until captchas are enabled there. Usually spambots catch up your new articles only after some days, which means that fresh articles on your blog are less exposed to spam. Since the usual blog comments only happen within a short time after publishing an article, it is a good idea to enforce captchas when an article is, say 7 days old. This will then not annoy valid users commenting on your fresh articles, but later hinder spambots to drop their garbage.

### <a name="A11"></a>Background color of the captcha

Here you can customize the background color of your auto-generated captcha image.

### <a name="A12"></a>Force comment moderation after how many days

You can enable the comment moderation for each trackback and comment to an article here. Enter the amount of days after which an article will be put in "moderation" state.

### <a name="A13"></a>What to do with comments when being auto-moderated?

Here you can set what happens to auto-moderated articles from the option above. Rejected comments will not be stored anywhere, and moderated comments you can later delete or toggle visible. You will only receive mails about moderated comments, and you will not be notified of rejected comments.

### <a name="A14"></a>Force trackback moderation after how many days

As a distinction to general comment moderatio, you can specifically only block trackbacks to older entries. This way you can leave normal (captcha'd) comments to pass through, while trackbacks could be generally dismissed.

### <a name="A15"></a>What to do with trackbacks when being auto-moderated

Just like the global auto-moderation, you can specify what happens to auto-moderated trackbacks.

### <a name="A16"></a>How to treat comments made via APIs

Here you can indicate what happens to all API-made comments (Trackbacks, wfwComment). You can either globally moderate them or reject them, or with the "none" option you can handle them not individually.

### <a name="A17"></a>Check Trackback URLs

This option will call the URLs that are given in a trackback and see if the URL of your entry that they refer to really shows up on their page. This option can significantly decrease trackback spam, but will also perform URL requests on your server to foreign servers, which both takes time and traffic.

### <a name="A18"></a>How many links before a comment gets moderated

Here you can specify the maximum amount of links (http://...) that are allowed within a comment until it gets auto-moderated.

### <a name="A19"></a>How many links before a comment gets rejected

Here you can specify the maximum amount of links (http://...) that are allowed within a comment until it gets rejected.

### <a name="A20"></a>Activate wordfilter

This will enable the wordfilter for URLs, author names and the comment body. If you set the option to "moderate", all comments/trackbacks that contain a word of the following filters will be moderated. If you set it to "reject", they will be completely rejected and you will get no notification about it.

### <a name="A21"></a>Wordfilter for URLs, author names, comment body

In these large textareas you can enter a ";" delimited number of regular expressions. If you just want to block names like "casino", "phentermine" etc. you can simply enter the words. But regular expressions would also allow you a broader range of filtering. See more about regular expressions here: [http://en.wikipedia.org/wiki/Regular\_expression](http://en.wikipedia.org/wiki/Regular_expression)

The most important rule is that in Regular Expressions there are a few special characters: "." means "any character", and ".\*" would mean "any ammount of any character".

You can seperate each rule of the wordfilters also with a ";" plus linebreak, if that is easier for you to read.

### <a name="A22"></a>Activate URL filtering by blogg.de Blacklist

The blogg.de blacklist contains a list of "bad" URL names that spambots enter as their homepage. The blogg.de blacklist is well maintained and should catch on bad URLs pretty soon. You can decide whether to "moderate" these comments that are marked as bad by the blogg.de blacklist, or to immediately "reject" them.

### <a name="A23"></a>Akismet API KEY

Akismet.com is a central anti-spam and blacklisting server. It can analyze your incoming comments and check if that comment has been listed as Spam. Akismet was developed for Word Press specifically, but can be used by other systems. You just need an API Key from [http://www.akismet.com/](http://www.akismet.com/) by registering an account at [http://www.wordpress.com/.](http://www.wordpress.com/.) If you leave this API key empty, Akismet will not be used.

Akismet will inspect submitted spam according to their central blacklist and decide if it is "bad" or "good". The Akismet API also supports to submit uncaught spam, but this is not yet supported by this Serendipity plugin.

### <a name="A24"></a>How to treat Akismet-reported spam

Set here what to do with comments/Trackback that Akismet reports as spam.

### <a name="A25"></a>Hide E-Mail addresses of commenting users

If this option is enabled, the email addresses of users that have commented on your blog will not be displayed on your blog. This option can also be set from within the general Serendipity configuration as well.

### <a name="A26"></a>Check e-mail addresses

If set to "Yes", email addresses will be checked for valid syntax. This prevents people from entering "nothing" or other invalid things as their email addresses.

### <a name="A27"></a>Required comment fields

Here you can enter which comment form fields you want your users to fill out. This way you can force people to leave their email address, for example.

### <a name="A28"></a>Choose logging method

One very important thing in blocking spam is to check, WHAT you are blocking. Since you are only notified of moderated spam by email, you might want to check what kind of spam you reject every day. For that you can enable this option and either set it to "Database" or "File". The preferred way is to use database-based logging, because then you can check the "serendipity\_spamblocklog" DB table with tools like phpMyAdmin easily. There you will also see rejection reasons!

### <a name="A29"></a>Logfile location

If you chose to log to a File (maybe because checking the database is too cumbersome for you), you need to specify the file location of the logfile you want to create here. Make sure you enter the full and absolute path to your logfile, and that your webserver can write to that file.

## <a name="A30"></a>Was that all?

Since spam adapts nearly daily, the best thing to keep spam low is to check your wordfilters, url filters and author name filters from time to time, and add new common URLs or Author names to your blacklist.

## <a name="A31"></a> Adapting spam from the Comment Moderation Panel

In your comment moderation panel, you have the option to immediately configure Anti-Spam measurements from the top of that panel.

Also you will see a wrench-icon near author names and URLs, which will put those names/URLS in the spamblock wordfilter automatically.

## <a name="A32"></a>Questions?

If you have further questions about blocking spam, or have some ideas on how to improve fighting spam, please drop by on our [Forums](http://board.s9y.org)!