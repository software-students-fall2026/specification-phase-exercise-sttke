# Specification Phase Exercise — The Slide Machine

This repository proposes improvements to The Slide Machine, which generates lecture slides from spoken teaching and can create a post-lecture quiz. Our design follows the material from preparation and generation through editing, sharing, and student review. Existing capabilities provide the starting point; the proposed interactions improve their clarity, continuity, and recovery from problems.

## Team members

- Spark Fan ([SparkFan-ui](https://github.com/SparkFan-ui)) — integration and documentation
- Yutong Xiao ([yx3295-star](https://github.com/yx3295-star)) — instructor research
- Tony Zibo Zhou ([TonyyZhou](https://github.com/TonyyZhou)) — student research
- Tony Dong ([tongdong016](https://github.com/tongdong016)) — wireframes
- Kevin Han ([kevinhan923](https://github.com/kevinhan923)) — clickable prototype

## Review of the Current Application

| # | Strength / weakness / gap | Specific observation in the live app | Task or screen | Observer |
| --- | --- | --- | --- | --- |
| 1 | Strength | Create account and Sign in put Sign up with Google / Sign in with Google above the email form, and "Forgot your password?" opens a Reset your password page that explains itself in one sentence. | Create account / Sign in | Spark Fan |
| 2 | Strength | With the microphone off, the empty lecture page says to click the + or microphone icons to start adding content; hovering the mic shows "Speak to add slides"; once on, it says "Start speaking to generate slides". | Lecture page (live capture) | Kevin Han |
| 3 | Strength | Lecture settings states that the settings apply to just this lecture, links to project-wide settings, explains that a blank Lecture title lets the AI title it from speech, and marks Seed notes "Saved automatically". | Lecture settings · General | Tony Dong |
| 4 | Strength | A shared deck (Fishing for squid) renders in its NYU design with a 1 / 7 counter, up and down votes, fullscreen, a translate dropdown and a per-slide menu offering "Speak this slide". | Deck viewer | Tony Zibo Zhou |
| 5 | Strength | Plans states "Every plan includes every feature. What changes is how much of each you may use", shows a check for all eight features in every column, and marks Free as "Your plan". | Plans | Spark Fan |
| 6 | Strength | The Add seed material dialog explains itself ("Give the AI background for this lecture before you begin. Optional — you can add more anytime"), offers Seed notes and a PDF, DOCX, TXT or photo upload, and can be skipped. | Add seed material dialog | Yutong Xiao |
| 7 | Weakness | In Discover, three lectures by one user show the project as `<="` and the author name followed by `<"=`, while every other row shows a readable project name such as Default project. | Home /app · Discover | Yutong Xiao |
| 8 | Weakness | The Add seed material dialog that follows + New lecture has no title field; the breadcrumb already reads Untitled lecture, and the Lecture title field lives in Lecture settings · General. | Add seed material dialog | Kevin Han |
| 9 | Weakness | For a newly created lecture with 0 slides, General access is already Public ("Anyone on the internet with the link can view") while People with access reads "Only you have access so far". | Lecture settings · Privacy & Sharing | Kevin Han |
| 10 | Weakness | The "1 / 7" slide counter under the slide is half hidden behind the footer bar that carries "API ok" and "Free plan ok". | Deck viewer | Tony Dong |
| 11 | Weakness | In List view the fullscreen icon is drawn on top of the downvote count at the top right, so the two controls overlap. | Deck viewer · List view | Tony Dong |
| 12 | Weakness | The page behind the Default project breadcrumb is headed "Default project" with another user's name as owner, yet lists the observer's own Untitled lecture (0 slides) beside that user's Fishing for squid, one owner name above two people's lectures. | Project page | Kevin Han |
| 13 | Weakness | In the observation session with Chel, instructions spoken to the app while presenting were transcribed into the slide as content instead of being treated as commands. | Lecture page (live capture on) | Tony Zibo Zhou |
| 14 | Weakness | In the two teacher sessions, both teachers, after seeing the landing page ("Speak freely — the slides will follow") and Home, said they were unsure what the app was for and where templates or materials live. | Landing page / Home /app | Yutong Xiao |
| 15 | Gap | The menu drawer lists Home, Profile, Account settings, About us, Send feedback, Privacy policy, Terms & conditions and Log out; no entry leads to the user's own projects or lectures. | Menu drawer | Tony Zibo Zhou |
| 16 | Gap | Both General access options are described in terms of "the link" ("with the link can view", "open with the link"), yet the Privacy & Sharing tab shows no link and no copy control. | Lecture settings · Privacy & Sharing | Yutong Xiao |
| 17 | Gap | Once the microphone is on, the page shows the red mic, "Start speaking to generate slides" and, while speaking, a caption line; no elapsed time or remaining Audio recording time, which Plans meters, appears. | Lecture page (live capture on) | Kevin Han |
| 18 | Gap | Discover offers only the Latest and Top tabs and a search box for "lectures, projects, people"; there is no way to narrow the list by course or topic. | Home /app · Discover | Spark Fan |

**Research context, separate from the live-app review:** instructor interviewees reported unclear purpose and category labels, difficulty finding material and templates, and time spent manually adjusting slides. Student interviewees liked the basic speech-to-slide workflow but reported context loss, hard-to-find editing controls, and limited study support.

## Prior Art & Originality

We compared the proposed work with the upstream [software design document, especially §18 Future Work and §19 Open Questions](https://github.com/bloombar/slide-machine/blob/better-faster/docs/SPEC.md), its [delivery roadmap](https://github.com/bloombar/slide-machine/blob/better-faster/docs/ROADMAP.md), and the [open issues](https://github.com/bloombar/slide-machine/issues) and [pull requests](https://github.com/bloombar/slide-machine/pulls). The review was last performed on 27 September 2026; the upstream default branch was `better-faster` at that time.

Existing or specified capabilities already include seed material, a template library, automatic layout choice, editing, deck sharing, quizzes, and Google Slides export. Real-time collaborative editing is explicitly listed as upstream future work. We therefore describe material reuse, template choice, Google Slides export, and collaboration as improvements to existing/planned workflows, **not** newly invented capabilities. Our proposed contribution is the interaction design that connects a guided preparation path and pre-share review to student summaries, questions linked to source slides, and active recall with recoverable failures.

## Stakeholders

The instructor findings below come from the instructor research notes. They report interviews with two teachers but combine many findings rather than attributing each point to a particular individual.

### Instructor stakeholders

| Participant | Context | Reported needs | Reported difficulties |
| --- | --- | --- | --- |
| Teacher 1 | College Radiation Physics instructor | Prepare lectures more quickly, reuse teaching content, find relevant resources, reduce formatting, understand the tool's purpose | The notes report unclear app purpose, difficult discovery, unclear categories, and manual work across the two teachers; they do not reliably assign each difficulty to Teacher 1. |
| Teacher 2 | Community nonprofit English teacher who also leads after-class childcare | Prepare lectures more quickly, reuse teaching content, find relevant resources, reduce formatting, understand the tool's purpose | The notes report the same combined themes but do not reliably assign each difficulty to Teacher 2. |

Across the two interviews, the needs are (1) less preparation time, (2) generation based on existing content, (3) easier template/material discovery, (4) less manual formatting, and (5) an understandable starting point. The reported frustrations are (1) unclear app purpose, (2) hard-to-find templates/materials, (3) unclear categories, (4) time-consuming manual preparation, and (5) manual layout adjustment.

### Student stakeholders

**Chel — student and presentation author.** Chel valued the speed of speech-to-slide creation but reported lost context between slides, awkward editing, uncertain language settings, difficult navigation in long decks, and difficulty locating image upload, undo/history, and export. Chel also wanted group collaboration, Google Slides compatibility, short review material, and active recall. Spoken instructions were sometimes treated as slide content.

**Lan — student and presentation author.** Lan found the basic generation process easy to learn but had difficulty with settings, controls, text/visual editing, adding images, sharing, and finding previous work. Lan wanted timing and rehearsal assistance, support for group presentations, important concepts, and related practice questions.

Together, their needs include faster presentation creation, flexible editing, coherent generated content, group collaboration, familiar export options, presentation preparation, concise review, and active practice. Their frustrations include context loss, hard-to-find controls, awkward editing, long-deck navigation, weak group workflows, limited rehearsal support, study material disconnected from practice, and speech instructions appearing as slide content.

## Product Vision Statement

The Slide Machine should guide instructors and student presenters from reusable material to a coherent, reviewable deck, then let students follow that deck into concise, source-linked review and practice, with clear feedback when a step fails.

## User Requirements

Existing capabilities named below are starting points. Each story specifies a new or changed interaction, not a claim that the underlying capability is missing. IDs connect stories to the design artifacts.

### Instructor user stories

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

### Student user stories

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

### Requirements to design traceability

| Workflow | User stories | Activity diagrams | Wireframes and prototype |
| --- | --- | --- | --- |
| Guided lecture creation and material recovery | T01–T03, T07, T10 | Getting started and creating slides | T01–T04, including upload failure |
| Design discovery, generation, and review | T04–T06, T08–T09, S03 | Getting started and creating slides; Finding and using templates | T05–T11, including no results and generation failure |
| Sharing and student study | T09, S08–S10 | Active recall | T12, S01–S06, including microphone fallback and feedback |
| Student group presentation | S01–S07, S11 | Real-time collaboration | S07–S15, including version recovery, rehearsal, export, and command confirmation |

## Activity Diagrams

### Instructor: getting started and creating slides

**Story:** T03 — As an instructor with existing material, I want to see what source content was accepted before generating, so that I know what the deck will use.

![Getting started and creating slides (activity diagram)](images/instructor-getting-started-activity.jpeg)

### Instructor: finding and using templates

**Story:** T05 — As an instructor browsing designs, I want understandable categories with previews, so that I can choose a template appropriate to my lecture.

![Finding and using templates (activity diagram)](images/instructor-templates-activity.jpeg)

### Student: real-time collaboration

**Story:** S01 — As a student presenter, I want to edit a presentation with teammates in real time, so that we can see each other's progress.

![Student Real-Time Collaboration Activity Diagram](images/student-collaboration-activity.png)

### Student: active recall

**Story:** S10 — As a student, I want to explain a concept aloud and receive feedback on missed points, so that I can practice active recall rather than only reread slides.

![Student Active Recall Activity Diagram](images/student-active-recall-activity.png)

## Wireframes

[Open the Figma design: Wireframes](https://www.figma.com/design/xSlHrGphQWleYhSJwaD4ST?node-id=7-2). It contains 27 black-and-white screens and states.

| Role | Screens covered | Main requirements |
| --- | --- | --- |
| Instructor | Home/guidance, new lecture, source selection and upload failure, template browser/no result/preview, generation/progress/failure, slide editing, pre-share review, sharing permissions (T01–T12) | T01–T10 |
| Student reader | Shared deck, summary, concept-linked question, answer feedback, active recall input and feedback (S01–S06) | S08–S10 |
| Student presenter | Dashboard, live collaboration, version history, image replacement, target duration, rehearsal and feedback, export, spoken-command confirmation (S07–S15) | S01–S07, S11 |

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

Full-size PNG exports are in [images/wireframes](images/wireframes).

**Instructor (T01–T12)**

| Screen | Wireframe |
| --- | --- |
| T01 Prepare your next lecture | <img src="images/wireframes/T01.png" width="360" alt="T01 Prepare your next lecture"> |
| T02 Create a lecture | <img src="images/wireframes/T02.png" width="360" alt="T02 Create a lecture"> |
| T03 Add teaching material | <img src="images/wireframes/T03.png" width="360" alt="T03 Add teaching material"> |
| T04 Upload failure | <img src="images/wireframes/T04.png" width="360" alt="T04 Upload failure"> |
| T05 Choose a design | <img src="images/wireframes/T05.png" width="360" alt="T05 Choose a design"> |
| T06 No matching designs | <img src="images/wireframes/T06.png" width="360" alt="T06 No matching designs"> |
| T07 Preview a design | <img src="images/wireframes/T07.png" width="360" alt="T07 Preview a design"> |
| T08 Generating slides | <img src="images/wireframes/T08.png" width="360" alt="T08 Generating slides"> |
| T09 Generation failure | <img src="images/wireframes/T09.png" width="360" alt="T09 Generation failure"> |
| T10 Edit generated deck | <img src="images/wireframes/T10.png" width="360" alt="T10 Edit generated deck"> |
| T11 Review before sharing | <img src="images/wireframes/T11.png" width="360" alt="T11 Review before sharing"> |
| T12 Share lecture | <img src="images/wireframes/T12.png" width="360" alt="T12 Share lecture"> |

**Student reader (S01–S06)**

| Screen | Wireframe |
| --- | --- |
| S01 Shared lecture reader | <img src="images/wireframes/S01.png" width="360" alt="S01 Shared lecture reader"> |
| S02 Lecture summary | <img src="images/wireframes/S02.png" width="360" alt="S02 Lecture summary"> |
| S03 Practice question | <img src="images/wireframes/S03.png" width="360" alt="S03 Practice question"> |
| S04 Practice feedback | <img src="images/wireframes/S04.png" width="360" alt="S04 Practice feedback"> |
| S05 Explain a concept aloud | <img src="images/wireframes/S05.png" width="360" alt="S05 Explain a concept aloud"> |
| S06 Recall feedback | <img src="images/wireframes/S06.png" width="360" alt="S06 Recall feedback"> |

**Student presenter (S07–S15)**

| Screen | Wireframe |
| --- | --- |
| S07 My presentations | <img src="images/wireframes/S07.png" width="360" alt="S07 My presentations"> |
| S08 Group deck | <img src="images/wireframes/S08.png" width="360" alt="S08 Group deck"> |
| S09 Version history | <img src="images/wireframes/S09.png" width="360" alt="S09 Version history"> |
| S10 Replace image | <img src="images/wireframes/S10.png" width="360" alt="S10 Replace image"> |
| S11 Presentation timing | <img src="images/wireframes/S11.png" width="360" alt="S11 Presentation timing"> |
| S12 Practice your talk | <img src="images/wireframes/S12.png" width="360" alt="S12 Practice your talk"> |
| S13 Rehearsal feedback | <img src="images/wireframes/S13.png" width="360" alt="S13 Rehearsal feedback"> |
| S14 Export presentation | <img src="images/wireframes/S14.png" width="360" alt="S14 Export presentation"> |
| S15 Confirm spoken instruction | <img src="images/wireframes/S15.png" width="360" alt="S15 Confirm spoken instruction"> |

## Clickable Prototype

**Public prototype:** [Slide Machine Prototype on Figma — anyone with the link can view, no login needed](https://www.figma.com/proto/KisgOB8gz8FuthCTWzZcll/Slide-Machine-Prototype?node-id=9-100&scaling=min-zoom&content-scaling=fixed&starting-point-node-id=9%3A100&show-proto-sidebar=1&page-id=0%3A1)

## Stakeholder Demo

**Lecture deck produced during the presentation:** [Slide Machine deck](https://theslidemachine.com/d/untitled-ebabb720)

## Exit Ticket

**Quiz distributed during the presentation:** [Exit-ticket quiz (Google Form)](https://docs.google.com/forms/d/e/1FAIpQLScKNKPF_kt75wiQPQaB1vsjukL42oGMyZvzEnlRy267WcCN0g/viewform)

**Corrections to generated questions before publishing:** No corrections were needed.
