# Zulip-terminal Changelog

## Next Release

No changes yet!

## 0.5.2 - 30 July 2020

This release contains the first batch of changes from this year's GSoC students, among other contributors - we're keen to get this out and let you have the improvements available!

### SECURITY NOTICE
This release fixes two security issues, so we strongly recommend upgrading immediately.

Note that notifications while running in WSL are temporarily removed in this release due to this.

### HIGHLIGHTS
- Links in messages are now shown more clearly with numeric references, with URLs as optional footnotes ('footlinks') and in the message information popup (#703/#618/#735)
- Typeahead/autocomplete suggestions are now shown dynamically in the footer (#540)
- The previous stream description popup can now be used to adjust stream properties (muting, pinning) (#695)
- An About popup was added to check application and server versions while running (#653/#616)
- Stream search and typeahead suggestions are ordered consistently, based on pinning and word sorting (#530)
- Messages from the server due to user-triggered interactions that fail are reported in the footer (#714/#427)
- Popup notifications for streams respect the desktop-notifications setting (#669)

### Interactivity improvements
- Messages are not marked as read while browsing through messages resulting from a search (#624/#723)
- On searching with no search text, exit search and focus on the list below (don't perform an empty search) (#551)
- Require <kbd>esc</kbd> to exit message compose box - avoiding loss of draft upon clicking elsewhere (#720/#652)
- Autocomplete now triggers correctly with leading text (including parentheses), eg `(#str` (#542)

### Visual improvements
- Pinned and unpinned streams are shown with a separator while searching (#577)
- Message reactions are shown clearer in the message information popup (#659)
- Links within messages are listed in the message information popup, above reactions (#708)

### Important bugfixes
- Fixed crash on startup, related to looking up unsubscribed streams with unread counts (#694/#706)
- Fixed crash when trying to send private message from user list (#677)
- Fix security issue due to limited quote escaping in notifications
- Fix security issue when running in profiling mode (fixed filename in /tmp)
- Upgraded dependencies, leading to fix for color support in mosh & urxvt (via urwid 2.1.1)
- Ensure recipient headers are shown in narrow message view (#671/#672)
- Unread counts and message updating continue to be improved (#711/#697/#696)

### Infrastructure improvements
- Known working terminal emulators added to `FAQ.md` - moved from `README` into `docs/` (#689)

## 0.5.1 - 13 May 2020

While not composed of as many significant changes as 0.5.0, this is a meaningful release focusing on message and UI improvements - enjoy!

### HIGHLIGHTS
- Lists in messages are displayed much more compactly, represent bulleted and numbered styles accurately, and indent appropriately for nested lists!
- Reactions are rendered more accurately and consistently, and are styled differently if you've reacted
- Bars adjacent to topic names and private message recipients are colored appropriately and thinner
- Theme names have changed to *zt_dark*, *zt_light*, *zt_blue* and *gruvbox_dark* (**NOTE** old names will continue working for now)
- Default (now *zt_dark*) theme colors should work more reliably across terminals
- Support for color depths other than the previous 256-color mode, including a polished monochrome mode, with new '--color-depth' option
- Stream/topic/user searches are clearly marked when they are in effect, in line with message search

### Interactivity improvements
- Move focus fully into topic search box before entering text (don't leave topic selected)
- After topic search, return to previously selected topic
- Clearly indicate when a stream/topic/user search is in effect, in line with message search

### Visual improvements
- Use bullet characters for unordered lists, in place of stars
- Render numbered lists fully and according to Zulip style (previously rendered as bulleted lists)
- Support nested lists (bulleted and numbered)
- Style reaction counts which include yourself differently (inverted colors, typically)
- Sort reactions alphabetically for consistency
- Support color depths other than 256-colors; try --color-depth=1 for a retro, high-constrast experience!
- Improve specificity of colors in default theme, enhancing rendering and consistency in 256 color mode
- Use triangle symbol (▶) to separate streams and topics, instead of simply '>'
- The 'bar' extending from topics or private message recipients is now thinner and colored if a stream

### Important bugfixes
- If notifications are enabled but the external script was not found, cleanly warn the user just once per session and avoid showing a traceback over the screen
- Names of reactions and inline emoji for the same icon could be different - use emoji list from Zulip server to unify them and remove dependency on emoji package
- Remove extra newlines present in lists, improving rendering and leading to better use of screen space

### Infrastructure improvements
- Improve Installation/Running/Configuration in README, including noting how to run a snapshot of the current development version, and that we have Dockerfiles
- Lint locally and in CI using flake8 (instead of pycodestyle), with continuation & quotes plugins, enforcing stricter, clearer rules on code style
- Tidy code using pyupgrade

## 0.5.0 - 16 April 2020

This release contains much of the remaining work from last year's GSoC students, and various other contributors - thanks to you all! (almost 200 commits)

If you've been waiting for autocomplete, popup notifications, mentions, better themes, search & platform support...this release is for you!

### HIGHLIGHTS
- Autocomplete users/groups/streams/emoji when composing messages, given a prefix (<kbd>ctrl</kbd>+<kbd>f</kbd> / <kbd>ctrl</kbd>+<kbd>r</kbd>)
- Popup notifications for private messages & mentions (NOTE: disabled by default; tools may be required on WSL/Linux)
- See details of messages in which you are mentioned - narrow to them using <kbd>#</kbd>
- All themes now considered usable (light/blue much improved)
- Search for messages only within a specific narrow, not just within all messages
- Support added for running on Python 3.8 and PyPy, and also on WSL (including WSL2)
- Sample Dockerfiles added, to enable building containers to run from any docker-enabled system

### Interactivity improvements
- Improved topic list handling (search topics, topics update)
- Support /me slash command
- Toggle display of stream description using <kbd>i</kbd>
- Enable/disable autohide setting at startup
- Extend support for vim-like navigation (scrolling)

### Visual improvements
- Add support to render tables in messages
- Improve rendering of links in messages
- Categorize and further reorganize help menu
- Show the year of a message, if it is not the current year
- Show server name & description in the title bar

### Important bugfixes
- Bug causing occasional screen corruption at startup (#456)
- On changing to a narrow which contains the focused message, retain focus on that message
- Message search results correctly reset between searches
- Improved unread count handling

### Infrastructure changes
- Split linters into separate Travis tasks to improve developer understanding
- Replace pytest-pep8 with pycodestyle for PEP8 linting
- Add isort as linter/reformatter for imports
- Use pip instead of pipenv in Travis to improve CI speed
- Depend upon later versions of zulip, urwid & urwid-readline packages

## 0.4.0 - 22 July 2019

Thanks to the core team and many new contributors for the almost 300 commits since 0.3.1!

### HIGHLIGHTS
- Cleaner style, compact, more functional - and lots of bugs fixed!
- Default to show both left and right panels (streams & users), with no_autohide mode
- Messages now only get marked read if you actively move onto them
- Clear indication of the current message view (narrow) next to the message search area
- 'Zoom' in and out of stream/topic narrows using <kbd>z</kbd> (also all-private-messages/one-conversation)
- Edit message content and subject/topic using <kbd>e</kbd> & see them marked & updated
- Toggle between listing streams & topics in a stream easily using <kbd>t</kbd>
- Examine who reacted to a message using the information menu accessible using <kbd>i</kbd>
- Mute a selected stream from within zulip-term using <kbd>m</kbd>
- Various areas now marked with shortcut keys in the UI, not just in the help menu (<kbd>?</kbd>)

### Interactivity improvements
- The 'no_autohide' option is now the default, with both left and right panels always shown
- Added <kbd>e</kbd> to edit your own sent message content & subject/topic
- Update message content and subject/topic appropriately from server (#401)
- Change views as per webapp if the edited message subject/topic changes
- Only mark messages read, if actively move across to message list and select them
- Added <kbd>z</kbd> hot/shortcut key to toggle between stream/topic or all-private/specific-person narrows
- Added <kbd>t</kbd> to toggle between streams & list of all topics in selected stream
- Added <kbd>m</kbd> to mute/unmute selected stream, with confirmation popup
- Added <kbd>i</kbd> to show further information of selected message (including reactions)
- Use <kbd>?</kbd> to show *and* hide help menu (<kbd>esc</kbd> continues to exit)
- Add additional shortcut key for sending messages (<kbd>ctrl</kbd>+<kbd>d</kbd>) (#176)
- Add hint in footer of how to copy text, if attempt to select text (with mouse) in terminal
- Stream search is now case-insensitive
- Add command-line option to check version (#280)
- Allow <kbd>f</kbd> and <kbd>P</kbd> shortcut keys to work from side panels (narrow starred & private messages)
- Warn on startup, if specified theme is lacking current required styles
- Upon unexpected crash, exit cleanly and log traceback to `zulip-terminal-tracebacks.log`

### Visual improvements
- Right-align unread-counts in left & right panels (as in webapp)
- Remove intrusive flashing cursor in side panels
- Truncate text in left & right panels cleanly with '…', avoiding text overflow (#237)
- Show users' status as `active` (Green), `idle` (Yellow) or `offline` (White) using different colors.
- Update user list every minute, not just at startup (#330)
- Sort user list alphabetically, case-independently (#264)
- Further improvement/reordering of shortcut keys in README & help menu (<kbd>?</kbd>)
- Improve styling of help menu, and how it scales with application width & height (#297, #307)
- Make stream icons bold and correct background color
- Themes improved (#254)
- Support terminal transparency in default theme (#377)
- Clarify that <kbd>ctrl</kbd>+<kbd>c</kbd> is the intended way to exit/quit (#208)
- Mark edited messages with 'EDITED' at their top-left
- Show current narrow with search box, above current-recipient indicator for message (#201, #340)
- Hide current-recipient indicator when fully narrowed (in topic or conversation)
- Improve rendering of quoted text with indents
- Display custom emoji text-equivalents in messages and reactions (#238)
- Readline keys are now listed in the online help
- Change main widget styles, to clearly separate three columns, with bold top-lines
- Minimize space taken up by search boxes & display shortcut keys for each
- Remove bullets & display shortcut keys for all messages, private messages & starred messages
- Style private message header like webapp (You and ...)

### Important bugfixes
- Bug undoing thumbs_up if not in same session (#334)
- Bug showing edited messages in raw text, not rendered version (#308)
- Bug quoting original message, not rendered version (#239)
- Bug where new messages from server would not be shown in message list
- Bug potentially mixing unread counts for messages from users & streams
- Bug with not showing self as recipient
- Bug increasing the unread counts if we sent the message
- Crash due to race in initialization (#391)
- Crash due to not supporting short color format for streams from older Zulip servers (#273)
- Crash pressing up on muted stream (#272)
- Crash when using certain keys in a stream with no previous conversations (#247)
- Crash in rare case of empty message content
- Crash on receiving multiple starred-message events
- Crash interacting with empty list of search results
- Crash when text entry was not disabled properly
- Crash on pressing <kbd>ctrl</kbd>+<kbd>4</kbd> (sending quit character)
- Crash if user has unsubscribed from streams
- Traceback on sending to multiple private recipients when narrowed to that conversation
- Set terminal locale to `utf-8` by default which removes issues with rendering double width characters.
- Exit cleanly if cannot connect to zulip server (#216)

### Infrastructure changes
- Remove support for python 3.4, which will have no further releases
- Depend upon later versions of zulip & urwid-readline packages
- Improve installation, development & troubleshooting notes in README
- Minimized initial registration & communication with zulip server
- Internal refactoring & centralization of code handling zulip server communication
- Centralize server event callbacks into Model
- Improve test coverage, fixtures & builds on Travis
- Simplify UI objects used in left & right panels

## 0.3.1 - 26 December 2018

### Interactivity improvements
- Much improved (& configurable on/off) autohide behavior for streams/users panels
- Toggle thumbs-up reactions to messages (<kbd>+</kbd>)
- Toggle star status of messages (<kbd>*</kbd> or <kbd>ctrl</kbd>+<kbd>s</kbd>)
- Narrow to starred messges (<kbd>f</kbd>, or via new button)
- Reply mentioning sender (<kbd>@</kbd>)
- Reply quoting mesage (<kbd>></kbd>)
- Use enter to reply to a message
- Disable responding to suspend (<kbd>ctrl</kbd>+<kbd>z</kbd>), since cannot resume (yet)
- Disable responding to <kbd>ctrl</kbd>+<kbd>s</kbd> for flow control, enabling use with starring

### Visual improvements
- Reorder streams into pinned and unpinned groups
- Style message contents (extracted using beautifulsoup)
- Improve recipient (eg. stream/topic) bar formatting
- Show star status of messages
- Show marker to left of messages
- Mark private streams with P instead of #
- Show unread count of muted streams as M
- Add `gruvbox` theme
- Internal help (<kbd>?</kbd>) more compact & reordered
- Random shortcut keys are shown at the bottom of the screen

### Important bugfixes
- Allow narrowing to cross-realm bots
- Support private messages with multiple users properly
- Avoid showing duplicate recipient bars when scrolling
- Correctly set pointer data (for next unread)
- Improve theme handling on command-line

### Infrastructure changes
- Documentation improvements
- Explicitly support latest versions of python 3.4 to 3.7
- Preliminary support for OSX/Darwin (tested by default)
- Higher test coverage
- Various internal refactoring

## 0.2.1 - 1 October 2018
### Bugfix release

## 0.2.0 - 15 July 2018
### First PyPI release
