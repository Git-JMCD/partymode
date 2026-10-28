# PartyMode guide

Everything PartyMode does, and how to set it up. The short version is on the
[home page](README.md).

- [Install](#install)
- [Using the chat](#using-the-chat)
- [What the agent can do](#what-the-agent-can-do)
- [Use it from a terminal agent](#use-it-from-a-terminal-agent)
- [Privacy and safety](#privacy-and-safety)
- [Optional: local AI generation](#optional-local-ai-generation)
- [Status](#status)
- [License](#license)

## Install

1. Download `PartyMode-<version>.zip` from [Releases](https://github.com/Git-JMCD/partymode/releases/latest).
2. In Blender 5.2 or newer, drag the zip onto Blender, or **Edit → Preferences → Get Extensions → ⌄ → Install from Disk**, pick the zip.
3. Click **PartyMode** in the 3D View header. The chat opens beside your viewport; click it again to
   close it (it reopens at the width you left it).

For the chat to answer, install and sign in to at least one agent:

| Agent | What you need | Billing |
|---|---|---|
| **Claude** | [Claude Code](https://claude.com/claude-code) | your Claude plan |
| **Codex** | [Codex CLI](https://github.com/openai/codex) | your ChatGPT plan |
| **OpenCode** | [OpenCode](https://opencode.ai), set up with a provider | OpenRouter, Hugging Face, Gemini, some free models, or local models through Ollama / LM Studio |

Click the agent chip in the message box to pick the agent, its model and how hard it thinks. Each
agent lists its own models (Claude's with their versions, Codex's and OpenCode's from the programs
themselves); type to filter a long list, or type any model name. Arrows and Enter pick, Esc closes.

The menu also shows each agent's **usage**: how much of its plan's 5-hour and weekly limits is
used (amber from 80%, red from 95%) and when the 5 hours reset. Codex's numbers come from its own
logs, so they include your sessions in its app or CLI. Claude's update with every Claude reply in
PartyMode; the refresh arrow asks again with one tiny message on its smallest model. OpenCode's
models have no plan windows. In a team, the lead is told its helpers' usage too, and keeps a
helper near its limit to small tasks.

**Preferences** (Edit › Preferences › Add-ons › PartyMode, or "All settings" in the menu): a
status box on top shows the server, which agents were found and the add-on's version, each with its
fix. Below it, five tabs:

- **Chat:** who answers, and a row per agent with its model, reasoning and team role.
- **Agents:** which agents the chat offers. Claude, Codex and OpenCode are built in. Grok Build,
  GitHub Copilot and Gemini CLI connect through the Agent Client Protocol (ACP): install one and
  switch it on. **Add an ACP agent** takes any other ACP agent by the command that starts it (for
  example `qwen --acp`). **Test** starts an ACP agent, connects it to Blender and lists its models
  without sending a message; a failed test is noted in PartyMode's feedback. Only agents switched on
  show in the agent menu and the team. ACP agents work through Blender's tools like the others: their
  own shell and file edits are refused. They don't report context size or plan usage. Meta's Muse
  models work through OpenCode, as a provider.
- **Web:** when agents may go online, and whether they ask first.
- **Look:** the chat's look, and marks in the viewport.
- **Setup:** agent programs, the server, ComfyUI and updates.

**Updates:** once a day, PartyMode asks GitHub whether a newer release is out (only while Blender's
**Allow Online Access** is on; turn it off under Setup › Updates). When one is, the chat's welcome
shows "PartyMode x.y.z is out · Install", and **Install** in the preferences' status box downloads it, checks it is this add-on at that version, and installs it over the old one
in place. Your chats, Sandbox and settings stay. It never installs while an agent is working.

## Using the chat

- Type what you want: *"add a wooden stool beside the table and check it stands on the floor"*.
- **Select and copy:** drag across the conversation to select text (double-click selects a word),
  then **Ctrl+C**. Esc or a click clears it.
- **@mentions:** type `@` to name a scene object, or press **@ selection**. The agent gets a short fact
  sheet on each one.
- **Sandbox:** a shelf in the .blend for references, SVG logos, notes and renders, shared with the
  agent. Open it with the tray button in the chat header or the **Sandbox** tab on the chat's right edge
  (it shows how many items it holds). Paste with Ctrl+V straight from Figma (Copy as PNG or Copy as SVG), a screenshot or the browser,
  or drop files on the chat; what you paste goes with your next message. Each card has one-click
  actions: an SVG becomes a 3D logo, a picture a plane or a colour palette for your objects.
- **Sandbox board:** the Sandbox is an endless canvas, like Figma's, where cards stay where you put
  them. Drag a card to move it, drag empty space (or middle-drag) to pan, scroll to zoom, drag a
  card's corner to resize it; Home or **Fit** frames everything. Drag the board's left edge to make
  it wider, or **Pop out** to give it an area of its own that you resize like any Blender area. The
  agent sees where cards sit (and can arrange them), so cards placed together read as a group.
- **Looks:** pick how the chat looks in the add-on's preferences. **Halo** (the default) is graphite
  with the answering agent's colour as light: a glowing orb, a lit focus ring and send key. **Signal**
  is an instrument panel: ink-black hairlines, tool steps as a timestamped log, labels in mono
  capitals. **Classic** is the original look in Blender's own fonts. Each agent (Claude, Codex,
  OpenCode) brings its own faint texture behind the chat, so who is answering reads at a glance.
  On a light Blender theme every look keeps the theme's colours.
- **Research without leaving Blender:** switch on **Research the next message** in the agent menu
  and the agent may search the web and read pages for that message, while your scene stays
  read-only. What it finds lands in the Sandbox: notes with links, and openly licensed pictures
  (searched through Openverse, with each one's licence, creator and page on its card; **Source**
  opens the page). Before each search, page or picture, the chat asks: **Allow**, **Allow for this
  chat** or **Deny**. You can turn the asking off in the preferences. The **Research** preference
  picks when the web is allowed:
  - **Off:** never.
  - **Per message** (the default): the switch, for one message.
  - **Auto:** whenever it helps. Once the agent has read the web, it asks once before it changes your
    scene that turn.
- **Background renders:** **Render** in the Sandbox makes a full render in a hidden second Blender, so
  yours stays free; it lands in the Sandbox, with progress and Cancel while it runs.
- **Suggestions:** select something and the chat offers a few next steps that fit it. After each reply the
  agent's guess at your next message waits in the empty message box: Tab takes it.
- **Mark an area:** press **Mark** and drag a box over part of the viewport (or any editor) to point at
  something that isn't a whole object: "make this corner less blobby". The agent sees a picture and a
  sharp close-up, and knows what's under the box in 3D: which faces, which material, where in metres.
  The red box stays on the model as you turn the view.
- **Render cards:** renders arrive as cards. A trial has **Keep**, **Before** and **Diff**; any render
  has **Lit render** / **Solid view**, **Undo last edit** and **Open**.
- **Quick actions** above the message box: Check scene, Lit render, Checkpoint (a save point), Undo.
- Tool steps fold into one line you can open. The header shows how full the agent's memory is, and
  past 60% offers to **continue in a new chat** with a handoff summary.
- Chats are saved. Reopen one from the sessions list and carry on, even with a different agent.
- The same chats are in your browser at `http://127.0.0.1:9900/chat`.

**Viewport bar.** The bar button beside **PartyMode** floats the same chat at the bottom of your
viewport. Only the bar takes your clicks and typing; everything else stays the viewport's.

## What the agent can do

67 tools, all running inside your Blender:

| Group | What it covers |
|---|---|
| Look | the scene, its hierarchy, any object's details, the areas you marked |
| Edit | run Python (with hints that correct common Blender API mistakes), undo |
| Safety | save points that survive restarts, try-before-you-keep trials with measured before/after, stop. A message you send while the agent is replying waits above the box and goes when the reply ends (Enter twice, or Send now, stops the reply so it goes straight away; × takes it back to edit) |
| Check | rests on / touching / clearance in metres, mesh health and real-world size, UV layouts, focused check renders; what fails is marked in the viewport (a red box where a part sank in, amber where a mesh has a hole), labelled in plain words |
| Repair | what the mesh check finds, fixed in one undo step: duplicate vertices, loose bits, zero-area faces, flipped normals; holes, faces inside the shape and generation debris when asked (never fills an object marked as open on purpose) |
| Lighting | studio, golden hour, noon, overcast and night in one call, with the light coming from where you say ("from the right", "backlit") so the shadows fall where you want; your own lights are kept or hidden, and calling again swaps the preset |
| Materials | wet, dirt in creases, worn edges, tint to a palette: layered over your textures and removable |
| Assets | Poly Haven models, textures and skies (CC0, at real size), plus your own asset libraries |
| Generate | your own ComfyUI workflows on your own GPU: text to image, text or image to 3D |
| Sandbox | references, SVG logos, notes and renders on an endless board kept in the file; turn them into planes, 3D logos or palettes, or save any of them as a file; full renders in the background |
| Review | contact sheets in one call: a turntable all round a prop, or a character across its clips, labelled and pinned to the Sandbox |
| Animation | foot sliding measured per step (also on rigs with plain bone names), the travel speed of an in-place clip so it won't skate in the engine, how much of a travelling clip is skating, and the loop seam (pops, and a last frame that repeats the first) |
| Tidy | find what makes a file heavy or hard to read (unused data, duplicate materials and images, empty collections, unused material slots, unapplied scale, default names, hidden heavy objects) and fix the safe ones in one undo step |
| Clean up | a generated or scanned mesh (hundreds of pieces, messy triangles) turned into clean quads, with its detail baked into colour, roughness and normal maps; the shape is measured against the original |
| Deliver | export for Unreal, Unity, Godot or the web, verified by importing the file back; levels of detail (each measured against the original: how far it strays in mm, and from how far away that is under a pixel), collision named the way each engine looks for it, and a warning for material nodes the file won't carry |
| Feedback | agents keep a journal of bugs, ideas, likes and dislikes about the add-on itself (`feedback_add`), outside the scene so undo or closing a file never loses it; every agent can read it |
| Rules | standing preferences per file or for every file ("always metres", "name meshes SM_…") |
| Team | your agents on one goal: tick helpers in the agent menu (Claude, Codex, OpenCode with a local or hosted model) and the agent you picked leads, handing each helper a task (more tasks for a busy helper wait their turn); they work at the same time, each on its own objects, and the lead checks their work and hands out fixes (a fix goes back to the same helper, which picks up where it left off; a helper that fails is reported to the lead straight away, so it can retry while the others keep working). You can talk to the lead while helpers work: your message goes to it straight away (or waits for its reply), the helpers keep going, and it sees where each one is; a helper with no word for 3 minutes shows "quiet for N min" in the chat, so a stall is easy to spot. Each helper's work (its steps, pictures and report) sits in a panel in its own colour, headed "helper for" the lead, so it never reads as the lead's own reply. Also: who did what, notes between agents, reading the chat, and claims ("I'm working on the bucket", even before it exists): another agent's edit of a claimed object is stopped before it runs and told who and why |

## Use it from a terminal agent

With Blender open, connect Claude Code (other MCP clients work the same way):

```bash
claude mcp add --transport http partymode http://127.0.0.1:9900/mcp
```

Each open Blender gets its own server: the first on 9900, a second on 9901, and so on. The add-on
preferences show which. A terminal agent and the chat's agent can work in the same Blender: each edit
is signed with who made it ("Agent (Codex): add wetness"), and they can leave each other notes.

### Without a Blender window (headless)

To leave Blender running in the background with no window, start it with your file and the add-on's
server (the add-on must be installed and enabled):

```bash
blender -b scene.blend --python-expr "import sys; next(m for n, m in sys.modules.items() if n.endswith('.agent_bridge')).serve_blocking()"
```

It prints the address it serves on and connects the same way as above. It uses the port in the add-on
preferences, or the next free one if a Blender window already has it; `serve_blocking(9905)` asks
for one port outright. Close the terminal (or press Ctrl+C) to stop it.

What's different without a window:

- **Save from the agent.** There's no File > Save, so ask the agent to save
  (`bpy.ops.wm.save_mainfile()`) before you stop Blender, or the changes are lost.
- **The web is turned down** while "Ask before the agent uses the web" is on, since there's no chat to
  ask in. Turn that preference off (in a Blender window) to let agents search and download here.
- **No undo:** `undo`, `try_edit` and `apply_trial` need a window. Save points (`checkpoint`) still work.
- The chat, the bar, marks and the Sandbox board are window-only. Checks still run and report in text.

## Privacy and safety

- The server listens on your own computer only (`127.0.0.1`) and refuses requests from web pages.
- Agents in the chat get this Blender's tools, plus file reading for Claude and OpenCode. They can't
  run shell commands or edit files outside Blender.
- They reach the web only for a message you send with **Research** on. That turn can't change your
  scene, so nothing read online can touch it. With Research set to **Auto**, the agent may use the web
  in any turn, but once it has, it asks before its first scene change that turn. The chat asks before each search, page or picture
  (on by default). Pictures come only over https, from public addresses, as images or SVG, up to
  25 MB.
- What you type, and the renders the agent looks at, go to the AI provider you picked. A local model
  keeps everything on your machine.
- Free models on some services may log or train on what you send. Check before using client work.
- The update check sends GitHub a plain request for the latest release, nothing about you or your
  scenes. It's skipped while Blender's Allow Online Access is off.

## Optional: local AI generation

Generation runs your own [ComfyUI](https://github.com/comfyanonymous/ComfyUI) at `127.0.0.1:8188`,
using saved workflows named in the add-on preferences (by default `IMAGE - Flux Schnell txt2img`,
`3D - TripoSG image to mesh` and `3D - TripoSG image to PBR mesh`). Everything else works without it.

**Remeshing** uses [Smart Remesh](https://superhivemarket.com/seller/milad_kambari) when it's installed
(a paid add-on; it handles more shapes) and Blender's own QuadriFlow otherwise.

## Status

Early, and moving quickly. Tested on Windows 11 with Blender 5.3 and 5.2. On 5.2, which can't show its undo history to
add-ons, save points restore by reloading their copy, `undo` only takes back the agent's own latest
edits, and the history of your own edits is less detailed. **macOS and Linux are untested:**
reports and fixes are very welcome.

## Reporting a bug

Bug reports are welcome: [open an issue](../../issues), and say what you asked for, what happened, and your Blender version and system.

## License

GPL-3.0-or-later, like Blender's own add-ons. The native build's patch is GPL-2.0-or-later, like
Blender's source. Poly Haven assets are CC0. The fonts in `addon/agent_bridge/fonts/` (Geist,
Geist Mono, Instrument Sans, JetBrains Mono, Martian Mono) are under the SIL Open Font License 1.1;
their licences sit beside them.
