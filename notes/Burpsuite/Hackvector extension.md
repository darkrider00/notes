Hackvertor is a tag-based conversion tool that supports various escapes and encodings including HTML5 entities, hex, octal, unicode, url encoding etc.

- It uses XML-like tags to specify the type of encoding/conversion used.
- You can use multiple nested tags to perform conversions.
- Tags can also have arguments allowing them to behave like functions.
- It has an auto decode feature allowing it to guess the type of conversion required and automatically decode it multiple times.
- Multiple tabs
- Character set conversion

# How to use Hackvertor

[](https://github.com/hackvertor/hackvertor#how-to-use-hackvertor)

To use Hackvertor once it has been installed, click on the Hackvertor tab in the main Burp Suite window. You can then type into the input box to create some text to convert. For instance if you want to convert some text to base64, select the text in the input box then click on the encode tab in Hackvertor, then find the base64 tag and click it. Hackvertor will then add the tag around the selected text and the output window will show a base64 encoded string of your text. It's worth noting that Hackvertor supports an unlimited amount of nesting, you can use multiple tags to encode or decode text. Hackvertor will work from the inner most tag to the outer tag and each step will be converted using the relevant tag you have chosen.

# Advanced usage

[](https://github.com/hackvertor/hackvertor#advanced-usage)

For more advanced users, you can use tags within repeater tabs. Simply click the repeater tab, right click and select the Hackvertor menu. Then you can use any tag within the repeater tab. Tags will be displayed in the repeater window but when a request is sent they will be converted by Hackvertor and the server will see the converted request. Hackvertor also have a message editor tab, you can select this tab from any request tab in Burp. This will then create the Hackvertor interface inside a request tab, allowing to use the Hackvertor interface to modify a request.

reference  : https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100