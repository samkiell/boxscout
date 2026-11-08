# Flow checklists

Adapt these. Remove steps that do not apply, add steps the app needs.

## Smoke test (default)
1. Load the homepage. Page renders, no error banner, main image or hero visible.
2. Click each top navigation item. Each page loads and the URL changes.
3. Click the primary call to action. It leads somewhere that makes sense.
4. Scroll to the footer. Footer links resolve.
5. Resize to a narrow mobile width. Nothing overflows, menu is usable.

## Signup and login
1. Open the signup page. Form fields are labeled.
2. Submit empty. Clear validation messages appear.
3. Submit with an invalid email. Rejected with a clear message.
4. Submit with a valid test account. Success state or next step appears.
5. Log out, log back in with the same account. Lands in the right place.
6. Try a wrong password. Error is shown, no crash.

## Ticketing or checkout (stop before real payment)
1. Browse to an event or product. Details, price, and date are shown.
2. Select a quantity or ticket type. Total updates correctly.
3. Change quantity, then remove. Total recalculates.
4. Proceed to checkout. Order summary matches the selection.
5. Fill required details. Validation works on bad input.
6. Reach the payment step. Confirm the provider loads in test mode. STOP here unless the user confirmed test mode.
7. Go back and confirm the cart is preserved.

## Hackathon demo check
1. Open the live demo link from a clean session, as a judge would.
2. Follow the main user story from the README or submission text.
3. Check empty states: what does a first time user see with no data?
4. Check the worst case: a bad input, a slow response, a missing permission.
5. Confirm the repo link, video link, and any form links in the submission work.
