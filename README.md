# Cycle: a private period tracker

A simple period tracker that shows where you are in your cycle, predicts your next period, and helps you spot patterns in symptoms and mood. No account, no ads, and your data never leaves your device.

**[Try the live app →](https://yayawarlife.github.io/My-Period/)**

![Log page with the cycle ring and daily log](screenshots/log.png)

---

## The problem

Period data is some of the most sensitive health information a person can record, yet most popular trackers ask you to create an account and store that data on company servers. Many also bury the basics (when is my next period, why do I feel like this) under feeds, upsells and notifications.

I wanted to find out how small a period tracker could be while still being genuinely useful: answer the core question in under five seconds, explain what's happening in the body in plain language, and keep every byte of data on the user's own device.

## Who it's for

**Primary user:** someone who wants to know when their next period is coming and which phase of their cycle they're in, without signing up for anything.

**Secondary user:** someone who wants to notice patterns, such as which symptoms show up before a period or how long their cycles really are, for example to bring to a doctor's appointment.

**Not designed for:** contraception or fertility treatment. Calendar-based predictions aren't accurate enough for either, and the app says so on the main screen.

## What it does

The app has three pages.

**Log.** A cycle ring shows today's cycle day and phase, colour-coded across the menstrual, follicular, ovulation and luteal phases, plus a countdown to the next period. One button logs a period day. Below it, a daily log captures mood, symptoms and notes for any past day.

**Calendar & insights.** A month calendar shows logged periods, expected periods, every phase and the fertile window. Tapping any past day opens its log. The insights panel shows average cycle and period length (from the last 6 logs), shortest and longest cycle, a cycle-length chart, upcoming dates, the most common symptoms and moods, and which symptoms appear in each phase.

**Learn.** Plain-language definitions of each phase, the fertile window, cycle length and period length, how the predictions are calculated, and when to talk to a doctor.

| Calendar & insights | Learn (mobile) | Dark mode |
| ![](screenshots/calendar.png) | ![](screenshots/learn-mobile.png) | ![](screenshots/calendar-dark-mobile.png) |

## Key product decisions

| Decision | Why | Trade-off |
| **Local-first, no account.** All data lives in the browser's local storage. | Removes the biggest privacy concern and the biggest sign-up drop-off at the same time. Nothing to breach, nothing to subpoena. | No sync across devices, and clearing browser data deletes the history. Export and backup is the top item on the roadmap. |
| **Tap days on/off instead of a start/end form.** | People often forget to log the end of a period, or log days late. Marking individual days is faster and forgiving. Days within two days of each other are grouped into one period automatically. | The grouping rule is a heuristic and could merge two close bleeding episodes. |
| **Averages use the last 6 cycles and last 6 periods.** | Recent cycles predict the next one better than a lifetime average, and six is enough to smooth out one odd month. | A single unusual cycle still nudges the prediction. Gaps under 15 or over 60 days are excluded because they're usually a missed log, not a real cycle. |
| **Ovulation is counted back from the next period**, not forward from the last. | The luteal phase is fairly stable at around 14 days, while the follicular phase varies. Counting backwards gives a better estimate for people with longer or shorter cycles. | It's still a calendar estimate. Without temperature or LH test data it can't confirm ovulation. |
| **A dedicated Learn page, linked from the current phase.** | Showing "Luteal phase" is only useful if people know what it means. Explaining it in context builds understanding and trust in the numbers. | More content to keep medically accurate. |
| **Mood and symptoms as one-tap chips, plus free-text notes.** | Fixed options make logging take seconds and make the insights (top symptoms, symptoms by phase) possible. Notes cover everything else. | Fixed lists can't capture every experience. |
| **One static HTML file, no framework or backend.** | Loads instantly, hosts free on GitHub Pages, works offline once loaded, and anyone can read the code to check that data stays local. | Harder to scale into a larger product without restructuring. |

## What I'd do next

1. **Export and import a backup file**, to remove the data-loss risk of local-only storage.
2. **Show a prediction range for irregular cycles** (for example "Nov 12–16") instead of a single date that implies false precision.
3. **Optional reminders** for an upcoming period, by turning the app into an installable web app.
4. **Flow level** on period days.

**How I'd measure success:** the share of new users who log at least two periods (the point at which predictions become personal), prediction accuracy (days between the predicted and actual start), and how many days per cycle people log symptoms or mood.

## How the predictions work

- **Next period** = start of the last period + average cycle length
- **Ovulation day** = average cycle length − 14 (day 14 of a 28-day cycle)
- **Fertile window** = 5 days before ovulation through 1 day after
- Until two periods are logged, the app assumes a 28-day cycle and a 5-day period

The full explanation is on the app's Learn page.

## Run it locally

No build step. Download `index.html` and open it in any browser.

## Disclaimer

This app gives estimates based on past cycles and general information about the menstrual cycle. It isn't medical advice and isn't reliable for birth control.

---

Built by [Priyanka](https://www.linkedin.com/in/dwivedi96/)
