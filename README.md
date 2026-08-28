# Journify · AI Trip Planner — Ada mockup

A single-file HTML mockup of the Journify travel-planner flow, driven by the
**`journify-itinerary`** Ada agent.

## What it does
1. **Produce itineraries** — day-by-day plan streamed from Ada into an Overview + Day 1…N tabs. The day tabs appear the moment generation starts and **light up** as each day fills in.
2. **Destination imagery** — hero + place thumbnails.
3. **Print the itinerary** — clean printable document generated from the itinerary text.
4. **Book your flight** — one **"Book your flight NOW!"** button sends a zero-input booking request to the agent; the booking playbook prepares a Malaysia Airlines round-trip link (KUL ⇄ destination, 1 adult, Economy) and the page is taken straight to the booking page via the `flight_booking` handoff event.

## Destination restrictions
Journify does not create itineraries for **Israel** or any Israeli city. This is enforced
in the agent, not the page: a `destination_provided` gate at the top of the
**[Itinerary v7] Journify Travel Itineraries** playbook classifies the requested destination
before anything else runs, and declines with a fixed message, then sends `##end##`.

A global guidance instruction was tried as a backstop and is deliberately **left disabled**:
it pre-empted the planner, so the playbook never executed (no `##end##`), and it leaked its
canned refusal onto allowed destinations.

The page holds **no list of cities**. It only reacts to what Ada sends: the refusal text,
followed by an `##end##` control signal that tells it the turn is over.

## Running it
The page talks only to the live `journify-itinerary` agent — there is no offline mode.
It must be served over **HTTPS** from an origin on the agent's `iframe_allow_list`
(see below); `file://` is blocked and the SDK never starts.

## The one gotcha
The Ada chat iframe is CSP-gated by the agent's `iframe_allow_list`. The **exact origin
serving this page must be whitelisted** on `journify-itinerary` — no trailing slash.
