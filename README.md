# H5P Theming
- [H5P Theming](#h5p-theming)
  * [Overview](#overview)
  * [Requirements](#requirements)
  * [Installation](#installation)
  * [How does it work?](#how-does-it-work-)
      - [Notes](#notes)
  * [Modification](#modification)
    + [Out of the box](#out-of-the-box)
    + [Theme expansion](#theme-expansion)
  * [Adding the theme to H5P](#adding-the-theme-to-h5p)
  * [FAQs](#faqs)
 
## Overview
**Description:** This is a custom theme to override the default blue H5P theme. This theme will apply font, border and background colours to select content types. It will not alter the UI of the H5P editor dashboard.

**Tested with:** H5P.com (SaaS). *May* also work with self-hosted and H5P.org

**Environment:** It is recommended to have a staging environment of H5P to preview and test all theming changes before applying changes organisation wide. Only **Administrators** can add custom CSS to H5P and view content types in Preview mode.

**Content types included in theme:**<br/>
*(**Note:** N/A = no styling necessary)*

- Accordion
- Arithmetic Quiz
- Audio Recorder
- Branching Scenario
- ~~Chart - N/A~~
- ~~Collage - N/A~~
- ~~Column - N/A~~
- Course Presentation
- Dialogue Cards
- Dictation
- Documentation Tool
- Drag and Drop
- Drag the Words
- Emoji Cloud
- ~~Fill in the Blanks - N/A~~
- Flashcards
- Guess the Answer
- Image Hotspot
- Image Slider
- Interactive Book
- Interactive Video
- ~~KewAr Code - N/A~~
- Mark the Words
- Multiple Choice
- Multipoll
- Quiz (Question Set)
- Single Choice Set
- Summary
- ~~Text - N/A~~
- True/False
- Virtual Tour
- Word Cloud

---
## Requirements
- Node.js
- Sass compiler
---
## Installation
1. Download (or clone) the repository by running:  
```$ git clone https://github.com/lauraoatie/h5p-theming.git```
2. After downloading, go to the project directory and run:  
```$ npm install```
3. Start watching for changes to `h5p-styles.scss` by running:  
```$ npm start```
4. Any modifications to `h5p-styles.scss` will automatically compile to `h5p-styles.css`
---
## How does it work?
The Sass colour variables in the table below have been applied to some global H5P components and individual elements across content types. The theming is simple and merely replaces the H5P blue with a different primary colour. 

To theme your H5P instance, specify new colours for the following:

`$primary`<br/>
`$primary-dar`<br/>
`$primary-dar2`<br/>
`$primary-med`

There are minor instances where the properties `filter` and `gradient` utilise hardcoded colour values.

| Variables | Usage |
| ----------- | ----------- |
| Primary colours |  |
|`$black: #262223;`<br/>`$white: #FFFFFF;`<br/>`$primary: #990033;`<br/>`$primary-dar: #c50143;`<br/>`$primary-dar2: #88002d;`<br/>`primary-med: #ec0264;` | <br/><br/>Background colour for buttons and elements.<br/>:hover/:active background or font colour.<br/>:focus  background or font colour.<br/>Gradient background colour. |
| Secondary colours | UI elements |
|`$white-grey: #FAFAFA;`<br/>`$grey-lig: #DEDEDE;`<br/>`$grey-lig2: #C5C5C5;`<br/>`$grey-lig3: #A2A2A2;`<br/>`$grey-med: #333333;`<br/>`$grey-med2: #3a3537;` | |
| Correct/Incorrect colours | (not applied to every instance) |
| `$correct: #9dd8bb;`<br/>`$correct-med: #47b47d;`<br/>`$correct-dar: #255c41;`<br/>`$incorrect: #f7d0d0;`<br/>`$incorrect-med: #dd2e2e;`<br/>`$incorrect-dar: #b71c1c;`| |
| Gamification colours | Arithmetic Quiz|
|`$teal: #45a29f;`<br/>`$teal-dar: #49837E;`<br/>`$orange-med: #b71c1c;`<br/>`$purple: #72518a;`||

#### Notes
- Some H5P content items retain the `:active` psuedo-class and require clicking elsewhere to return to the `link` state. As a result, is recommended to select a suitable accessible `hover/active` colour that is similar to the link colour to avoid a jarring experience for users.
- Text anchors have intentionally been left unstyled and will assume the brower defaults.
- The theme standardises the look of buttons, therefore inconsistently applied box-shadows, transitions, etc. across content types have been removed.
- See **FAQs** for more information on styling particulars.
---
## Modification
**Requirement:** Administrator access to H5P is needed to upload and preview custom styles. 

**Preparation:** Create a suite of content types to use for testing. Ensure all types, where applicable, include:
- Tip text / Hover text / Feedback text
- Show scores
- Enable Retry
- All possible nested content types (e.g. Course Presentation, Interactive Book, etc.)
- Hyperlinks, images, and/or video URLs

***Note:** These steps should be performed on a **staging** instance of H5P prior to deployment to production.*
1. Login to H5P as an Administrator
2. Go to **Manage Content**
3. Click **Add Content** 
4. Create a new content type by selecting from the available content types or select **Upload**

### Out of the box
1. Open the **h5p-theming** folder in a code editor (e.g. Visual Studio Code)
2. Run `npm install`
2. Run `npm start` (any saved changes to h5p-styles.scss will now automatically compile to h5p-styles.css)
3. Open **h5p-styles.scss**
3. Replace the existing colour variable values with your own (search the sheet for `filter` and `gradient` to locate hardcoded instances that require updating)
4. **Save**

### Theme expansion
All styling for individual content types must be included inside `.h5p-content`. Some global UI elements (buttons, progress bars, etc.) exist ouside `.h5p-content` and should be defined first.

Most H5P content types include a useful parent classname (`.h5p-branching-scenario`, `.h5p-multichoice`). In the absence of one, it may be a global class (`.h5p-core-button`, `.joubel-simple-rounded-button`).

**Have your unstyled H5P content item ready to preview**
1. In a browser, login to H5P as an Administrator
2. Go to **Manage Content**
3. Select a test H5P content type that has *not* been included in the theming list above. It will open in **View** mode.
 
**Add your theme colours**

4. Open the **h5p-theming** folder in a code editor
5. Run `npm install`
6. Run `npm start` (any saved changes to h5p-styles.scss will now automatically compile to h5p-styles.css)
6. Open **h5p-styles.scss**
7. Replace the existing colour variable values with your own (search the sheet for `filter` and `gradient` to locate hardcoded instances that require updating). If modifying variable names, perform a find and replace on the file to update all instances.
8. **Save**

**Inspect content type to determine elements for theming**

8. Return to the browser and inspect the test H5P content type you wish to theme
9. Copy/paste selectors and properties suitable for override into **h5p-styles.scss**
10. *Optional:* Only for the brave and to cover all bases. Open the relevant H5P stylesheet(s) from the inspector, then search for the current selector to locate additional usage and styling that may require override
11. In **h5p-styles.scss** replace the pasted H5P colour/s with your theme colour variable/s
12. **Save**
---
## Adding the theme to H5P
1. Once you have modified the theme, copy the contents of **h5p-styles.css**
2. Login to your **staging** instance of H5P, go to **Manage Organisation** > **Settings** > **Custom CSS**
3. Paste the contents of **h5p-styles.css** into the **Preview** textarea
4. **Save settings**
17. To preview changes, refresh the browser window containing your test H5P content type
6. Thoroughly test all interactivity in the content type
7. When theming and testing are complete, click **Copy working.css to organization.css** to enable it organisation wide for others to view
8. Follow these steps when deploying to Production
---
## FAQs
| Question | Answer |
| ----------- | ----------- |
| Can I change the fonts used? | Adjusting the font-family across H5P is not advised unless content types are rigorously tested across browsers and devices. There are *many* typefaces and font icons in use across H5P with no standard unit of measurement (px, em, %), and some elements change in position and size following interaction or at media queries. |
| Can I add assets? | It is not possible to add additional assets during theming (i.e. background images, fonts, scripts etc.) as custom theming via H5P is limited to CSS with no access to asset directories.  |
| Can I change existing assets? | It is possible in some instances to target the `:before` or `content` properties to make adjustments if you can ascertain the font icon libraries used, however it is not advised. Minor blue-based icons and images that could not be overriden remain. |
| Why are hyperlinks blue? | Text hyperlinks have intentionally been left unstyled and will assume the brower defaults. This is due to the multitude of background colours in use across H5P and the ability of Authors to set unique background colours to some elements as they create content. If adjusting link colours, rigorous testing is required for all content types to ensure sufficient contrast is present for accessibility. |
| Why can't I just do a find and replace on the H5P stylesheet and use that as my theme? | There are multiple stylesheets in use by H5P, over 30 shades of blue applied across the H5P items covered by this theme, and a blanket approach would also affect the H5P UI dashboards. This theme is designed to only target the bare essentials. |
| My styles aren't working or have stopped working | 1. Check your Sass syntax<br/>2. Try placing your block outside `.h5p-content {}`<br/>3. Ensure changes are Saved<br/>4. Hard-refresh your browser to view changes<br/>5. The content type may have been by H5P and requires restyling |
