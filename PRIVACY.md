# Privacy Policy — Social Friends

**Last updated: 2026-04-11**
**Effective date: 2026-04-11**

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
  pick are saved to your account.
- Your calendar is read **on-device only**. Calendar data never leaves
  your phone.
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

### 3. Your hangs and notes

When you log a hang or plan one, we store:

- The friend (or friends) it was with
- The date and optional time
- Optional activity tag, energy rating, mood, and free-text note

When you add a note to a friend, we store the note text and any
follow-up date you set. Notes can be up to 5 000 characters.

### 4. Photos you upload

If you upload a profile photo or a photo of a hang, we store it in
encrypted-at-rest storage (Supabase Storage). Only your authenticated
account can access these photos.

### 5. Device permissions

The app asks for the following OS permissions. Each is explained in the
permission prompt at the moment it is requested.

| Permission   | When we ask                                     | What we do with it                                       |
|--------------|--------------------------------------------------|-----------------------------------------------------------|
| Contacts     | When you tap "Add from contacts"                 | Read your contact list to show a picker; only the friends you select are saved. |
| Calendar     | When you enable hang auto-detection              | Read recent events on-device to suggest hangs to log. **Never uploaded.** |
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

### 7. Home screen widgets

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
| **Apple / Google**| Push notification tokens                              | Global                     | Delivering reminder notifications            |

We do **not** share data with:

- Advertising networks
- Data brokers
- Social networks (beyond the sign-in providers above)

Google Calendar data is **never** sent to any of these providers. It
stays on your device.

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
- **Withdraw consent** — wherever we relied on consent (e.g. analytics),
  you can withdraw it at any time.
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
