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
    street: Fürstenallee 11
    city: Paderborn
    region: Detmold
    postcode: '33102'
    country: Deutschland
    country_code: DE
  coordinates:
    latitude: '51.73179'
    longitude: '8.73465'
  directions: Room FU.201.1
  office_hours:
    - '09:30 to 17:30'
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
