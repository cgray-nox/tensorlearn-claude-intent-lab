# Intent: results-ready notification (PRD N-17)

Sources: `inputs/01-approved-prd.md` (approved 2026-09-18), `inputs/02-current-meeting.md` (discovery notes 2026-09-20). `inputs/03-superseded-request.md` is superseded history and approves nothing here.

## Problem

P-1. The fictional clinic receives avoidable calls from patients checking whether their results are ready (PRD N-17, Problem and outcome).

## Proposed outcome

O-1. A patient is notified when a result is ready for their review in the existing authenticated portal.
O-2. A notification is eligible only after a doctor has reviewed and released the result. "Ready" does not mean the laboratory upload finished (PRD; discovery notes, product owner).
O-3. The message says only that an update is available and directs the patient to the existing authenticated portal.

How success will be observed:
- S-1. Fewer status-only calls, counted separately from clinical questions and compared against a measured baseline (discovery notes, support lead).
- S-2. Delivery failures are tracked and handled without sending duplicate patient messages (PRD).
- S-3. No numeric target is approved. The baseline and the target will be agreed during discovery, so none is stated here.

## Affected users and systems

- A-1. Patients who receive the notification.
- A-2. The existing authenticated portal and its existing result route, where the patient views the result. It is adequate as is (discovery notes, engineering lead).
- A-3. Doctors who review and release results, and the support team that handles status calls.
- A-4. The notification channel is not yet decided (see OPEN-1).

## Out of scope

- X-1. Portal redesign.
- X-2. Appointment scheduling.
- X-3. Clinical interpretation.
- X-4. Notifying third parties. Referring-doctor notification is a separate open question (OPEN-2), not decided here.
- X-5. A new patient dashboard, which is a separate project (discovery notes, engineering lead).
- X-6. Items that appear only in the superseded request and are not approved: automatic sending as soon as the lab uploads, the test result in an SMS, copying the referring doctor, and a 90% call reduction in one week.

## Constraints

- C-1. A doctor must review and release the result before any notification is eligible.
- C-2. No diagnosis, test result, clinical measurement or treatment detail in the message or in notification or operational logs (PRD; discovery notes, privacy owner).
- C-3. Access is authenticated in the existing portal. Results are not attached, and there is no public result link.
- C-4. No duplicate notification for the same released result version.
- C-5. Delivery failures are handled without duplicate patient messages.
- C-6. Consent and the delivery channel are still under review, so no channel is approved.

## Open questions

- OPEN-1. Which channel (SMS, email or portal push)? Owners: product owner and privacy owner, after consent and delivery review.
- OPEN-2. Should the referring doctor be notified? Owners: clinical owner and privacy owner, who must decide recipient authorization. It is not approved by the PRD and must not be inferred from the old request.

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
