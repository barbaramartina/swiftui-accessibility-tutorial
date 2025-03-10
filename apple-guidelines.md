# Apple Guidelines
Even if you would like to have a platform agnostic guidelines, I recommend to always check the specific Apple Platform guidelines and make sure that your overall guidelines comply to it.

- [Accessibility guidelines](https://developer.apple.com/design/human-interface-guidelines/accessibility)
- [VoiceOver](https://developer.apple.com/design/human-interface-guidelines/voiceover)
- [Typography and dynamic type](https://developer.apple.com/design/human-interface-guidelines/typography)

## Typography
An important passage of the guidelines is the following one, remarking that you should consider which text is more important, and do not indiscriminately make every text bigger when reacting to dynamic sizes.
You have other alternatives to bring clarity (such as larger content viewer).

    Prioritize important content when responding to text-size changes. Not all content is equally important. When someone chooses a larger text size, they typically want to make the content they care about easier to read;     they don’t always want to increase the size of every word on the screen. For example, when people increase text size to read the content in a tabbed window, they don’t expect the tab titles to increase in size.         
    Similarly, in a game, people are often more interested in a character’s dialog than in transient hit-damage values.

**Avoid custom sizes** 
Apple provides a wide variety of fonts and sizes which automatically adjust to different platforms and dynamic content sizes. Avoid redefining the sizes and if you implement custom fonts, try to adopt the recommended Apple sizes.

**Consider adjusting the layout when the dynamic size type changes**
You can do so by using the environment value:

```swift
/// accessing the selected content size (user an select it in Settings in the iPhone)
 @Environment(\.dynamicTypeSize) var sizeCategory

if sizeCategory > DynamicTypeSize.medium {
    // if the size category grows then let's just display each fruit in a separate row
    Text("Dry fruits:")
    Text("Nuts")
    Text("Peanuts")
    Text("Fresh fruits:")
    Text("Apple")
    Text("Mandarinen")
    Text("Mangoes")
} else {
    // if the size category is equal or less than medium, then let's add an horizontal stack to not occupy much space in the list
    HStack {
        Text("Dry fruits:")
        Text("Nuts")
        Text("Peanuts")
    }
    HStack {
        Text("Fresh fruits:")
        Text("Apple")
        Text("Mandarinen")
        Text("Mangoes")
    }
}
```
