# zumoauth — deployment, step by step

Written to be followed literally. Every click named. If a screen doesn't match
what's described, stop rather than guessing — Cloudflare renames things
periodically. Nothing here is destructive; any step can be redone.

Total time: about 20 minutes. Steps 1–6 are one-time.

---

## Before you start

Have `zumoauth-worker.js` open in a text editor, ready to copy.
Log in at **dash.cloudflare.com**. The left sidebar is your map.

---

## Step 1 — Create the KV namespace

KV is Cloudflare's key-value store. Student records live here. Create it first,
because the Worker needs something to attach to.

1. Left sidebar → **Storage & Databases**
   (older accounts: **Workers & Pages** → **KV** — same destination)
2. Click **KV**
3. Click **Create a namespace** (top right, blue)
4. In **Namespace Name**, type exactly:

       robot_trainer_students

5. Click **Add**

**Checkpoint:** `robot_trainer_students` appears in the list with 0 keys.
Not there? It wasn't created. Redo.

---

## Step 2 — Create the Worker

1. Left sidebar → **Compute (Workers)**
   (may read **Workers & Pages**)
2. Click **Create** (top right)
3. Click **Start with Hello World**
   (sometimes **Hello World** or **Create Worker**)
4. In the name field, replace what's there with exactly:

       zumoauth

   Spelling matters. The site calls `zumoauth.weymuthd.workers.dev`. A typo
   here breaks everything with no useful error message.
5. Click **Deploy**
6. Wait. You get a success screen with a URL like
   `https://zumoauth.weymuthd.workers.dev`

**Checkpoint:** open that URL in a new tab. You should see `Hello World!`.
That confirms the Worker exists and is reachable. It does nothing useful
yet — expected. Keep this tab open, you'll reuse it.

---

## Step 3 — Paste in the real code

1. From the Worker's page, click **Edit Code** (top right)
   (may read **Quick Edit**, or show a `</>` icon)
2. An editor opens. The left pane holds the Hello World starter code.
3. Click once inside the left pane.
4. Select everything: **Ctrl+A** (Windows) or **Cmd+A** (Mac)
5. Press **Delete**. The pane should be completely empty.
6. Open `zumoauth-worker.js`, select all, copy.
7. Click back in the empty pane, paste.
8. Click **Deploy** (top right of the editor). Confirm if asked.

**Checkpoint:** reload the tab from step 2. You should now see:

       {"error":"no such route"}

That is **correct**. The Worker is running and telling you the root path isn't
a route it handles. Still seeing `Hello World!`? The deploy didn't take —
redo step 8.

---

## Step 4 — Bind the KV namespace

The Worker cannot reach KV until you connect them. This is the step most often
skipped, and it fails silently.

1. Leave the editor — click **zumoauth** in the breadcrumb, or go to
   **Compute (Workers)** and click `zumoauth`.
2. Click the **Settings** tab
3. Find **Bindings** → click **Add** (or **Add binding**)
4. Choose type **KV namespace**
5. Two fields appear:
   - **Variable name** — type exactly:

         STUDENTS

     All capitals. The code looks for `env.STUDENTS`. Lowercase breaks it.
   - **KV namespace** — choose `robot_trainer_students` from the dropdown
6. Click **Deploy** or **Save**

**Checkpoint:** Bindings now lists one entry, `STUDENTS` →
`robot_trainer_students`. Empty section means it didn't save.

---

## Step 5 — Add the session secret

1. Still in **Settings**, find **Variables and Secrets**
2. Click **Add**
3. **Type** — choose **Secret**, not Text. Secret encrypts the value.
4. **Variable name** — type exactly:

       SESSION_SECRET

5. **Value** — mash the keyboard, 40+ characters, letters and numbers.
   You never need to remember or retype this.
6. Click **Deploy** or **Save**

**Checkpoint:** the list shows `SESSION_SECRET` with the value hidden as dots —
the same way `ANTHROPIC_API_KEY` looks in your other Worker.

---

## Step 6 — Create the test student

No record, no login. Students cannot create their own accounts. That is
deliberate — it's why a stranger can't sign up.

1. Left sidebar → **Storage & Databases** → **KV**
2. Click `robot_trainer_students`
3. Click **Add entry** (may read **+ Add** or **Create entry**)
4. **Key** — type exactly:

       student:teststudent

   The `student:` prefix is required. It's how the code finds records.
5. **Value** — paste this, one line, exactly:

       {"username":"teststudent","pinHash":null,"salt":null,"createdAt":"2026-07-18","progress":{},"events":[]}

6. Leave expiration blank. These records should never expire.
7. Click **Add** or **Save**

**Checkpoint:** the namespace shows 1 key.

---

## Step 7 — Test the whole chain

Upload `login.html`, `home.html`, and the updated `style.css` to the
robot-trainer repo first. Wait a minute after pushing — GitHub Pages takes a
moment to rebuild.

1. Go to `https://weymuth.github.io/robot-trainer/login.html`
2. Username: `teststudent`
3. Leave the PIN box **blank**. Click **Continue**
4. **Expected:** the page switches, says no PIN is set for teststudent, asks
   you to pick one.
5. Type a 6-digit PIN twice. Click **Set PIN and continue**
6. **Expected:** you land on home, top bar reading "Signed in as teststudent"
7. Click **Sign out**
8. Sign in again — `teststudent`, this time with the PIN you set
9. **Expected:** straight to home
10. Click **Textbook**. zumo opens in a new tab; this page stays put.
11. Back in Cloudflare: **KV** → `robot_trainer_students` →
    `student:teststudent` → **View/Edit**
12. **Expected:** the value now contains `pinHash`, `salt`, `lastLogin`, and
    inside `events`, an entry reading `"textbook"` with a timestamp.

Step 12 showing that event means the whole chain works — auth, session,
tracking, storage.

---

## If something fails

| Symptom | Cause | Fix |
|---|---|---|
| "Can't reach the server" | Worker name typo, or not deployed | URL must be exactly `zumoauth.weymuthd.workers.dev` and show `{"error":"no such route"}` |
| "That username isn't on the roster" | KV key wrong | Must be `student:teststudent`, not `teststudent` |
| Login works, home bounces back to login | Cookie blocked | Check the browser isn't blocking third-party cookies; try another browser to confirm |
| Works, but no event in KV | Binding missing | Redo step 4. `STUDENTS`, all capitals |
| `{"error":"server error"}` | KV not bound | Same as above |

---

## Adding real students in September

Repeat step 6 per student, changing only the username. Key is
`student:<username>`, lowercase, email prefix only:

    {"username":"weymuthd","pinHash":null,"salt":null,"createdAt":"2026-09-01","progress":{},"events":[]}

Twelve students is twelve entries, about five minutes by hand. If that's
tedious, say so and I'll write a bulk-import method — but at this class size,
by hand is fewer moving parts.

---

## Resetting a forgotten PIN

1. **KV** → `robot_trainer_students` → `student:<username>` → **Edit**
2. Change `"pinHash":"<long string>"` to `"pinHash":null`
3. Change `"salt":"<string>"` to `"salt":null`
4. Save

The student signs in with a blank PIN and picks a new one.

**Their work is not lost.** PIN is a credential, not identity — progress and
events hang off the username and are untouched. Do not delete the whole
record; that erases everything.

---

## What this does not do

- No teacher view. Reading a student's record means opening KV by hand.
- No progress writing yet — outbound-click events only. Progress lands when
  code submission is built.
- No scroll or dwell tracking. That needs a snippet inside the zumo book
  pages, which is a zumo edit, and waits for the book to be finished.

## Note on the 6-digit PIN

A 6-digit PIN is one million combinations — weak in isolation. Three things
make it acceptable here: PBKDF2 at 250,000 iterations makes cracking a KV dump
slow, a per-student salt means one cracked PIN doesn't help with any other, and
8 wrong tries triggers a 10-minute lockout, which makes online guessing
useless.

This protects schoolwork from classmates. It is not bank-grade. No grades, no
personal data beyond a username.
