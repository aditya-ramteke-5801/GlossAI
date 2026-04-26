# Gloss AI

**A reading companion that helps you actually understand the books you read.**

## The Problem

Reading challenging literature — classic novels, dense non-fiction, literary fiction — is hard. You hit a word you don't know and lose momentum. You read a paragraph three times and still aren't sure what the author meant. You finish a chapter and can't remember what happened. Most people either push through without understanding, or give up entirely.

Existing tools don't solve this well. Dictionary apps give you a definition but not what the word means *in context*. SparkNotes gives you a summary but doesn't help you engage with the actual text. Audiobooks let you consume passively without building comprehension. None of these tools meet you *inside* the reading experience itself.

## The Insight

The best way to understand a book is to read it with someone who already has — a friend who can explain a confusing passage in plain language, tell you what a word means in *this specific scene*, quiz you to check if you're actually following, and push you to articulate your own thoughts.

Gloss AI puts that friend inside your reading experience.

## What Gloss AI Does

Gloss AI is a local-first web app where you upload a PDF and read it with AI-powered tools available at every step:

**Understand words in context** — Highlight any word to get its pronunciation, definition, and what it specifically means in the scene you're reading. Not a generic dictionary entry — an explanation that references the characters, themes, and moment in the story. Save words to build your vocabulary over time.

**Simplify hard passages** — Select a confusing paragraph and get it rewritten in plain, everyday English. Dialogue is preserved with speaker labels so you never lose track of who said what. You see both versions side by side.

**Chat about what you're reading** — Ask questions about any passage or chapter. "Why did this character do that?" "What does the author mean here?" "What's the historical context?" Conversations are saved per-chapter so you can pick up where you left off.

**Test your comprehension** — Generate quizzes on chapters you've read. Questions cover plot recall, character motivation, themes, and vocabulary — the things that matter for actually understanding a book, not trivia.

**Build vocabulary with spaced repetition** — Every word you look up is saved to a vocabulary bank with its definition and the context where you found it. Practice mode uses spaced repetition so words move from short-term recognition to long-term retention.

**Write to think** — Each chapter has a notes section. You must write at least 200 words of notes before advancing to the next chapter. This is intentional friction — writing forces you to process what you read instead of passively consuming it.

## Product Decisions Worth Noting

**The 200-word notes gate.** This is the most opinionated feature. You cannot skip ahead without writing about what you just read. It feels restrictive, but it's the difference between reading and *understanding*. The gate is what makes Gloss AI a learning tool rather than just a reading tool.

**Simple language in AI responses.** Every prompt is tuned to avoid academic jargon. The AI explains things like a well-read friend, not a literature professor. Words like "juxtaposition," "hedonistic," and "paradigm" are explicitly banned from responses.

**Context-aware, not generic.** The AI always knows which book, chapter, and passage you're looking at. A definition for "grave" in a funeral scene is different from "grave" describing someone's expression. Every response is grounded in where you are in the text.

**Vocabulary as a byproduct of reading, not a chore.** You don't go to a separate app to learn words. You encounter a word while reading, tap it, and get a definition grounded in the exact scene you're in. Save it with one click. The vocab bank builds itself as you read, and spaced repetition turns those encounters into lasting knowledge.

**Chapter-level organization.** Chats, notes, vocabulary, and bookmarks are all scoped to chapters. This mirrors how people naturally think about books — "that part in chapter 5" — and keeps context manageable for the AI.

## Tech Stack

- React + Vite
- Zustand (state management)
- Dexie.js / IndexedDB (local storage)
- pdfjs-dist (PDF parsing)
- OpenAI API (gpt-4o / gpt-4o-mini / DALL-E 3)
- Tailwind CSS v4

## Setup

```bash
npm install
```

Create a `.env` file:

```
VITE_OPENAI_API_KEY=sk-your-key-here
```

Run the dev server:

```bash
npm run dev
```

Open `http://localhost:5173` in your browser.

## Usage

1. Upload a PDF from the library screen
2. Start reading — highlight words to define them, highlight passages to simplify or chat about them
3. Write your chapter notes (200 words minimum) to unlock the next chapter
4. Take quizzes to test your understanding
5. Review and practice saved words in the Vocabulary Bank

## Project Structure

```
src/
  api/openai.js          — OpenAI API calls (definitions, quiz, simplify, chat, covers)
  components/
    Library.jsx           — Home screen with book grid and upload
    Reader.jsx            — Main reading interface and navigation
    ReadingPane.jsx       — Text rendering with word/passage selection
    ChapterSidebar.jsx    — Chapter list, vocabulary, chats, and notes tabs
    NotesPanel.jsx        — Chapter notes with 200-word gate
    DefinitionPopup.jsx   — Contextual word definition popup
    SimplifyPopup.jsx     — Plain-English passage rewrite
    ChatPanel.jsx         — Chapter-level chat with the book
    QuizMode.jsx          — Comprehension quiz generation
    VocabBank.jsx         — Vocabulary list with spaced repetition
    PracticeMode.jsx      — Flashcard practice mode
    BookCard.jsx          — Book card with reading progress
    SettingsModal.jsx     — Settings, API usage stats, data export/import
    UploadZone.jsx        — Drag-and-drop PDF upload
    ProgressBar.jsx       — Reading progress bar
  utils/
    pdf-parser.js         — PDF text extraction with chapter detection
    cover-generator.js    — Deterministic SVG cover generation
    spaced-repetition.js  — SRS scheduling for vocabulary practice
  db.js                   — IndexedDB schema and usage tracking
  store.js                — Zustand store for user preferences
  App.jsx                 — Router setup
  main.jsx                — Entry point
```
