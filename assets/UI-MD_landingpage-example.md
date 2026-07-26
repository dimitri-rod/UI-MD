# landingpage_example.md

**Dark mode. Background: $Color,Background$. Surface: $Color,Surface$. Text: $Color,Text$. Accent 1: $Color,Accent 1$. Accent 2: $Color,Accent 2$. Heading font: $Font,Heading$. Body font: $Font,Body$.**

> Navbar
*align-center, justify-space-between, padding: 20px 5%, position: sticky-top, background: $Color,Background$*
>> UI-MD
*font-weight: 700, font-size: 20px*
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*variant: ghost, font-size: 14px*
>> [Get Started](signup)
*background: $Color,Accent 1$, padding: 8px 20px, border-radius: 8px*

> Hero
*align-center, justify-center, text-align: center, padding: 120px 5%, max-width: 800px, margin: 0 auto*
>> # Design at the speed of thought.
*font-size: 80px, background: linear-gradient(90deg, $Color,Accent 1$, $Color,Accent 2$), background-clip: text*
>> ### A markdown-native language for AI-driven interfaces. Stop writing boilerplate.
*font-size: 20px, opacity: 70%, margin-top: 16px*
>> [Start Free Trial](signup)
*background: $Color,Accent 2$, padding: 14px 28px, border-radius: 8px, on-hover: box-shadow 0 0 24px $Color,Accent 2$*
>> ![Preview of a screen built in UI-MD](preview.png)
*border-radius: 16px, box-shadow: 0 20px 40px rgba(0,0,0,0.4)*

> Pricing Section
*align-center, flex-col, padding: 100px 5%*
>> ## Simple, transparent pricing.
*font-size: 40px, font-weight: 700, text-align: center*
>> [x] Monthly
>> [ ] Annual, save 20%
*single-select, border-radius: 999px, padding: 8px*
// switching to Annual should update all three card prices to reflect the 20% discount

>> Developer Card
*background: $Color,Surface$, border-radius: 16px, padding: 40px*
>>> ### Developer
*font-size: 24px*
>>> Free forever, for one project.
*opacity: 70%, margin: 12px 0*
>>> [Get Started](signup)
*width: 100%*

>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, border-radius: 16px, padding: 40px, transform: scale(1.05)*
>>> ### Pro
*font-size: 24px*
>>> $29/month, unlimited projects.
*opacity: 70%, margin: 12px 0*
>>> [Get Started](signup)
*width: 100%, background: $Color,Accent 1$, border-radius: 8px*

>> Enterprise Card
*background: $Color,Surface$, border-radius: 16px, padding: 40px, opacity: 90%*
>>> ### Enterprise
*font-size: 24px*
>>> Custom pricing, talk to sales.
*opacity: 70%, margin: 12px 0*
>>> [Contact Sales](contact)
*width: 100%, variant: outline, border: 1px solid $Color,Accent 1$*

> FAQ Section
*align-center, flex-col, padding: 80px 5%*
>> ## Frequently asked questions.
*font-size: 32px, font-weight: 700, text-align: center*
>> <> Search questions...
*width: 400px, margin: 24px 0, padding: 12px 16px, border-radius: 8px, background: $Color,Surface$*
>> <All>
>> <Billing>
>> <Setup>
>> <API>
*pill-shaped, gap: 12px, active one gets background $Color,Accent 1$*

> Footer
*align-center, justify-space-between, padding: 60px 5%, border-top: 1px solid $Color,Surface$*
>> Acme Corp © 2026. All rights reserved.
*opacity: 50%, font-size: 14px*
>> :twitter: :github: :discord:
*gap: 16px, color: $Color,Accent 1$*
