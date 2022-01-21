# RedHook.js
![npm](https://img.shields.io/npm/l/redhook.js?color=pink&style=flat-square)
![sourcerank](https://img.shields.io/librariesio/sourcerank/npm/redhook.js?color=pink&style=flat-square)
![types](https://img.shields.io/npm/types/redhook.js?color=pink&style=flat-square)
![npm version](https://img.shields.io/npm/v/redhook.js?color=pink&style=flat-square)
![keywords](https://img.shields.io/github/package-json/keywords/japandotorg/RedHook.js?color=pink&style=flat-square)
![release](https://img.shields.io/github/release-date-pre/japandotorg/RedHook.js?color=pink&style=flat-square)
![last commit](https://img.shields.io/github/last-commit/japandotorg/RedHook.js?color=pink&style=flat-square)



![discord](https://img.shields.io/discord/772708529744248842?color=pink&style=for-the-badge)

## Installation
` - ` `npm install RedHook.js` <br>
` - ` `yarn add RedHook.js`

## Examples

### Basic Usage
```js
const { Webhook } = require('redhook.js');
const hook = new Webhook("YOUR WEBHOOK URL");

const IMAGE = 'https://imgur.com/gallery/R9xW7ha';
hook.setUsername('REDHOOK');
hook.setAvatar(IMAGE);

hook.send("I love lemons!");
```

### Custom embeds
```js
const { Webhook, MessageBuilder } = require('redhook.js');
const hook = new Webhook("YOUR WEBHOOK URL");

const embed = new MessageBuilder()
    .setTitle('title is testing')
    .setAuthor('Author go brr', 'https://imgur.com/gallery/R3VTnfe', 'https://www.github.com/japandotorg')
    .setURL('https://www.github.com/japandotorg')
    .addField('First field', 'this is inline', true)
    .addField('Second field', 'this is not inline')
    .setColor('#2f3136')
    .setThumbnail('https://imgur.com/gallery/R3VTnfe')
    .setDescription('Beep Boop, is this a description? :)')
    .setImage('https://imgur.com/gallery/R3VTnfe')
    .setFooter('Hey its a footer', 'https://imgur.com/gallery/R3VTnfe')
    .setTimestamp();
    
hook.send(embed);
```

Keep in mind that the custom embed method `setColor` takes in a decimal color/a hex color (pure black and white hex colors will be innacurate). You can convert hex colors to decimal using this website here: [https://convertingcolors.com](https://convertingcolors.com)

### Sending Files 
```js
const { Webhook } = require('redhook.js');
const hook = new Webhook('YOUR WEBHOOK URL');

hook.sendFile('../example.png');
```

### Preset messages
```js
const { Webhook } = require('redhook.js');
const hook = new Webhook('YOUR WEBHOOK URL');

//Sends an information message
hook.info('**Information hook**', 'Information field title here', 'Information field value here');

//Sends a success message
hook.success('**Success hook**', 'Success field title here', 'Success field value here');

//Sends an warning message
hook.warning('**Warning hook**', 'Warning field title here', 'Warning field value here');

//Sends an error message
hook.error('**Error hook**', 'Error field title here', 'Error field value here');
```

### Custom settings
```js
const { Webhook } = require('redhook.js');
const hook = new Webhook({
    url: "YOUR WEBHOOK URL",
    //If throwErrors is set to false, no errors will be thrown if there is an error sending
    throwErrors: false,
    //retryOnLimit gives you the option to not attempt to send the message again if rate limited
    retryOnLimit: false
});

hook.setUsername('Username'); //Overrides the default webhook username
hook.setAvatar('YOUR_AVATAR_URL'); //Overrides the default webhook avatar
```

## Notes
discord-webhook-node is a promise based library, which means you can use `.catch`, `.then`, and `await`, although if successful will not return any values. For example:

```js
const { Webhook } = require('redhook.js');
const hook = new Webhook("YOUR WEBHOOK URL");

hook.send("Hello there!")
.then(() => console.log('Sent webhook successfully!'))
.catch(err => console.log(err.message));
```

or using async:
```js
const { Webhook } = require('redhook.js');
const hook = new Webhook("YOUR WEBHOOK URL");

(async () => {
    try {
        await hook.send('Hello there!');
        console.log('Successfully sent webhook!');
    }
    catch(e){
        console.log(e.message);
    };
})();
```

By default, it will handle Discord's rate limiting, and if there is an error sending the message (other than rate limiting), an error will be thrown. You can change these options with the custom settings options below.

## API
### Webhook - class
```
Constructor
- options (optional) : object
    - throwErrors (optional) : boolean
    - retryOnLimit (optional) : boolean

Methods
- setUsername(username : string) returns this
- setAvatar(avatarURL : string (image url)) returns this
- async sendFile(filePath : string)
- async send(payload : string/MessageBuilder)
- async info(title : string, fieldName (optional) : string, fieldValue (optional) : string, inline (optional) : boolean)
- async success(title : string, fieldName (optional) : string, fieldValue (optional) : string, inline (optional) : boolean)
- async warning(title : string, fieldName (optional) : string, fieldValue (optional) : string, inline (optional) : boolean)
- async error(title : string, fieldName (optional) : string, fieldValue (optional) : string, inline (optional) : boolean)
```

### MessageBuilder - class
```
Methods
- setText(text: string)
- setAuthor(author: string (text), authorImage (optional) : string (image url), authorUrl (optional) : string (link))
- setTitle(title: string)
- setURL(url: string)
- setThumbnail(thumbnail : string (image url))
- setImage(image : string (image url))
- setTimestamp(date (optional) number/date object)
- setColor(color : string/number (hex or decimal color))
- setDescription(description : string)
- addField(fieldName : string, fieldValue: string, inline (optional) : boolean)
- setFooter(footer : string, footerImage (optional) : string (image url))
```
