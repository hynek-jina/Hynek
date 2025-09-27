# Proposal for Improving Wallet of Satoshi

Wallet of Satoshi is one of the most popular lightning wallets thanks to its simplicity and ease of use. However, even the smallest UX or UI issues can quickly become friction points for users who interact with the app multiple times a day. By addressing these details, Wallet of Satoshi can further strengthen its position as the go-to lightning wallet for newcomers.

The following proposed improvements focus on three key areas: **UI consistency, user experience optimization, and contact management.** Each change aims to reduce friction, eliminate unnecessary steps, and make the app more intuitive while preserving its core simplicity.

## Proposed Improvements

### UI

- Standardize screen layouts – keep the back button consistently in the same position.
- Standardize how balance and fiat values are displayed.
- Allow users to hide fiat display.
- Let users set their preferred default input (fiat or bitcoin).
- Remove full bitcoin display option – sats-only is sufficient.
- Toggle between `sats` / `₿` / `no unit` display.

### UX

- Remove unnecessary decimal input (This adds 2 extra clicks per payment - for example with CZK).
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

