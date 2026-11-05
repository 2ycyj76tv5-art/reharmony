# REHARMONY v3: exact steps for each person

**New in v3:** all the Stage 1 exercises from the OUH NHS *Wrist fractures* leaflet are now in the concert: palm up/down (forearm rotation), the dart-thrower movement, fist/open hand (tendon gliding), and thumb to the base of the little finger. Long stretches (10-30 s) become a held note (fermata), with a countdown in the headset. There are ready-made programmes (Stage 1, Stage 2, Swelling pump, ...) and a pain check (0-10) before and after.

**The idea in one line:** the clinician conducts in front of a webcam and **Mozart copies their arms** in VR; the patient (Quest 3) follows Mozart's orders with their wrist, and every correct movement plays the music on a **speaker** both people can hear.

## What you need

| Device | Who | What runs on it |
|---|---|---|
| **Laptop 1** (Windows, RTX 5060) | P1 | `START_SERVER.bat` (the server). Also the patient page in **Pro mode**. |
| **Laptop 2** + **external speaker** + its **webcam** | P2 / clinician | `clinician.html`: the camera tracks the clinician, the music plays here |
| **Meta Quest 3** | the patient | `patient.html` in the Quest Browser (standalone), or via Link (Pro mode) |
| Phone hotspot (backup) | anyone | Use it if the venue Wi-Fi blocks devices from seeing each other |

Apps: **Python 3.12** on laptop 1 (tick "Add to PATH"). **Chrome or Edge** on both laptops. For Pro mode only: **Meta Horizon Link** on laptop 1.
Laptop 1 needs **internet the first time** (it downloads the camera-tracking files once, about 15 MB). three.js is already included.

---

## STEP 1 (P1): start the server
1. Unzip `REHARMONY_v2.zip`, open the `reharmony` folder, and double-click **`START_SERVER.bat`**.
2. **Windows Firewall:** tick **Private networks** and click **Allow**.
3. The window prints two addresses: **Quest 3 (patient)** and **Clinician (other device)**. Keep the window open.

## STEP 2 (P2): the clinician laptop
1. Plug in the **speaker**. Open the **Clinician** address in Chrome or Edge, then click **Advanced → Proceed**.
2. Follow the screen. It's a guided page with 5 steps:
   1. **Welcome & connect:** press **Turn on sound** (you should hear a chord) and **Turn on camera** (allow the camera). Stand about 1.5 m back so your arms are visible.
   2. **Calibrate:** choose the hand, press **Save relaxed position**, then **Start measuring** → the patient moves gently (up, down, both sides, then palm down and palm up with the elbow tucked in) → **Finish measuring**. Then tap the patient's **pain score before** (0-10).
   3. **Plan the concert:** choose the music (two Mozart pieces + Beethoven), the difficulty, then a **programme**:
      - **Stage 1 · after the cast** (OUH leaflet): fist & open hand, thumb to each finger + base, wrist up & down and palm up & down with **10 s holds**, dart thrower. 5 repetitions.
      - **Stage 2 · longer stretches**: wrist and forearm with **30 s holds**, the other hand gently helps. Only when the physio says so.
      - **Swelling pump**: hand raised, quick full fists.
      - **Classic concert** / **Thumb & fingers**.
      You can still switch each exercise group on or off and change the hold time and repetitions.
   4. **Conduct:** choose **Automatic** (follows the plan), **Camera gestures** (your movements give the orders) or **Buttons only**.
   5. **Results:** tap the **pain score after**, then see the chart, table and CSV (the CSV includes holds, pain before/after and the programme).
3. The panel on the right always shows **what the patient sees** (live 3D), the live wrist angles and your camera.

**Camera gestures (Conduct step, "Camera gestures" mode):**
- Make one clear, quick stroke with your **right hand**: **up** = wrist up, **down** = wrist down, **to your left / right** = toward the patient's thumb or little finger (the screen takes care of which hand is in therapy).
- **Left thumb to a fingertip** (or to the base of your little finger), held for half a second = that thumb exercise.
- **Left fist**, held for half a second = "make a full fist".
- Mozart copies both your arms the whole time the camera is on.

Keyboard backup on the clinician laptop: **↑ ↓ ← →** wrist exercises · **Q / E** palm down / up · **W / S** dart throw back / forward · **F / G** fist / open · **1-4** thumb to fingertips · **5** thumb to base of little finger · **Space** pause · **Esc** skip the intro.

## STEP 3 (patient): the Quest 3

**Standalone (simplest):**
1. Put the controllers down (hand tracking on: Quest Settings → Movement tracking → Hand tracking).
2. Open the **Browser**, type the **Quest 3 (patient)** address, then **Advanced → Proceed**.
3. Press **Enter the concert hall**.

**Pro mode (better graphics, uses laptop 1's graphics card):**
1. On laptop 1, open **Meta Horizon Link** and connect the Quest (cable or Air Link). In the Link app: **Settings → General → OpenXR Runtime → Set Meta Horizon Link as active**. For hand tracking over Link, also turn on **Settings → Beta → Developer runtime features** (if it's not available, the patient can hold a controller instead; see below).
2. On laptop 1, open **https://localhost:8443/patient.html** in **Chrome or Edge**. The page says *"Quest 3 Pro mode"*.
3. Press **Enter the concert hall**. The picture now comes from laptop 1 through Link.

**If hand tracking isn't available** (some Link setups), the patient holds **one Touch controller** in the therapy hand. Tilting the controller measures the wrist. Trigger / grip / A / B stand in for thumb to pointer / middle / ring / little.

## What happens in a session
1. **Intro** (clinician presses *Play the intro for both of us*): Mozart and Clara explain the story, both roles, and why gentle regular exercise helps. It has voices and music on the speaker, subtitles in VR, and a cinematic camera on the clinician screen.
2. **Instrument:** the patient tilts the hand left or right to choose from **13 instruments** and pinches thumb and pointer to pick.
3. **Concert:** Mozart gives each order with a big gesture, a golden baton trail and a scroll ("Lift your bow!"). The music stand shows a picture of the movement. When the patient reaches the target and holds it, the next phrase plays, Mozart says *Bravo* and the orchestra wakes up section by section. Each exercise has its own musical ornament (a turn for palm up/down, a harp glissando for the dart throw, a drum roll for the fist, a harp spread for the open hand, a gong for the thumb-to-base). During a long stretch, Mozart holds his arms up in a fermata, the orchestra holds a growing chord and the scroll counts down.
4. **Finale:** the full orchestra plays, the audience applauds, and the results appear.

## Testing without the headset
Open the patient page on any laptop and click **Keyboard mode**. Tick *"Play the music on this device too"* if no clinician laptop is connected. Keys: ↑/↓ wrist up/down · ←/→ thumb side / little side · Q/E palm down/up · W/S dart back/forward · F/G fist/open · 1-4 thumb to fingertips · 5 thumb to base of little finger · Esc skips the intro.

## Roles until the pitch
| Person | Job |
|---|---|
| **P1** | Server + Quest (standalone first, then try Pro mode). Tune target % and hold time with real hands. |
| **P2** | Clinician laptop: camera position and lighting, practise the gestures, run sessions. |
| **P3** | Sound check with the real speaker (volume, piece choice), test all 13 instruments, check the intro voices. |
| **P4** | Patient in every test, slides, pitch script, evaluation sheet, and play the intro video in the pitch. |

## If something goes wrong
- **The Quest can't open the page:** same Wi-Fi? Firewall allowed? Try a phone hotspot for all devices, then restart the server.
- **Camera says "problem":** allow camera access in the browser (lock icon → Camera → Allow). Laptop 1 must have had internet once to download the tracking files. The buttons always work.
- **No sound:** press *Turn on sound* again, and check the speaker is the Windows output device.
- **Mozart doesn't copy you:** step back so your shoulders, elbows and hands are all in the camera picture, in good light.
- **It runs slowly on the Quest:** use Pro mode, or close other Quest apps.

## Easiest: the online website (no server, any network)
The folder **REHARMONY_website** (also in its own zip) is the whole website, ready to host for free:
1. **Host it once** on GitHub Pages (permanent link) or Netlify Drop. The steps are below.
2. **Everyone opens the same link**, e.g. `https://yourname.github.io/reharmony/`:
   - **Clinician laptop:** **I am the Maestro → Start a session**. The screen shows a **4-digit code** and a **QR code**.
   - **Quest 3 Browser:** **I am the Player** → type the code on the big number pad → **Join the concert** → **Enter the concert hall**.
3. The two devices connect through a free public relay (MQTT over secure WebSocket). They only need internet, not the same Wi-Fi, and no firewall settings. "✓ Paired" and the live delay show as usual.

**GitHub Pages (about 5 minutes, free, the link never changes)**
1. Create a free account on github.com → **New repository** → name it `reharmony` → **Public** → **Create**.
2. Click **uploading an existing file** → drag **everything inside** the `REHARMONY_website` folder (index.html, clinician.html, patient.html, the `js` and `vendor` folders) → **Commit changes**.
3. **Settings → Pages** → *Branch*: `main`, folder `/ (root)` → **Save**. After about 1 minute your link appears: `https://<your-name>.github.io/reharmony/`.

**Netlify Drop (fastest, about 1 minute):** go to app.netlify.com/drop, sign in (free), and drag the `REHARMONY_website` folder onto the page. You get a link like `https://random-name.netlify.app`.

Notes: the online relay is a public service, so only movement numbers are sent and no names. Use the CSV button on the results page to keep the data. The Unity app still uses the laptop server (`START_SERVER.bat`).

## Pairing: how you know the patient and clinician are in sync
- The clinician page shows a **room code** (e.g. `1490`) and a **QR code** of the patient link in step 1.
- **The headset pairs by itself** when only one clinician page is open (the usual case, with clinician and patient in the same room). Nothing to type.
- With **several clinician pages** on the same server (e.g. the online link at a hackathon), the patient's start screen asks for the room code: type the 4 digits and press **Join**. Opening `…/patient.html?room=1490` (the QR link) also joins directly. In Unity, put the code in `ReharmonySettings.RoomCode`.
- **Proof of sync** on the clinician screen:
  - **"✓ Paired: the headset is live"**, plus **Live delay: … ms**, checked every 1.5 s. On normal Wi-Fi this is 5–40 ms; above 300 ms it warns about slow Wi-Fi.
  - **👋 Wave to the patient**: the headset flashes "Your clinician waves hello!", Mozart celebrates, and the screen confirms *"✓ Seen in the headset after … ms"*.
  - The header pill shows **Headset ✓ 12 ms** at all times. It turns to **Headset ?** if the headset stops answering (taken off, asleep).
- The patient's start screen says **"Paired with your clinician ✓ (room 1490)"**.
- The room code stays the same when the clinician page is reloaded.

## Online link (devices on different networks)
Double-click **START_ONLINE.bat** instead of START_SERVER.bat. The first time it downloads `cloudflared`, a free tool from Cloudflare, so it needs internet. After 5–15 seconds the black window prints:
```
Quest 3 (patient):   https://something-random.trycloudflare.com/patient.html
Clinician:           https://something-random.trycloudflare.com/clinician.html
Unity app address:   wss://something-random.trycloudflare.com/ws
```
- These links work from **any network** (school Wi-Fi, 4G, home), and there's **no "Advanced → Proceed"** step: the certificate is real.
- They are also saved in **ONLINE_LINKS.txt**. The link **changes every time** you restart, so send the new one to your team.
- Anyone with the link can open it, so share it only with your team.
- The local links (same Wi-Fi) still work at the same time.

## Unity version (optional)
The folder **REHARMONY_Unity** has a native Quest 3 app made in Unity. It uses the same server and the same clinician page. Read `REHARMONY_Unity/README_UNITY.md`. The server now also opens port **8080** and broadcasts on UDP **8099** so the Unity app finds the laptop by itself. If Windows asks, allow Python on private networks.

## Safety
REHARMONY supports a physiotherapy plan; it doesn't replace it. Targets are always a percentage of the range measured in calibration. The leaflet's guidance is used throughout: work to an "unpleasant stretch" (about 5/10) that settles within about 30 minutes. The headset reminds the patient to stop and tell the clinician if anything feels sharp. The clinician can pause at any time (Space).
