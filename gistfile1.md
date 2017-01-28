# Discord Webhook

## It's a JSON

If you don't know nothing about JSON, please spend some of your time on learning JSON structure.

Recommended sources:

* [Learn X in Y minutes, Where X=json](https://learnxinyminutes.com/docs/json/)
* [JSON official site](http://json.org/)

## Structure of Webhooks

Before using of Webhooks you must to know the structure. All elements listed here are *optional* but you still must use `content` or `embeds` object at least once. This is a minimal requirement.

```ini
`element` : `[data type]` - description

[string] - text. Markdown Syntax
[url of image] - just a link. Example: `http://www.w3schools.com/html/pic_mountain.jpg`
[url of website] - link too. Example: `http://www.google.com/`
[array] - comma-separated elements. Example: [{"color":15424},{"color":56133}]
[number] - just a number. Example: 555555, duh...
[bool] - boolean... Can be true or false only. Example: "inline" : true
[object] - something you don't must worry about
```

* `username` : `[string]` - if used, overrides the default username of the webhook
* `avatar_url` : `[url of image]` - if used, overrides the default avatar of the webhook
* `content` : `[string]` - simple message, the message contents (up to 2000 characters)
* `embeds` : `[array]` - array of embed objects. That means you can use more than one in same body
  * `author` : `[object]` - embed author object
    * `name` : `[string]` - name of author
    * `url` : `[url of website]` - url of author. If used `name` become hyperlink
    * `icon_url` : `[url of image]` - url of author icon
  * `title` : `[string]` - title of embed
  * `url` : `[url of website]` - url of embed. If used `title` become hyperlink
  * `description` : `[string]` - description text
  * `color` : `[number]` - color code of the embed. You must to use Decimal numeral system, not Hexadecimal. Use [color picker](http://htmlcolorcodes.com/color-picker/) and [converter](http://www.binaryhexconverter.com/hex-to-decimal-converter)
  * `fields` : `[array]` - array of embed field objects
    * `name` : `[string]` - name of the field
    * `value` : `[string]` - value of the field
    * `inline` : `[bool]` - if true fields will be displayed in same line but there can be max 3 in same line or max 2 if you used thumbnail
  * `thumbnail` : `[object]` - embed thumbnail object
    * `url` : `[url of image]` - url of thumbnail
  * `image` : `[object]` - embed image object
    * `url` : `[url of image]` - url of image
  * `footer` : `[object]` - embed footer object
    * `text` : `[string]` - footer text, Doesn't support Markdown
    * `icon_url` : `[url of image]` - url of footer icon

### Example webhook

```json
{
  "username": "Webhook",
  "avatar_url": "https://i.imgur.com/4M34hi2.png",
  "content": "Text message. Up to 2000 characters.",
  "embeds": [
    {
      "author": {
        "name": "Birdie♫",
        "url": "https://www.reddit.com/r/cats/",
        "icon_url": "https://i.imgur.com/R66g1Pe.jpg"
      },
      "title": "Title",
      "url": "https://google.com/",
      "description": "Text message. You can use Markdown here. *Italic* **bold** __underline__ ~~strikeout~~ [hyperlink](https://google.com) `code`",
      "color": 15258703,
      "fields": [
        {
          "name": "Text",
          "value": "More text",
          "inline": true
        },
        {
          "name": "Even more text",
          "value": "Yup",
          "inline": true
        },
        {
          "name": "Use `\"inline\": true` parameter if you want to write fields in same line.",
          "value": "okay..."
        },
        {
          "name": "Thanks!",
          "value": "You welcome :wink:"
        }
      ],
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
    }
  ]
}
```

### And how it looks

![example](https://i.imgur.com/kvEZU97.png "Example")

## Getting Started

### Account on IFTTT

Go to [IFTTT](https://ifttt.com/) and create an account (if you don't already have one).

### Webhook on Discord

1. Go to **Server settings** -> **Webhooks** -> **Create Webhook**
1. Setup name, avatar and channel for posting. Copy *Webhook URL*. **Do not share! Very dangerous!**
1. Press **`Save`** and then **`Done`** button

## Creating Applet

### If `this`

1. Go to [My Applets](https://ifttt.com/my_applets)
1. Press `[+]this`
1. `Choose a service`. In theory you can use all of them. Some of them needs authefication (Twitter, Reddit, Youtube). Don't worry, it's safe ;)
1. `Choose trigger`. Read description below every trigger and choose the needed one
1. `Complete trigger fields`

### Then `that`

1. Press `[+]that`
1. `Choose action service`. You need `Maker`. Use search bar
1. `Choose action`. Choose `Make a web request`
1. Paste your *Webhook URL* to **URL** field
1. Select `POST` method
1. Select `application/json` content type
1. And now the hardest part™. You need to create your JSON body. Follow the structure, use it as example and don't forget about common sense. Press `Ingredients+` button and put them into appropriate fields If something says `URL` put it in "url", if something says `Image` try to put that into `"image": {"url":""}`. You need to put all objects into curly braces `{ }`. There no universal solution
1. Press `Create Action` and then `Finish`
1. Done!

## Tips

* Don't forget to check your JSON body with JSON validator. If you don't know any use next ones:
  * [JSON Formatter](http://jsonformatter.org/)
  * [JSONLint](http://jsonlint.com/)
  * [JSON Editor Online](http://www.jsoneditoronline.org/)
* If webhook *doesn't works* check logs for errors. **My Applets** -> *choose applet* -> *press on gear* -> __*View activity log*__. `Maker error` means your JSON body have errors.
* Discord have built-in embeds for Twitter, Youtube and other sites so you can just add link to webhook: `{"content": "{{Link}}"}`.
* If you don't know how to use JSON check this [guide](https://learnxinyminutes.com/docs/json/).
* Too hard? Use [picture guide](https://imgur.com/a/Zkdgo) instead!

### Examples

#### Reddit

```json
{
  "embeds": [
    {
      "title": "{{Title}}",
      "description": "[Link]({{PostURL}})",
      "image": {
        "url": "{{ImageURL}}"
      },
      "footer": {
        "text": "Author: {{Author}}"
      }
    }
  ]
}
```