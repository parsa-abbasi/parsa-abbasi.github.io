---
# An instance of the Contact widget.
widget: contact

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 130

title: Contact
subtitle:

content:
  # Automatically link email and phone or display as text?
  autolink: true

  # Email form provider
  form:
    provider: netlify
    formspree:
      id:
    netlify:
      # Enable CAPTCHA challenge to reduce spam?
      captcha: false

  # Contact details (edit or remove options as required)
  email: parsa.abbasi1996@gmail.com
  address:
    city: Rasht
    region: Guilan
    country: Iran
    country_code: IR
  contact_links:
    - icon: twitter
      icon_pack: fab
      name: DM Me
      link: 'https://twitter.com/ParsaAbbasi1996'
    - icon: discord
      icon_pack: fab
      name: We can have a talk on Discord
      link: https://discordapp.com/users/705420786529337395

design:
  columns: '2'
---
