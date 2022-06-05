
[meta]: # (CSS_URL=../theme.css)
[meta]: # (DOCUMENT_TITLE=systems - viveknathani)

# character encodings

This is a very interesting topic, yet many programmers are not well versed with the intricacies of the process of encoding. Let's first understand what character encoding means? It is the process of converting the characters you see on your screen, into a format understood by computers. Computers understand bits. So, you need to transform your character into some form of bits. The problems in this domain involve agreeing upon a common encoding format that covers a large set of characters understood by humans.

## ASCII

Initially, the characters we were really concerned with were the English characters, numbers, and some special characters. This complete character set could be represented in 7 bits. Their decimal representation ranges from 0 to 127, giving you 128 characters to work with.

## extending ASCII

7-bit representation was fine. But, people wanted to cover more than just English characters. Also, computers use bytes. A byte has 8-bits. So, you have an extra bit to spare after covering ASCII. So the extra bit kept wondering:

<img src="./meme-extra-bit.jpg"/>

Everybody had ideas what to do with the extra bit. Everybody kept the range 0 to 127 like ASCII. They were different in what should be done in the range 128 to 255. These different systems were called code pages. Everybody tried to cover their own languages, German, Spanish, Japanese, etc..

This worked well, as long as you assumed that a character would take 1 bytes in memory and you only speak in one language. As Internet became a widespread thing, strings were moved from one computer to another, often in different countries. Everybody had their own way of interpreting bits. Hence, the whole thing fell apart.

But then, something cool happened.

<img src="./meme-enter-unicode.jpg"/>

## unicode

The idea of Unicode is, "Everyone in the world should be able to use their own language on phones and computers.".
Previous ideas revolve around assigning a byte or a set of bytes for each character. Unicode revolves around "providing a unique number for every character, no matter what platform, device, application or language". This unique number is called code point. It is written like this: U+0041. U+ means unicode, followed by hexadecimal numbers. There is no real limit on the number of letters that Unicode can represent. Hence, there is no limit on the size of a Unicode character in memory. 

For example, 'Hello' translates to: U+0048 U+0065 U+006C U+006C U+006F. 

Now, people started wondering about how Unicode should be stored in memory and there were following ideas. 
1. Assign two bytes to each Unicode character. So 'Hello' becomes => 00 48 00 65 00 6C 00 6C 00 6F. But, this could also be => 48 00 65 00 6C 00 6C 00 6F 00. Some processors stored bits in big-endian mode (left-most bit first) and some in little-endian mode (right-most bit first). So, people had to start their strings with two extra bytes that represent how the bytes were stored. (U+FEFF for big-endian, U+FFEE for little-endian). This extra character is called as the Unicode Byte Order Mark. 
2. Preserve backward compatibility with ASCII. So, the first 128 characters of Unicode are just as same as ASCII. They take a byte in memory. For more characters, assign more number of bytes. This is called UTF-8 encoding. The maximum number of bytes in UTF-8 is 4. Hence, UTF-8 is a variable length encoding format. Also, with UTF-8, you can represent emojis.
3. UTF-16: In the UTF-16 encoding, code points less than 216 are encoded with a single 16-bit code unit equal to the numerical value of the code point. The newer code points greater than or equal to 216 are encoded by a compound value using two 16-bit code units. This is called as a "surrogate pair". This makes it incompatible with ASCII. Like UTF-8, this is variable length encoding too. But UTF-16 helps in representing more emojis. 
4. UCS-2: UCS-2 (2-byte Universal Character Set) produces a fixed-length format by simply using the code point as the 16-bit code unit. This produces exactly the same result as UTF-16 for the majority of all code points. 

There are more ways but this is what every programmer should know. Hence, a string is meaningless if you do not specify how it is encoded. This is why emails are expected to have a header of the form, `Content-Type: text/plain; charset="UTF-8"`. For a web page, it should ideally have something like, `<meta http-equiv="Content-Type" content="text/html; charset=utf-8">`. Whatever your encoding is, you should specify it. When you don't, browsers try to so do some guess work. Sometimes, they would be correct. Sometimes, not. Hence, be explicit. Otherwise, 

<img src="./meme-be-clear.jpeg">

## unicode in javascript

If you deal with javascript a lot, you should know how unicode works in javascript. 
ECMAScript, the standardized version of JavaScript, defines how characters should be interpreted. JavaScript engines are allowed to use either UCS-2 or UTF-16. JavaScript engines are free to use UCS-2 or UTF-16 internally. Most engines use UTF-16, but whatever choice they made, it’s just an implementation detail that won’t affect the language’s characteristics. The ECMAScript/JavaScript language itself, however, exposes characters according to UCS-2, not UTF-16. The only difference is that technically, UCS-2 doesn’t allow surrogate characters, while JavaScript strings do. Hence, this is like UCS-2 + surrogate pairs. Very close to being similar to UTF-16. Weird, I know. 

UCS-2 with surrogates on being compared with UTF-16:
<img src="./meme-ucs-utf.jpg"/>

Relevant functions in javascript: 
```
String.prototype.charCodeAt()
// The charCodeAt() method returns an integer between 0 and 65535 representing the UTF-16 code unit at the given index.
If the Unicode code point cannot be represented in a single UTF-16 code unit (because its value is greater than 0xFFFF) then the code unit returned will be the first part of a surrogate pair for the code point. If you want the entire code point value, use codePointAt(). 
String.prototype.codePointAt()
// The codePointAt() method returns a non-negative integer that is the Unicode code point value at the given position.
String.fromCharCode()
// The static String.fromCharCode() method returns a string created from the specified sequence of UTF-16 code units. 
```

Fin.

<img src="./meme-chalta-hu.jpg"/>



