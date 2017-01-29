# Discord Webhook

## It's a JSON

If you don't know anything about JSON, please, spend some of your time on learning JSON structure.

Recommended sources:

* [Learn X in Y minutes, Where X=json](https://learnxinyminutes.com/docs/json/)
* [JSON official site](http://json.org/)

## Structure of Webhooks

Before using of Webhooks you have to know the structure. All elements listed here are *optional* but you still need use `content` or `embeds` object at least once. This is a minimal requirement.

```ini
`element` : `[data type]` - description

[string] - text. Supports Markdown Syntax
[url of image] - just a link. Example: `http://www.w3schools.com/html/pic_mountain.jpg`
[url of website] - link too. Example: `http://www.google.com/`
[array] - comma-separated elements. Example: [{"color":15424},{"color":56133}]
[number] - just a number. Example: 555555, duh...
[bool] - boolean... Can be true or false only. Example: "inline" : true
[object] - something you don't need to worry about
```

* `username` : `[string]` - if used, it overrides the default username of the webhook
* `avatar_url` : `[url of image]` - if used, it overrides the default avatar of the webhook
* `content` : `[string]` - simple message, the message contains (up to 2000 characters)
* `embeds` : `[array]` - array of embed objects. That means, you can use more than one in same body
  * `author` : `[object]` - embed author object
    * `name` : `[string]` - name of author
    * `url` : `[url of website]` - url of author. If `name` was used, it becomes a hyperlink
    * `icon_url` : `[url of image]` - url of author icon
  * `title` : `[string]` - title of embed
  * `url` : `[url of website]` - url of embed. If `title` was used, it becomes hyperlink
  * `description` : `[string]` - description text
  * `color` : `[number]` - color code of the embed. You have to use Decimal numeral system, not Hexadecimal. Use [color picker](http://htmlcolorcodes.com/color-picker/) and [converter](http://www.binaryhexconverter.com/hex-to-decimal-converter)
  * `fields` : `[array]` - array of embed field objects
    * `name` : `[string]` - name of the field
    * `value` : `[string]` - value of the field
    * `inline` : `[bool]` - if true, fields will be displayed in same line, but there can only be 3 max in same line or 2 max if you used thumbnail
  * `thumbnail` : `[object]` - embed thumbnail object
    * `url` : `[url of image]` - url of thumbnail
  * `image` : `[object]` - embed image object
    * `url` : `[url of image]` - url of image
  * `footer` : `[object]` - embed footer object
    * `text` : `[string]` - footer text, doesn't support Markdown
    * `icon_url` : `[url of image]` - url of footer icon

### Example for a webhook

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
          "name": "Use `\"inline\": true` parameter, if you want to display fields in same line.",
          "value": "okay..."
        },
        {
          "name": "Thanks!",
          "value": "You're welcome :wink:"
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

Visit [IFTTT](https://ifttt.com/) and create an account (if you don't already have one).

### Webhook on Discord

1. Go to **Server settings** -> **Webhooks** -> **Create Webhook**
1. Setup name, avatar and the channel, where it will be posted. Copy *Webhook URL*. **Do not share! Very dangerous!**
1. Click **`Save`** and then the **`Done`** button

## Creating an Applet

### If `this`

1. Go to [My Applets](https://ifttt.com/my_applets)
1. Click `[+]this`
1. `Choose a service`. In theory you could use all of them. Some of them need authentification (Twitter, Reddit, Youtube). Don't worry, it's safe ;)
1. `Choose the trigger`. Read the description below every trigger and choose the needed one
1. `Complete trigger fields`

### Then `that`

1. Click `[+]that`
1. `Choose the action service`. You need `Maker`. Use the search bar
1. `Choose action`. Choose `Make a web request`
1. Paste your *Webhook URL* to **URL** field
1. Select `POST` method
1. Select `application/json` content type
1. And now the hardest part™. You need to create your JSON body. Follow the structure, use it as an example and don't forget about common sense. Press `+ Ingredient` button and put them into appropriate fields. If something says `URL` put it in "url", if something says `Image`, try to put that into `"image": {"url":""}`. You need to put all objects into curly braces `{ }`. There is no universal solution
1. Click `Create Action` and then `Finish`
1. Done!

## Tips

* Don't forget to check your JSON body with a JSON validator. If you don't know any use one of these:
  * [JSON Formatter](http://jsonformatter.org/)
  * [JSONLint](http://jsonlint.com/)
  * [JSON Editor Online](http://www.jsoneditoronline.org/)
* If the webhook *doesn't work* check logs for errors. **My Applets** -> *choose applet* -> *click gear* -> __*View activity log*__. `Maker error` means your JSON body have errors.
* Discord has built-in embeds for Twitter, Youtube and other sites so you can just add the link to the webhook: `{"content": "{{Link}}"}`.
* Too hard? Use the [picture guide](https://imgur.com/a/Zkdgo) instead!

## Examples

### Reddit

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