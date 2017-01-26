# Discord webhooks

## Structure of Discord Webhook

Before using of Webhooks you must to know the structure. All elements listed there are *optional* but you still must use `content` or `embeds` object at least once. This is minimal requirement.

![example](https://i.imgur.com/kvEZU97.png "Example")

```json
{
    "username": "Webhook",
    "avatar_url": "https://i.imgur.com/4M34hi2.png",
    "content": "Text message. Up to 2000 characters.",
    "embeds": [{
        "author": {
            "name": "Birdie♫",
            "url": "https://www.reddit.com/r/cats/",
            "icon_url": "https://i.imgur.com/R66g1Pe.jpg"
        },
        "title": "Title",
        "url": "https://google.com/",
        "description": "Text message. You can use Markdown here. *Italic* **bold** __underline__ ~~strikeout~~ [hyperlink](https://google.com) `code`",
        "color": 15258703,
        "fields": [{
            "name": "Text",
            "value": "More text",
            "inline": true
        }, {
            "name": "Even more text",
            "value": "Yup",
            "inline": true
        }, {
            "name": "Use `\"inline\": true` parameter if you want to write fields in same line.",
            "value": "okay..."
        }, {
            "name": "Thanks!",
            "value": "You welcome :wink:"
        }],
        "thumbnail": {
            "url": "https://upload.wikimedia.org/wikipedia/commons/3/38/4-Nature-Wallpapers-2014-1_ukaavUI.jpg"
        },
        "image": {
            "url": "https://upload.wikimedia.org/wikipedia/commons/5/5a/A_picture_from_China_every_day_108.jpg"
        },
        "footer": {
            "text": "Woah! So cool! :smirk:",
            "icon_url": "https://i.imgur.com/fKL31aD.jpg"
        }
    }]
}
```

* `username` - if used, overrides the default username of the webhook
* `avatar_url` - if used, overrides the default avatar of the webhook
* `content` - the message contents (up to 2000 characters)
* `embeds` - array of embed objects
  * `author` - embed author object
    * `name` - name of author
    * `url` - url of author
    * `icon_url` - url of author icon
  * `title` - title of embed
  * `url` - url of embed
  * `description` - description of embed
  * `color` - [color](http://htmlcolorcodes.com/color-picker/) code of the embed. You need to use Decimal numeral system, not Hexadecimal. Use [converter](http://www.binaryhexconverter.com/hex-to-decimal-converter)
  * `fields` - array of embed field objects
    * `name` - name of the field
    * `value` - value of the field
    * `inline` - whether or not this field should display inline (bool)
  * `thumbnail` - embed thumbnail object
    * `url` - source url of thumbnail (only supports http(s) and attachments)
  * `image` - embed image object
    * `url` - source url of image (only supports http(s) and attachments)
  * `footer` - embed footer object
    * `text` - footer text
    * `icon_url` - url of footer icon (only supports http(s) and attachments)

## Getting Started

### Account on IFTTT

Go to [IFTTT](https://ifttt.com/) and create an account (if you don't already have one).

### Webhook on Discord

1. Go to **Server settings** -> **Webhooks** -> **Create Webhook**;
1. Setup name, avatar and channel for posting. Copy *Webhook URL*. **Do not share! It can be dangerous!**;
1. Press **`Save`** and then **`Done`** button;

### If `this`

1. Go to [My Applets](https://ifttt.com/my_applets);
1. Press `[+]this`;
1. `Choose a service`. In theory you can use all of them. Some of them needs authefication (Twitter, Reddit, Youtube). Don't worry, it's safe;
1. `Choose trigger`. Read description below every trigger;
1. `Complete trigger fields`;

### Then `that`

1. Press `[+]that`;
1. `Choose action service`. You need `Maker`. Use search bar;
1. `Choose action`. Choose `Make a web request`;
1. Paste your *Webhook URL* to **URL** field;
1. Select `POST` method;
1. Select `application/json` content type.
1. And now the hardest part™. You need to create your JSON body. Follow the structure, use it as example and don't forget common sense. If something says `URL` put it in "url", if something says `Image` try to put that into `"image": {"url":""}`. You need to put all objects into curly braces `{ }`;
1. Press `Create Action` and then `Finish`.
1. Done! Good job!

### Tips

* Don't forget to check your JSON body with JSON validator. If you don't know any use [this](http://jsonlint.com/) one.
* If webhook *doesn't works* check logs for errors. **My Applets** -> *choose applet* -> *press on gear* -> __*View activity log*__. Maker error means your JSON body have errors.
* Discord have built-in embeds for Twitter, Youtube and other sites so you can just add link to webhook: `{"content": "{{Link}}"}`.

### Examples

#### Reddit

```json
{
    "embeds": [{
        "title": " {{Title}}",
        "image": {
            "url": "{{ImageURL}}"
        },
        "footer": {
            "text": "Author: {{Author}} | [Link]( {{PostURL}})"
        }
    }]
}
```