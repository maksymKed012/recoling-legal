# RecoLing Privacy Policy

**Last updated: 17 October 2026**

This policy explains what data the RecoLing iOS app and its server handle, why, who else receives it, and what you can do about it.

## 1. Who we are

RecoLing is provided by Maksym Ked, an individual developer, who is the data controller for the personal data described in this policy.

Contact for privacy questions and requests: [maksym.ked@gmail.com](mailto:maksym.ked@gmail.com)

## 2. What the app does

RecoLing turns photos of your handwritten language-lesson notes into flashcards. You take or choose a photo, and the app sends it to our server. Our server asks an AI model (Anthropic's Claude) to read the vocabulary pairs in the photo and sends them back to the app. You review the suggested cards, and then they are saved on your device. There are no user accounts, no cloud sync and no payments.

## 3. Data we process

| Data | What it is | Why we use it |
| --- | --- | --- |
| **Photo of your notes** | Before upload, the app resizes the photo and saves it as a new JPEG (at most 1200 px on the long edge and about 512 KB). This happens only when you choose to import a photo. | To extract vocabulary from it. |
| **Language pair** | The source and target languages you pick for the deck, for example "Italian" and "English". | To tell the AI which languages to look for. |
| **Extracted vocabulary** | The word pairs the AI reads from your photo. | To return draft cards to you. |
| **Device ID** | A random identifier that the app creates on first use and stores in the iOS Keychain. It is not your Apple advertising identifier, and it does not contain your name or any details about your device. | To limit how many imports one device can make in a short time, which protects the service from abuse. |
| **Connection data** | When the app contacts our server, our hosting provider records your IP address, the app's user-agent string, the time, the request path, the response status and the request size. | To run, secure and troubleshoot the server. |

Our own server logs record the method and path of each request (for example `POST /extract`) and technical error details. They are not designed to contain your photo, your device ID or your vocabulary. **TODO(max): this is only fully true once the logging fix described in the PR is deployed. At the moment, a malformed request can cause its body, including the image, to be written to the error log.**

## 4. AI processing (Anthropic)

To extract vocabulary, our server sends your photo and your language pair to **Anthropic**, the company that makes the Claude AI models, through the Anthropic API. We do not send Anthropic your device ID, your IP address or any other identifier.

Anthropic's published position for API customers, checked on 17 October 2026:

- **Training:** by default, Anthropic does not use inputs or outputs from its commercial products, including the Anthropic API, to train its models ([source](https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training)). Anthropic's Commercial Terms say: "Anthropic may not train models on Customer Content from Services" ([source](https://www.anthropic.com/legal/commercial-terms)).
- **Retention:** Anthropic automatically deletes API inputs and outputs from its systems within 30 days. It may keep them longer where the law requires it, or to enforce its Usage Policy. Content flagged as violating that policy may be kept for up to 2 years ([source](https://privacy.claude.com/en/articles/7996866-how-long-do-you-store-my-organization-s-data)).

Anthropic processes this data under its [Commercial Terms](https://www.anthropic.com/legal/commercial-terms), which include its Data Processing Addendum. Anthropic's own privacy policy is at <https://www.anthropic.com/legal/privacy>. That policy states that it does not apply to content Anthropic processes on behalf of its business customers, so the Commercial Terms are what govern your photos.

## 5. What stays on your device

These are stored **only on your device** and are never sent to our server:

- your decks, cards (including any images you add to cards) and study and review history, which are kept in a local database;
- your settings, and your daily reminder time, which the app schedules as a local notification on your device.

If you export a deck to CSV, the file goes wherever you choose to send it from the iOS share sheet.

Deleting the app deletes your decks, cards, review history and settings. We cannot recover them for you, because we never had a copy.

The device ID is kept in the iOS Keychain. According to Expo, whose SecureStore module the app uses, iOS may keep Keychain data after the app is deleted, so the same device ID may be reused if you reinstall the app ([source](https://docs.expo.dev/versions/latest/sdk/securestore/)).

## 6. How long we keep data

| Data | Where | How long |
| --- | --- | --- |
| Photo, language pair, extracted vocabulary | Our server | Held in memory only while your request is being processed, not stored. See the logging TODO in section 3. |
| Photo, language pair, extracted vocabulary | Anthropic | Deleted within 30 days, with the exceptions described in section 4. |
| Device ID: rate-limit counters | Upstash | Expire automatically within about 2 minutes of your last request. |
| Device ID: rate-limit usage statistics (hourly counts per device ID of allowed and blocked requests) | Upstash | **TODO(max): these records currently have no automatic expiry. Disable rate-limit analytics or add an expiry, then state the period here.** |
| Connection data and server logs | Railway | We can access them for 7 days, the log retention for our Railway plan. Railway's documentation says that upgrading a plan restores older logs, so Railway may store them for longer. **TODO(max): ask Railway how long logs are actually stored, then state that here.** |

## 7. Who we share data with

We use these service providers, and only to run RecoLing:

- **Anthropic**: AI processing of your photo (see section 4).
- **Railway**: hosts our server and keeps its logs. [Railway privacy policy](https://railway.com/legal/privacy)
- **Upstash**: hosts the database used for rate limiting by device ID. [Upstash privacy policy](https://upstash.com/trust/privacy.pdf)

We do not sell your data. The app contains no advertising, no analytics or crash-reporting SDKs, and no tracking. We do not combine your data with data from other companies.

## 8. International transfers

Our providers process data outside the UK and the EU:

- **Anthropic** stores API data in the United States. We use Anthropic's default global routing, so the AI model that reads your photo may run in any of Anthropic's available locations, which Anthropic lists as the US, Europe, Asia and Australia ([source](https://privacy.claude.com/en/articles/7996890-where-are-your-servers-located-do-you-host-your-models-on-eu-servers), [data residency docs](https://platform.claude.com/docs/en/manage-claude/data-residency)).
- **Railway** runs our server in its US West region, in the United States.
- **Upstash** stores the rate-limit data in its London, UK region (AWS eu-west-2) only.

Safeguards for these transfers: **TODO(max): confirm the transfer mechanism with each provider, for example the UK International Data Transfer Addendum or the EU Standard Contractual Clauses in their data processing agreements, and name it here.**

## 9. Your rights (UK and EU GDPR)

**Our legal basis:** **TODO(max): confirm the lawful basis. Suggested draft, to be checked: processing your photo and language pair is necessary to provide the import feature you ask for (contract), and the device ID and connection data are used for our legitimate interest in keeping the service secure and preventing abuse.**

You have the right to:

- ask for a copy of the personal data we hold about you (access);
- ask us to correct it (rectification) or delete it (erasure);
- ask us to restrict how we use it, or object to our use of it, including use based on legitimate interests;
- receive the data you gave us in a portable format (portability);
- complain to a data protection authority. In the UK this is the Information Commissioner's Office ([ico.org.uk](https://ico.org.uk/make-a-complaint/)). In the EU it is the authority in your country.

**How to make a request:** email us at the address in section 1. We will reply within one month. Because RecoLing has no accounts, the only server-side records we could link to you are those tied to your device ID, and we may need that ID to find them. **TODO(max): the app does not currently show the device ID to the user. Decide how users can provide it, or explain what you can do without it.**

The simplest way to remove everything stored on your device is to delete the app.

## 10. Children

RecoLing is not directed at children under 13, and we do not knowingly collect personal data from them. If you believe a child has used the app and you want data removed, contact us.

## 11. Changes to this policy

If we change how RecoLing handles data, we will update this page and the "Last updated" date at the top. If a change is significant, we will also note it in the app's release notes.
