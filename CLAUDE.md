# Marketing Campaign Tasks - Development Progress

**Project:** Interactive Task Management for Marketing Campaigns
**Repository:** https://github.com/mattmartin65/marketing-campaign-tasks
**Target Platform:** Vercel with Vercel KV database
**Users:** Matt & Petra

---

## Current Status (Session 1)

**Token Usage:** 119k / 200k (60%)
**Last Updated:** 2026-01-31
**Git Commit:** `03ca110` - Phase 1 complete and pushed to GitHub

### ✅ Phase 1 COMPLETE - Date Restructuring

**All changes committed and pushed to GitHub**

1. **Removed date fields from main task detail sections** ✅
   - Replaced start/end date inputs with calculated "Duration" display
   - Updated all 11 task-meta sections (tasks 1.1-3.4)
   - Added `date-range-display` spans with IDs
   - **Location:** Lines 1125-2250 in index.html

2. **Updated subtaskData structure** ✅
   - Added `startDate` and `endDate` fields to all 50+ subtasks
   - Fields initialized as `null` (to be filled by users)
   - **Location:** Lines 3014-3089 in index.html

3. **Added date inputs to subtask rows** ✅
   - Modified `toggleSubtasks()` function to render date inputs
   - Each subtask now has start/end date inputs
   - Inputs trigger `saveSubtaskDates()` and `calculateAllDateRanges()` on change
   - **Location:** Lines 3146-3154 in index.html

4. **Created date calculation JavaScript functions** ✅
   - `saveSubtaskDates()` - Saves subtask dates to localStorage
   - `loadSubtaskDates()` - Restores subtask dates from localStorage
   - `calculateTaskDateRange(taskId)` - Calculates min/max dates from subtasks
   - `calculateAllDateRanges()` - Updates all main task duration displays
   - Auto-loads and calculates on page load
   - **Location:** Lines 3250+ in index.html

5. **Added CSS styling** ✅
   - `.subtask-dates` - Flex container for date inputs
   - `.subtask-date-input` - Styled date input fields
   - `.date-range-display` - Styled duration display
   - `.date-range-display.scheduled` - Highlighted when dates are set
   - **Location:** Lines 300-380 in index.html

6. **Created CLAUDE.md progress file** ✅
   - Comprehensive documentation
   - Commands for next session
   - Testing checklist
   - Technical decisions

### 🎯 Ready for Phase 2

**Next Action:** Test locally, then set up Vercel

### 📋 Remaining Tasks

#### Phase 1 Testing (Ready to Test)
- [ ] Open index.html in browser (file:// or local server)
- [ ] Test date functionality:
  - Click "Medflow Gastro Emails" row to expand subtasks
  - See 4 email subtasks with start/end date inputs
  - Add dates to Email 1: Start=Feb 1, End=Feb 3
  - Add dates to Email 2: Start=Feb 4, End=Feb 6
  - Verify main task shows "Duration: Feb 1 - Feb 6"
  - Refresh page, verify dates persist
  - Check detail view shows same duration
- [ ] Test Gantt chart integration (may need update)
- [ ] Test with multiple tasks

#### Phase 2: Vercel Project Setup
- [ ] Create `package.json` with @vercel/kv dependency
- [ ] Create `.gitignore` for Vercel files
- [ ] Install Vercel CLI: `npm i -g vercel`
- [ ] Run `vercel login` and `vercel link`

#### Phase 3: Vercel KV Database
- [ ] Create KV database in Vercel dashboard
- [ ] Create `/api/tasks.js` serverless function
  - GET endpoint (fetch all data)
  - POST endpoint (save updates)
- [ ] Copy KV credentials to `.env.local`
- [ ] Test API locally with `vercel dev`

#### Phase 4: Frontend Migration to API
- [ ] Replace `saveProgress()` with API POST call
- [ ] Replace `loadProgress()` with API GET call
- [ ] Replace `saveSubtaskDates()` with API integration
- [ ] Replace `saveDateProgress()` with API integration
- [ ] Replace `updatePriority()` with API integration
- [ ] Add error handling and loading states
- [ ] Add auto-refresh polling (every 10 seconds)

#### Phase 5: Multi-User Features
- [ ] Add user picker modal (Matt/Petra selection)
- [ ] Store user choice in sessionStorage
- [ ] Include user in all save operations
- [ ] Add "Last updated by" indicator
- [ ] Add notification when other user makes changes

#### Phase 6: Deployment
- [ ] Create `vercel.json` configuration
- [ ] Commit all changes to GitHub
- [ ] Run `vercel --prod` to deploy
- [ ] Test multi-user functionality
- [ ] Verify data persistence
- [ ] Share deployed URL

---

## File Changes

### Modified Files
- `index.html` - Main application (extensive changes)
  - Lines 1125-2250: Removed date fields from task-meta sections
  - Lines 3014-3089: Added startDate/endDate to subtaskData
  - Lines 3146-3154: Updated subtask row rendering with date inputs
  - Lines 300-380: Added CSS for subtask dates and date displays
  - Lines 3250+: Added date calculation functions

### Files to Create
- `package.json` - Node.js dependencies
- `vercel.json` - Deployment configuration
- `.gitignore` - Ignore Vercel/Node files
- `.env.local` - Environment variables (KV credentials)
- `api/tasks.js` - Serverless API function

---

## Key Technical Decisions

### Why Vercel over Netlify?
- **Vercel KV**: Built-in Redis-based database
- **Simpler**: No external database service needed
- **Free tier**: 256MB storage, 100k requests/month
- **Real-time ready**: Low-latency key-value storage

### Data Structure in Vercel KV
```javascript
{
  tasks: {
    'summary-1.1': { done: false, priority: 1, comments: '' },
    'subtask-1.1.1': {
      done: true,
      comments: 'Draft ready',
      startDate: '2026-02-01',
      endDate: '2026-02-03'
    },
    // ... all tasks and subtasks
  },
  lastUpdated: '2026-01-31T10:30:00.000Z',
  lastUpdatedBy: 'matt'
}
```

### Date Calculation Logic
- **Subtask dates**: User sets start/end for each subtask
- **Main task dates**: Automatically calculated as:
  - Start = earliest subtask start date
  - End = latest subtask end date
  - Display = "Feb 1 - Feb 10" or "Not scheduled"

---

## Testing Checklist

### Date Functionality
- [ ] Click main task row to expand subtasks
- [ ] See date input fields on each subtask
- [ ] Set start date on subtask 1
- [ ] Set end date on subtask 1
- [ ] Verify main task shows "Feb X - Feb Y"
- [ ] Set dates on subtask 2 (earlier start, later end)
- [ ] Verify main task updates to show full range
- [ ] Refresh page, verify dates persist
- [ ] Check Gantt chart reflects subtask dates

### Multi-User Sync (After Phases 3-5)
- [ ] Open as Matt in Chrome
- [ ] Open as Petra in Firefox/Incognito
- [ ] Matt updates a task
- [ ] Petra sees update within 10 seconds
- [ ] Petra updates different task
- [ ] Matt sees update within 10 seconds
- [ ] Check "Last updated by" shows correct user

---

## Quick Reference

### Important IDs
- **Main tasks:** `summary-1.1` through `summary-3.4` (11 tasks)
- **Subtasks:** `subtask-X.Y.Z` (50+ total)
- **Date displays:** `date-range-display-summary-X.Y`

### localStorage Keys (Current)
- `petra-marketing-tasks` - Task completion & comments
- `petra-task-priorities` - Priority levels
- `petra-subtask-dates` - Subtask start/end dates
- `petra-gantt-data` - Gantt chart data

### localStorage Keys (After Migration)
- Will be replaced by Vercel KV
- Single key: `marketing-tasks-data`
- localStorage kept as offline fallback

---

## Commands for Next Session

```bash
# If continuing implementation:
cd /Users/mattmartin/Documents/marketing/marketing

# Create package.json
npm init -y
npm install @vercel/kv

# Install Vercel CLI (if not installed)
npm i -g vercel

# Login to Vercel
vercel login

# Link project
vercel link

# Run locally
vercel dev

# Deploy
vercel --prod
```

---

## Notes for Continuation

If starting a new chat:
1. Review this CLAUDE.md file
2. Check current phase in todo list
3. Test existing date functionality first
4. Continue with Phase 2 (Vercel setup)

**GitHub Repo:** All changes are committed to main branch at:
https://github.com/mattmartin65/marketing-campaign-tasks
