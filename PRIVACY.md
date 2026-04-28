# Privacy Policy — Social Friends

**Last updated: April 28, 2026**
**Effective date: April 28, 2026**

---

## Who we are

Social Friends is a personal-relationship manager ("friendship CRM")
that helps you stay intentional about the people in your life. This
policy explains what data the app collects, why, who we share it with,
how long we keep it, and what choices you have.

- **App name:** Social Friends
- **Publisher:** Skand Shekatkar (sole developer)
- **Contact for privacy questions:** designskand@gmail.com

If you have questions about this policy or want to exercise any of the
rights described below, email designskand@gmail.com and we will
respond within 30 days.

---

## The short version

- We store the bare minimum needed to make the app work: your account,
  your friends, the hangs you log, your notes, and your preferences.
- Your friends list and notes are **private to you**. No other user
  of Social Friends can see them.
- Your device contacts are read only when you ask to add a friend.
  The full contact list is **never uploaded** — only the friends you
  pick are saved to your account. When you open the contact picker, we
  send the contact phone numbers to our server in-memory to find which
  of them already use Kindrd; we do not store those phone numbers.
- Your calendar (Google or Apple) is read **on-device only**. Calendar
  data never leaves your phone.
- You control whether other Kindrd users can find you via your phone
  number. You can turn this off any time in Settings → Privacy.
- We do not sell your data. We do not share it for advertising.
- You can delete your account and all your data at any time from
  Settings → Account → Delete my account.
- The app is not intended for anyone under **18 years old**.

---

## What we collect and why

### 1. Account data — required to run the app

| Data                                                | Source                       | Why we need it                                  | Legal basis (GDPR)           |
|-----------------------------------------------------|------------------------------|-------------------------------------------------|------------------------------|
| Name, optional profile photo, optional birth year   | You, during onboarding       | Display in the app, age gate (18+)              | Contract (Art. 6(1)(b))      |
| Google user ID (if you sign in via Google)          | Google                       | Authentication                                  | Contract                     |
| Apple user ID (if you sign in via Apple)            | Apple                        | Authentication                                  | Contract                     |
| Phone number (your own)                             | You, during onboarding/auth  | Lets friends who have your number find you on Kindrd; stored on your `profiles` row | Contract |
| `discoverable` flag (default ON)                    | You                          | If OFF, your profile is excluded from any other user's contact-match query  | Consent (Art. 6(1)(a))      |

We store account data in our backend (Supabase — see "Third parties"
below). It is protected by Row-Level Security so only your own
authenticated session can read or modify it.

### 2. Your friends list — data about people who may not use the app

This is the category most apps don't have to talk about, and it is the
most important one for us to be transparent about.

When you add a friend, we store:

- Their name (as you type it or as it appears in your device contacts)
- Their phone number (if you choose to add one)
- A contact ID that lets us look up their device-contact photo locally
- **Their birthday, if it was set in your device contacts.** On iOS we read
  the birthday field from your contacts via Apple's `CNContactBirthdayKey`
  (no separate permission — covered by the Contacts permission you
  already granted). The same birthday is also auto-filled from your
  Kindrd friend's profile if they have set their own birthday and you are
  accepted-friends with them.
- Any notes, tags, life events, or hang history you attach to them
- A reminder frequency and any other preferences you set for them

We store this data on our servers so the app can work across devices
and restore your data if you lose your phone. **No other Social Friends
user can see the friends on your list** — it is protected by
Row-Level Security in the database.

**Important: legal basis for non-user data.** We rely on **legitimate
interest (GDPR Art. 6(1)(f))** as our basis for storing data about
people who have not themselves consented to Social Friends. We have
weighed the risks and believe the interest is proportionate, because:

- The data is pre-existing in your device contacts, which you have
  access to under your own relationship with the person.
- The data is never shared with any other Social Friends user.
- The data is never used for advertising or profiling.
- The data is never sold or otherwise disclosed to third parties.
- You can delete any friend at any time, and we will hard-delete all
  their data immediately.
- Any friend can email designskand@gmail.com and ask to have
  their data removed, and we will comply within 30 days.

If you are not comfortable storing information about a particular
person, don't add them to the app.

### 2a. Contact discovery (phone-number matching)

When you open the contact picker, the app sends the phone numbers from
your device contacts to our server-side function
(`find_kindrd_users_by_phones`). The server checks which of those numbers
belong to existing Kindrd accounts and returns only the matching profiles
(name and avatar) so you can add them as friends.

- Contact phone numbers are used **in-memory** for the matching call and
  are **not stored** anywhere on our servers.
- Only profiles that have `discoverable = true` are returned. You can
  turn `discoverable` off at any time in **Settings → Privacy**, in
  which case your profile is **never** returned in any other user's
  contact-match query.
- Default for `discoverable` is ON for new accounts.

### 3. Your hangs and notes

When you log a hang or plan one, we store:

- The friend (or friends) it was with
- The date and optional time
- Optional activity tag, energy rating, mood, and free-text note

When you add a note to a friend, we store the note text and any
follow-up date you set. Notes can be up to 5 000 characters.

### 3a. "Free to hang" slots

When you broadcast that you are free to hang, we store the slot in the
`free_slots` table (start time, end time, optional location and note,
audience scope) and any responses your friends make in `slot_responses`
('in', 'maybe', 'pass').

- Free slots are visible **only to friends in the audience you chose**,
  enforced via Row-Level Security.
- When a slot's `end_at` has passed (or you cancel it), it becomes
  invisible in the app. The row is retained but is not shown to anyone.
- You can hard-delete slots or responses at any time, or wipe everything
  when you delete your account.

### 3c. Polls

When you create a poll, we store the poll question, options, and
audience (a list of friend IDs) in the `polls` table, and votes in the
`poll_votes` table.

- Polls and votes are visible only to the creator and the audience
  friend IDs, enforced via Row-Level Security.
- Polls are not processed by any third party.

### 3d. Places (the Places tab)

When you add a place to "want to visit" or "visited", we store:

- A reference to the place: name, address, latitude/longitude, and a
  Google Place ID (when the place was found via Google Places). These
  rows live in the `places` table — a shared catalogue, so multiple
  users referencing the same restaurant deduplicate to the same row.
- Your association with that place — whether you want to visit or have
  visited, optional rating ("loved" / "liked" / "fine"), optional notes
  about the place, optional link to a hang you logged there. Stored in
  `place_associations`.
- Optional "open to going with company" interest with an optional time
  window — stored in `place_interests`. Visible only to the friends in
  your chosen audience tier (RLS-enforced).
- Pairwise comparisons you record in the ranking flow ("which was
  better — Cafe A or Cafe B?") in `place_pair_comparisons`. These
  derive a calibrated rating score that is stored on your association
  rows.

Friends connected to you on Kindrd can see your visited and want-to-visit
places (Row-Level Security ties this to a confirmed friendship). They
cannot see your private notes — only the place reference + status.

When you search for a place, we send the search text and (if you have
granted location) your approximate coordinates to **Google Places API**
to fetch matching venues. We do not store the search query itself. When
you tap a venue, we fetch its details (address, photo reference, types)
and store the result in our `places` table.

When you open the Map sub-view, the **Google Maps SDK** loads map tiles
from Google's servers. Google may receive your IP address and the
coordinates of the area you are viewing. Map tile rendering is
client-side; we do not log or store your map interactions.

You can clear your places by deleting your account (which deletes all
associations and interests) or by individually removing them from the
Places tab.

### 4. Photos you upload

If you upload a profile photo or a photo of a hang, we store it in
encrypted-at-rest storage (Supabase Storage). Only your authenticated
account can access these photos.

### 4a. Operational data we keep about your app activity

To prevent abuse and enforce rate limits on certain APIs, we keep a small
operational log:

- `rpc_call_log` — records the timestamps and names of certain rate-limited
  API calls you make (e.g. contact-discovery lookups). Used for abuse
  prevention and rate-limit enforcement. Retained for 30 days; pruned
  automatically by a daily cleanup job.

### 5. Device permissions

The app asks for the following OS permissions. Each is explained in the
permission prompt at the moment it is requested.

| Permission   | When we ask                                     | What we do with it                                       |
|--------------|--------------------------------------------------|-----------------------------------------------------------|
| Contacts     | When you tap "Add from contacts"                 | Read your contact list to show a picker; only the friends you select are saved. |
| Calendar (Google) | When you enable hang auto-detection         | Read recent events on-device to suggest hangs to log. **Never uploaded.** |
| Calendar (Apple, iOS only) | When you enable Apple Calendar import on iOS | Read events from your local and iCloud calendars via Apple's EventKit framework, on-device only, to suggest hangs to log. **Never uploaded.** |
| Notifications| When you enable reminders                        | Send gentle reminders to check in with friends.           |
| Photos       | When you add a profile or hang photo             | Let you pick a photo from your library.                   |
| Camera       | When you take a new photo in the app             | Let you snap a photo to attach to your profile or a hang. |

### 6. Analytics (opt-in)

We use **PostHog** (an analytics product) to understand how people use
Social Friends so we can make it better. Analytics is **off by default**
and only turns on if you choose to opt in during onboarding
or in Settings → Privacy.

When analytics is on, we collect:

- Anonymous usage events (screen views, button taps)
- Device type, OS version, app version, language
- A random, app-local ID (not linked to your email or name)

We do **not** collect:

- Your name, friend list, or any hang content
- Your precise location
- Your device advertising ID

You can turn analytics off at any time in Settings → Privacy → "Share
anonymous usage data". Turning it off stops all future collection.

### 7. Wrapped (monthly and yearly summaries)

Server-side scheduled jobs (Supabase `pg_cron`) run on your existing
data to compute monthly and yearly Wrapped summaries (e.g. top friends,
hang counts, streaks). The Wrapped data itself stays in our existing
tables — **no new categories of data are collected** to produce it.

When configured, we send a push notification via Apple Push Notification
service (APNs) to let you know your Wrapped is ready. The notification
payload contains only a short message and the Wrapped period, never
your friends or hang content.

We queue your monthly Wrapped in a `wrapped_pushes` table on the 1st of
each month — a small row containing your user ID, the Wrapped period,
and a "ready" timestamp. The row is deleted when you open the Wrapped
or 30 days later, whichever comes first.

### 8. Home screen widgets

If you enable a home screen widget, the widget displays a snapshot of
your next suggested friend on your device. This snapshot is stored
locally on your device only and is not uploaded anywhere.

---

## Third parties we share data with

We only share data with providers who help us run the app, under
written data-processing agreements.

| Provider          | What they process                                     | Where                      | Purpose                                      |
|-------------------|-------------------------------------------------------|----------------------------|----------------------------------------------|
| **Supabase**      | Account, friends, hangs, notes, photos, preferences   | Northeast Asia (Tokyo)     | Database + auth + storage                    |
| **Google (OAuth)**| Google user ID if you sign in with Google             | Global                     | Authentication                               |
| **Apple (OAuth)** | Apple user ID if you sign in with Apple               | Global                     | Authentication                               |
| **PostHog**       | Anonymous usage events (only if you opt in)           | United States              | Product analytics                            |
| **Sentry**        | Crash + error reports (stack traces, OS/device, app version — never your friends, notes, or messages) | United States | Diagnose bugs and crashes |
| **Apple / Google**| Push notification tokens                              | Global                     | Delivering reminder notifications            |
| **Google Maps + Places API** | Search queries you type into the place finder, your IP address (when the SDK loads tiles), and the place IDs you tap on | Global | Render map tiles, find venues by name, fetch place details |

We do **not** share data with:

- Advertising networks
- Data brokers
- Social networks (beyond the sign-in providers above)

Google Calendar and Apple Calendar (EventKit) data is **never** sent
to any of these providers. It stays on your device.

---

## Where your data is stored

Your data is stored on servers located in **Northeast Asia (Tokyo)**,
operated by Supabase. If you are located in the European Economic Area,
the UK, or Switzerland, transfers outside your region are covered by
Standard Contractual Clauses (SCCs) as published by the European
Commission.

---

## How long we keep your data

- **Account data, friends, hangs, notes, photos:** kept until you
  delete them, or until you delete your account.
- **Anonymous analytics events:** retained by PostHog for up to
  12 months.
- **Backups:** database backups are kept for up to 30 days for
  disaster recovery.

When you delete your account, we hard-delete all your data from our
live database immediately. Backup copies containing your data age out
within 30 days.

---

## Your rights

Depending on where you live, you have some or all of the following
rights over your personal data:

- **Access** — ask for a copy of what we hold about you.
- **Rectification** — ask us to correct inaccurate data.
- **Erasure ("right to be forgotten")** — ask us to delete your data.
- **Portability** — ask for an export of your data in a machine-readable format.
- **Object / restrict processing** — ask us to stop processing data
  for a specific purpose.
- **Withdraw consent** — wherever we relied on consent (e.g. analytics
  or being discoverable by phone number), you can withdraw it at any
  time. Turn off **Settings → Privacy → Discoverable** to stop being
  matched in other users' contact lookups.
- **Lodge a complaint** — with your local data protection authority.
  EU users can find theirs at
  <https://edpb.europa.eu/about-edpb/about-edpb/members_en>.

To exercise any of these rights, email designskand@gmail.com. You can
also delete your account and all associated data directly from
Settings → Account → Delete my account.

### California residents (CCPA/CPRA)

You have the right to know what personal information we collect, to
delete it, to correct it, and to opt out of any "sale" or "sharing"
of personal information. **We do not sell or share personal
information** as those terms are defined in the CCPA/CPRA. To
exercise your rights, email designskand@gmail.com.

### Users in India (DPDP Act, 2023)

You have rights of access, correction, erasure, and grievance
redressal. Our Grievance Officer is Skand Shekatkar, reachable at
designskand@gmail.com, and responds within 30 days.

---

## Children

Social Friends is **not intended for anyone under 18 years old**.
During onboarding we ask for your birth year and block accounts below
that age. We store only the year, not the full date of birth.

We do not knowingly collect personal information from anyone under 18.
If you believe a child under 18 has created an account, email
designskand@gmail.com and we will delete the account promptly.

---

## Security

- All network traffic between the app and our servers is encrypted
  via TLS 1.2+.
- All database tables enforce Row-Level Security so your data is
  only accessible from your own authenticated session.
- Storage buckets (photos) are private and access-controlled.
- We run static analysis on every change.

No system is 100 % secure. If you discover a vulnerability, please
email designskand@gmail.com.

---

## Changes to this policy

We may update this policy from time to time. When we do, we will
update the "Last updated" date at the top and, for material changes,
notify you inside the app before the changes take effect.

---

## Contact

- **Privacy questions:** designskand@gmail.com
- **Security reports:** designskand@gmail.com
- **Support:** designskand@gmail.com
