# Study Buddy - Test Prep
# Will work for all SIS students
Simple, fun exercise app for test preparation. JSON-driven — add exercises per subject, deploy to Cloudflare Pages.

## Cloudflare Pages — Build Settings

| Setting | Value |
|---------|-------|
| **Framework preset** | None |
| **Build command** | _(leave empty)_ |
| **Build output directory** | `/` |
| **Root directory** | `/` |

No build step needed — pure static HTML + JSON.

## How to Add Exercises

Edit the JSON files in `exercises/` folder:

- `exercises/english.json`
- `exercises/math.json`
- `exercises/history.json`
- `exercises/portuguese.json`
- `exercises/science.json`

Push to GitHub → Cloudflare auto-deploys.

## JSON Schema

Each subject file follows this structure:

```json
{
  "subject": "English",
  "icon": "📚",
  "color": "#4A90D9",
  "tests": [
    {
      "id": "unique-test-id",
      "title": "Test Title",
      "sections": [ ... ]
    }
  ]
}
```

### Exercise Types

#### 1. Fill in the blank (`fill`)
```json
{
  "title": "For or Since?",
  "type": "fill",
  "instruction": "Complete with FOR or SINCE",
  "hint": "Optional hint text shown in blue box",
  "questions": [
    {
      "before": "Text before the blank",
      "after": "text after the blank.",
      "answer": "since",
      "accept": ["since"]
    }
  ]
}
```

#### 2. Multiple choice (`multiple_choice`)
```json
{
  "title": "Choose the correct option",
  "type": "multiple_choice",
  "instruction": "Select the correct answer.",
  "questions": [
    {
      "text": "I have ___ water since this morning.",
      "options": ["save", "saved", "saving"],
      "answer": 1
    }
  ]
}
```
`answer` = zero-based index of correct option (0 = first, 1 = second, etc.)

#### 3. Match columns (`match`)
```json
{
  "title": "Match the columns",
  "type": "match",
  "instruction": "Click left item, then click its match on the right.",
  "pairs": [
    { "left": "Turning off the lights", "right": "...helps to save energy." }
  ]
}
```
Right column is auto-shuffled. Student clicks left then right to pair.

#### 4. Unscramble sentences (`unscramble`)
```json
{
  "title": "Unscramble the sentences",
  "type": "unscramble",
  "instruction": "Click words in order to build the sentence!",
  "questions": [
    {
      "words": ["We", "have", "recycled", "paper", "for", "two", "weeks."],
      "answer": "We have recycled paper for two weeks."
    }
  ]
}
```
Words are auto-shuffled. Student clicks to build sentence.

## Workflow: Creating Exercises with AI

1. Ask an AI (ChatGPT, Gemini, Claude) to create exercises for the test topic
2. Convert to JSON following the schemas above
3. Paste into the subject's JSON file under `tests[].sections[]`
4. Push to GitHub — Cloudflare deploys automatically

### Example AI prompt:
> Create exercises in JSON format for a 4th grade English test.
> Topic: Present Perfect with For and Since.
> Use these types: fill, multiple_choice, unscramble.
> Follow this JSON schema: [paste schema above]
