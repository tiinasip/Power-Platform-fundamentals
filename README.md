# Power-Platform-fundamentals
Course work for Power Platform fundamentals KAMK
## Mauku  - Services for music classes
### Background
Mauku is a music association that supports 9–15-year-old pupils enrolled in music classes at a specific elementary school. The association owns a wide variety of brass instruments, which pupils can rent. However, music teachers decide who receives an instrument, as the unrented instruments are stored at the school, and the teachers are best acquainted with each pupil’s skill level.

Pupils play the rented instruments in the class orchestra, and rental contracts typically last for four years. In addition to instrument rentals, Mauku supports music events, camps, and trips.

Since Mauku can only support its members, a separate registration system is in use. Parents sign up their child and pay an annual membership fee. Throughout the school year, Mauku sends invoices, informational letters, and invitations to various events.

So far, Mauku has only used the membership registration system. While this system complies with GDPR and remains in use, processes for event registrations, instrument rentals, and member communications require improvement. Instruments are not currently registered digitally, leading to considerable manual work to track who has which instrument and its condition.

### Power Platform usage 
### Rental process – the core problem
The project begins by creating a digital inventory of instruments. Each instrument is recorded in a Dataverse table, assigned a unique ID, and photographed. Additional information—such as age, condition, and maintenance history—is also recorded.

A rental application is built using Power Apps. When a music teacher hands out an instrument, they use the app on their mobile device to register the rental immediately. Power Apps also verifies whether the pupil is a registered member—rentals are not allowed for non-members. Using the membership data, Power Automate sends an email to the pupil's parents, inviting them to sign the rental agreement. Parents can complete the process via a Microsoft Form or within Power Apps, where they can review the terms and conditions and accept the annual rental fee. If they do not sign the agreement, the pupil must return the instrument.

If the contract is not signed within three days, Power Automate sends reminder emails to the parents. After 14 days, Power Automate notifies the teacher through Power Apps to retrieve the instrument.

When a pupil returns an instrument, the teacher logs the return using Power Apps, and Power Automate notifies the parents accordingly. All rental data is updated in Dataverse and synchronized with the membership registration system, which handles detailed member data and invoicing.

#### Technical solution:
For teachers, canvas app is created in Power Apps. Teachers use mobile devices to register rentals and returns quickly  and canvas apps offer full control over layout and user experience, which works for task-based scenarios. However, it requires more work to be created, but as teachers are a key stakeholderd, the association has to make the app as good as possible. Canvas apps offers the flexibility and optimizing the flow for minimal clicks, which is crucial for busy tearchers. Canvas apps also embed logical conditions as “check if the pupil is a member before allowing rental” easier.

Teachers’ app has four main navigations: rent instruments, return instrument, view rentals and other tasks. 

Rent instrument screen layout includes:
*	Instrument Search / Scanner: Search by name or scan QR/barcode
*	Photo & Info Display: Pull from Dataverse to show instrument condition/photo
*	Pupil Selection: Dropdown or search by name/class
*	Membership Check: Auto-check membership status
  *	Show warning if not a member (disable rental submission)
* Start Date / Expected Return Date: Auto-populate or select
*	Submit Button:
**	OnSubmit:
*** Create Rental record
***	Set Instrument.Status = "Rented"
***	Trigger Power Automate flow to email parents with rental agreement

Return instrument screen layout:
* Select rental from "active rentals" list
*	Optional: Upload photo of returned instrument
*	"Condition" dropdown or notes
*	Trigger maintenance flag if needed
*	On submit:
**	Set Instrument.Status = "Available"
**	Set Rental.Status = "Returned"
** Trigger Power Automate flow to notify parents

View rentals:
*	Status = "Active" (can be changed to nonactive)
*	Show instrument, pupil, start date, return date, and contact link to parents
*	Possibility to navigate maintenance information

Other tasks:
*	Checkbox: "Send Reminder" to trigger email via Power Automate
*	Button: "Report Damage" to trigger a maintenance workflow
*	Link to Power BI Dashboard (embedded in app)

Teachers’ app is the first to be created. If seen useful, application to follow rentals through app is created for Mauku admins as well. This, however, needs to discussed first, it may be that Power BI reports are timely enough. For admins, model-driven app could created in Power Apps to manage instruments, see all rentals, update condition/status, and run reports. The model-driven apps are built directly on Dataverse and are ideal for CRUD operations (Create, Read, Update, Delete) and workflow automation. 

## Invoicing, web pages and reporting
Invoicing information flows from the registration system into Dataverse. Power BI is used to generate reports showing how many instruments are rented, how many invoices are pending, and the condition of the instruments. It also helps estimate future investment needs.

Power Pages is used to build a website that includes a feedback form. Feedback triggers Power Automate flows. For example, if a parent reports a problem with an instrument's carrying bag, the teacher is automatically notified. If the feedback contains a development idea, it is forwarded to the Mauku board members by email.

Power Pages is also used for event registrations. For example, if there is a concert trip, participants fill out a registration form. If a participation fee applies, Power Automate triggers the invoicing process.

## Further development
Once the instrument rental system is functioning effectively, the next phase is to develop and expand the solution.

One consideration is whether Mauku can retire the current membership system and transfer all data to the Power Platform. This would consolidate registration and invoicing into a single environment, streamlining administration.

Such a transition would centralize all data in Dataverse and expand the scope of Power BI reporting, as all administrative tasks would be handled within the Power Platform. For example, Mauku’s administrator would manage invoicing directly from there.

At that point role-based access and data security need to be created. It ensures that teachers, board members, parents, and pupils only have access to information and tools relevant to their roles.

Teachers could have their dedicated teacher dashboard, where they could easily see who has which instrument, check maintenance history, log observations (e.g., skill development, instrument condition) and send messages directly to parents.

Members could also update their contact information—such as email addresses and phone numbers—via Power Pages. The self-service portal could be enhances to show instrument and rental details, upcoming events and registrations and open invoices.

AI tools will be introduced to improve communication. Initially, they will be used for translating messages for parents who do not speak Finnish. Later, they will help improve the clarity of newsletters and automate social media updates.

A chatbot will be developed to assist new members by answering frequently asked questions, such as which instruments are available, rental fees, and the possibility of financial aid.

One easy and straight-forward development is to automatise financial aid process. Forms for applying for discounts or financial assistance are created. After the applicant is filled the form, Power Automate routes the application to appropriate reviewers and notify the family of the decision via email

Power BI development is endless. New reports can be created for all the new data and perceived need. It also streamlines board meetings, as the information is easily available.

Mauku’s board activities would benefit greatly from AI. AI could write memos, create project plans, help to create financial statements etc. The work load of volunteers would decrease, as there is less manual work with documents.
