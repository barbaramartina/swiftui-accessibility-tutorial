# SwiftUI Accessibility Tutorial
In this repository I will focus on dissecting the iOS Settings options and connecting them to the available technical modifiers and configurations needed to support them in our apps.

If you would like to read about what will be required, accessibility-wise for complying with the Accessibility Act, 
by June 2025 and to inform yourself about deadlines and the full scope of the act you can read the articles linked at the end in the **“References”** section.

## Accessibility development strategy
Either if you’re making your app more accessible, or you’re just starting to add accessibility features within it, before engaging in the odyssey of extending your product usage and making it more usable for a larger number of users who either on a permanent or temporal basis need specific features, 

I would suggest developing a gradual plan and getting very clear agreements within your teams (QA/Development/Project Managers/Support teams/Legal teams, etc), about how the roadmap will be when it comes to adding more accessibility features to your app. There are tons of configurations which are possible. You can support external keyboards / braille devices for example, but if you’re just starting, making sure that VoiceOver works well would be a base step. 

I suggest defining a concrete basic set of accessibility features and develop a plan to bring new portions of your app up to standard, but also bear in mind what you will do with older code, older screens, which you might not be touching for a while. Being clear about that will save you time and avoid misunderstanding. Let’s say that you do not come into concrete written agreements about what is possible to test and what is (for the moment) not covered, then you could end up in a situation where your QA team starts trying out very different settings from within the Apple Settings when it comes to accessibility, and if each QA has a different testing strategy and pay attention to different settings, and you did not establish an acquisition gradual step by step strategy, this will generate noise, back and forth, ongoing discussions among different parts of your team… it will be messy… accessibility is not a clearly defined topic and do have subjective interpretations, even though the platforms establish certain guidelines. 

Also you might want to consider the time and effort that you realistically have within your schedule to bring more accessibility into your app. Remember that by June 2025 you should comply with the Accessibility Act requirements, and unless there is an extension, there would be scenarios that your products will need to cover. 
As it is happening with GDPR, where lawyers and lawyers companies are checking the adoption of the directives, 
I think that the same will start happening with Accessibility, so pay attention, be careful, use your resources to make sure that in a reasonable amount of time you can reach a good-enough accessibility coverage… and then, build up from there… over time. Do not try to go for all, from the very beginning. 
And make sure that you do not end up in an unorganized testing / bug reporting / details discussion / eternal backs and forths. 
So, let’s go to analyze the anatomy of accessibility in an iPhone.

| **Step**                            | **Key Actions**                                          | **Considerations**                                      |
|-------------------------------------|--------------------------------------------------------|--------------------------------------------------------|
| **1. Start Accessibility Improvements** | - Identify accessibility needs  <br> - Plan for temporary/permanent user needs | - Focus on usability expansion |
| **2. Develop a Gradual Plan**        | - Align teams (QA, Dev, PMs, Legal, Support)  <br> - Define roadmap for features | - Start with VoiceOver support  <br> - Consider future options (Braille, external keyboards) |
| **3. Manage Legacy Code & Screens**  | - Define which parts of the app will be updated <br> - Plan for older screens & untouched code | - Avoid inefficiencies and misalignment |
| **4. Standardize Testing Strategy**  | - Ensure a clear, written QA strategy <br> - Define what is tested and what is excluded | - Prevent inconsistent testing across different team members |
| **5. Consider Time & Effort**        | - Assess realistic implementation timeline <br> - Plan for June 2025 Accessibility Act compliance | - Learn from GDPR enforcement trends |
| **6. Final Approach**                | - Achieve a reasonable level of accessibility <br> - Organize bug reporting and testing | - Improve progressively over time |


## Usage
Making an analysis of some studies or surveys, you could give yourself an idea about what accessibility features are the most needed / used. I have found some resources which could be a guide for deciding the priorities when it comes to adopting certain features. For example in this survey of millions of users in the Netherlands, in 2024, it was found that 38% of persons turn on dark mode, while 22% make their fonts larger, 9,7% use zoom on the screen, 9,8% have turned on bold text, 3,6% use speak selection, 0,02% use VoiceOver. https://appt.org/en/stats.

<kbd>
<img width="555" alt="Screenshot 2025-03-09 at 7 07 06 PM" src="https://github.com/user-attachments/assets/cc69a9d2-c314-4797-abe8-4b6b1e6164dd" />
</kbd>

But, I would not recommend just reading current usage statistics, since it could be that people do not make use of certain features just because the support offered right now is not great. 

Another idea to collect numbers, is to try finding scientific studies, which are usually constricted to certain application domains, but you could perhaps find some closer to your user base, such as for example https://www.sciencedirect.com/science/article/abs/pii/S095058492400123X.
In this sense, which accessibility support you would prioritize will be very related to the field in which your app is working.

## Apple Guidelines
Even if you would like to have a platform agnostic guidelines, I recommend to always check the specific Apple Platform guidelines and make sure that your overall guidelines comply to it.

- [Accessibility guidelines](https://developer.apple.com/design/human-interface-guidelines/accessibility)
- [VoiceOver](https://developer.apple.com/design/human-interface-guidelines/voiceover)
- [Typography and dynamic type](https://developer.apple.com/design/human-interface-guidelines/typography)

### Typography
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

## Some reflections on tracking
If you are going to track which accessibility values your users are selecting, 
I would think carefully about it, most probably there is a reduced number of users which will set some accessibility features,
make sure that you disclose in the Apple Privacy Pages any tracking you use about these sensitive values. And if possible, do not make any tracking on them.

## Learning accessibility
Apple has a great tutorial when it comes to perhaps the most difficult feature to learn: VoiceOver. 
I would recommend doing that tutorial, more than just once. It took me around 3 or 4 times till I started to get a feeling of the gestures.

<kbd>
<img width="378" alt="Screenshot 2025-03-07 at 11 37 59 PM" src="https://github.com/user-attachments/assets/ffec04df-0389-402a-9ab3-a30967c4d0e5" />
</kbd>

## Quick testing while developing
### Accessibility Inspector

<kbd>
<img width="338" alt="Screenshot 2025-03-08 at 12 41 29 PM" src="https://github.com/user-attachments/assets/e87bd830-b1d8-475f-ad20-0d84e59a059b" />
</kbd>kbd>

Support yourself with the accessibility inspector. In my experience it is unreliable. If you see that it stops working,
try closing it completely and launching it again. When it works, it does help a lot to inspect elements and play around with some settings in the simulator.

You can also use the Accessibility Inspector to run audits and get warnings about some of the most ground features.

<kbd>
<img width="258" alt="Screenshot 2025-03-07 at 11 38 41 PM" src="https://github.com/user-attachments/assets/77c9b00f-f20e-4d46-874d-f8413434923f" />
<img width="257" alt="Screenshot 2025-03-07 at 11 38 47 PM" src="https://github.com/user-attachments/assets/4d5b1c91-f50f-4cd7-b74b-8b5c016d5a13" />
</kbd>

### Previews
Previous are a great way to quickly have feedback, ideally you should rely on the system defined font types,
I recommend against adjusting the font sizes unless you have a custom font, otherwise you will lose all the  benefits from the development environment,
such as previews and modifiers overview. Using a system font with a different sizing will cause you issues, 
since there is not way to make the previews and Apple UIs-modifier work, so it will slow you down while developing, just because your font is 1 pixel bigger or smaller. It’s not a good practice. 

<kbd>
<img width="340" alt="Screenshot 2025-03-07 at 10 45 24 PM" src="https://github.com/user-attachments/assets/fc3f226d-65d4-4798-83c9-d31d77a04b21" />
<img width="461" alt="Screenshot 2025-03-07 at 10 45 46 PM" src="https://github.com/user-attachments/assets/2a00c2a5-fd28-482e-b55c-f6b50241768f" />
<img width="560" alt="Screenshot 2025-03-08 at 12 32 16 PM" src="https://github.com/user-attachments/assets/68c64ca9-a50e-4521-9992-f2ed17fe74d1" />
</kbd>

## Auditing your apps and testing
Apple has great documentation and step by step testing instructions for each of the accessibility groups. 
I recommend you to check them out: [Testing Accessibility](https://developer.apple.com/documentation/accessibility/performing-accessibility-testing-for-your-app)

### Automatic auditing
You can also create an UI test target and perform automatic accessibility audits.

<kbd>
<img width="557" alt="Screenshot 2025-03-08 at 12 44 29 PM" src="https://github.com/user-attachments/assets/8f0903e5-6b42-4183-855c-1e829eba94ce" />
</kbd>

You will be able to see the test errors and also the tests results logs are pretty cool, even with videos of the runs.

<kbd>
<img width="384" alt="Screenshot 2025-03-08 at 12 47 47 PM" src="https://github.com/user-attachments/assets/780221f3-a1af-4c32-9bd7-4da59804cc6b" />
<img width="760" alt="Screenshot 2025-03-08 at 12 48 23 PM" src="https://github.com/user-attachments/assets/2f286da6-d7c0-42e1-a75e-d02f8dca000d" />
<img width="760" alt="Screenshot 2025-03-08 at 12 49 21 PM" src="https://github.com/user-attachments/assets/a97e129d-1cab-43a7-9fe9-b60af5d4f29d" />
</kbd>

#### Ignoring legacy UI
For UI elements which you can’t improve at the moment, you can ignore them in the automated UI checks with the following code

```swift
import XCTest

final class AccessibilityTutorialUIAudit: XCTestCase {

    func testAutomatedAccessibility() {
        let myApp = XCUIApplication()
        myApp.launch()
        
        // this is how you ignore specific elements which you know
        // have issues and you can't solve at the moment (like legacy UI)
        let handler: ((XCUIAccessibilityAuditIssue) -> Bool) = { issue in
            if issue.element == myApp.staticTexts["stepper.description"] {
                false // ignore problems with this text which is clipped
            } else {
                true // check any other error
            }
        }
        
        do {
            // you can either audit all, or a set of checks
            try myApp.performAccessibilityAudit(for: [.contrast, .dynamicType, .textClipped], handler)
        } catch {
            XCTFail("The automated accessibility audit fail because [\(error.localizedDescription)]")
        }
    }
}
```

## Environment values
There are a set of environments values that you will have at your disposition while implementing accessibility in SwiftUI, you can access to all of them here: https://developer.apple.com/documentation/swiftui/environmentvalues/

They will allow you to react to user’s choices, such as not [playing any animation on images](https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityplayanimatedimages )
or [reduceMotion which will indicate you that animations should be slower](https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityreducemotion)

### Environment value: Assistive Access
*Settings  > Accessibility > Assistive Access*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityassistiveaccessenabled
Assistive Access is a unique iOS feature that facilitates independent iPhone use for those with cognitive impairments. Assistive Access-optimized essential apps and experiences include larger on screen elements, more focused functionality, and an easier-to-navigate interface that makes it clear what actions are feasible.

### Environment value: Dim Flashing Lights
*Settings  > Accessibility > Motion > Dim Flashing Lights*
From iOS 17. 
Whether the setting to reduce flashing or strobing lights in video content is on. This setting can also be used to determine if UI in playback controls should be shown to indicate upcoming content that includes flashing or strobing lights.
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilitydimflashinglights
https://developer.apple.com/documentation/mediaaccessibility/responding-to-changes-in-the-flashing-lights-setting

### Environment value: Differentiate without color
*Settings  > Accessibility > Display and Text Size > Differentiate without color*
If this is true, UI should not convey information using color alone and instead should use shapes or glyphs to convey information.
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilitydifferentiatewithoutcolor

### Environment value: invert colors
*Settings  > Accessibility >  Display and Text Size > Classic Invert*
*If this property’s value is true then the display will be inverted. In these cases it may be needed for UI drawing to be adjusted to in order to display optimally when inverted.*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityinvertcolors

### Environment value: larger displays enabled
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

### Environment value: Play animated images
*Settings  > Accessibility > Motion > Auto-Play animated images*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityplayanimatedimages

### Environment value: Prefers head anchor alternatives
*Settings  > Accessibility >  *
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityprefersheadanchoralternative

### Environment value: quick actions enabled
*Settings  > Accessibility >  *
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityquickactionsenabled

### Environment value: reduce motion
*Settings  > Accessibility >  Motion > Reduce Motion*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityreducemotion

### Environment value: reduce transparency
*Settings  > Accessibility >  Display and Text Size > Reduce transparency*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityreducetransparency

### Environment value: show buttons shapes
*Settings  > Accessibility >   Display and Text Size > Show buttons shape*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityshowbuttonshapes

### Environment value: switch control enabled
*Settings  > Accessibility >  (Physical and motor) Switch Control*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityswitchcontrolenabled

### Environment value: voiceover enabled
*Settings  > Accessibility >  VoiceOver*
https://developer.apple.com/documentation/swiftui/environmentvalues/accessibilityvoiceoverenabled

### Environment value: Legibility weight
*Settings  > Accessibility >  Display and Text Sizes > Bold Text *
https://developer.apple.com/documentation/swiftui/environmentvalues/legibilityweight


## Accessibility traits
There is a way to add or remove traits to your views, for example, if you want to inform that some of your views update frequently, you could opt for adding the trait “updatesFrequently” to it https://developer.apple.com/documentation/swiftui/accessibilitytraits/updatesfrequently

## Accessibility and UI tests
Be careful with some accessibility modifiers, such as hidden children or setting isAccessibilityElement, since they have an effect on how the accessibility tree will be generated and therefore some identifiers might turn out hidden.


# Accessibility Anatomy 
To begin with, I will try to be concise. I will list each of the options, groups by accessibility area: Vision / Hearing / Physical and Motor / Speech / Accessories and General.
Example applications

Apple itself has listed, for each of the categories mentioned above, some applications which have done a great job, so for inspiration you can checkout this list https://apps.apple.com/mv/story/id1266441335

## Vision
In this group of settings we do have VoiceOver, Motion, Display and Text, Zoom and Spoken Content.

<kbd>
<img width="373" alt="Screenshot 2025-03-07 at 11 42 12 PM" src="https://github.com/user-attachments/assets/ae2ff757-c590-4b72-ba8c-f064bfbbfaf9" />
</kbd>

### VoiceOver
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


#### Rotors
An interesting helpful addition would be to add a new rotor entry, that will be seen when the user makes the rotor gesture. In that way, when they rotate around the rotor, you can provide custom actions. Checkout this for an example: https://developer.apple.com/documentation/swiftui/view/accessibilityrotor(_:entries:)
Sorting: VoiceOver and other assistive technology operate in a manner similar to natural reading. This implies top left to bottom right in English for example. For the most part, assistive technology made the correct choice. However, occasionally we create designs that don't read like this. The order in which assistive technology accesses components can be configured by using the.accessibility(sortPriority: ) modification. You must group elements in a stack (HStack, VStack, or ZStack) in order to accomplish this. Next, apply the modifier.accessibilityElement(children:.contain). VoiceOver will focus on the item earlier if we give.accessibility(sortPriority: ) a greater number. 

<kbd>
<img width="573" alt="Screenshot 2025-03-07 at 11 42 12 PM" src="https://github.com/user-attachments/assets/c5e8019a-d192-4d06-ab6c-06ef5b964837" />
</kbd>

### Motion
There is an option in Settings > Accessibility > Reduce Motion, that users can choose when animations could trigger undesired effects for them. According to Apple’s documentation “Vestibular disorders are caused by problems affecting the inner ear and parts of the brain that control balance and spatial orientation. Symptoms can include loss of balance, nausea, and other physical discomfort. Vestibular disorders are more common than you might guess: affecting as many as 69 million people in the United States alone.”
You can react to the user preference by reading the environment variable accessibilityReduceMotion, and reacting either removing animations or making them slower /. More appropriate.

<kbd>
<img width="630" alt="Screenshot 2025-03-07 at 11 42 32 PM" src="https://github.com/user-attachments/assets/6b34053d-ed5e-40b0-9cac-371bd9e757a4" />
<img width="326" alt="Screenshot 2025-03-07 at 11 42 55 PM" src="https://github.com/user-attachments/assets/9e122bf8-7ee2-438f-a345-7adfb3986e26" />
</kbd>

### Display Text and Sizes
By going to Settings -> Display and Brightness -> Text Size the users will be able to select a preference for the size of text they would like to see.
You can adjust your texts automatically  by using the “font(…” modifier in SwiftUI, watch for your views truncation mode, make sure that the text is not truncated, or that is the text is very long, it can occupy at least a minimum amount of lines which can help the user to understand the associated content on the screen.
Additionally by accessing the dynamic type size you can make adjustments in your layout to accommodate different sizes preferences
Go to my previous article, mentioned before, to see the source code.

<kbd>
<img width="535" alt="Screenshot 2025-03-07 at 11 43 33 PM" src="https://github.com/user-attachments/assets/39faa0c9-a0b2-4292-8e40-ba46ffdceef7" />
</kbd>

### Spoken Content
When using the capabilities of the spoken content feature, your users will be able to read the screen or the selected text. To avoid verbosity, you could make use of a modifier which allows you to hide some views from the accessibility features. For example when some of your table cells are too populated with information, you might want to hide some images or text which would add much verbosity to the spoken content feature. 
https://developer.apple.com/documentation/swiftui/view/accessibilityhidden(_:)

<kbd>
<img width="456" alt="Screenshot 2025-03-07 at 11 43 51 PM" src="https://github.com/user-attachments/assets/cfb884ec-8a2b-443a-b469-d31388269eca" />
</kbd>

### Zoom

<kbd>
<img width="442" alt="Screenshot 2025-03-07 at 11 44 17 PM" src="https://github.com/user-attachments/assets/460894db-152d-4913-9b34-ff8c2b8fc29a" />
</kbd>

## Physical and Motor

<img width="342" alt="Screenshot 2025-03-07 at 11 44 17 PM" src="https://github.com/user-attachments/assets/b159b2b7-c898-4898-8cdc-033640a41536" />


To check your apps and see how they work with VoiceControl, you can checkout this article https://developer.apple.com/documentation/accessibility/voice-control
For providing custom actions for example when there are too many tiny buttons in one table view cell for example, if VoiceOver needs to read the whole screen and goes per every cell and read each action again and again, this can result in a very overwhelming experience.


For this, you can use custom accessibility actions, grouping the container view (supposing all those little buttons are in a stack view for example), mark it as “accessibilityElement(children: .ignore)” and then associate accessible actions. When the user has VoiceOver enabled, they can swipe down and double tap to select the actions, they will be swiping and double tapping in the container area, giving the user a much bigger portion of the screen to iterate through the actions, instead of having to precisely point their fingers to a tiny heart button, for example, to like a content.
https://developer.apple.com/documentation/uikit/uiaccessibilitycustomaction


# Some words on the European Accessibility Act
https://ec.europa.eu/social/main.jsp?catId=1202&intPageId=5581&langId=en

## Micro Enterprises and SMEs
Be aware that each country should have their own local legal translation of the Act. 
And that the act makes some differentiation in regards how it needs to be translated into concrete regulations for microenterprises and SMEs (“‘small and medium-sized enterprises’ or ‘SMEs’ means enterprises which employ fewer than 250 persons and which have an annual turnover not exceeding EUR 50 million, or an annual balance sheet total not exceeding EUR 43 million, but excludes microenterprises;”)

## Content produced before June 28, 2025
To avoid overwork while preparing for adopting the Act, be aware that there are some boundaries drawn by the initial directive defined in 2019 (article 2, point 4, https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32019L0882):

- “This Directive does not apply to the following content of websites and mobile applications:
    a) pre-recorded time-based media published before 28 June 2025;
    b) office file formats published before 28 June 2025;
    c) online maps and mapping services, if essential information is provided in an accessible digital manner for maps intended for navigational use;
    d) third-party content that is neither funded, developed by, or under the control of, the economic operator concerned;
    e) content of websites and mobile applications qualifying as archives, meaning that they only contain content that is not updated or edited after 28 June 2025.“


What all mobile app and websites should comply to is defined by the directive in Annex I, this is a minimum of requirements, and some type of services need to comply to a wider scope.

| **Requirement**                                                  | **Details**                                                                                                     |
|------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Accessibility Compliance**                                     | “All products shall comply with the accessibility requirements set out in Section I of Annex I.”                |
| **Information Provision**                                        | The product must contain information about how to use it, including labelling, instructions, and warnings.       |
| **Sensory Channel Accessibility**                                | Information must be made available through multiple sensory channels, understood by users, and presented in a way that is comprehensible. |
| **Font and Layout Requirements**                                 | Information must be presented in appropriate fonts that are the right size and shape, with adjustable spacing between letters, lines, and paragraphs. |
| **Contrast and Use Scenario Consideration**                      | Information must be presented with enough contrast and consider anticipated use scenarios.                      |

t must also be presented in fonts that are appropriate in size and shape, take into account anticipated use scenarios, use enough contrast, and have adjustable spacing between letters, lines, and paragraphs.

### Requirements on the instructions for use of a product
They should be made available through multiple sensory channels, presented in fonts that are appropriate in size and shape, consider anticipated usage scenarios and use enough contrast, with adjustable letter, line, and paragraph spacing, and be made available in text formats that can be used to create alternate assistive formats. 

Additionally, any non-textual content should be accompanied by an alternate presentation. provide a description of the product's user interface, including handling, control and feedback, input and output; describe the functionality offered by the functions designed to meet the needs of people with disabilities; and describe the hardware and software that interfaces the product with assistive devices.

### User interface and functionality design
| **Requirement**                                                    | **Details**                                                                                                         |
|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **Sensory Channel Usage**                                          | The device must use multiple sensory channels for operation, information, control, orientation, and communication, with alternatives for vision, hearing, voice, and tactile elements. |
| **Visual Adjustability**                                            | The product must allow adjustable brightness, contrast, and magnification for visual elements.                        |
| **Alternative to Colour**                                           | The product must provide alternatives to colour when used to identify components, signal actions, or transmit information. |
| **Alternative to Audio Signals**                                    | The product must provide alternatives to audio signals for identification, indication of actions, and communication.  |
| **Audio Control**                                                   | The device must allow users to adjust the volume, speed, and quality of audio, reducing noise and improving clarity.  |
| **Manual Control Adjustments**                                      | Products requiring manual operation must have tactile, distinguishable parts and allow sequential control with alternatives to fine motor skills. |
| **Seizure Safety**                                                 | The product must not trigger seizures in photosensitive individuals.                                               |
| **Privacy Protection**                                              | Accessibility features must be implemented in a way that protects user privacy.                                     |
| **Alternative Identification Method**                               | The product must provide an identification and control method other than biometrics.                               |
| **Function Consistency and Time for Interaction**                   | The product must ensure consistent functionality and allow enough adjustable time for user interaction.             |


### Support services
Support services, such as help desks, contact centres, technical support, relay services, and training services, should, where available, offer information in accessible communication modes regarding the product's accessibility and compatibility with assistive technologies.


#### References
- https://ec.europa.eu/social/main.jsp?catId=1202&intPageId=5581&langId=en
- https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32019L0882


