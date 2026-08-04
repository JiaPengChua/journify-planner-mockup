# Journify · AI Trip Planner — Ada mockup

A single-file HTML mockup of the Journify travel-planner flow, driven by the
**`journify-itinerary`** Ada agent.

## What it does
1. **Produce itineraries** — day-by-day plan streamed from Ada into an Overview + Day 1…N tabs. The day tabs appear the moment generation starts and **light up** as each day fills in.
2. **Destination imagery** — hero + place thumbnails.
3. **Print the itinerary** — clean printable document generated from the itinerary text.
4. **Book your flight** — one **"Book your flight NOW!"** button sends a zero-input booking request to the agent; the booking playbook prepares a Malaysia Airlines round-trip link (KUL ⇄ destination, 1 adult, Economy) and the page is taken straight to the booking page via the `flight_booking` handoff event.

## Two modes (toggle top-right)
- **Offline preview** — works immediately with no setup; a built-in generator streams a realistic, v7-shaped itinerary so you can demo the whole flow (tabs, print, ask-anything follow-up).
- **Live · Ada** — wires the headless Embed SDK (`embed2.js`) to `journify-itinerary` and renders the real streamed itinerary.

## Just want to see it
Open the hosted link and use **Offline preview** — everything works with no setup.

## Enabling Live mode (the one gotcha)
The Ada chat iframe is CSP-gated by the agent's `iframe_allow_list`. To connect Live mode, the **exact origin serving this page must be whitelisted** on `journify-itinerary`, and the page must be served over HTTPS (plain `file://` is blocked — the SDK never starts). Offline preview needs none of this.
