# SPO024-1: Carbohydrate Absorption Practical

A self-contained, static laboratory teaching application for University of Bedfordshire Level 4 nutrition students. No database, account, build pipeline, or external API is required.

## Publish using GitHub Pages

1. Use the GitHub repository `MikeLNewell/Glucose-absorption`.
2. Upload `index.html`, `styles.css`, `app.js`, `analysis.mjs`, the `examples` folder and the `tests` folder to the root of the repository.
3. In the repository, select **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, `main`, `/ (root)`, then **Save**.
5. The website should be available at `https://mikelnewell.github.io/Glucose-absorption/` once GitHub Pages deployment has succeeded.

The website works from GitHub Pages subdirectories because assets are referenced relatively. A local HTTP server can be used for testing: `python3 -m http.server 8000`, then open `http://localhost:8000/`. ES modules do not run reliably through `file://` URLs.

## Using the practical

1. Each team opens the website on one laptop or tablet, enters its team name and anonymous participant code, and confirms the laboratory safety briefing. Food names must be identical across teams if their data are to be grouped.
2. The lecturer can edit the local food options from **Lecturer analysis → Configure your practical**. Because there is no shared database, those settings are **only on that device**. Students on other devices can use **Other food (enter details)** and enter the exact food name, available carbohydrate and portion issued by the lecturer. Default food carbohydrate values are illustrative; check real product labels.
3. Record a baseline glucose measurement. After the five-minute food consumption period ends, click **Begin post-ingestion timer**.
4. Take measurements at 15, 30, 45, 60, 75 and 90 minutes. Enter the meter result in mmol/L. Actual time is automatically entered when the glucose value is recorded, and can be corrected manually. Follow the approved laboratory SOP; the app is not a medical device.
5. Complete the six optional rounds of physiology challenges between sampling events. Each browser keeps its own score. There is no shared leaderboard.
6. In **Results & analysis**, review the graphs, calculated variables and written interpretation. **Export CSV** before leaving the laboratory. You can also download a JSON backup of the entire local session.
7. Each team submits its CSV to the lecturer by an existing channel such as the learning platform, email or USB. On the lecturer's device, use **Lecturer analysis → Choose CSV files** to import multiple files, view class mean ± SD by food condition and export a consolidated CSV.

## Data management and limitations

- Each browser stores its own current session using `localStorage`. No information is sent to the internet by this application. Clearing browser storage or switching devices will lose unexported session information.
- Exported CSVs include a pseudonymous participant identifier, food condition, scheduled and actual times, glucose readings and optional notes. Avoid entering participant names or personally identifying medical information.
- The 90-minute iAUC is calculated from positive area above baseline. Every measurement must be present, measured times must increase, and an observed reading must reach at least 90 minutes. If the last reading is beyond 90 minutes, the line between the preceding and final recorded values is interpolated to 90 minutes. It does not infer missing intermediate data.
- Classroom observations do not directly quantify intestinal glucose absorption or constitute formal glycaemic index testing.
- Class means use measurements by scheduled time; individual iAUC uses actual times. Only descriptive statistics are calculated.
- To explore without collecting blood samples, click **Explore demonstration** on the setup page and **Load example class data** on the lecturer page. All example data are synthetic and labelled.
- The experimental timer uses the device clock. Audible reminders can only play while the page is open and active; do not rely on them as the sole sampling reminder.
- Access to the lecturer interface is not restricted. The class-comparison and food-configuration tools are intentionally local and non-sensitive; it is not an authenticated staff portal.

## Run tests

With Node.js 18+:

```bash
node tests/analysis.test.mjs
```

No package installation is necessary.

## Files

- `index.html` — accessible layout and five functional views
- `styles.css` — responsive styling
- `app.js` — local state, timer, questions, graph rendering, exports and lecturer workflow
- `analysis.mjs` — tested numerical calculations, CSV parsing and aggregation
- `tests/analysis.test.mjs` — maths and CSV integration tests

The `examples/` folder contains six labelled synthetic team CSV files. These can be imported together from the Lecturer analysis screen to check the complete aggregation workflow before class.