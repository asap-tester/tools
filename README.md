# Micro App Browser
### A built-in tool launcher for Quick Search — one HTML file, zero setup

---

## What is this?

It's a single HTML file that works like a mini app store inside Quick Search.

Users swipe left → instead of Notes, a clean browser opens with a curated list of productivity tools. Tap any tool → it opens instantly. No internet needed. No installation. Nothing to download.

Everything lives in **one file**: `micro_app_browser.html`

---

## What's inside

| Section | What it does |
|---|---|
| **Workspace** | Shows tools you've opened or pinned. Your personal shortlist. |
| **Discover** | A grid of all available tools, sorted by category. |
| **Search** | Type anything — finds tools by name, description, or tag. |

---

## How to add a new tool

Open `micro_app_browser.html` in any text editor (Notepad works).

Find this section near the top of the JavaScript — it looks like this:

```
const CATALOG = [
  {id:'zonemap', name:'ZoneMap', emoji:'🗺️', desc:'...', tags:[...], category:'Productivity', url:'https://...'},
  {id:'cleardesk', name:'ClearDesk', emoji:'🧹', desc:'...', tags:[...], category:'Productivity', url:'https://...'},
  ...
];
```

To add a new tool, copy any one line and paste it at the end — just before the `];` closing bracket. Then fill in your own details:

```
{id:'mytool', name:'My Tool Name', emoji:'🔧', desc:'One line about what it does.', tags:['tag1','tag2'], category:'Productivity', url:'https://yourlink.com'},
```

**Field guide — what each part means:**

| Field | What to put |
|---|---|
| `id` | A short unique word, no spaces. Example: `mytool` |
| `name` | The display name shown on the card |
| `emoji` | One emoji that represents the tool |
| `desc` | One sentence describing what the tool does |
| `tags` | Words users can search by. Example: `['focus','timer']` |
| `category` | Pick one: `Productivity` `Dashboards` `Decision Tools` `Study` `Timers` `Calculators` |
| `url` | The full link to the tool. Must start with `https://` |

Save the file. Done.

---

## How to add a new category

In the same file, find this line:

```
const CATEGORIES = ['Productivity','Dashboards','Decision Tools','Study','Timers','Calculators'];
```

Add your new category name inside the brackets, in quotes, separated by a comma:

```
const CATEGORIES = ['Productivity','Dashboards','Decision Tools','Study','Timers','Calculators','My New Category'];
```

Then use that exact same name in your tool's `category` field.

---

## How it gets into Quick Search

The file goes into the Android app's assets folder:

```
app/
└── src/
    └── main/
        └── assets/
            └── micro_app_browser.html   ← put it here
```

The WebView loads it via:
```
file:///android_asset/micro_app_browser.html
```

---

## One thing the dev needs to enable

Links won't open unless this setting is turned on in the Android WebView config:

```java
webView.getSettings().setAllowUniversalAccessFromFileURLs(true);
```

Or links can be handled inside `shouldOverrideUrlLoading` to open in-app or in the system browser. That's the only code change needed on the Android side.

---

## File facts

| | |
|---|---|
| File size | ~28KB |
| External dependencies | None |
| Internet required | No |
| Frameworks used | None — plain HTML, CSS, JavaScript |
| Data storage | Browser localStorage (prefix: `qsmab_`) |

---

## Built by

A student, Quick Search user.
Built with AI assistance as a proof-of-concept around Issue #194.
