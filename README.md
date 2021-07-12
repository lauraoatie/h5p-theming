# H5P Theming
- [H5P Theming](#h5p-theming)
  * [Overview](#overview)
  * [Requirements](#requirements)
  * [Installation and usage](#installation-and-usage)
  * [Deployment to H5P.com](#deployment-to-h5pcom)
  * [Using your own colours](#using-your-own-colours)
      - [Notes](#notes)
  * [Theme expansion](#theme-expansion)
    + [Preparation](#preparation)
    + [Guidelines](#guidelines)
    + [Styling elements](#styling-elements)
  * [FAQs](#faqs)
 
## Overview
**Description:** This is a custom theme to override the default blue H5P theme. This theme will apply font, border and background colours to select content types. It will not alter the UI of the H5P editor dashboard.

**Tested with:** H5P.com (SaaS). *May* also work with self-hosted and H5P.org

**Environment:** It is recommended to have a staging environment of H5P to preview and test all theming changes before applying changes organisation wide. Only **Administrators** can add custom CSS to H5P and view content types in Preview mode.

**Content types included in theme:**<br/>

| Content types | | |
| ----------- | ----------- | ----------- |
| Accordion | Drag and Drop | Mark the Words |
Arithmetic Quiz | Drag the Words | Multiple Choice |
Audio Recorder | Emoji Cloud | Multipoll |
Branching Scenario | ~~Fill in the Blanks - N/A~~ | Quiz (Question Set) |
~~Chart - N/A~~ | Flashcards | Single Choice Set |
~~Collage - N/A~~ | Guess the Answer | Summary |
~~Column - N/A~~ | Image Hotspot | ~~Text - N/A~~ |
Course Presentation | Image Slider | True/False |
Dialogue Cards | Interactive Book | Virtual Tour |
Dictation | Interactive Video | Word Cloud |
Documentation Tool | ~~KewAr Code - N/A~~ |

*(**Note:** N/A = no individual styling necessary or item uses global styles)*

---
## Requirements
- Node.js
- Sass compiler
---
## Installation and usage
1. Download (or clone) the repository by running:  
```
$ git clone https://github.com/lauraoatie/h5p-theming.git
```
2. After downloading, go to the project directory and run:  
```
$ npm install
```
3. Start watching for changes to `h5p-styles.scss` by running:  
```
$ npm start
```
4. Any modifications to `h5p-styles.scss` will automatically compile to `h5p-styles.css`

See [Using your own colours](#using-your-own-colours) and [Theme expansion](#theme-expansion) for theming guidance.

---
## Deployment to H5P.com
**Requirement:** Administrator access to H5P is needed to upload custom styles. 
1. Once you have modified the theme, copy the contents of `h5p-styles.css`
2. Login to H5P.com, go to **Manage Organisation** > **Settings** > **Custom CSS**
3. Paste the contents of `h5p-styles.css` into the **Preview (Working.css)** field
4. Click **Save settings**
5. Open each of the content types from the table above to view and test the changes
6. When you are ready to deploy changes to all users, click **Copy working.css to organization.css** to enable it organisation wide

---
## Using your own colours
The Sass colour variables in the table below have been applied to some global H5P components and individual content types. The theming is simple and merely replaces the H5P blue with a different color-primary colour. 

To theme your H5P instance, specify new colours for the following:

`$color-primary`<br/>
`$color-primary-medium`<br/>
`$color-primary-dark`<br/>
`$color-primary-darker`

There is a minor instance where the property `filter` utilises a hardcoded colour value.

| Variables | Usage |
| ----------- | ----------- |
| Primary colours |  |
|`$black: #262223;`<br/>`$white: #FFFFFF;`<br/>`$color-primary: #990033;`<br/>`$color-primary-dark: #c50143;`<br/>`$color-primary-darker: #88002d;`<br/>`$color-primary-medium: #ec0264;` | <br/><br/>Background colour for buttons and elements.<br/>:hover/:active background or font colour.<br/>:focus  background or font colour.<br/>Gradient background colour. |
| Secondary colours | UI elements |
|`$color-off-white: #FAFAFA;`<br/>`$color-grey-lightest: #DEDEDE;`<br/>`$color-grey-lighter: #C5C5C5;`<br/>`$color-grey-light: #A2A2A2;`<br/>`$color-grey-medium: #333333;`<br/>`$color-grey-medium-dark: #3a3537;` | |
| Correct/Incorrect colours | (not applied to every instance) |
| `$color-correct: #9dd8bb;`<br/>`$color-correct-medium: #47b47d;`<br/>`$color-correct-dark: #255c41;`<br/>`$color-incorrect: #f7d0d0;`<br/>`$color-incorrect-medium: #dd2e2e;`<br/>`$color-incorrect-dark: #b71c1c;`| |
| Gamification colours | Arithmetic Quiz|
|`color-game-1: #45a29f;`<br/>`$color-game-1-medium: #49837E;`<br/>`$color-game-2: #b71c1c;`<br/>`$color-game-3: #72518a;`||

#### Notes
- Some H5P content items retain the `:active` psuedo-class and require clicking elsewhere to return to the `link` state. As a result, is recommended to select a suitable accessible `hover/active` colour that is similar to the link colour to avoid a jarring experience for users.
- Text anchors have intentionally been left unstyled and will assume the browser defaults.
- The theme standardises the look of buttons and other elements, therefore inconsistently applied box-shadows, transitions, etc. across content types have been removed.
- See [**FAQs**](#faqs) for more information on styling particulars.
---
## Theme expansion
**Requirement:** Administrator access to H5P is needed to upload and preview custom styles. 

### Preparation
Create instances of any content types that you wish to theme. Ensure all types, where applicable, include:
- Hyperlinks, images, and/or video URLs
- Tip text / Hover text / Feedback text
- Show scores
- Enable Retry
- All possible nested content types (e.g. Course Presentation, Interactive Book, etc.)

### Guidelines
All styling for individual content types must be included inside `.h5p-content`. Some global UI elements (buttons, progress bars, etc.) exist outside `.h5p-content` and should be defined first.

Most H5P content types include a useful parent class name (`.h5p-branching-scenario`, `.h5p-multichoice`). In the absence of one, it may be a global class (`.h5p-core-button`, `.joubel-simple-rounded-button`).

### Styling elements

1. Open the content type in your browser and inspect the element you wish to theme
2. Copy/paste selectors and properties suitable for override into `h5p-styles.scss`
3. *Optional: (Only for the brave and to cover all bases)* Open the relevant H5P stylesheet(s) from the inspector, then search for the current selector to locate additional usage and styling that may require override
4. Consider using one of the existing Sass variables as the new property value

---
## FAQs
| Question | Answer |
| ----------- | ----------- |
| Can I change the fonts used? | Adjusting the font-family across H5P is not advised unless content types are rigorously tested across browsers and devices. There are *many* typefaces and font icons in use across H5P with no standard unit of measurement (px, em, %), and some elements change in position and size following interaction or at media queries. |
| Can I add assets? | While it is possible to add addtional theme assets (i.e. background images, fonts, scripts etc.), these assets cannot be hosted on H5P.com, you would need to use another hosting provider. |
| Can I change existing assets? | It is possible in some instances to target the `:before` or `content` properties to make adjustments if you can ascertain the font icon libraries used, however it is not advised. Minor blue-based icons and images that could not be overriden remain. |
| Why are hyperlinks blue? | Text hyperlinks have intentionally been left unstyled and will assume the browser defaults. This is due to the multitude of background colours in use across H5P and the ability of Authors to set unique background colours to some elements as they create content. If adjusting link colours, rigorous testing is required for all content types to ensure sufficient contrast is present for accessibility. |
| Why can't I just do a find and replace on the H5P stylesheet and use that as my theme? | There are multiple stylesheets in use by H5P, over 30 shades of blue applied across the H5P items covered by this theme, and a blanket approach would also affect the H5P UI dashboards. This theme is designed to only target the bare essentials. |
| My styles aren't working or have stopped working | 1. Check your Sass syntax<br/>2. Try placing your block outside `.h5p-content {}`<br/>3. Ensure changes are Saved<br/>4. Hard-refresh your browser to view changes<br/>5. The content type may have been updated by H5P and requires restyling |
