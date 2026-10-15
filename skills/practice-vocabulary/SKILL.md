---
name: practice-vocabulary
description: Run vocabulary practice with the learner's saved Polidict words — meaning recall, writing, listening and speaking exercises — and save confirmed results. Use when the learner wants to practise, review, quiz or drill their Polidict words, asks what is due, or wants exercises after writing feedback.
---

# Practise Polidict vocabulary

Polidict stores the learner's words and schedules reviews. You run the exercises in the conversation; Polidict saves only the results the learner confirms.

## 1. Choose a batch

1. Call `get_learning_context` when the language, groups or due words are unclear. Ask which language only when the learner studies several and context does not say.
2. Call `get_training_items` once for the batch. Defaults: ten words, `selection: recommended`, meaning skill. Map ordinary requests to parameters:
   - "what's due" → `due`; "new words" → `new`; "anything" or a specific group → `all` or `groupIds`
   - "spelling", "listening", "speaking" → the matching skill
3. Each word's `practiceTargets` names the skill and meaning to practise. Use it to pick exercises; never practise a skill or meaning it does not list.
4. An empty batch means nothing suitable: say so plainly and offer another selection, skill or group.

Keep `practiceId`, item IDs, versions and enum values out of the conversation.

## 2. Run exercises

Ask one question at a time unless the learner asks for several together. Never reveal an answer before the learner attempts it.

| Skill | Prompt | Hidden until the attempt |
|---|---|---|
| Meaning | Show the word; ask what it means | Meanings, translations |
| Writing | Give a meaning, translation or clue | The spelling |
| Listening | Play real audio (`speechUrl`, or your own audio support) | The spelling |
| Speaking | Ask the learner to say the word aloud | — |

- Listening needs audio the learner can actually hear. Without it, explain the limit and offer another skill.
- Speaking needs a real audio assessment from your client or the learner's own self-assessment after speaking aloud. Never infer pronunciation from typed text.
- When several questions are open, refer to unanswered ones only by number. Never mention their word, spelling or meaning in feedback, save questions or summaries.
- A reveal or skip is not an attempt and has no result.

## 3. Grade and give feedback

Grade the actual attempt, then show the correct answer and brief feedback.

| Rating | When |
|---|---|
| AGAIN | Incorrect, forgotten or blank |
| HARD | Correct, but with evident difficulty (hints, partial recall, several tries) |
| GOOD | Clear correct recall — the default for a correct answer |
| EASY | Only when the learner says recall was effortless |

Never infer ease from polished wording or response speed. Set `assessmentSource` honestly: `model` for your own assessment, `learner` for the learner's self-assessment.

## 4. Ask before every save

After each answered exercise, ask a separate question: save this result? Ask for failures too.

- Never offer, request or accept permission to save future answers automatically, even if the learner suggests it.
- If the learner declines, save nothing for that exercise.
- On approval, call `submit_training_results` with `confirmed: true`, the batch `practiceId`, a new `requestId`, and each word's latest `expectedVersion`. Retry with exactly the same input.
- Only `progressSaved: true` confirms the save. Use `updatedItems` versions for later saves in the same batch.
- `WORD_CHANGED`: reread the word and check the exercise is still valid before resubmitting.

## Writing feedback

When the learner asks you to check their writing, feedback alone does not change Polidict progress. Offer a follow-up vocabulary exercise on the mistakes, then ask whether to save its result.

## Limits

- Unsaved exercises live only in this conversation; Polidict cannot restore them later.
- Report progress with `get_word_progress` in ordinary words: new, learning, learned, mastered, next review date. Never invent accuracy percentages or claim mastery from one skill.
