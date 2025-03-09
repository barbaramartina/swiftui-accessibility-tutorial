# VoiceOver
For VoiceOver, what you could do within your app includes:

- Adding appropriate descriptions for relevant images
- Try not to add descriptions to each single little image and icon to avoid overloading the user.
- Use meaningful accessibility labels on the views which you want to describe in more detail. Work closely with your copy team, to make also accessibility available in different languages. https://developer.apple.com/documentation/swiftui/view/accessibilitylabel(_:)
- Do not include words which are already in the component, for example if you have a button which has text like “Call now”, do not add a label saying “This button allows you to call now”, but choose something more appropriate which informs the user better.
- Make it easier to input commands by using inputLabels Adding an input label, will help users to control UI elements in a more friendly way, when the use case applies. For example, if you have a list of items, then you could add an accessibility input label to reduce the amount of text that the user would need to speak into VoiceOver to control the element. The user can tap each row to get a list of groceries category details. By using accessibilityInputLabels() the user can just speak “Tap Fruits” into VoiceOver commands. Without the modifier, a voice control user would have to say something like "Tap Fruits Apples Bananas Mango” to activate this link. https://developer.apple.com/documentation/swiftui/view/accessibilityinputlabels(_:)-8ann4
- Accessibility Value: You can add a value to a UI element, such as a button or a slider, and provide the current value associated with it. For example, if you have a button which will increment the radius of a search, then you can label the button as “Search radius” and add a value, which will speak the current value selected. (check my previous article to see code for this)
- Hints: In addition to labels, you could also provide, in special circumstances, more information to the users about what will happen after they select a certain option. Hints should not repeat information that VoiceOver already can present to the user, and should not be overused. I suggest to use hints only in critical elements, where the actions can not be reversed, or the users would enter a billing agreement for example. But also, keep in mind that any very critical information should be already presented before either in text elements that VoiceOver will read or in labels on non-text elements. And the users can also disable hints, to make VoiceOver less verbose going to General > Accessibility > VoiceOver > Verbosity > Speak Hints. https://developer.apple.com/documentation/swiftui/view/accessibilityhint(_:)-8bh2s
https://developer.apple.com/documentation/uikit/uiaccessibilitycustomaction When there are too many tiny buttons in one table view cell for example, if VoiceOver needs to read the whole screen and goes per every cell and read each action again an again, this can result in a very overwhelming experience. For this, you can use custom accessibility actions, grouping the container view (supposing all those little buttons are in a stack view for example), mark it as “accessibilityElement(children: .ignore)” and then associate accessible actions. When the user has VoiceOver enabled, they can swipe down and double tap to select the actions, they will be swiping and double tapping in the container area, giving the user a much bigger portion of the screen to iterate through the actions, instead of having to precisely point their fingers to a tiny heart button, for example, to like a content.
- Grouping. https://developer.apple.com/documentation/swiftui/view/accessibilityelement(children:). To be able to group some views together and change the behaviour of a container, you can use the mentioned modifier and choose to either ignore, combine or contain the children views into the container view. It is important in cases where you want a container to be first, and then another one second, since VoiceOver will read first all the elements of a container in order.
- Headers can help users who use the rotor To give structure to the content of a screen you can choose to mark sections within it. It will help the user to navigate the content of the view. For this they need to have the -

```swift
NavigationStack{
    VStack(alignment: .leading){
                
    /// Header Level 2
    Text("A list of grocery items")
        .font(.headline)
        .accessibilityAddTraits(.isHeader)
        .accessibilityHeading(.h2)
        .padding()

        // other ui elements with other headings

    }
}
```

- VoiceOver Rotor Heading enabled, and swipe up and down to access different levels of headings. https://developer.apple.com/documentation/swiftui/accessibilityheadinglevel
- Images: you can give them a descriptive name or use Image(decorative: "my-image")) for hiding them from the generation of the Accessibility user interface tree.

<img width="404" alt="Screenshot 2025-03-07 at 11 41 30 PM" src="https://github.com/user-attachments/assets/e8682b76-73fa-4414-b7c4-f4d5ac8cebfc" />


## Rotors
An interesting helpful addition would be to add a new rotor entry, that will be seen when the user makes the rotor gesture. In that way, when they rotate around the rotor, you can provide custom actions. Checkout this for an example: https://developer.apple.com/documentation/swiftui/view/accessibilityrotor(_:entries:)
Sorting: VoiceOver and other assistive technology operate in a manner similar to natural reading. This implies top left to bottom right in English for example. For the most part, assistive technology made the correct choice. However, occasionally we create designs that don't read like this. The order in which assistive technology accesses components can be configured by using the.accessibility(sortPriority: ) modification. You must group elements in a stack (HStack, VStack, or ZStack) in order to accomplish this. Next, apply the modifier.accessibilityElement(children:.contain). VoiceOver will focus on the item earlier if we give.accessibility(sortPriority: ) a greater number. 
