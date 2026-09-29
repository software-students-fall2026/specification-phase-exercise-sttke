# Specification Phase Exercise — The Slide Machine

This repository proposes improvements to The Slide Machine, which generates lecture slides from spoken teaching and can create a post-lecture quiz. Our design follows the material from preparation and generation through editing, sharing, and student review. Existing capabilities provide the starting point; the proposed interactions improve their clarity, continuity, and recovery from problems.

## Team members

- _Spark Fan___________________ — integration and documentation (A)
- _Tony Zibo Zhou___________________ — instructor research (B)
- _Yutong Xiao___________________ — student research (C)
- _Tony Dong___________________ — wireframes (D)
- _Kevin Han___________________ — clickable prototype (E)

## Review of the current application

| # | Strength / weakness / gap | Specific observation in the live app | Task or screen | Observer |
| --- | --- | --- | --- | --- |
| 1 | Strength | Create account and Sign in put Sign up with Google / Sign in with Google above the email form, and "Forgot your password?" opens a Reset your password page that explains itself in one sentence. | Create account / Sign in | A |
| 2 | Strength | With the microphone off, the empty lecture page says to click the + or microphone icons to start adding content; hovering the mic shows "Speak to add slides"; once on, it says "Start speaking to generate slides". | Lecture page (live capture) | E |
| 3 | Strength | Lecture settings states that the settings apply to just this lecture, links to project-wide settings, explains that a blank Lecture title lets the AI title it from speech, and marks Seed notes "Saved automatically". | Lecture settings · General | D |
| 4 | Strength | A shared deck (Fishing for squid) renders in its NYU design with a 1 / 7 counter, up and down votes, fullscreen, a translate dropdown and a per-slide menu offering "Speak this slide". | Deck viewer | C |
| 5 | Strength | Plans states "Every plan includes every feature. What changes is how much of each you may use", shows a check for all eight features in every column, and marks Free as "Your plan". | Plans | A |
| 6 | Strength | The Add seed material dialog explains itself ("Give the AI background for this lecture before you begin. Optional — you can add more anytime"), offers Seed notes and a PDF, DOCX, TXT or photo upload, and can be skipped. | Add seed material dialog | B |
| 7 | Weakness | In Discover, three lectures by Levi Gilbert-Adler show the project as `<="` and the author as `Levi Gilbert-Adler<"=`, while every other row shows a readable project name such as Default project. | Home /app · Discover | B |
| 8 | Weakness | The Add seed material dialog that follows + New lecture has no title field; the breadcrumb already reads Untitled lecture, and the Lecture title field lives in Lecture settings · General. | Add seed material dialog | E |
| 9 | Weakness | For a newly created lecture with 0 slides, General access is already Public ("Anyone on the internet with the link can view") while People with access reads "Only you have access so far". | Lecture settings · Privacy & Sharing | E |
| 10 | Weakness | The "1 / 7" slide counter under the slide is half hidden behind the footer bar that carries "API ok" and "Free plan ok". | Deck viewer | D |
| 11 | Weakness | In List view the fullscreen icon is drawn on top of the downvote count at the top right, so the two controls overlap. | Deck viewer · List view | D |
| 12 | Weakness | The page behind the Default project breadcrumb is headed "Default project · Christina Lin" yet lists the observer's own Untitled lecture (0 slides) beside her Fishing for squid, one owner name above two people's lectures. | Project page | E |
| 13 | Weakness | In the observation session with Chel, instructions spoken to the app while presenting were transcribed into the slide as content instead of being treated as commands. | Lecture page (live capture on) | C |
| 14 | Weakness | In the two teacher sessions, both teachers, after seeing the landing page ("Speak freely — the slides will follow") and Home, said they were unsure what the app was for and where templates or materials live. | Landing page / Home /app | B |
| 15 | Gap | The menu drawer lists Home, Profile, Account settings, About us, Send feedback, Privacy policy, Terms & conditions and Log out; no entry leads to the user's own projects or lectures. | Menu drawer | C |
| 16 | Gap | Both General access options are described in terms of "the link" ("with the link can view", "open with the link"), yet the Privacy & Sharing tab shows no link and no copy control. | Lecture settings · Privacy & Sharing | B |
| 17 | Gap | Once the microphone is on, the page shows the red mic, "Start speaking to generate slides" and, while speaking, a caption line; no elapsed time or remaining Audio recording time, which Plans meters, appears. | Lecture page (live capture on) | E |
| 18 | Gap | Discover offers only the Latest and Top tabs and a search box for "lectures, projects, people"; there is no way to narrow the list by course or topic. | Home /app · Discover | A |

**Research context, separate from the live-app review:** instructor interviewees reported unclear purpose and category labels, difficulty finding material and templates, and time spent manually adjusting slides. Student interviewees liked the basic speech-to-slide workflow but reported context loss, hard-to-find editing controls, and limited study support. These reports inform the proposal; they do not replace the team observations required above.

## Prior art and originality

We compared the proposed work with the upstream [software design document, especially §18 Future Work and §19 Open Questions](https://github.com/bloombar/slide-machine/blob/better-faster/docs/SPEC.md), its [delivery roadmap](https://github.com/bloombar/slide-machine/blob/better-faster/docs/ROADMAP.md), and the [open issues](https://github.com/bloombar/slide-machine/issues) and [pull requests](https://github.com/bloombar/slide-machine/pulls). The review was last performed on 27 September 2026; the upstream default branch was `better-faster`. Recheck these moving sources before submission.

Existing or specified capabilities already include seed material, a template library, automatic layout choice, editing, deck sharing, quizzes, and Google Slides export. Real-time collaborative editing is explicitly listed as upstream future work. We therefore describe material reuse, template choice, Google Slides export, and collaboration as improvements to existing/planned workflows, **not** newly invented capabilities. Our proposed contribution is the interaction design that connects a guided preparation path and pre-share review to student summaries, questions linked to source slides, and active recall with recoverable failures. The design itself requires team and stakeholder validation; we do not claim an unverified exclusive implementation idea.

## Stakeholders

The instructor findings below come from the supplied B research document. It reports interviews with two teachers but combines many findings rather than attributing each point to a particular individual. The student findings come from the existing C research in this repository. Interviewees are identified by role or pseudonym; full names and contact details should be shared privately with the course staff, not published in this README.

### Instructor stakeholders (B)

| Participant | Context | Reported needs | Reported difficulties |
| --- | --- | --- | --- |
| Teacher 1 | College Radiation Physics instructor | Prepare lectures more quickly, reuse teaching content, find relevant resources, reduce formatting, understand the tool's purpose | B reports unclear app purpose, difficult discovery, unclear categories, and manual work across the two teachers; it does not reliably assign each difficulty to Teacher 1. |
| Teacher 2 | Community nonprofit English teacher who also leads after-class childcare | Prepare lectures more quickly, reuse teaching content, find relevant resources, reduce formatting, understand the tool's purpose | B reports the same combined themes but does not reliably assign each difficulty to Teacher 2. |

Across the two interviews, the needs are (1) less preparation time, (2) generation based on existing content, (3) easier template/material discovery, (4) less manual formatting, and (5) an understandable starting point. The reported frustrations are (1) unclear app purpose, (2) hard-to-find templates/materials, (3) unclear categories, (4) time-consuming manual preparation, and (5) manual layout adjustment.

#### Interview notes from B (added verbatim from partB_TeacherResearch.docx)

**Teacher participants.** We interviewed two teachers to understand their current workflow for preparing lecture materials and their experience using The Slide Machine.

- Teacher 1: Teaches Radiation Physics in the college.
- Teacher 2: Teaches community nonprofit English courses and leads an after-class childcare for kids.

The interviews focused on how teachers currently prepare slides and quizzes, what they found difficult when using The Slide Machine, and what improvements could make the preparation process easier.

**Teacher goals and needs.** Based on the interviews, the following teacher needs were identified:

- Reduce preparation time — Teachers want to spend less time preparing lecture materials and formatting slides.
- Generate slides from existing teaching content — Teachers would like to provide existing materials or content and have the system generate related slides.
- Find relevant templates and materials more easily — Teachers need a clearer way to locate appropriate templates and teaching materials.
- Reduce manual slide formatting — Teachers would like the system to automatically arrange slide layouts instead of requiring extensive manual adjustments.
- Understand the purpose of the application clearly — Teachers need to understand how The Slide Machine can support their lecture-slide preparation before they can use it effectively.

**Teacher problems / pain points.** The interviews identified the following problems:

- The purpose of the application is not immediately clear. One teacher was unsure how the application could help with lecture slides.
- Finding templates and materials can be difficult. One teacher reported that it was initially difficult to find appropriate templates and materials.
- The categories are not sufficiently clear. One teacher reported that the categories were unclear, making it take longer to find relevant resources.
- Slide preparation requires too much manual work. One teacher reported that making slides takes too much time because many elements still need to be adjusted manually.
- Manual layout adjustment increases preparation effort. One teacher specifically suggested that automatic layout arrangement would make the process easier.

**Teacher user requirements.**

- Clear guidance and onboarding — Provide clear instructions and guidance so teachers can quickly understand what The Slide Machine does, how it can help with lecture preparation, and how to use its main features.
- Faster slide preparation — Reduce the time teachers need to spend creating and preparing lecture slides.
- Generate slides from existing materials — Allow teachers to provide existing teaching materials or lecture content and generate related slides automatically.
- Automatic slide layout — Automatically arrange text, images, and other content into a clear slide layout instead of requiring teachers to adjust everything manually.
- Clearer template and material categories — Organize templates and teaching materials into clear and understandable categories.
- Easier template and material discovery — Make it easier for teachers to browse, search for, and select appropriate templates and teaching materials.
- Reuse existing teaching content — Allow teachers to use content they have already prepared instead of creating materials from scratch.
- Easy editing and customization — Allow teachers to easily adjust generated slides when the content or layout needs to be changed.
- Review generated materials — Allow teachers to review and modify generated materials before using or sharing them.
- Reduce repetitive preparation work — Automate repetitive tasks involved in creating and formatting teaching materials.

### Student stakeholders (C)

**Chel — student and presentation author.** Chel valued the speed of speech-to-slide creation but reported lost context between slides, awkward editing, uncertain language settings, difficult navigation in long decks, and difficulty locating image upload, undo/history, and export. Chel also wanted group collaboration, Google Slides compatibility, short review material, and active recall. Spoken instructions were sometimes treated as slide content.

**Lan — student and presentation author.** Lan found the basic generation process easy to learn but had difficulty with settings, controls, text/visual editing, adding images, sharing, and finding previous work. Lan wanted timing and rehearsal assistance, support for group presentations, important concepts, and related practice questions.

Together, their needs include faster presentation creation, flexible editing, coherent generated content, group collaboration, familiar export options, presentation preparation, concise review, and active practice. Their frustrations include context loss, hard-to-find controls, awkward editing, long-deck navigation, weak group workflows, limited rehearsal support, study material disconnected from practice, and speech instructions appearing as slide content.

#### Interview notes from C (added verbatim from the C research README)

**Stakeholder 1 — Chel.** Role: Student / Student Presenter-Author. Key findings: Student 1 found the speech-to-slide generation process efficient and easy to understand, especially the ability to turn rough spoken ideas into structured slides. However, the student experienced context loss between slides, awkward manual editing, unclear language-setting behavior, difficulty navigating longer decks, and problems finding functions such as image upload, undo/history, and PPTX export. As a student presenter, the student emphasized the need for real-time group collaboration and better compatibility with Google Slides. As a learner, the student wanted condensed review materials, AI questioning, and active-recall practice. The student also found that when giving spoken instructions to the AI, the system sometimes treated those instructions as presentation content and inserted them into the slide as bullet points instead of interpreting them as commands.

**Stakeholder 2 — Lan.** Role: Student / Student Presenter-Author. Key findings: Student 2 found the interface simple and understood the basic presentation-generation workflow quickly. However, the student had difficulty with language settings, unfamiliar button behavior, limited text and visual editing, image insertion, sharing, and locating previously generated material. For presentation work, the student wanted presenter view, duration control, rehearsal feedback, progressive reveal, citations, editable charts, and stronger support for group presentations. For studying, the student wanted automatic extraction of important concepts and practice questions directly connected to those concepts.

**Student goals / needs**

1. Efficient presentation creation — Students want to quickly transform rough spoken ideas into structured slides without starting from a blank presentation.
2. Flexible slide editing — Students want to freely edit text, images, layouts, and formatting after AI generation.
3. Real-time group collaboration — Students want multiple teammates to work on the same presentation simultaneously and see one another's changes.
4. Compatibility with existing presentation tools — Students want presentations to work smoothly with tools such as Google Slides and PowerPoint.
5. Coherent content across slides — Students want generated slides to maintain context and logical continuity throughout a presentation.
6. Presentation delivery and rehearsal support — Students want tools such as duration control, presenter view, and rehearsal feedback to prepare for class presentations.
7. Efficient exam review — Students want long lecture decks condensed into key concepts, summaries, or cheat sheets.
8. Active learning and practice — Students want AI-generated questions, active recall, and verbal practice to help them evaluate their understanding.

**Student problems / frustrations**

1. Context can be lost between generated slides — Later slides may fail to follow logically from earlier content.
2. Manual editing is limited or awkward — Adjusting text, layout, images, and formatting can be more difficult than in familiar presentation tools.
3. Some controls are difficult to discover or understand — Students had difficulty locating language settings, image upload, undo/history, export, and sharing functions.
4. System feedback is sometimes unclear — Students were sometimes unsure whether an action, such as changing language settings or opening a menu, had succeeded.
5. Long decks can be difficult to navigate — Missing or unclear page numbering, history, or overview features make it harder to locate specific content.
6. Group presentation workflows are limited — Students expected stronger support for simultaneous editing and collaboration on group assignments.
7. Presentation preparation tools are incomplete — Students wanted support for timing, rehearsal, presenter notes, and presentation delivery after the slides were generated.
8. Lecture materials offer limited active study support — Students wanted stronger connections between summaries, important concepts, practice questions, and active recall.
9. Spoken instructions can be mistaken for slide content — When students give the AI instructions about how to modify or generate a presentation, the system may treat those commands as content and place them directly into the slide as bullet points, making it difficult to distinguish between instructions and material intended for the audience.

## Product vision statement

The Slide Machine should guide instructors and student presenters from reusable material to a coherent, reviewable deck, then let students follow that deck into concise, source-linked review and practice, with clear feedback when a step fails.

## User requirements

Existing capabilities named below are starting points. Each story specifies a new or changed interaction, not a claim that the underlying capability is missing. IDs connect stories to the design artifacts.

### Instructor user stories (B)

1. **T01** — As a first-time instructor, I want task-based guidance that shows how lecture preparation works, so that I know where to start.
2. **T02** — As an instructor preparing a lecture, I want a visible path from source material to deck review, so that I can finish preparation without searching for the next step.
3. **T03** — As an instructor with existing material, I want to see what source content was accepted before generating, so that I know what the deck will use.
4. **T04** — As an instructor reviewing slides, I want a suitable automatic layout and an easy way to choose an alternative, so that layout correction takes less time.
5. **T05** — As an instructor browsing designs, I want understandable categories with previews, so that I can choose a template appropriate to my lecture.
6. **T06** — As an instructor searching templates or material, I want filters and a useful no-results state, so that an unsuccessful search does not stop me.
7. **T07** — As an instructor starting another lecture, I want to identify and reuse previous teaching material, so that I do not reenter it.
8. **T08** — As an instructor correcting generated slides, I want a direct edit path that preserves unaffected work, so that I do not have to regenerate the whole deck.
9. **T09** — As an instructor about to teach or share, I want to review the deck and any unresolved items first, so that I can correct them before others see it.
10. **T10** — As an instructor repeating preparation tasks, I want relevant prior choices to be offered for confirmation, so that I can avoid unnecessary repeated setup.

### Student user stories (C)

1. **S01** — As a student presenter, I want to edit a presentation with teammates in real time, so that we can see each other's progress.
2. **S02** — As a student presenter, I want a clear transfer path to Google Slides, so that my team can keep using its familiar tools.
3. **S03** — As a student presenter, I want generated slides to preserve earlier context, so that the deck remains logically coherent.
4. **S04** — As a student presenter, I want undo and accessible version history, so that I can recover content after a mistake.
5. **S05** — As a student presenter, I want to upload and replace slide images directly, so that I can use the visuals I need.
6. **S06** — As a student presenter, I want to set a target duration, so that my presentation fits the assignment time limit.
7. **S07** — As a student presenter, I want rehearsal feedback on timing, speaking pace, and filler words, so that I can practice before presenting.
8. **S08** — As a student, I want a concise summary of a lecture deck, so that I can review important ideas before an exam.
9. **S09** — As a student, I want practice questions connected to their concepts and source slides, so that I know what to revisit.
10. **S10** — As a student, I want to explain a concept aloud and receive feedback on missed points, so that I can practice active recall rather than only reread slides.
11. **S11** — As a student presenter, I want the system to distinguish spoken editing commands from slide content, so that instructions do not become audience-facing bullets.

**Cross-role rule:** a shared deck and its study material must respect the deck's access settings. A generated summary or question should point to its source slide, and a failed upload or generation should preserve material the user has already supplied. Real-time collaboration (S01) remains overlapping upstream future work, while Google Slides export (S02) is an improvement to an existing capability.

## Activity diagrams

### B1 — Getting started and creating slides

**Story:** T03 — As an instructor with existing material, I want to see what source content was accepted before generating, so that I know what the deck will use.

![B1 — Getting started and creating slides (activity diagram from B)](images/instructor-getting-started-activity.jpeg)

### B2 — Finding and using templates

**Story:** T05 — As an instructor browsing designs, I want understandable categories with previews, so that I can choose a template appropriate to my lecture.

![B2 — Finding and using templates (activity diagram from B)](images/instructor-templates-activity.jpeg)

### C1 — Real-time collaboration

**Story:** S01 — As a student presenter, I want to edit a presentation with teammates in real time, so that we can see each other's progress.

![Student Real-Time Collaboration Activity Diagram](images/student-collaboration-activity.png)

### C2 — Active recall

**Story:** S10 — As a student, I want to explain a concept aloud and receive feedback on missed points, so that I can practice active recall rather than only reread slides.

![Student Active Recall Activity Diagram](images/student-active-recall-activity.png)

## Wireframes (D)

[Open the Figma design: D Wireframes — B+C complete](https://www.figma.com/design/xSlHrGphQWleYhSJwaD4ST?node-id=7-2). It contains 27 black-and-white screens and states; the former v1 page was removed.

| Role | Screens covered | Main requirements |
| --- | --- | --- |
| Instructor | Home/guidance, new lecture, source selection and upload failure, template browser/no result/preview, generation/progress/failure, slide editing, pre-share review, sharing permissions (T01–T12) | T01–T10 |
| Student reader | Shared deck, summary, concept-linked question, answer feedback, active recall input and feedback (S01–S06 in **Figma screen naming**) | S08–S10 |
| Student presenter | Dashboard, live collaboration, version history, image replacement, target duration, rehearsal and feedback, export, spoken-command confirmation (S07–S15 in **Figma screen naming**) | S01–S07, S11 |

Figma frame numbers identify screens; the **user-story IDs above identify requirements**. Their numbers are intentionally independent. The screens are design proposals and do not assert that all 27 interactions exist in the current product.

#### Existing screens changed by the proposal

Nothing that exists today is renamed or removed. The rows below are the only changes to existing screens; every other existing screen in the prototype is reused as it is.

| Existing screen | Change after the proposal | Wireframe |
| --- | --- | --- |
| Menu drawer | A new item **My presentations** sits between Profile and Account settings and opens S07. Every other item keeps its place. | <img src="images/wireframes/Menu-drawer.png" width="360" alt="Menu drawer after the change"> |
| Home /app | **+ New lecture** and the **+** button open T02 Create a lecture, the guided path through the Material, Design, Generate, Review and Share steps, instead of opening the Add seed material dialog directly. For a student, a lecture row in Discover opens S01 Shared lecture reader. The layout is unchanged. | Layout unchanged |
| Project page | For a student, a lecture card opens S01 Shared lecture reader. The layout is unchanged. | Layout unchanged |
| Lecture page with live capture on | When the live caption contains an editing instruction, the S15 Confirm spoken instruction overlay appears over the page. The page itself is unchanged. | See S15 below |
| Lecture settings › Privacy & Sharing | Unchanged. S08 Invite teammates and T12 Copy and share lead here, so sharing keeps its current place. | Layout unchanged |

**Moves, stated explicitly.** The Add seed material dialog that opens after + New lecture is replaced as the first step by the Material step (T02–T04), which asks for the same lecture title, notes and files; Lecture settings › General still holds them afterwards. The Design step (T05–T07) is a guided way into the design choice that Lecture settings › Design offers today; that tab stays. S14 Export presentation is reached from an Export button on the group deck (S08) and offers Google Slides, PDF and YAML; the existing Lecture settings › Export tab stays.

#### Screen index

The prototype screens carry the live app's header and footer so that a reviewer recognises where they are; layout and content follow D's Figma wireframes. Full-size PNG exports are in [images/wireframes](images/wireframes).

**Instructor (T01–T12)**

| Screen | What the instructor sees | Wireframe |
| --- | --- | --- |
| T01 Prepare your next lecture | First-time start page: Your lectures with Open lecture, the four Getting started steps, See how it works, Create a lecture. | <img src="images/wireframes/T01.png" width="360" alt="T01 Prepare your next lecture"> |
| T02 Create a lecture | Step Material: Lecture title, Project, Recent lectures with Browse previous; Cancel, Continue. | <img src="images/wireframes/T02.png" width="360" alt="T02 Create a lecture"> |
| T03 Add teaching material | Upload a file (PDF, DOCX or TXT) or Reuse material through Find previous material; Back, Continue. | <img src="images/wireframes/T03.png" width="360" alt="T03 Add teaching material"> |
| T04 Upload failure | "File could not be added"; the material already selected is kept; Cancel, Try again, Choose a file. | <img src="images/wireframes/T04.png" width="360" alt="T04 Upload failure"> |
| T05 Choose a design | Step Design: Search designs, category list, design cards with Preview; Back, Continue. | <img src="images/wireframes/T05.png" width="360" alt="T05 Choose a design"> |
| T06 No matching designs | Empty state with Clear filters and Browse all designs; the source material stays selected. | <img src="images/wireframes/T06.png" width="360" alt="T06 No matching designs"> |
| T07 Preview a design | Large preview with design notes; Customize, Use this design. | <img src="images/wireframes/T07.png" width="360" alt="T07 Preview a design"> |
| T08 Generating slides | Step Generate: status line and progress bar, Return home; the deck opens in T10 when generation finishes. | <img src="images/wireframes/T08.png" width="360" alt="T08 Generating slides"> |
| T09 Generation failure | "Slides could not be generated"; notes and design selection are safe; Edit material, Cancel, Retry. | <img src="images/wireframes/T09.png" width="360" alt="T09 Generation failure"> |
| T10 Edit generated deck | Slide rail, slide preview, Edit tools (Edit text, Change layout, Replace image, Add slide), Review deck. | <img src="images/wireframes/T10.png" width="360" alt="T10 Edit generated deck"> |
| T11 Review before sharing | Slide list, review status (slides checked, items to inspect), Open slide, Mark reviewed; Back to edit, Share lecture. | <img src="images/wireframes/T11.png" width="360" alt="T11 Review before sharing"> |
| T12 Share lecture | Who can view, Lecture link; Cancel, Copy and share. | <img src="images/wireframes/T12.png" width="360" alt="T12 Share lecture"> |

**Student reader (S01–S06)**

| Screen | What the student sees | Wireframe |
| --- | --- | --- |
| S01 Shared lecture reader | Slide rail, slide preview, Concepts panel, Study this deck, Previous and Next. | <img src="images/wireframes/S01.png" width="360" alt="S01 Shared lecture reader"> |
| S02 Lecture summary | Concept list and Key ideas, each with View slide; Back to deck, Practice concepts. | <img src="images/wireframes/S02.png" width="360" alt="S02 Lecture summary"> |
| S03 Practice question | Question card with options; View source slide, Submit answer. | <img src="images/wireframes/S03.png" width="360" alt="S03 Practice question"> |
| S04 Practice feedback | What you understood, What to revisit, source slide thumbnail; Try again, Next question, Open source slide. | <img src="images/wireframes/S04.png" width="360" alt="S04 Practice feedback"> |
| S05 Explain a concept aloud | Transcript area, Start recording, Type instead, and the fallback note for a denied microphone; Back. | <img src="images/wireframes/S05.png" width="360" alt="S05 Explain a concept aloud"> |
| S06 Recall feedback | Covered and Missing points, Lecture reference; Explain again, Next concept, View source. | <img src="images/wireframes/S06.png" width="360" alt="S06 Recall feedback"> |

**Student presenter (S07–S15)**

| Screen | What the student presenter sees | Wireframe |
| --- | --- | --- |
| S07 My presentations | Group presentation card (teammates, slides) with Open presentation and Share with team; Recent work; New presentation. | <img src="images/wireframes/S07.png" width="360" alt="S07 My presentations"> |
| S08 Group deck | Slide rail with slide owners, slide preview, Collaborators panel; Invite teammates, Export, Version history, Present. | <img src="images/wireframes/S08.png" width="360" alt="S08 Group deck"> |
| S09 Version history | Version list and preview; Cancel, Restore this version. | <img src="images/wireframes/S09.png" width="360" alt="S09 Version history"> |
| S10 Replace image | Slide preview and Select a visual (Choose an image, Browse library); Cancel, Replace image. | <img src="images/wireframes/S10.png" width="360" alt="S10 Replace image"> |
| S11 Presentation timing | Target duration, Estimated timing with slides that need shorter delivery; Cancel, Save target. | <img src="images/wireframes/S11.png" width="360" alt="S11 Presentation timing"> |
| S12 Practice your talk | Slide preview, Practice timer, Start rehearsal; Exit practice, Finish and review. | <img src="images/wireframes/S12.png" width="360" alt="S12 Practice your talk"> |
| S13 Rehearsal feedback | Duration, pace, filler words, per-slide timeline; Back to deck, Practice again. | <img src="images/wireframes/S13.png" width="360" alt="S13 Rehearsal feedback"> |
| S14 Export presentation | Google Slides, PDF or YAML; Cancel, Export. | <img src="images/wireframes/S14.png" width="360" alt="S14 Export presentation"> |
| S15 Confirm spoken instruction | Detected instruction shown over the live deck; Add as slide text, Apply edit, Cancel. | <img src="images/wireframes/S15.png" width="360" alt="S15 Confirm spoken instruction"> |

## Clickable prototype (E)

**Public prototype:** [Slide Machine Prototype on Figma — anyone with the link can view, no login needed](https://www.figma.com/proto/KisgOB8gz8FuthCTWzZcll/Slide-Machine-Prototype?node-id=9-100&scaling=min-zoom&content-scaling=fixed&starting-point-node-id=9%3A100&show-proto-sidebar=1&page-id=0%3A1)

The prototype is one Figma page with 43 screens: 16 wireframes of existing screens (Landing, Log in, Register, Forgot password, Home, Menu drawer, Project page, Lecture page with live capture off and on, Add seed material, Lecture settings, Privacy & Sharing, Deck viewer, Account settings, Profile, Plans) and the 27 proposal screens T01–T12 and S01–S15 listed above. Every button that leads to another screen is linked. Buttons that act inside a screen (Edit text, Add slide, Previous and Next, Mark reviewed, the radio options) stay on the same screen.

The left sidebar of the prototype lists three flows: Instructor, Student flows, and Instructor first-time guidance. Pick one, then click through. Clicking anywhere that is not a link briefly highlights every link on the screen, and the R key restarts the flow.

| Role | Starting screen | Screens in order |
| --- | --- | --- |
| Instructor | Landing (existing) | Landing, Log in, Home, + New lecture, T02 Create a lecture, T03 Add teaching material (T04 Upload failure on a bad file), T05 Choose a design (T06 No matching designs, T07 Preview a design), T08 Generating slides (T09 Generation failure; T10 opens by itself after 3 seconds), T10 Edit generated deck, T11 Review before sharing, T12 Share lecture, S01 Shared lecture reader as a student sees it |
| Student reader | Home (existing) | A Discover row or a Project page card, S01 Shared lecture reader, S02 Lecture summary, S03 Practice question, S04 Practice feedback, S05 Explain a concept aloud, S06 Recall feedback |
| Student presenter | Home (existing) | Menu drawer, S07 My presentations, S08 Group deck, then S09 Version history, S10 Replace image, S11 Presentation timing, S12 Practice your talk, S13 Rehearsal feedback and S14 Export presentation; Invite teammates opens Lecture settings › Privacy & Sharing (existing); the spoken-instruction path is Discover "Default project", Project page, Untitled lecture, live capture on, caption line, S15 Confirm spoken instruction |
| Instructor first-time guidance | T01 Prepare your next lecture | Create a lecture opens T02, Open lecture opens T10, See how it works opens T02 |

## Stakeholder demo

**Lecture deck produced during the presentation:** ____________________

## Exit ticket

**Quiz distributed during the presentation:** ____________________

**Corrections to generated questions before publishing:** ____________________
