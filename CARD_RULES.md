# Clanki card rules — working spec

Standing rules for how cards should be generated/updated. Goal: every new or
updated card comes out right the first time, so fixes don't have to be made
card by card. Example cards are listed at the bottom.

_Last updated: 2026-11-16_

---

## A. Back-of-card layout

1. **Answer**: large, bold, short (flashcard style). You can grade yourself from this line alone.
2. **Why**: smaller blurb with the trial, reasoning, or mechanism. Only when it adds something.
3. **Correction note**: small grey fine print at the very bottom:
   "Corrected [YYYY-MM]: earlier version said X, because Y." It's there for reference only;
   it should never be needed to find the right answer.
4. **Example EKGs/images** each get a label on the back saying what they show.

## B. Links

5. A named criterion, score, sign, or eponym in a card (e.g., "Sgarbossa") becomes an
   **inline hyperlink** on that word to a page explaining what it is and how it's used.
   HTML: `<a href="URL">Term</a>`
6. Source priority:
   | Topic | First choice | Backup |
   |---|---|---|
   | EKG findings, criteria, critical care | LITFL | ECG Weekly / Dr. Smith's ECG blog |
   | Imaging signs and findings | Radiopaedia | — |
   | Clinical scores and calculators | MDCalc | LITFL |
   | Diseases and general topics | StatPearls (NCBI) | — |
   | Guideline-based recommendations | The guideline itself | — |
7. **Every link is checked before it goes on a card.** No guessed URLs.
8. Links go in the **source data**, not in edits made in the app, so the generator
   doesn't overwrite them.
9. Only add a link when it helps understanding. Terms the card already explains don't need one.
10. (Considered) A separate **Links** field for reference lists at the bottom of the back,
    shown only when it has content. Inline links are the current preference.

## C. Tags

11. `Clanki::guideline::<source-year>` on any card that depends on a guideline
    (e.g., `Clanki::guideline::AHA-HF-2022`), so cards can be reviewed when guidelines change.
12. `Clanki::corrected::<YYYY-MM>` on any card whose content was fixed.

## D. EKG questions

13. **The question names the exact skill being tested.** "What pattern is this?" is only
    allowed when recognizing the pattern is the point of the card.
14. **Give the diagnosis when it isn't what's being tested**, e.g.
    "This patient has LBBB. What is the axis?" You know what to answer and still see the pathology.
15. **Several example EKGs per card is good** (it keeps you from memorizing one tracing),
    but **the answer has to be true for every example**. If the examples differ (e.g., one LBBB
    with a normal axis, one with LAD), split them into different cards or make the answer
    cover both.
16. (Optional, needs template JS) **Rotating examples**: show one example at random each
    review instead of all of them stacked.

## E. Guideline accuracy

17. For questions about starting treatment, stage by **ACC/AHA stage**, not NYHA class alone
    (NYHA class can improve; stage can't go back).

## F. Image library (planned project, needs your computer, to be triaged later)

18. **Build an image index** of the Anki media folder: filename, which notes use it and
    their tags, a short description of what it shows, and topic keywords.
19. **Check the index before searching the web** when creating or fixing a card.
20. **Link images across related cards**, not only the card each image came with.
21. **Duplicates and quality**: when several images cover the same thing, mark the best one.
22. Do it in batches by subject (e.g., cardiology/pulm first). How to triage is still to be decided.

---

## Example cards (to be applied)

### 1. HFrEF first-line therapy (general deck)
- **Problem:** The correct answer was buried in the "Clanki update" fine print. The original
  Extra wrongly said CONSENSUS showed ACEi beat ARBs (it was enalapril vs placebo in NYHA IV).
  The card only listed ACEi/ARB + BB.
- **Intent:** Test when each GDMT drug starts.
- **Proposed back:**
  - **Answer:** Stage B (asymptomatic, LVEF ≤40%): ACEi (ARB if intolerant) + evidence-based
    β-blocker. Stage C (symptomatic): all 4 pillars: ARNI (or ACEi/ARB) + β-blocker + MRA + SGLT2i.
  - **Why:** Each pillar lowers mortality and HF hospitalizations on its own, so all four are
    started early. Evidence-based β-blockers are only carvedilol, metoprolol succinate, and bisoprolol.
    Loop diuretics are for congestion and don't lower mortality.
  - **Fine print:** Source: 2022 AHA/ACC/HFSA HF guideline. Corrected 2026-11: earlier version
    misdescribed CONSENSUS and listed only ACEi/ARB + BB as first line.
- **Tags:** `Clanki::guideline::AHA-HF-2022`, `Clanki::corrected::2026-11`
- **Open question:** one combined card or split into stage B and stage C cards?

### 2. RBBB vs LBBB (EKG deck, NoteKey `g5-cmp-rbbb-vs-lbbb`)
- Make "Sgarbossa" in the table an inline link to
  https://litfl.com/sgarbossa-criteria-ecg-library/ (already done by hand in the app;
  needs to go in the source).
- Remove the bare URL from the Answer field.
- **Possible new card:** Sgarbossa criteria on its own (3 original criteria + Smith-modified
  ST/S ratio), for LBBB and paced rhythms.
