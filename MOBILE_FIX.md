# Mobile registration dialog fix — 2026-10-01

The mobile CSS set top/left to zero and reset `transform`, but Tailwind's independent `translate: -50% -50%` remained active. At 390 × 844 the editor's observed rectangle was (-195, -422, 390, 844), matching the reported clipping.

`mobile-dialog.css` explicitly resets both `translate` and `transform` in the existing mobile breakpoint. The editor fills the viewport with a vh fallback and dynamic viewport sizing. The heading and save/cancel footer stay visible; the middle form area scrolls independently. Desktop layout, camera integration, storage keys and record formats are unchanged.

Build: `python3 build-camera.py index.html`.

Verification: reproduced the original clipping in Chrome at 390 × 844. Inspected corrected layouts at 320 × 568, 375 × 667, and 390 × 844. Used the actual form to enter name/location/memo, choose a room, save at 320px, reopen, edit, scroll to the lower fields, and save again at 375px. Verified camera dialog opening and return to the populated editor (local HTTP preview uses the documented native-camera fallback). These are browser viewport checks, not physical iPhone/Safari or Android hardware tests.
