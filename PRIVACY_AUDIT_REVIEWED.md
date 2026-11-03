# Medgnosia — Privacy Review Notes

**App:** Medgnosia  
**Package:** `com.medgnosia.app`  
**Developer:** nasrouDev  
**Contact:** nasroudev@gmail.com  
**Review document date:** November 3, 2026

## Scope and limitation

These notes reorganize the technical audit supplied by the developer. They are not an independent source-code re-audit, legal opinion, or guarantee of Google Play approval. Re-check the current release source code, merged manifest, Gradle dependency graph, SDK behavior, and Play Console declarations before submission.

## Behavior reported by the supplied technical audit

The supplied audit reports that the inspected app:
- Stores profile preferences, study progress, question activity, flashcards, exam schedules, and media in local Android app storage (Room, DataStore, and app-private files).
- Keeps study-assistant conversation state in memory and implements the assistant with local rule-based logic.
- Does not require user accounts and does not provide cloud sync.
- Does not include Firebase, advertising, analytics, or crash-reporting SDKs in the inspected dependency set.
- Uses camera access for optional profile-photo capture and notification/alarm functionality for study reminders and exam notifications.
- Can export/share user-selected flashcard content through Android's sharing mechanism.

These statements describe only the inspected version represented by the supplied audit. They must not be treated as permanent guarantees.

## Important checks before release

1. **Re-audit the exact release build.** Check the merged release manifest, all runtime permissions, Gradle dependencies (including transitive dependencies), network/security configuration, and any code paths that make network requests.
2. **Verify the assistant implementation.** Confirm that prompts and responses are genuinely local and that no remote API, embedded web view, external intent, or third-party service receives prompts.
3. **Verify backup behavior.** Review Android Auto Backup / data-extraction rules. Uninstalling an app does not necessarily prove that every copy or backup of its data is immediately erased from every device or backup destination.
4. **Verify image access.** Confirm whether the app uses the system Photo Picker, broad media permissions, or camera permission, and describe only the actual behavior.
5. **Review exact-alarm permissions separately.** `SCHEDULE_EXACT_ALARM` and `USE_EXACT_ALARM` have distinct Android/Google Play eligibility and declaration requirements. Do not assume they are approved merely because reminders use alarms; verify current policy and the app's eligibility.
6. **Review health-related content.** The app is described as educational, but users may enter free-text content. Warn users not to enter identifiable patient information or confidential clinical records. Ensure the app's Health apps declaration and store listing accurately describe its function.
7. **Check the current target SDK.** The target SDK/version in the earlier audit is dated and should be read from the actual release Gradle configuration; do not reuse the old Android-version label.
8. **Keep disclosures synchronized.** The public Privacy Policy, Google Play Data safety form, app permissions, store listing, and actual behavior must match.

## Data Safety form — do not copy blindly

The earlier audit suggested selecting “No” for data collection/sharing because the app's described data remains on-device. This may be the correct outcome if the release build truly does not transmit or share any applicable user data, but the developer must verify the current Google Play Data safety definitions and all SDK behavior for the exact release. On-device-only access is not the same as saying the app does not process information; answer the form according to the Play Console's current definitions.

Do not select encryption, deletion, or other answers based only on this note. Verify each question against the shipped implementation and current Play Console guidance.

## Public contact details

- Developer name: nasrouDev
- Privacy contact: nasroudev@gmail.com
- Country: Algeria
- Package: `com.medgnosia.app`

## Maintenance

Whenever the app adds accounts, cloud sync, remote AI/API calls, analytics, crash reporting, advertising, new permissions, or new data-handling behavior, update the Privacy Policy and re-complete the relevant Play Console disclosures before publishing that version.
