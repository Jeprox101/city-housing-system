# city-housing-system
CITY HOUSING DEVELOPMENT OFFICE - MANAGEMENT SYSTEM (Front-end prototype)
=========================================================================

Built with plain HTML5, CSS3 and vanilla JavaScript.
No frameworks, no backend, no build step.


HOW TO RUN
----------
Option 1 (recommended): VS Code + Live Server
  1. Open the CITY-HOUSING-SYSTEM folder in VS Code.
  2. Right-click index.html and choose "Open with Live Server".

Option 2: double-click index.html (it also works from file://).

All scripts are normal <script> files (no ES modules), so there is no
CORS problem when loading the sample data files.


FOLDER STRUCTURE
----------------
index.html                 Page layout, sidebar, script loading order
assets/css/
  style.css                Colors, layout, buttons, badges, modal, toast
  dashboard.css            Dashboard cards, bars, activity list
  forms.css                Form fields and validation messages
  tables.css               Search toolbar, tables, profile windows
  responsive.css           Laptop / tablet / small-screen rules
assets/data/               SAMPLE DATA (seed only)
  applicants.js            20 sample applicant records
  users.js                 6 sample staff accounts
  status.js                Statuses, programs, roles, permissions, lists
assets/js/
  storage.js               DB object: all LocalStorage reading / writing
  app.js                   Helpers, icons, permissions, toast, modal, confirm
  filtering.js             Search, filters and sorting
  applicants.js            Records tables + profile (View) + Delete
  dataForm.js              Applicant registration form + validation
  editing.js               Edit applicant window
  dashboard.js             Dashboard statistics and lists
  users.js                 User management
  navigation.js            Sidebar / page switching (loaded last, starts app)


SCRIPT LOADING ORDER (important)
--------------------------------
1. assets/data/status.js, applicants.js, users.js   (sample data + config)
2. storage.js    (data layer)
3. app.js        (helpers)
4. filtering.js, applicants.js, dataForm.js, editing.js,
   dashboard.js, users.js                            (features)
5. navigation.js (must be last: it starts the app)

If you add a new script, place it before navigation.js.


HOW DATA IS STORED
------------------
- First run: the sample data from assets/data/*.js is copied into LocalStorage.
- After that, LocalStorage is the source of truth. Adding, editing and
  deleting records is saved there and survives a browser refresh.
- Data is saved per browser. Another browser or computer starts with the
  sample data again.
- To start over: Users page > "Reset sample data" (administrators only).
  You can also clear the site data in the browser.
- LocalStorage keys: chdo_applicants, chdo_users, chdo_activities,
  chdo_seeded_v1, chdo_current_user.


MODULES
-------
Dashboard          Live counts, recent applications, status overview,
                   quick actions, recent activity.
Users              Staff list, add / edit / delete, profile, roles, status.
Data Form          Register an applicant (automatic Application ID and Age,
                   required-field validation, duplicate warning).
Applicants/Records All applicants: search, filters, sorting, View / Edit / Delete.
Approved           Status = Approved.
For Review         Status = For Review.
For Survey         Status = For Survey.
Rejected / Denied  Status = Rejected or Denied.

Changing an applicant's status (Edit) moves the record to the matching
page automatically. Nothing is transferred by hand.

First Name, Middle Name, Last Name and Suffix are separate fields in the
form, the stored data, the tables and the profile.

Application ID format: CHDO-YYYY-0001 (the next free number is used; a
duplicate ID is never saved).


ROLES (demo)
------------
Use the "Signed in as" menu at the top right to switch users and see
what each role can do. This prototype has no passwords.

  Administrator  Add / edit / delete applicants, manage users, reset data.
  Staff          Add and edit applicants. Cannot delete or manage users.
  Viewer         Read-only.

The rules are in assets/data/status.js (permissions).


COMMON CHANGES
--------------
- Housing programs, suffixes, regions, statuses: assets/data/status.js
- Default Region / Province / City on the form: formDefaults in status.js
- Barangay / Province / City suggestions: *Suggestions lists in status.js
- Sample applicants: assets/data/applicants.js
  (only used on first run or after "Reset sample data")
- Colors: the variables at the top of assets/css/style.css


NOTES
-----
- This is a front-end prototype. Anyone with access to the browser can see
  the stored data. Do not enter real personal information until a secure
  backend with real login is added.
- Uses LocalStorage (about 5 MB per browser).

