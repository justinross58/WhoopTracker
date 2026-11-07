# WhoopTracker — Live HR

A single-page web app that shows live heart rate, R-R intervals and HRV (RMSSD) from a
WHOOP 4.0 band, right in Chrome on Android. No app to install.

It uses the band's **standard Bluetooth Heart Rate service** (`0x180D` / `0x2A37`), so it
only listens: nothing is written to the band and no stored data is removed. The WHOOP app
keeps working normally alongside it.

## Host it on GitHub Pages

Web Bluetooth only works over HTTPS, which GitHub Pages provides.

1. Create a new repository and add `index.html` (and this README) to the root.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose
   `main` and `/ (root)`, then **Save**.
4. After a minute your page is live at `https://justinross58.github.io/WhoopTracker/`.

## Use it on your phone

1. Open the page in **Chrome** on Android (Samsung Internet and Firefox don't support Web Bluetooth).
2. Optional: Chrome menu → **Add to Home screen** so it opens like an app.
3. Tap **Connect band**, allow Bluetooth/Nearby devices, and pick your `WHOOP …` band.
4. If it connects but no heart rate appears, turn on **Heart Rate Broadcast** in the WHOOP
   app's device settings and reconnect.
5. Tap **Save CSV** to download the session (`time_iso, unix_ms, heart_rate_bpm, rr_ms`).

**Demo** shows simulated data so you can try the page without the band.

## Limits

- Chrome drops the Bluetooth connection when the screen locks or you switch apps. The page
  keeps the screen on while connected and reconnects automatically when you come back, but
  it isn't meant for all-day background collection. That needs an installed app.
- Only heart rate and R-R intervals are available through the standard service. Raw sensor
  data and the band's stored history need the WHOOP custom service (see
  [johnmiddleton12/wearable](https://github.com/johnmiddleton12/wearable)).
- RMSSD is calculated over the last 60 seconds of R-R intervals after dropping impossible
  beats (outside 300–2000 ms) and jumps of more than 20%.

Not a medical device. Not affiliated with WHOOP, Inc.
