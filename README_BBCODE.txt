[SIZE="5"][COLOR="SeaGreen"]ALC Benchmark[/COLOR][/SIZE]
[COLOR="Gray"][i]Tests every Auto Lua Memory Cleaner method, Memory Garbage Collector and Shissu's LUA Memory against the game on its own, with a loading screen step, and shows Lua memory, the add-on pool and what each freed.[/i][/COLOR]

[SIZE="3"][COLOR="DarkOrchid"]Dependencies:[/COLOR][/SIZE]

This addon requires:
[LIST]
[*] [url="https://www.esoui.com/downloads/info4917-LibAPH.html"][COLOR="#FF69B4"]LibAPH[/COLOR][/url] [COLOR="Gray"][i](Required Unified helpers shared with my addons)[/i][/COLOR]
[/LIST]

Compatible with:
[LIST]
[*] [url="https://www.esoui.com/downloads/info4388-AutoLuaMemoryCleaner.html"][COLOR="#FF69B4"]Auto Lua Memory Cleaner[/COLOR][/url] [COLOR="Gray"][i](Needed for ALL TEST and ALC ONLY TEST)[/i][/COLOR]
[*] [url="https://www.esoui.com/downloads/info4086-MemoryGarbageCollector.html"][COLOR="#FF69B4"]Memory Garbage Collector[/COLOR][/url] [COLOR="Gray"][i](PC; gets its own phases in ALL TEST and a side in LOADING SCREEN TEST when it is installed)[/i][/COLOR]
[*] [url="https://www.esoui.com/downloads/info883-ShissusLUAMemory.html"][COLOR="#FF69B4"]Shissu's LUA Memory[/COLOR][/url] [COLOR="Gray"][i](PC; gets its own phases in ALL TEST and a side in LOADING SCREEN TEST when it is installed)[/i][/COLOR]
[/LIST]

[SIZE="3"][COLOR="DarkOrchid"]Demos[/COLOR][/SIZE]

[b]PC[/b]
[SPOILER]
[b]Results summary[/b]
[IMG]https://i.postimg.cc/90JpKTZJ/ALC-BENCHMARK-PC-results-summary.gif[/IMG]

[b]Timeline[/b]
[IMG]https://i.postimg.cc/Wb1SrWcD/ALC-BENCHMARK-PC-timeline.gif[/IMG]
[/SPOILER]

[b]Console[/b]
[SPOILER]
[b]Comparing runs[/b]
[IMG]https://i.postimg.cc/90V8vCkk/ALC-BENCHMARK-CONSOLE-COMPARE.gif[/IMG]

[b]Timeline[/b]
[IMG]https://i.postimg.cc/PxbKb0q9/ALC-BENCHMARK-CONSOLE-TIMELINE.gif[/IMG]

[b]Resizing the window[/b]
[IMG]https://i.postimg.cc/HkKSTQKP/ALC-BENCHMARK-CONSOLE-RESIZING.gif[/IMG]

[b]Resizing and moving the window[/b]
[IMG]https://i.postimg.cc/TYdN02gg/ALC-BENCHMARK-CONSOLE-RESIZING-MOVING.gif[/IMG]
[/SPOILER]

[SIZE="3"][COLOR="DarkOrchid"]Tests[/COLOR][/SIZE]

[LIST]
[*] [COLOR="Lime"]ALL TEST:[/COLOR] Vanilla, every ALC cleanup method [COLOR="Gray"][i](Automatic, Background, Aggressive, Deep Clean)[/i][/COLOR], and on PC Memory Garbage Collector and Shissu's LUA Memory, each with and without a loading screen; needs at least one of these cleaners. Every phase starts from a /reloadui. Each cleaner cleans once in each of its own phases, then cleans on its own for the rest of that phase [COLOR="Gray"][i](ALC with your threshold and cleanup delay, the other two on their own timers)[/i][/COLOR], and is held outside its own phases. Optional simulated actions [COLOR="Gray"][i](off by default)[/i][/COLOR]: idling, a short simulated combat and the inventory, then random ones, the same in every phase; Results, Summary and Timeline show what they triggered. The conclusion sets each cleaner against Vanilla and the other two against ALC.
[*] [COLOR="Lime"]ALC ONLY TEST:[/COLOR] the same test without the Vanilla phases.
[*] [COLOR="Lime"]VANILLA ONLY TEST:[/COLOR] Vanilla cleanups without ALC or other cleaners. Every phase starts from a /reloadui, like the ALC tests. Nothing cleans but the game's collector. Needs ALC disabled or its Auto Lua Cleanup off, and any other cleaners you use disabled too.
[*] [COLOR="Lime"]LOADING SCREEN TEST:[/COLOR] times loading screens only, for any mix of Vanilla, ALC, Memory Garbage Collector and Shissu's LUA Memory [COLOR="Gray"][i](the last two on PC)[/i][/COLOR]. Start inside a house you own: every load is a trip to one other house and back, after a few warm-up loads that are not counted. The same garbage is made before every load; Vanilla travels with it and every other side cleans it first. The order turns every round so drift hits every side alike. The Loading Screens page shows each side's median and spread, and each side against Vanilla with a verdict: faster, slower, about the same, or not settled yet.
[/LIST]

Each test runs with test garbage [COLOR="Gray"][i](50 MB held on PC, the add-on pool filled to 65 MB on console, held until 10 s before each phase ends, plus extra MB/s the cleaners can clean; Advanced Test changes both)[/i][/COLOR] or as [COLOR="Lime"]Real world[/COLOR] [COLOR="Gray"][i](only what your add-ons make)[/i][/COLOR], and can add a "+ reload" phase per method.

[SIZE="3"][COLOR="DarkOrchid"]What it records[/COLOR][/SIZE]

[LIST]
[*] Lua memory and the add-on pool: start, end, average and peak, plus before and after each loading screen and reload.
[*] ALC's cleanups, the method each one used and what it freed.
[*] What Vanilla freed [COLOR="Gray"][i](the game's own collector, and the loading screens and reloads in the phases)[/i][/COLOR], listed apart from ALC's; the benchmark's own loading screens before Before and After are left out of the verdict.
[*] On console, each "Low Add-On memory" warning, marked green when the phase survived it and red when it failed.
[*] Results, Summary, Timeline and Loading Screens pages in one window. The Summary opens with a conclusion, groups the rest under Best phases, Vanilla and Test, and has a Test time table under the phases: what the test's time went on, next to the total of every test it is compared with.
[*] Saved tests can be compared, several at a time; the conclusion then says whether they agree. An ALC ONLY TEST and a VANILLA ONLY TEST can also be compared as if they were one ALL TEST.
[*] A test cut off by a logout, disconnect or crash is kept, and it can be continued from the phase it stopped in.
[*] Low memory protection [COLOR="Gray"][i](when the game reports an add-on memory limit)[/i][/COLOR]: the game turns add-ons off at about 90 MB of add-on pool, so a phase keeps running while the pool stays at or below 88 MB, and the game's "Low Add-On memory" warning is only noted. It also acts early when the pool is climbing fast enough to reach 89.5 MB within a second, in every step of the test. The test's own garbage slows down from 85 MB [COLOR="Gray"][i](down to 5% near 88 MB)[/i][/COLOR]. The moment the pool goes past 88 MB, that phase fails with the pool it reached, and the test saves and reloads at once, before the game can disable the add-ons, and carries on with the next phase. In ALC phases on console ALC keeps the pool down itself from 70 MB, and with ALC's Reload When Add-On Memory Is Almost Full on, its reload counts for the phase and the test carries on. Turned off, the test carries on so you see what the game does. A phase that fails or is cut off shows in red with the reason on every page.
[*] The window stays closed during a test; a line of text under the compass shows the phase, timer and focus. If you open the window while a phase measures, the Summary says so and how many KB per second its redraws made.
[*] An edited saved test is marked as edited and invalid, and can't be compared with other tests. A test from another account or server is marked as such, and only tests recorded by the same account can be compared.
[/LIST]

[SIZE="3"][COLOR="DarkOrchid"]Slash Commands[/COLOR][/SIZE]

[LIST]
[*] [color=#00FFFF]/alcbench[/color]: shows or hides the window.
[*] [color=#00FFFF]/alcbench alc <seconds> <MB/s> real reload[/color]: starts ALL TEST.
[*] [color=#00FFFF]/alcbench alconly <seconds> <MB/s> real reload[/color]: starts ALC ONLY TEST.
[*] [color=#00FFFF]/alcbench vanilla <seconds> <MB/s> real reload[/color]: starts VANILLA ONLY TEST.
[*] [color=#00FFFF]/alcbench memory[/color]: shows or hides Lua and add-on pool memory at the top right of the screen.
[*] [color=#00FFFF]/alcbench setfps <FPS or uncapped>[/color]: caps the game at that frame rate [COLOR="Gray"][i](10 to 1000)[/i][/COLOR] or removes the cap, in chat and on screen [COLOR="Gray"][i](PC)[/i][/COLOR].
[*] [color=#00FFFF]/alcbenchbugreport[/color]: opens the bug report copy box [COLOR="Gray"][i](PC)[/i][/COLOR].
[*] [color=#00FFFF]/alcbench fill <MB>[/color]: makes that much garbage now.
[*] [color=#00FFFF]/alcbench stop[/color]: stops the test [COLOR="Gray"][i](or the loading screen test)[/i][/COLOR] and keeps what it measured.
[*] [color=#00FFFF]/alcbench clear[/color]: deletes all saved results.
[*] [color=#00FFFF]/alcbench help[/color]: prints the command list in chat.
[/LIST]

[COLOR="Gray"][i](seconds, MB/s, real and reload are optional and can go in any order)[/i][/COLOR]

Right-click the window [COLOR="Gray"][i](or press the Options button on a controller)[/i][/COLOR] for the tests under Run Test, the saved tests, and the test settings, Memory display and the test status line [COLOR="Gray"][i](under the compass)[/i][/COLOR] under Advanced options. On PC the menu also has Set FPS with the current cap in green.

[center]
[b][COLOR="Orange"]⚠️ CONSOLE TESTING NOTES ⚠️[/COLOR][/b]
This addon was developed and tested on [b][COLOR="#FF69B4"]PC / Steam Deck[/COLOR][/b] [COLOR="Gray"][i](using Force Console Flow for console testing)[/i][/COLOR].

[SIZE="5"][COLOR="Red"]LICENSE & USAGE[/COLOR][/SIZE]

Copyright © 2026 [COLOR="#FF69B4"]@APHONlC[/COLOR]. All rights reserved. See LICENSE.md

[COLOR="Gray"][i](For permissions or inquiries, contact [COLOR="#FF69B4"]@APHONlC[/COLOR] on ESOUI.)[/i][/COLOR]

[SIZE="5"][COLOR="Red"]Credits[/COLOR][/SIZE]
[b][COLOR="Orange"]I would like to thank the following:[/COLOR][/b]
[COLOR="Gray"][i](For providing resources and their awesome projects)[/i][/COLOR]
[url="https://wiki.esoui.com/Main_Page"][color=#fa9c1b]ESOUI Wiki[/color][/url]
[url="https://forums.elderscrollsonline.com/en/discussion/694799/console-addon-memory"][color=#fa9c1b]ESO Forums[/color][/url]
[url="https://github.com/esoui/esoui"][color=#fa9c1b]@sirinsidiator[/color][/url]

[b][color=#9CD04C]Check out my other addons/projects:[/color][/b]

[url="https://www.esoui.com/downloads/fileinfo.php?id=4388#info"][color=#fa9c1b]Auto Lua Memory Cleaner[/color][/url]
[url="https://www.esoui.com/downloads/fileinfo.php?id=4116#info"][color=#fa9c1b]Permanent Memento[/color][/url]
[url="https://www.esoui.com/downloads/fileinfo.php?id=3249#info"][color=#fa9c1b]Tamriel Trade Center, HarvestMap, ESO-Hub, ESOUI Auto-Updater[/color][/url] [COLOR="Gray"][i](Linux, macOS, SteamDeck, & Windows)[/i][/COLOR]

[b][color=#ff3300][SIZE="4"]BUG REPORTS[/SIZE][/color][/b]
If you encounter any issues, please submit a report here
[/center]
