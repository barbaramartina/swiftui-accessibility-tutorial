# Accessibility development strategy
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


