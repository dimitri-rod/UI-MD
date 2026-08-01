// A landing page in UI-MD. Precise where the value matters, plain words where it doesn't —
// mixed freely, often in the same rule. Both compile the same.

**Dark mode.**
**$Color,Background$ #0A0A0F, $Color,Surface$ #14141C, $Color,Text$ #E8E6F0**
**$Color,Accent 1$ #7C3AED, $Color,Accent 2$ #22D3EE**
**$Font,Heading$ "Playfair Display" serif, $Font,Body$ "Inter" sans-serif**

> Navbar
*sticky top, space-between, padding: 20px 5%, background: $Color,Background$*
>> UI-MD
*confident, like it knows what it's doing*
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*ghost, 14px*
>> [[Get Started]](signup)
*background: $Color,Accent 1$, padding: 8px 20px, border-radius: 8px*

> Hero
*deep breath energy — calm, centered, room to exist. max-width: 800px, padding: 120px 5%*
>> # Design at the speed of thought.
*font-size: 80px, background: linear-gradient(90deg, $Color,Accent 1$, $Color,Accent 2$), background-clip: text*
>> ### A markdown-native language for AI-driven interfaces. Stop writing boilerplate.
*soft, like a whisper right after the shout. opacity: 70%, margin-top: 16px*
>> [[Start Free Trial]](signup)
*background: $Color,Accent 2$, padding: 14px 28px, border-radius: 8px, on hover: glow*
>> ![Preview of a screen built in UI-MD](preview.png)
*floaty, like it's hovering just above the page. border-radius: 16px*

> Pricing Section
*align-center, flex-col, padding: 100px 5%, gap: 32px*
>> ## Simple, transparent pricing.
*font-size: 40px, font-weight: 700, text-align: center*
>> [x] Monthly
>> [ ] Annual, save 20%
*single-select, cute little switch, satisfying to toggle*
// switching to Annual updates all three card prices with the discount

>> Developer Card
*background: $Color,Surface$, border-radius: 16px, padding: 40px*
>>> ### Developer
>>> Free forever, for one project.
*opacity: 70%, margin: 12px 0*
>>> [[Get Started]](signup)
*width: 100%, chill — no pressure, just here if you need it*

>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, border-radius: 16px, padding: 40px*
>>> ### Pro
>>> $29/month, unlimited projects.
*opacity: 70%, margin: 12px 0*
>>> [[Get Started]](signup)
*width: 100%, background: $Color,Accent 1$, loud and proud — this is the one*

>> Enterprise Card
*background: $Color,Surface$, border-radius: 16px, padding: 40px, on hover: border 1px solid $Color,Accent 1$, lift 4px*
>>> ### Enterprise
>>> Custom pricing, talk to sales.
*opacity: 70%, margin: 12px 0*
>>> [[Contact Sales]](contact)
*width: 100%, outline, understated — almost whispering*

> FAQ Section
*calm, centered, breathing room. padding: 80px 5%*
>> ## Frequently asked questions.
*font-size: 32px, font-weight: 700, text-align: center*
>> <> Search questions...
*width: 400px, simple and inviting, not demanding*
>> <All>
>> <Billing>
>> <Setup>
>> <API>
*clickable, toggles active, little pills, the picked one lights up with $Color,Accent 1$*
>> Can I switch between monthly and annual billing?
*accordion, one open at a time, border-bottom: 1px solid $Color,Surface$*
// six or so, spanning billing, setup and API

> Footer
*space-between, padding: 60px 5%, border-top: 1px solid $Color,Surface$, fading out gently*
>> Acme Corp © 2026. All rights reserved.
*opacity: 50%, font-size: 14px*
>> :twitter: :github: :discord:
*gap: 16px, color: $Color,Accent 1$, tucked away, not asking for attention*
