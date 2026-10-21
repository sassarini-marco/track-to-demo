---
name: present
description: "Prepare the demo presentation: agree the deck content with the team, build it as a Claude Slides deck on the team's design system, and after validation export the .pptx on the team's template. Use it for the pitch, slides, demo rehearsal or judges' questions."
---

# Present
Arguments: $ARGUMENTS
Reply in the user's language. Read BRIEF.md and WORK.md. Respect the demo and Q&A lengths in the schedule.
Never invent results, metrics or integrations. Keep mock, implemented and verified apart, and say which data is synthetic.

1. Content before form. Propose the deck outline from WORK.md: problem and promise, live demo with the wow moment,
   why trust it, results and limits; one line of content per slide, timings and speakers. Ask the team what to change.
   Nobody answers: go on and mark it "to confirm".
2. The deck. Create a Claude "Slides" Artifact titled "Deck · <project>" with the design system the brief names for the
   deck, which overrides any default. Use real screenshots of the running app; a screenshot you need and do not have, capture it from the real demo
   with the planned demo login, never a placeholder. Speaker notes go in each slide's notes.
   Write the link in the brief's "Deck" line and commit.
3. Validation. The team comments on the deck; read the comments, apply the requested changes, ask for confirmation.
   Do not export before the team validates.
4. The .pptx. If the brief names a slide template, work on a copy of it with the pptx skill, keeping its masters and
   layouts: same content and order as the validated deck, real screenshots, speaker notes. Save it next to the template in
   templates/, out of git unless the team allows it. Without a template, tell the team to download the validated deck as .pptx
   from the deck's download menu. A template but no pptx skill: say so, give the install command from kickoff and the deck link.
5. PRESENTATION.md: script, speaker notes, rehearsals to do before the freeze, likely questions and answers, links.
   Update your rows in WORK.md, then commit.
Use real screenshots and recordings as support and backup. No alternative theme, no automatic video.
