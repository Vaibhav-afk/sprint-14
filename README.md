# JIRA Ticket Requirements

## [CEN-6799](https://anyonehome.atlassian.net/browse/CEN-6799) — Twilio voicemail AI transcription

- After a Twilio voicemail recording is available, send it to the InhabitAI transcriber.
- Track the job as **Pending**, **Completed**, or **Failed**.
- On success, save the caller's transcript and conversation summary against the correct guest card or case. Exclude IVR prompts.
- On failure, do not save partial results as successful; keep an error log for support.
- Do not process non-Twilio voicemails or voicemails without an available recording. Showing statuses in CRM is not part of this ticket.

## [CEN-6798](https://anyonehome.atlassian.net/browse/CEN-6798) — Reuse calculator preferences

- Keep the agent's selected add-ons and other calculator choices during the current prospect interaction.
- Preselect those choices when the calculator is reopened, even for another unit, while still allowing changes.
- Clear the choices when the interaction ends.
- Do not save calculation history or add a guest card calculations tab.

## [CEN-6797](https://anyonehome.atlassian.net/browse/CEN-6797) — Fees and add-ons in TMLP

- Show all **Mandatory Fees** first, with each fee's name and amount.
- Show **Personalized Add-Ons** below them and include only selectable recurring fees, including recurring household fees such as pet rent.
- Calculate TMLP as: **base rent + all mandatory fees + selected recurring add-ons**.
- Exclude application fees, deposits, move-in fees, and all other one-time fees.
- Display property specials without changing the total. Keep recurring-fee calculations consistent with CRM quote logic.

## [CEN-6796](https://anyonehome.atlassian.net/browse/CEN-6796) — Calculate TMLP in the flyout

- Show the selected unit's rent matrix inside the pricing calculator flyout.
- Selecting a matrix cell must update the base rent, unit of interest, desired lease term, and dependent totals immediately.
- Allow the agent to change the unit inside the calculator.
- Keep the move-in date read-only and hide **Expire offer on**.
- Display any active property special, but do not provide an include/exclude option or change the total.

## [CEN-6795](https://anyonehome.atlassian.net/browse/CEN-6795) — Open the TMLP pricing calculator

- For TMLP-enabled properties, show a calculate-price icon on each lease-term cell after a unit row is expanded.
- Open the pricing calculator in a flyout over the unit list when the icon is clicked.
- Closing the flyout must return the agent to the same unit-list position and context.
- For non-TMLP properties, hide or disable the icon and show: **“Price calculation is not available for this property.”**
- This ticket only adds the icon and flyout shell; it does not add calculator logic or a guest card pricing tab.

## [CEN-6794](https://anyonehome.atlassian.net/browse/CEN-6794) — Expand units and select a lease term

- Replace the unit-level Select/Show/Hide and **View Pricing** controls with expandable unit rows that show the rent matrix.
- Clicking a price cell must immediately save the unit of interest and desired lease term on the case.
- Apply this to all multifamily properties with unit pricing, whether TMLP is enabled or not.
- Do not change the bed-count summary **Select** controls.

## [CEN-6759](https://anyonehome.atlassian.net/browse/CEN-6759) — Return Lead Summary from DedupeContact

- When DedupeContact finds a guest card for a new AI leasing phone, chat, or SMS session, return its saved `contact_ai_summary`.
- Return the same summary for all three channels; do not generate a new summary or return every old transcript.
- If no matching summary exists, allow the conversation to continue without one and do not invent content.
- Do not change guest-card matching, Conversation Summary behavior, maintenance assistants, or CRM screens.

## [CEN-6707](https://anyonehome.atlassian.net/browse/CEN-6707) — Record maintenance SMS transfers

- When CharlieIQ hands an AI maintenance SMS conversation to a live agent, record the transfer for reporting.
- Add both the AI and live-agent handlers to `service_request1__c.answered_by_list`.
- Add a matching record to `service_request_call_transfer`.
- Make SMS transfers distinguishable from voice transfers, and do not record a transfer when AI resolves the issue itself.
- The recording work must not delay messages or agent responses. This depends on CEN-6624 and must align with CEN-6625 and CEN-6699.

## [CEN-6701](https://anyonehome.atlassian.net/browse/CEN-6701) — Service Request SMS transcript

- Add **View Transcript** next to **Download Call** on the Contact Center Service Request detail page.
- Show it only when the case origin is SMS.
- If no transcript exists, disable it and show: **“No transcript found for this interaction.”**
- If a transcript exists, open the full conversation in a lightbox using the same format as CRM and CEN-6700.
- Do not change **Download Call** or behavior for non-SMS cases.

## [CEN-6700](https://anyonehome.atlassian.net/browse/CEN-6700) — Guest Card SMS transcript

- Add **View Transcript** next to **Download Call** on the Contact Center guest card detail page.
- Show it only when the case origin is SMS.
- If no transcript exists, disable it and show: **“No transcript found for this interaction.”**
- If a transcript exists, open the full conversation in a lightbox using the CRM transcript format.
- Do not change **Download Call** or behavior for non-SMS cases.

## [CEN-6696](https://anyonehome.atlassian.net/browse/CEN-6696) — Central Issue on Service Requests

- Add **Central Issue** as the rightmost checkbox in the Work Order Details row and move **SOS Call** left to make room.
- When checked, show **Description Of Issue** and a **Send** button.
- Require a non-empty description, allow up to 1000 characters, and keep **Send** disabled until text is entered.
- When unchecked, hide the extra controls and clear any entered description.
- On **Send**, save the checkbox and description so both appear correctly when the service request is reopened.

# Potential Blocker Questions

## CEN-6799

- What authentication, request, and postback format from CEN-6670 should be used?
- What are the retry, timeout, and duplicate-postback rules?
- Which existing fields store the status, transcript, summary, and guest card/case link?

## CEN-6798

- What exact event starts and ends a “prospect interaction”?
- Should temporary preferences survive a page refresh or multiple browser tabs?
- What happens when a saved add-on is unavailable for the next unit?

## CEN-6797

- Which field identifies a mandatory fee, and what is the source of truth?
- How are variable, conditional, or non-monthly recurring fees converted to a monthly amount?
- Are taxes, concessions, prorated amounts, and zero-dollar fees included or displayed?

## CEN-6796

- Which API saves the unit and lease term, and how should save failures be shown?
- When changing units, which units are available and what lease term is selected by default?
- If several property specials are active, which ones should be displayed?

## CEN-6795

- For non-TMLP properties, should the icon be hidden or disabled? A tooltip requires a visible control.
- Should clicking an icon pass that cell's unit, term, and price into the flyout?
- Must closing the flyout preserve scroll position, expanded rows, filters, and the selected cell?

## CEN-6794

- What should appear when a unit has no pricing matrix or loading fails?
- Can more than one unit row be expanded at once?
- How should the UI show saving, success, or failure after a price is selected?

## CEN-6759

- What response field name and format do the phone, chat, and SMS assistants expect?
- If `contact_ai_summary` has multiple rows, how is the current summary selected?
- Are there size, privacy, or permission rules for returning the summary?

## CEN-6707

- Which exact event confirms that a live agent has taken over?
- What handler values and SMS transfer type must be written for reporting?
- How should retries avoid duplicate transfer records and `answered_by_list` entries?

## CEN-6701

- Which record or API links a service request to the correct SMS conversation?
- If there are several SMS threads, should the lightbox show one or all of them?
- What permissions, ordering, timestamps, and sender labels are required?

## CEN-6700

- Which record or API links a guest card case to the correct SMS conversation?
- If the guest card has several SMS interactions, which one should be displayed?
- What permissions, ordering, timestamps, and sender labels are required?

## CEN-6696

- Which database fields and API endpoint save the checkbox and description?
- Does unchecking and sending permanently clear a previously saved description?
- Does **Send** save only these fields or the whole Service Request, and how are failures shown?
