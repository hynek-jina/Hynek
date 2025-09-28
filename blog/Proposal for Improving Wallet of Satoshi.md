# Proposal for Improving Wallet of Satoshi

Wallet of Satoshi is one of the most popular lightning wallets thanks to its simplicity and ease of use. However, even the smallest UX or UI issues can quickly become friction points for users who interact with the app multiple times a day. By addressing these details, Wallet of Satoshi can further strengthen its position as the go-to lightning wallet for newcomers.

The following proposed improvements focus on three key areas: **UI consistency, user experience optimization, and contact management.** Each change aims to reduce friction, eliminate unnecessary steps, and make the app more intuitive while preserving its core simplicity.

## Proposed Improvements

### UI

- Standardize screen layouts
  - There are different type of buttons (ie in the amount entry screen) - filled/transparent, yellow/gray, different sizes. Sometimes an icon is included, sometimes not
  - The tab navigation works differently in receive than in the POS view
  – Back button is not consistently in the same position - scan has it in right bottom, otherwise it's in the top
- Standardize how balance and fiat values are displayed.
  - The POS view also looks unnecessarily different from the receive view 
- Allow users to hide fiat display.
- ~Let users set their preferred default input (fiat or bitcoin).~ _It already preselects the last used, which is even better_
- Remove full bitcoin display option – sats-only is sufficient.
- Toggle between `sats` / `₿` / `no unit` display.
  - The `no unit` display can be useful when is the unit obvious from context. Removing the unit label entirely avoids confusion or debates about notation. It’s already clear that values are in sats.

### UX

- Remove unnecessary decimal input in POS (This adds 2 extra clicks per payment - for example with CZK).
- When tapping *Receive*, go directly to amount entry. 
- In Menu, make backup the most important and visible option.

### Contacts

- Display contacts on the home screen.
- When adding a contact, automatically append `@walletofsatoshi.com` unless specified otherwise.
- Add validation to ensure the contact actually exists (prevents typos and errors).
- Add the user’s own profile to contacts – this could also allow quick receive via LNURL.
- After completing a payment, offer the option to save the recipient as a contact.
- Enable “favorite contacts” for quick access.
- Move “delete contact” option inside the edit contact screen (to prevent accidental removal).

<img width="2908" height="1900" alt="WoS proposal" src="https://github.com/user-attachments/assets/c5c4f6f2-8532-4f3a-be29-82d62e9fe775" />

