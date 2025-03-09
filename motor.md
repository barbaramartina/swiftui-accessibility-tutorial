# Physical and Motor

<img width="342" alt="Screenshot 2025-03-07 at 11 44 17 PM" src="https://github.com/user-attachments/assets/b159b2b7-c898-4898-8cdc-033640a41536" />


To check your apps and see how they work with VoiceControl, you can checkout this article https://developer.apple.com/documentation/accessibility/voice-control
For providing custom actions for example when there are too many tiny buttons in one table view cell for example, if VoiceOver needs to read the whole screen and goes per every cell and read each action again and again, this can result in a very overwhelming experience.


For this, you can use custom accessibility actions, grouping the container view (supposing all those little buttons are in a stack view for example), mark it as “accessibilityElement(children: .ignore)” and then associate accessible actions. When the user has VoiceOver enabled, they can swipe down and double tap to select the actions, they will be swiping and double tapping in the container area, giving the user a much bigger portion of the screen to iterate through the actions, instead of having to precisely point their fingers to a tiny heart button, for example, to like a content.
https://developer.apple.com/documentation/uikit/uiaccessibilitycustomaction
