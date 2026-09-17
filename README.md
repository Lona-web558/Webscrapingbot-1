# Webscrapingbot-1

# Follower Tracker

A tiny single-file HTML/CSS/JS demo that checks whether a given X (Twitter) profile URL and WhatsApp channel URL match expected platform domains, and tallies a mock "follower" count.

## Files

- `follower-tracker.html` — self-contained page (HTML + CSS + JS, no dependencies)

## How it works

1. Two sample links are hardcoded in the script:
   - `user` — an X profile URL
   - `whatsappurl` — a WhatsApp channel URL
2. Clicking **Run autostart** calls `autostartbutton()`, which:
   - Checks if `user` contains `"x.com"` → adds 10 to `netfollows`, logs `X <count>`
   - Checks if `whatsappurl` contains `"https://whatsapp.com"` → adds 10 to `netfollows`, logs `WhatsApp <count>`
   - If the WhatsApp check fails, logs `Unknown platform`
3. Output is printed both to the browser console and to the on-page log box.

## Usage

Open `follower-tracker.html` in any browser. No build step, no server required.

## Known logic quirk

The current structure is:

```js
if (user.includes(twitterapi)) {
  ...
}
if (whatsappurl.includes(whatsappapi)) {
  ...
} else {
  console.log("Unknown platform");
}
```

Because the two checks are separate `if` statements (not `if / else if`), the `"Unknown platform"` message only fires based on the **WhatsApp** check — it doesn't consider whether the X check passed or failed. If you want "Unknown platform" to mean *neither* link matched, combine the checks, e.g.:

```js
if (user.includes(twitterapi)) {
  netfollows += 10;
  log("X " + netfollows);
} else if (whatsappurl.includes(whatsappapi)) {
  netfollows += 10;
  log("WhatsApp " + netfollows);
} else {
  log("Unknown platform");
}
```

## Customizing

Update `user` and `whatsappurl` in the `<script>` block to point at real links you want to validate.
