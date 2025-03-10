# Quick testing while developing
## Accessibility Inspector

<kbd>
<img width="338" alt="Screenshot 2025-03-08 at 12 41 29 PM" src="https://github.com/user-attachments/assets/e87bd830-b1d8-475f-ad20-0d84e59a059b" />
</kbd>

Support yourself with the accessibility inspector. In my experience it is unreliable. If you see that it stops working,
try closing it completely and launching it again. When it works, it does help a lot to inspect elements and play around with some settings in the simulator.

You can also use the Accessibility Inspector to run audits and get warnings about some of the most ground features.

<kbd>
<img width="258" alt="Screenshot 2025-03-07 at 11 38 41 PM" src="https://github.com/user-attachments/assets/77c9b00f-f20e-4d46-874d-f8413434923f" />
<img width="257" alt="Screenshot 2025-03-07 at 11 38 47 PM" src="https://github.com/user-attachments/assets/4d5b1c91-f50f-4cd7-b74b-8b5c016d5a13" />
</kbd>

## Previews
Previous are a great way to quickly have feedback, ideally you should rely on the system defined font types,
I recommend against adjusting the font sizes unless you have a custom font, otherwise you will lose all the  benefits from the development environment,
such as previews and modifiers overview. Using a system font with a different sizing will cause you issues, 
since there is not way to make the previews and Apple UIs-modifier work, so it will slow you down while developing, just because your font is 1 pixel bigger or smaller. It’s not a good practice. 

<kbd>
<img width="340" alt="Screenshot 2025-03-07 at 10 45 24 PM" src="https://github.com/user-attachments/assets/fc3f226d-65d4-4798-83c9-d31d77a04b21" />
<img width="461" alt="Screenshot 2025-03-07 at 10 45 46 PM" src="https://github.com/user-attachments/assets/2a00c2a5-fd28-482e-b55c-f6b50241768f" />
<img width="560" alt="Screenshot 2025-03-08 at 12 32 16 PM" src="https://github.com/user-attachments/assets/68c64ca9-a50e-4521-9992-f2ed17fe74d1" />
</kbd>

# Auditing your apps and testing
Apple has great documentation and step by step testing instructions for each of the accessibility groups. 
I recommend you to check them out: [Testing Accessibility](https://developer.apple.com/documentation/accessibility/performing-accessibility-testing-for-your-app)

## Automatic auditing
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

## Ignoring legacy UI
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
