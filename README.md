# Star Trek Timelines Spreadsheet Tool
A tool to help with crew management in Star Trek Timelines

**NOTE** This tool does not (and will never) automate any part of the game play; its sole purpose is to help players organize their crew using the functionality built within or with a spreadsheet application of their choice.

**DISCLAIMER** This tool is provided "as is", without warranty of any kind. Use at your own risk!
It should be understood that *Star Trek Timelines* content and materials are trademarks and copyrights of [Disruptor Beam, Inc.](https://www.disruptorbeam.com/tos/) or its licensors. All rights reserved. This tool is neither endorsed by nor affiliated with Disruptor Beam, Inc. ( [more](/docs/DBSupport.png) )

[More tools and information here](https://iampicard.github.io/)

## Install and run the tool

I recommend you install the development environment and play with the source code yourself; make improvements and submit PRs to help your fellow players. See [contribution guidelines](/docs/CONTRIBUTING.md).

However, if you're only interested in installing and running the tool, head on to the [releases](https://github.com/IAmPicard/StarTrekTimelinesSpreadsheet/releases) page and pick a recent release to install.

## Features

### TODO - based on user feedback

- [ ] List all crew (even unowned one)
- [ ] Voyage recommendations (this is actually in progress now, and an initial version will be included in the next release)
- [ ] Dark mode (white is way too bright): I agree but HTML / CSS is not my cup of tea - any help from a frontend guy/girl would be welcome
- [ ] Export (CSV or XLS) for item list
- [ ] Gauntlet improvements (I know I left that half-done, sorry)
- [ ] Show more details in the fleet table (like captain level)
- [ ] Export voyage log
- [ ] Recommendations tab redesign (too messy, not user friendly)
- [ ] Arena recommendations (? not sure what that means, maybe best crew for manning a ship)
- [ ] Helper tools for items (what's most needed, where to find them, notification when replicator uses are about to go unused)
- [ ] XP in the crew list (to know who can still earn XP)
- [ ] Option to hide frozen crew and buy-back crew everywhere
- [ ] Crew traits not readable on smaller screen resolutions

#### Other popular feedback
**Reload / refresh (or variants)**. I get asked for this a lot; unfortunately, DB didn't really design the game for that. You can see the same issue if you play on the phone and Facebook / Steam at the same time; things quickly go out-of-sync. However, I did add a "Refresh" button in the popout that shows up when you click on your captain name (upper-left). This will refresh everything (not just one tab), but it will be slightly faster than closing and reopening the app

**Display 100 FF/FE stats for all crew**. For this to work, I'd need to depend on a different data source besides the game server itself (most popular recommendation is the stt.wiki). While I appreciate the stt.wiki and the work put into it, I don't believe that data is reliable (nor is it readily parsable / consistently formatted). In a very early version of my tool I depended on the stt.wiki for the crew portrait images (and my app became unusable when the wiki was down for a few days). I'll only trust the official game server for data (as that's the only reliable source).

### Crew management

![Screenshot tool](/docs/Screenshot-Tool.png "Tool screenshot")

The first tab lets you manage your crew. You can sort by various fields, (un)group by rarity as well as export the data in Excel, CSV, JSON or HTML formats.

### Item management

![Screenshot Items](/docs/Screenshot-Items.png "Items screenshot")

This tab lists out all the items you currently have, along with their quantity and type.

### Ship management

![Screenshot Ships](/docs/Screenshot-Ships.png "Ships screenshot")

This tab lists out all the ships you currently have, along with their stats.

### Missions

![Screenshot Missions](/docs/Screenshot-Missions.png "Missions screenshot")

This tab give an overview of all accepted missions and cadet challenged, along with individual requirements and player stats for each quest and challenge, as well as crew success rates for each challenge (node).

### Crew recommendations

![Screenshot CrewRecommendations](/docs/Screenshot-CrewRecommendations.png "CrewRecommendations screenshot")

*Work in progress!*

This tab will make recommendations about which crew you can freeze or airlock, and which you need to keep in your active roster, primarily for cadet challenges.

### Gauntlet

![Screenshot Gauntlet](/docs/Screenshot-Gauntlet.png "Gauntlet screenshot")

In this tab you can get recommendations for which crew to use in your next gauntlet (if you didn't already start it), and odds for crew matches (if you already started a gauntlet). Please see source code for details, the algorithm is still "hand-wavy" at this point and could use input from someone more experienced with statistical analysis.

![Screenshot Gauntlet Round](/docs/Screenshot-GauntletRound.png "Gauntlet Round screenshot")

### Fleet

![Screenshot Fleet](/docs/Screenshot-Fleet.png "Fleet screenshot")

Basic information about your fleet such as a member list with their last online and event ranks and starbase rooms' status.

### Share your crew stats

![Screenshot Sharing](/docs/Screenshot-ShareOnline.png "Sharing screenshot")

You can export a formatted html page with your crew stats and (optionally) your mission completion stats either to the local PC or directly upload it online, ready to send a link wherever you want - maybe your fleet-mates or to the forum / reddit / discord to ask for advice or just brag :wink: .

### Crew active state

![Screenshot Voyage](/docs/Screenshot-Voyage.png "Voyage screenshot")

You can inspect the active state of crew by clicking on the little "baloon" icon. This can tell you whether the crew is currently on a shuttle adventure or on a voyage as well as details about remaining time, loot, etc.

## Development environment

### To get started:
Clone the repo and build.

Minimal set of steps required (on a Windows machine)
* `git clone --recurse-submodules https://github.com/IAmPicard/StarTrekTimelinesSpreadsheet.git`
* `cd StarTrekTimelinesSpreadsheet\sttapi`
* `npm install`
* `cd ..`
* `npm install`
* `node_modules\.bin\electron-rebuild.cmd`
* `npm run dev`

*Note*: if for some reason the above steps are not sufficient, you may need to manually build in STTApi\AssetParser (with npm install) before building STTApi.

##### Development
* Run `npm run dev` to start webpack-dev-server. Electron will launch automatically after compilation.

##### Production
_You have two options, an automatic build or two manual steps_

###### One Shot
* Set ELECTRON_BUILDER_ALLOW_UNRESOLVED_DEPENDENCIES=true and run "electron-builder" to build the native package
* Run `npm run package` to have webpack compile your application into `dist/bundle.js` and `dist/index.html`, and then an electron-packager run will be triggered for the current platform/arch, outputting to `builds/`

###### Manual
_Recommendation: Update the "postpackage" script call in package.json to specify parameters as you choose and use the `npm run package` command instead of running these steps manually_
* Run `npm run build` to have webpack compile and output your bundle to `dist/bundle.js`
* Then you can call electron-packager directly with any commands you choose

If you want to test the production build (In case you think Babili might be breaking something) after running `npm run build` you can then call `npm run prod`. This will cause electron to load off of the `dist/` build instead of looking for the webpack-dev-server instance. Electron will launch automatically after compilation.

## Privacy and security
There is no server associated with this tool, all state stays on your device. Here's a comprehensive list of URLs that the tool accesses (all these URLs are accessed over a secure (HTTPS) connection):
- https://thorium.disruptorbeam.com/ : this is the login URL for DisruptorBeam; your username / password or Facebook access token is sent to this URL in order to get an access_token. This URL is only accessed during login.
- https://stt.disruptorbeam.com/ : this is the main Star Trek Timelines API endpoint URL, owned by DisruptorBeam.
- https://api.github.com/repos/IAmPicard/StarTrekTimelinesSpreadsheet/releases : this URL contains the list of tool releases. It's accessed during application boot (and from the About tab) to check for new versions. No data is sent along with the request (it's just a GET).
- https://logic.azure.com : this URL is accessed when (and only if) you submit user feedback. The only data included with the request are the fields in the feedback dialog itself. No other data is sent.
- https://ptpb.pw : this URL is accessed when (and only if) you use the Share dialog to share your crew stats online.
- https://www.facebook.com/v2.8/dialog/oauth : this URL is only accessed if you use the Facebook login option. It's used to obtain a facebook access token which is later sent to DB's server to get an access_token.

The tool never stores your username or password and it only sends it to DisruptorBeam's official servers for login purposes. If you check the "Stay logged in" checkbox in the login dialog, the tool will store an access_token on your local device in the IndexedDB database.

I encourage you to only use a version of the tool from a trusted source (such as the [Releases](https://github.com/IAmPicard/StarTrekTimelinesSpreadsheet/releases) page on GitHub). If a "well intentioned" person online offers to send you a modified version with "extra features" ask for the source code and manually compare against what's here in the repo to ensure no malicious functionality was added.
