Below is a rough outline of the features that we are targeting for CHEFS.

[Post your ideas, leave a comment or vote on what CHEFS features we should build next ](https://chefs-fider.apps.silver.devops.gov.bc.ca/)

## v0.0.1 - Alpha - Initial Proof of Concept

* [x] View list of forms you have some access on  
* [x] Create a new form  
* [x] Form builder (simple view)  
* [x] Form builder (advanced view)  
* [x] Save Form Design  
* [x] View a form and Submit a form to the database  
* [x] Authentication for IDIR users  
* [x] Form visibility for all IDIR  
* [x] Share button for a form to get the direct link, and generate a QR Code  
* [x] Role based access control to manage a form with 5 roles (owner, team manager, editor, form reviewer, submitter)

## v0.1.0 - Alpha - Functional Submissions

* [x] View submission page styled without the app navigation header
* [x] Styling fixes for accessibility
* [x] Privacy Risk Assessment (draft)
* [x] Download form schema in the form designer view  
* [x] Back, Refresh or Close warning before leaving the page (designer or submission)  
* [x] Export submissions for a form within date range
* [x] Home page / landing page content
* [x] Ability to refresh your browser without losing your form design progress
* [x] Disclaimer and Statement of Responsibility for Users

## v0.2.0 - Beta - Form Editing and Management

* [x] Edit form and save new version
* [x] Manage form team members and access
* [x] Marking forms as deleted
* [x] Email notifications for a submission to the form reviewer
* [x] Email notifications for a submission to the submitter
* [x] Public (anonymous) form submissions

## v1.0.0 - MVP: Publishing, Uploads and Status Management

* [x] Publish and unpublish a form
* [x] Attach a document [Authenticated (IDIR) only]
* [x] Minimal state/status management for each form submission record
* [x] Email notification for state changes
* [x] User orientation/help materials
* [x] OpenAPI and documentation

## v1.1.0 - Drafts, Invitations, and Edit support

User Improvements

* [x] Create and edit draft submissions
* [x] Invite colleagues to draft submissions

Staff Improvements

* [x] Enhance state management and note support
* [x] Form Designer UI unification
* [x] Add submission edit support
* [x] Add soft delete submission support
* [x] CSV export format updates

Other Improvements

* [x] Update to formiojs 4.13
* [x] Convert application to JSON logging

## v1.2.0 - Integrations

* [x] Access form data from external web application
* [x] Generate pdf/xls/doc of submission and reports
* [x] Authentication with BCeID

## v1.3.0 - Return to User

* [x] Update default print header to always show BCGov logo
* [x] Return submission to submitter for edits
* [x] Update dependencies and infrastructure to Node 16 LTS
* [x] Expose JWT Token data to Formio components

## v1.4.0 - Continuous Improvement

* [x] Improved documentation and tutorials
* [x] Form Administrators are notified on status updates on forms AND can add an optional comment to submitter
* [x] Submitters are notified on status updates including completion
* [x] Authentication with Business BCeID
* [x] Added undo/re-do to the Form Designer
* [x] CHEFS Admins can change form owners
* [x] Technical Debt - confirm load and performance capability
* [ ] Integrate with COMS for file uploads and to allow access to attachments via the API
* [ ] Reviewers can download multiple submissions at once and attach a template permanently

## vx.x - Looking at next....

* [ ] Collaborate with CITZ team to architect as a government wide solution
* [ ] Include fields in email notifications
* [ ] Custom spatial form component
* [ ] Filter list of submissions with the API
* [ ] Analytics/BI
* [ ] View submission versions
* [ ] Show notes in exported submissions
* [ ] Improve developer documentation
* [ ] Auto-save a form during build
* [ ] Virus scan file uploads; possibly then allow public forms to allow file uploads
* [ ] Improve the Submissions View
* [ ] Multi authentication methods (ie both Business BceId and IDIR??) 
* [ ] Pre-populate forms with idir or bceid information??

