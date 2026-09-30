# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->
I am a student contributor learning to make careful, reproducible bug
reports. I will describe what I tried and what I observed, and I will
label guesses as guesses. Maintainers can expect me to be direct about
my limits and to follow the repository's stated process.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
### Rule: Separate observation from theory

I say what I saw first and mark a suspected cause as unconfirmed.

- Wrong: "This is caused by a null result in the search code."
- Right: "When I searched for `bluejay-482`, the editor pane disappeared; I have not confirmed the cause."

### Rule: Bound claims to my test

I report only the setup and results I personally observed; I do not turn one attempt into a claim about everyone.

- Wrong: "This happens to everyone on every machine."
- Right: "I reproduced this on Windows 11 with version 3.6.15; I have not tested other systems."

### Rule: Make the contribution concrete

When I claim an issue, I say what I plan to investigate or submit instead of using urgency or enthusiasm as a substitute for a next step.

- Wrong: "Claiming this; someone has to fix it ASAP!"
- Right: "I can investigate the search result handling and will post a minimal reproduction or findings before proposing a change."

### Rule: Keep the report focused

I include details that help reproduce or understand this issue and leave out unrelated judgments about priority or the people maintaining the project.

- Wrong: "This app is unusable and this should be the top priority."
- Right: "With the steps below, the editor pane closes when the search has no matches."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
- I never claim a cause unless I have evidence for it.
- I never claim that other users or systems are affected based only on my own test.
- I never demand a priority or deadline from maintainers.
- I never say I will submit a fix unless I intend to do that work.
