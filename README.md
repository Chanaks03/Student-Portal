# Campus — Student Portal

A modern, responsive personal academic workspace built with semantic HTML5, CSS3, and vanilla JavaScript. It is a static application: no authentication, backend, database, package installation, or build step is required. The demo uses a fictional BS Information Technology student and fictional academic records.

## Features

- **Dashboard:** live local date and time, term information, enrolled subject count, weighted grade average, pending and upcoming tasks, today's classes, recent announcements, academic chart, progress bars and quick links.
- **Class Schedule:** Monday–Saturday weekly and daily views, today highlighting, color-coded classes, instructor and room information, next class, and add/edit/delete records.
- **Grades:** subject units, three grading periods, weighted subject grade, GWA, academic remarks, academic-year and semester filters, customizable grading scale and weights, chart, print layout and record management.
- **Announcements:** expandable local demonstration notices, priorities, categories, search, read/unread status and unread counters.
- **Tasks:** searchable assignments, priority and status filters, due dates, overdue indicators, completion progress and full record management.
- **Calendar:** monthly view, previous/next/today navigation, category colors, personal event management and automatically synchronized assignment deadlines.
- **Profile:** editable student information, image preview, upload, removal, save and cancel. Images are resized before local storage.
- **Settings:** theme mode, accent color, notification badge preferences, grading settings, JSON backup export/import and confirmed reset.

## Technologies

HTML5, CSS Grid/Flexbox, vanilla JavaScript, the localStorage API, Canvas, and native dialogs. Optional CDN resources: Chart.js 4.4.9, Lucide 0.468.0, and the Inter Google Font. When these resources cannot load, the site uses its own Canvas charts with hover labels, built-in SVG line icons, and system fonts. Personal record data is not sent to these services by the application; loading third-party assets does make ordinary network requests.

## Folder structure

```text
student-portal/
├── index.html
├── css/
│   ├── style.css
│   └── responsive.css
├── js/
│   ├── app.js            # routing, shared UI, dialogs, charts, search
│   ├── dashboard.js      # dashboard and derived summaries
│   ├── schedule.js       # timetable and class editor
│   ├── grades.js         # grade records and grading preferences
│   ├── announcements.js  # local notices and read status
│   ├── tasks.js          # assignments and status management
│   ├── calendar.js       # calendar and event editor
│   ├── profile.js        # profile, images, settings and backups
│   └── storage.js        # demo data, data validation, storage and calculations
├── assets/
│   ├── images/academic.svg
│   └── icons/favicon.svg
├── .nojekyll
└── README.md
```

## Local setup

1. Extract the ZIP file and enter the `student-portal` folder.
2. You can open `index.html` directly to preview the layout, but some browsers restrict persistent storage on `file:` URLs. For reliable behavior, use a static web server.
3. If Python is installed, open a terminal in the project folder and run:

   ```sh
   python -m http.server 8000
   ```

   On Windows, `py -m http.server 8000` is an alternative. Visit `http://localhost:8000/` in your browser. VS Code Live Server is also suitable. Neither is needed when hosting on GitHub Pages.
4. Use the sidebar to navigate. Add sample records or edit the existing ones. Refresh the page to check that your changes persist in the same browser and origin.

## Deploy to GitHub Pages

1. Create a GitHub repository named `student-portal` (a public repository works on standard free accounts).
2. Upload the **contents** of the extracted `student-portal` folder to the repository root. Ensure `index.html` is at the root, with `css`, `js`, and `assets` as sibling folders. Do not upload the ZIP as the only file.
3. Commit the files to the `main` branch. The `.nojekyll` file is optional but included for static publishing.
4. Open the repository's **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Choose branch **main** and folder **/ (root)**, then Save.
7. Once GitHub publishes the site, open the URL shown in Pages settings, normally `https://YOUR-USERNAME.github.io/student-portal/`.

Hash-based navigation and relative paths support deployment under a repository subdirectory without a rewrite server. No API key or server is needed.

## Customize

- Edit your details through Student Profile and customize the theme or grading system in Settings.
- Modify `P.seed()` in `js/storage.js` to change the initial fictional content. Existing browser data is preserved until you reset it or change the storage key; back up any important personal changes before doing so.
- Change the CSS variables near the beginning of `css/style.css` for the default palette, spacing, surfaces, and typography. The accent is also initialized in `P.seed()`.
- Navigation labels and icon definitions are in `js/app.js`. Each page's renderer is in its corresponding JavaScript file.
- Announcements are static demo notices. To publish shared notices, update the sample source and redeploy; already saved browsers retain their local copy until reset or a compatible import. The site does not fetch official school notices.

## Grading rules

The default sample uses a percentage scale, 75% passing threshold, and period weights of 30% prelim, 30% midterm, 40% final. These are demonstration choices, not an institution's official policy.

- Weighted subject grade = sum of each period grade multiplied by its weight.
- GWA = sum of completed subject weighted grades × units, divided by the total units of those completed subjects.
- Missing period grades are shown as incomplete and excluded from GWA. Zero is a valid percentage grade, not a missing grade.
- You may choose the lower-is-better 1–5 point scale, a passing threshold and period weights totaling 100%. Existing grades are not silently converted; grades outside the selected scale must be cleared or removed before switching.
- The initial seven fictional subjects total 20 units and produce a GWA of 94.34% (rounded).

## Storage and privacy

Records and preferences are stored as JSON using localStorage, with the key `campus.portal.v2`. The dashboard derives its summaries from the same records. Each browser/origin has its own workspace. There is no cloud sync, real school integration, sign-in, database encryption, or access control. Local storage may be inspected by anyone with access to the browser, and may be erased by clearing browser data. Private browsing or blocked/full storage can prevent persistence; the portal displays a warning and keeps changes in memory for the session so a backup can be exported.

Settings → Export downloads a JSON backup. Import validates its format, record types and values before requesting confirmation to replace the current workspace. Reset requires confirmation and restores the fictional demo. Backups are not encrypted: store them carefully and never commit actual student IDs, grades, contact information, photos, backups or passwords to a public GitHub repository. Use only non-sensitive sample records for public demos.

## Verification and browser notes

All JavaScript files passed `node --check`. The complete application was exercised in Chromium with the same HTML, CSS and scripts inlined (the test environment blocks normal local/remote navigation and external CDNs). Tested: all eight renderers; class, grade, task and event add/edit/delete; weighted grade and GWA; task status updates; read status; profile save; theme changes; storage writes through a test storage adapter; export/import and invalid-backup rejection; invalid class-time validation; profile image upload; task search; daily timetable filter; reset; and document width at 390px across all eight views. The offline chart fallback was visually checked. Direct network-loaded Chart.js/Lucide, real-origin persistence, GitHub deployment and Firefox/Safari/Edge testing were not independently verified in this environment. The site uses standard modern browser APIs and provides fallbacks for CDN and storage failures.
