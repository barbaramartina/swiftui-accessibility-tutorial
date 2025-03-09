# Environment values
There are a set of environments values that you will have at your disposition while implementing accessibility in SwiftUI, you can access to all of them here: https://developer.apple.com/documentation/swiftui/environmentvalues/

They will allow you to react to user’s choices, such as not [playing any animation on images](https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityplayanimatedimages )
or [reduceMotion which will indicate you that animations should be slower](https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityreducemotion)

## Environment value: Assistive Access
*Settings  > Accessibility > Assistive Access*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityassistiveaccessenabled
Assistive Access is a unique iOS feature that facilitates independent iPhone use for those with cognitive impairments. Assistive Access-optimized essential apps and experiences include larger on screen elements, more focused functionality, and an easier-to-navigate interface that makes it clear what actions are feasible.

## Environment value: Dim Flashing Lights
*Settings  > Accessibility > Motion > Dim Flashing Lights*
From iOS 17. 
Whether the setting to reduce flashing or strobing lights in video content is on. This setting can also be used to determine if UI in playback controls should be shown to indicate upcoming content that includes flashing or strobing lights.
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilitydimflashinglights
https://developer.apple.com/documentation/mediaaccessibility/responding-to-changes-in-the-flashing-lights-setting

## Environment value: Differentiate without color
*Settings  > Accessibility > Display and Text Size > Differentiate without color*
If this is true, UI should not convey information using color alone and instead should use shapes or glyphs to convey information.
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilitydifferentiatewithoutcolor

## Environment value: invert colors
*Settings  > Accessibility >  Display and Text Size > Classic Invert*
*If this property’s value is true then the display will be inverted. In these cases it may be needed for UI drawing to be adjusted to in order to display optimally when inverted.*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityinvertcolors

## Environment value: larger displays enabled
*Settings  > Accessibility >  Display and Text Size > Larger Accessibility Sizes*

Standard components such as the Status Bar, Toolbar Items, Tab Bar Items, and Navigation Bar Items automatically display the Large Content Viewer. 

You must ensure that the Large Content Viewer is supported if you are limiting the text size of elements or if you are utilizing custom components that shouldn't expand for bigger accessibility text sizes.
If you want to activate the Larger Content Viewer, then make sure that you selected the Larger Accessibility Sizes, and that you are using a large size, then you can go to the Alarms App for example, and there you will see that some buttons did not grow. For those, Apple provides the Larger Viewer. Tap and hold in some of them and you will see that they are presented in a larger view, in the middle of the screen.

<kbd>
<img width="278" alt="Screenshot 2025-03-07 at 11 37 59 PM" src="https://github.com/user-attachments/assets/85b8f21d-e26c-44da-86e8-3fc9333c7c9e" />
<img width="278" alt="Screenshot 2025-03-07 at 11 37 59 PM" src="https://github.com/user-attachments/assets/f491d764-d3c5-4b78-a513-55b082e4b97e" />
</kbd>

https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilitylargecontentviewerenabled

For example, if we limit a button to an specific dynamic sizes, then we can offer the larger preview using the following code:

```swift
 private var buttonLimitedInSize: some View {
        Button("Add") {
            // action
        }
        // adding this modifier prevents the button from growing larger than this size
        .dynamicTypeSize(DynamicTypeSize.xxxLarge)
        // and using this will show it in the larger viewer when the user taps and holds on it
        .accessibilityShowsLargeContentViewer()
    }
```

## Environment value: Play animated images
*Settings  > Accessibility > Motion > Auto-Play animated images*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityplayanimatedimages

## Environment value: Prefers head anchor alternatives
*Settings  > Accessibility >  *
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityprefersheadanchoralternative

## Environment value: quick actions enabled
*Settings  > Accessibility >  *
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityquickactionsenabled

## Environment value: reduce motion
*Settings  > Accessibility >  Motion > Reduce Motion*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityreducemotion

## Environment value: reduce transparency
*Settings  > Accessibility >  Display and Text Size > Reduce transparency*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityreducetransparency

## Environment value: show buttons shapes
*Settings  > Accessibility >   Display and Text Size > Show buttons shape*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityshowbuttonshapes

## Environment value: switch control enabled
*Settings  > Accessibility >  (Physical and motor) Switch Control*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityswitchcontrolenabled

## Environment value: voiceover enabled
*Settings  > Accessibility >  VoiceOver*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityvoiceoverenabled

## Environment value: Legibility weight
*Settings  > Accessibility >  Display and Text Sizes > Bold Text *
https://developer.apple.com/documentation/swiftui/environmentvalues/legibilityweight

