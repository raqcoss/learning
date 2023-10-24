# NOTES ON MARKDOWN NOTATION

https://www.markdownguide.org/basic-syntax/
**bold text**
__bold text__
*italic text*
_italic text_
***really important***
___bold and italic text___

> Block quote
>
> also in the same block
>> Nested Blockquotes

#### Ordered lists
1. First item
2. Second item
3. Third item
    1. Indented item
    2. Indented item
4. Fourth item

#### Unordered Lists
- item
- item

+ item
+ item

* item
* item

#### Code blocks
Code blocks are normally indented four spaces or one tab. When they’re in a list, indent them eight spaces or two tabs.

- item
- item

        <html>
          <head>
            <title>Test</title>
          </head>
  
- item

At the command prompt, type `nano`.

```
big code
```
#### Images
![Tux, the Linux mascot](/assets/images/tux.png)

#### Links
My favorite search engine is [Duck Duck Go](https://duckduckgo.com).
My favorite search engine is [Duck Duck Go](https://duckduckgo.com "The best search engine for privacy").

#### URLs and Email Addresses
<https://www.markdownguide.org>
<fake@example.com>

#### Reference-style Links

In a hole in the ground there lived a hobbit. Not a nasty, dirty, wet hole, filled with the ends
of worms and an oozy smell, nor yet a dry, bare, sandy hole with nothing in it to sit down on or to
eat: it was a [hobbit-hole][1], and that means comfort.

[1]: <https://en.wikipedia.org/wiki/Hobbit#Lifestyle> "Hobbit lifestyles"

#### Escaping characters
Use \

# Markdown Cheat Sheet

Thanks for visiting [The Markdown Guide](https://www.markdownguide.org)!

This Markdown cheat sheet provides a quick overview of all the Markdown syntax elements. It can’t cover every edge case, so if you need more information about any of these elements, refer to the reference guides for [basic syntax](https://www.markdownguide.org/basic-syntax/) and [extended syntax](https://www.markdownguide.org/extended-syntax/).

## Basic Syntax

These are the elements outlined in John Gruber’s original design document. All Markdown applications support these elements.

### Heading

# H1
## H2
### H3

### Bold

**bold text**

### Italic

*italicized text*

### Blockquote

> blockquote

### Ordered List

1. First item
2. Second item
3. Third item

### Unordered List

- First item
- Second item
- Third item

### Code

`code`

### Horizontal Rule

---

### Link

[Markdown Guide](https://www.markdownguide.org)

### Image

![alt text](https://www.markdownguide.org/assets/images/tux.png)

## Extended Syntax

These elements extend the basic syntax by adding additional features. Not all Markdown applications support these elements.

### Table

| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |

### Fenced Code Block

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

### Footnote

Here's a sentence with a footnote. [^1]

[^1]: This is the footnote.

### Heading ID

### My Great Heading {#custom-id}

### Definition List

term
: definition

### Strikethrough

~~The world is flat.~~

### Task List

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

### Emoji

That is so funny! :joy:

(See also [Copying and Pasting Emoji](https://www.markdownguide.org/extended-syntax/#copying-and-pasting-emoji))

### Highlight

I need to highlight these ==very important words==.

### Subscript

H~2~O

### Superscript

X^2^


