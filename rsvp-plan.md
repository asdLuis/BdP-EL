# Plan · RSVP / Confirmación de asistencia

**Intent:** Decide where a guest's confirmation actually *goes*, who receives it, and how the couple can see the list of reservations — then wire it into `boda-de-plata.html`.

**Status:** DECIDED — the form now routes to WhatsApp (Option A/D hybrid, zero backend). Implemented in `boda-de-plata.html`.

---

## 0. Decision taken

The couple chose to send confirmations to **WhatsApp**. Implemented as a **deep link**: on submit, the page builds a message from the form fields and opens `https://wa.me/524421175673?text=…`; the guest taps send. This needs **no server and no API keys** — the trade-off is that confirmations arrive only when the guest presses send, and there is no built-in tally (count manually in the chat). If a *list you can look at* is ever needed, revisit Option B (Google Sheet).

---

## 1. How it works now

The site is a single static HTML file. There is no server behind it.

What the "Confirmar asistencia" form does when tapped:

| Step | What happens |
|---|---|
| Guest fills Nombre / Asistentes / Contacto / Nota | Values sit in the browser only |
| Guest taps **Confirmar asistencia** | A script checks the name is not empty, then opens WhatsApp to **+52 442 1175673** with a message built from the fields (nombre, asistentes, contacto, nota), and shows the "Gracias · Abrimos WhatsApp…" panel |
| Data is sent anywhere? | Only when the guest presses send in WhatsApp. No email, no spreadsheet |
| Guest taps **Escribir por WhatsApp** | Opens the same chat with a generic prefilled message |
| Guest taps the phone number | Opens the phone dialer to **+52 442 1175673** |

> The couple receives confirmations as WhatsApp messages. There is no tally — count manually from the chat. For a spreadsheet, switch to Option B.

---

## 2. Where the confirmation can go — the options

| # | Option | Who receives it | Where you *see* it | Setup cost | Guest effort | Keeps the on-page form? |
|---|---|---|---|---|---|---|
| A | **WhatsApp / phone only** (hide the form) | The phone that owns 442 1175673 | WhatsApp chat / call log | None (free) | Taps button, writes & sends | No — form removed |
| B | **Google Form + Google Sheet** (embed or link) ⭐ | The Google account that owns the form | A live Google Sheet (name, party size, notes) | ~20 min, free | Fills a second form | Replaced by Google’s form |
| C | **Form service** (Formspree / Getform / Basin / Netlify Forms) | The email address you set | Inbox email + service dashboard | ~20 min, free tier | None — uses the existing form | **Yes** — nicest result |
| D | **Form → your WhatsApp** (CallMeBot / Twilio) | The phone that pays for the bot | WhatsApp chat | Medium; fragile, rate-limited | None | Yes |
| E | **Hosted RSVP tool** (Zola, Withjoy, Paperless Post…) | Their platform | Their dashboard + guest list | ~30 min | Leaves your site | No |

---

## 3. Recommendation

**Option B (Google Form → Google Sheet), with Option A’s WhatsApp button kept as a fallback.**

Why:

- The couple’s real need is *“a list I can look at and count”* — a Sheet gives exactly that, for free, with zero server and zero code to maintain.
- It works from a static page: the Google Form can be embedded directly inside the existing RSVP section, so the design stays intact around it.
- The WhatsApp button stays underneath for anyone who prefers it, so no one is blocked.

**If the couple wants the polished, on-brand form (not a Google Form iframe) to email them**, choose **Option C (Formspree)**. Free tier easily covers a wedding; the existing `#rsvp-form` is wired with a one-line `fetch()` to your endpoint, and every confirmation lands in the inbox + Formspree dashboard. Trade-off: the "list" is an inbox/dashboard rather than a spreadsheet.

**Option A alone** is fine only if the couple is happy counting manually from WhatsApp. Simplest, but no tally and confirmations depend on guests actually pressing send.

---

## 4. Decision needed from the couple

1. **Channel** — Google Sheet (B), email via form service (C), or WhatsApp-only (A)?
2. **Destination owner** — whose Google account / email / phone? (the couple’s, or a trusted organizer’s). This decides who can see the reservations.
3. **Keep the on-page form?** — yes (B/C/D) or remove it and rely on WhatsApp (A).
4. **Confirm the WhatsApp number** — is **442 1175673 → +52 442 1175673** the right number and does it have WhatsApp enabled? (already used for the tap-to-call and WhatsApp links)

---

## 5. Wiring steps (after the decision)

- **Option B — Google Form + Sheet**
  1. Build a Google Form with the same four fields (Nombre, Número de asistentes, Teléfono/correo, Nota).
  2. Link it to a Google Sheet; confirm responses appear there.
  3. Replace the `#rsvp-form` block with the Google Form iframe (or a styled "Abrir formulario" button on mobile).
  4. Keep the WhatsApp button and phone link below it.
- **Option C — Formspree (or similar)**
  1. Create the form endpoint; copy the URL.
  2. Add `action="https://formspree.io/f/XXXX" method="POST"` to `#rsvp-form` (or a `fetch()` so the current "Gracias" panel still appears).
  3. Email notifications go to the destination inbox; the dashboard shows all submissions.
- **Option A — WhatsApp only**
  1. Remove the `#rsvp-form` and the "success" panel.
  2. Enlarge the WhatsApp button to primary and keep the phone link.

---

## 6. Open questions / risks

- **Spam** — a public form can attract bots; Google Forms and Formspree both have light spam handling. Not a concern at wedding scale.
- **Privacy** — guest phone numbers/emails will live in whoever’s Google account or inbox owns the destination. Choose the owner deliberately.
- **Deadline** — the page says confirm **before 20 Nov 2026**; the destination just needs to be checked after that date.
- **Number** — verify the WhatsApp number is correct and active before launch.
- **Photos (separate)** — the Google Drive album link is a later step; not part of this RSVP plan.

---

## 7. Next step

Reply with:
- the **channel** (B Google Sheet / C email service / A WhatsApp-only), and
- the **destination** (whose Google account / email / phone),

then hand this plan back to Design mode and I’ll wire `boda-de-plata.html` accordingly — keeping the existing black-and-white design system and the WhatsApp fallback.
