# Fire Emblem style tactics

A turn based tactics game that runs in a browser. One HTML file, no install,
no account. Open it on a phone, a tablet or a computer and play. Up to six
people can play the same battle across separate devices.

Live at `casimbahadar.github.io/fe-tactics/`.

---

## What you can play

### The campaign
Eighteen chapters, each built around one thing to learn: armour that needs
magic, fliers that need bows, a wall of resistance, a healer, mounts, flight.
Six of those chapters are real gates, meaning a company without the answer is
genuinely stopped rather than merely slowed. The difficulty of each was set by
running the chapter hundreds of times at different enemy levels and reading
the results, not by guessing.

Nobody dies permanently. A soldier who falls is back for the next chapter,
keeps their experience, and can be rebuilt before the next march.

### Score Run
One battle. Type a seed and everyone who types the same seed gets the same
map, the same enemies and the same six soldiers, so scores can be compared.
Combat rolls stay random. Points: a win is 1000, each kill 50, each turn taken
costs 20, each soldier lost costs 150.

### Gauntlet
Five battles that get harder, with one squad and no healing in between.
Damage and weapon wear carry over. Anyone who dies is gone for the rest of the
run. Experience earned counts for the run only. The difficulty was found by
having a bot play whole gauntlets: sloppy play dies around the third battle,
while a squad that heals up before each fight can go the distance.

### Split Field
Two to six squads on one map against a shared enemy army, all scored
separately. You can attack rival squads, but each rival killed costs you 100
points. When the enemies have a choice of equal targets they go for whoever
has damaged them most, then the weakest, then whichever squad the turn number
picks. That rule is stated on screen so nothing feels arbitrary.

### Hold the Point
A guarded fort in the middle. End your turn with a soldier alive on the fort
and you score a hold; three holds wins. Stepping off or losing that soldier
freezes your count until you take the fort back. At turn 15 the most holds
wins, then the higher score.

### Team Battle
Players against players with no computer army, in nine formats: 1v1, 1v2,
1v3, 1v4, 1v5, 2v2, 2v3, 2v4 and 3v3. Squads on the same side cannot hurt
each other, do not block each other's movement, and their scores add
together. Win by clearing the other side off the map or by leading at turn 20.

---

## Playing with other people

**On one device.** Split Field, Hold the Point and Team Battle can be passed
between people on a single phone. Each player moves only their own squad.

**Across devices.** Challenges, then Online. One player opens a room, picks
how many players it holds, and shares a six character code. Everyone else
types the code. The player who opened the room starts it whenever they like;
two is enough, you never have to fill the room. It works across any mix of
phones, tablets and computers.

Everyone sees the same map and the same dice, because the battle is played
from a shared list of moves rather than by sending pictures of the board
around. Moves appear within about a second.

There is a **Test the connection** button that checks the whole chain from one
device with nobody else involved. Worth running before showing the game to
anyone, since the server sleeps when unused and takes a moment to wake.

---

## Bringing your own squad

Any challenge can be fought with:

- **The standard six**, which keeps scores comparable between players.
- **Your own roster.**
- **Your roster under a budget**, 60 points at one per level.
- **A company code** somebody sent you.

Anything other than the standard six is scored on a separate board, so each
board only compares like with like.

**Company codes.** Company, then Share, turns your squad into a block of text
anyone can paste. Names, classes, levels, the stats they grew, what they carry
and its remaining uses all travel. Pictures you uploaded yourself do not,
because six of them would make the code far longer to paste; those soldiers
use their class picture instead. Anything the receiving game cannot use is
dropped with a note rather than breaking the import, and edited codes cannot
smuggle in impossible levels or stats.

---

## Building your own campaigns

The builder is on the cover screen.

**The world.** Name your continent, describe it, and list countries one per
line as `Aldenmark - horse country, rich, tired of paying for a war it did
not start`. This is saved with the campaign and travels with its share code.

**The story.** Pick one of six kinds: a grim war, a personal revenge, a
hopeful road with something underneath, a war to unite the land, a crisis over
who rules, or after the war. Each chapter then opens with a short briefing
built from your world. You can read every sentence the game can use and
rewrite any of them in your own words, and write `{land}`, `{country}` or
`{place}` where you want a name filled in. A sentence is only used when the
names it asks for exist, so an empty world still reads properly.

**Chapters.** Paint the map, place enemies, set the objective and the turn
limit, choose which enemies can be recruited by talking to them.

**Maps.** Chapters can use a ready made map instead of a painted one. Maps
made by other people are added on the Maps screen and stored in your browser
with their own tiles, so the file is never needed again. There is also a map
library kept beside the game: it lists what is available and downloads a map
only when you ask for it, so the library can grow without slowing the game
down.

Campaigns can be shared as a code or downloaded as a file.

---

## Soldiers

Build them yourself or generate a company. Classes combine two weapon types.
Soldiers grow, form bonds with whoever fights beside them, get tired if worked
too hard, and can be rebuilt for free if a build turns out badly.

Portraits can be uploaded. Any size or shape works: the whole picture is
scaled to fit the portrait window, so nothing is cut off and nothing is
stretched.

---

## How maps are made

Generated maps follow rules taken from real Fire Emblem chapter maps: one
connected walkable field with no sealed pockets, no lone wall tiles, water as
proper bodies rather than straggling lines, woods and hills grown as clumps,
and clear ground at the edges for both sides to muster. The tiles themselves
come from real Fire Emblem tilesets, and each one was chosen using that
tileset's own terrain data rather than by guessing what a tile looked like.
Four looks are available: plains, desert, mountain and snow.

Tap any square in battle to be told what it is and what it does for you.

Maps larger than the screen scroll, and the board follows whoever you select.

---

## How this is built

One HTML file with everything inside it, including the tiles and the
portraits. No build step, no libraries, no framework. It runs from a web
address, from a file on your computer, and offline once loaded. Online play is
the only part that needs a connection.

**Testing.** Nearly fifty test harnesses run the actual shipped code, not a
copy of it. Every new feature gets a harness written before the feature
exists, so it can be shown to fail first. Some notable ones:

- Six separate client processes play whole online matches against each other
  and must finish with identical boards and identical results.
- The battle is proved to depend on nothing but its own shared dice, by
  replaying the same match with the random generator pinned to opposite
  extremes and requiring identical output.
- Generated briefings are produced in the hundreds and checked for unfilled
  gaps, broken sentences, invented names, repetition, and vagueness.
- Map generation is checked across dozens of seeds for connectivity, clumping
  and terrain balance.
- The online server is tested by pretending to be an anonymous browser and
  confirming it refuses everything it should.

**The server**, used only for online play, stores rooms and the list of moves.
It holds no accounts and no personal information. Every read and write goes
through a checked server function; the tables themselves are closed.

---

## Credits

Tiles and portraits come from the Fire Emblem community graphics repository.
Maps made by other people carry their author's name in the game.

Built by Casim with Claude.
