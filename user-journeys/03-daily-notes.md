# 03. Daily Notes Journey

## Overview

Daily notes are the **core feature** of Happie Couple. They form the foundation for all other features (agendas, insights, analytics). This journey must be frictionless and habitual.

---

## User Goal

**"I want to quickly capture a moment or feeling about my relationship."**

---

## Entry Points

Users can start adding a note from multiple places:

1. **Notes Tab** → Floating Action Button (+ icon)
2. **Notes Tab Empty State** → "Add Your First Note" button
3. **Push Notification** → "Time for your daily check-in" → Opens AddNoteScreen
4. **Date Ideas** → "Save this date" → Can add note about it

---

## Journey Steps

### Step 1: User Taps "Add Note"

**From**: Notes Tab
**Trigger**: Tap FloatingActionButton or empty state CTA
**Navigate To**: `AddNoteScreen`

**Screen Transition**: Slide up animation (modal)

---

### Step 2: AddNoteScreen

**Screen**: `lib/screens/notes/add_note_screen.dart`

**Form Fields** (in order):

#### 1. Note Title (Required)
```
┌─────────────────────────────────┐
│ Title                           │
│ ┌─────────────────────────────┐ │
│ │ e.g., "Date night at home"  │ │
│ └─────────────────────────────┘ │
└─────────────────────────────────┘
```
- **Type**: Text input
- **Validation**: Required, 1-100 characters
- **Placeholder**: "What happened?"

#### 2. Note Content (Required)
```
┌─────────────────────────────────┐
│ Note                            │
│ ┌─────────────────────────────┐ │
│ │ We cooked dinner together   │ │
│ │ and watched our favorite    │ │
│ │ show...                     │ │
│ │                             │ │
│ └─────────────────────────────┘ │
└─────────────────────────────────┘
```
- **Type**: Multiline text area
- **Validation**: Required, 10-5000 characters
- **Placeholder**: "Describe what happened and how you felt..."
- **Height**: Expands as user types

#### 3. Mood Score (Required)
```
┌─────────────────────────────────┐
│ How did you feel?               │
│                                 │
│    ☆  ☆  ☆  ★  ★               │
│   Very sad   →   Very happy     │
└─────────────────────────────────┘
```
- **Type**: Star rating (1-5)
- **Default**: 3 (neutral)
- **Visual**: Interactive star icons
- **Labels**: "Very sad" (1 star) to "Very happy" (5 stars)

#### 4. Note Type (Required)
```
┌─────────────────────────────────┐
│ Note Type                       │
│                                 │
│  [  Positive  ] [Negative] [Neutral]  │
└─────────────────────────────────┘
```
- **Type**: Segmented control / Button group
- **Options**:
  - 😊 Positive (green)
  - 😔 Negative (red)
  - 😐 Neutral (gray)
- **Auto-suggest**: Based on mood score (4-5 = Positive, 1-2 = Negative, 3 = Neutral)

#### 5. Privacy Level (Required)
```
┌─────────────────────────────────┐
│ Who can see this?               │
│                                 │
│  ( ) Private (Only me)          │
│  (•) Shared (Me + Partner)      │
└─────────────────────────────────┘
```
- **Type**: Radio buttons
- **Default**:
  - If partner linked: "Shared"
  - If no partner: "Private" (only option)
- **Important**: Clearly communicate privacy level

#### 6. Tags (Optional)
```
┌─────────────────────────────────┐
│ Tags (optional)                 │
│ ┌─────────────────────────────┐ │
│ │ communication, date-night    │ │
│ └─────────────────────────────┘ │
│                                 │
│ Suggested: #quality-time #fun   │
└─────────────────────────────────┘
```
- **Type**: Tag input (comma-separated)
- **Validation**: Optional, max 5 tags
- **Smart Suggestions**: Based on content analysis
- **Common Tags**: communication, intimacy, conflict, fun, quality-time, appreciation

---

### Step 3: User Fills Form

**Typical Time**: 2-5 minutes
**User Experience**:
- Auto-save draft every 30 seconds (future enhancement)
- Can navigate away without losing progress
- Form validation on field blur

**Validation Feedback**:
- ✅ Valid field → Green checkmark
- ❌ Invalid field → Red border + error message
- ⚠️ Missing required → "This field is required"

---

### Step 4: User Saves Note

**Trigger**: Tap "Save Note" button

**What Happens**:
1. **Validate All Fields**
   ```javascript
   if (title.isEmpty) → Show error
   if (content.length < 10) → Show error: "Add more detail"
   if (moodScore == null) → Show error
   ```

2. **Save to Firestore**
   ```
   Creating NoteModel object
       ↓
   Call FirestoreService.saveNote()
       ↓
   Upload to Firestore (/notes/{noteId})
       ↓
   Success!
   ```

3. **Post-Save Actions**
   ```
   If note is "Shared" + partner linked:
       ↓
   Send notification to partner
       ↓
   "💕 Your partner shared something positive!"
   ```

4. **Navigate Back**
   ```
   Dismiss AddNoteScreen
       ↓
   Return to NotesScreen
       ↓
   New note appears at top of list
   ```

**Success Indicators**:
- ✅ Snackbar: "Note saved successfully!"
- 🎊 First note: "🎉 Great start! Keep it up!"
- ↩️ Smooth transition back to list

**Loading State**:
- Show spinner on "Save" button
- Disable form inputs
- Message: "Saving..."

---

### Step 5: View Saved Notes

**Screen**: `NotesScreen`

**Layout**: List of notes, newest first

**Each Note Card Shows**:
```
┌─────────────────────────────────────┐
│  😊 Date night at home              │
│  ★★★★★ | Positive | 2 hours ago    │
│                                     │
│  We cooked dinner together and      │
│  watched our favorite show...       │
│                                     │
│  🏷️ date-night, quality-time        │
│  🔒 Private                         │
└─────────────────────────────────────┘
```

**Elements**:
- **Emoji**: Based on note type (😊/😔/😐)
- **Title**: Bold, 16px
- **Metadata Line**: Mood | Type | Time ago
- **Content Preview**: First 2 lines
- **Tags**: Clickable tag chips
- **Privacy Icon**: 🔒 Private or 👥 Shared

**Interactions**:
- **Tap card** → View full note detail
- **Long press** → Options menu (Edit, Delete, Share)
- **Swipe left** → Delete (with confirmation)

---

### Step 6: Filtering & Search

**Filter Options** (top of NotesScreen):

1. **By Tab** (if partner linked):
   ```
   [ All ] [ Mine ] [ Partner's ]
   ```

2. **By Type** (dropdown):
   ```
   [ All Notes ▼ ]
   ├─ All Notes
   ├─ Positive Only
   └─ Negative Only
   ```

3. **Search** (icon button):
   - Opens search dialog
   - Searches title, content, tags
   - Real-time results as user types

---

## Success Patterns

### Habit Formation:

**Goal**: User adds notes regularly (3+ per week)

**Strategies**:

1. **Daily Reminder Notification**
   - Time: 7 PM (user configurable)
   - Message: "Time for your daily check-in 💕"
   - Tap → Opens AddNoteScreen

2. **Streak Tracking** (future)
   - "You've added notes for 7 days in a row! 🔥"
   - Gamification to maintain habit

3. **Low-Friction Entry**
   - FAB always visible in Notes tab
   - Quick access from notifications
   - Auto-suggestions to reduce thinking

4. **Positive Reinforcement**
   - Encourage after each note
   - Weekly summary: "You added 5 notes this week!"

---

## Edge Cases & Error Handling

### 1. Network Offline
**Scenario**: User saves note without internet

**Handling**:
- Save to local storage (SQLite/Hive)
- Show indicator: "Saved locally. Will sync when online."
- Auto-sync when connection restored
- Don't block user from continuing

### 2. Very Long Content
**Scenario**: User writes 10,000 character note

**Handling**:
- Firestore limit: Check before save
- Show warning at 4,500 chars: "Note is getting long. Consider splitting."
- Hard limit at 5,000: "Maximum length reached"

### 3. Inappropriate Content
**Scenario**: User writes harmful content (self-harm, abuse)

**Handling** (future enhancement):
- Content moderation AI
- Detect crisis keywords
- Show: "We noticed your note mentions difficult topics. Would you like crisis resources?"
- Link to HelpSupportScreen

### 4. Accidental Delete
**Scenario**: User swipes to delete by mistake

**Handling**:
- Confirmation dialog: "Delete this note?"
- Options: [Cancel] [Delete]
- After delete: Snackbar with "Undo" button (5 seconds)

---

## Analytics Events

Track these events for understanding usage:

```javascript
// Event: note_creation_started
{
  source: 'fab' | 'empty_state' | 'notification',
  has_partner: boolean,
  user_note_count: number
}

// Event: note_saved
{
  note_type: 'positive' | 'negative' | 'neutral',
  mood_score: 1-5,
  privacy_level: 'private' | 'shared',
  char_count: number,
  tags_count: number,
  time_to_complete: seconds
}

// Event: note_viewed
{
  is_own_note: boolean,
  note_age_days: number
}
```

---

## Performance Considerations

### Loading Notes List:

**Challenge**: User has 1000+ notes

**Solution**:
- Firestore query with `.limit(50)`
- Pagination: Load more on scroll
- Index on `noteDate` for fast sorting
- Cache recent notes locally

### Image Support (Future):

**Challenge**: Photos in notes increase size

**Solution**:
- Use Firebase Storage for images
- Store image URLs in note document
- Lazy load images in list view
- Compress images before upload

---

## User Feedback Insights

### What Users Love:
- ✅ "So simple to add a note"
- ✅ "Love seeing patterns in my moods"
- ✅ "Sharing with partner brings us closer"

### Improvement Requests:
- 🔧 Voice input for notes (dictation)
- 🔧 Add photos to notes
- 🔧 Export notes as PDF
- 🔧 Reminder to review old notes

---

## Files Involved

- `lib/screens/notes/notes_screen.dart`
- `lib/screens/notes/add_note_screen.dart`
- `lib/services/firestore_service.dart`
- `lib/models/note_model.dart`
- `lib/widgets/note_card.dart`

---

**Next Journey**: [04. Weekly Coaching](04-weekly-coaching.md)
