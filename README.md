# Sync Companion

Sync Companion is a Reddit bot originally developed for /r/ffxiv that helps reduce moderator workload with subreddit automation and synchronizing sidebars with widgets. It is provided as an open source bot for your own hosting.

Want to suggest an improvement or report a bug? Submit an [issue](https://github.com/zeno-mcdohl/sync-companion/issues). If you're seeking to submit changes, just open a Pull Request.

--------------

<!-- TOC -->

- [Sync Companion](#sync-companion)
    - [Features](#features)
    - [Setup](#setup)
        - [Prerequisites](#prerequisites)
        - [Installation](#installation)
        - [Initialization](#initialization)
    - [Instructions for Moderators](#instructions-for-moderators)
        - [Adding new content](#adding-new-content)
        - [Editing existing content](#editing-existing-content)
        - [Deleting content](#deleting-content)
    - [Configuration](#configuration)

<!-- /TOC -->

## Features

* Allows for sidebar to be structured data.
* Synchronizes sidebar text and widgets. Widget types supported:
  * Textarea
  * Community List
* Any form of markdown used.
* Multiple lines of text.
* Ability to update a sidebar section without a correlating widget.
* Preserve widget color set from mod tools.
* Various automations:
  * Twitch stream list for specific game (currently not functioning).
  * Discord members online count.
  * Countdown clock to a target date and time.
* Sidebar character limit warning via modmail.

## Setup

### Prerequisites

See `requirements.txt`. This bot has been developed and tested under:

* Linux 5.1.17
* Python 3.6.6
* PRAW 6.3.1

### Installation

1) Download this bot code 
2) Copy `config.ini.example` to `config.ini`, and `praw.ini.example` to `praw.ini`
3) Enter your API information into praw.ini as [instructed here](https://praw.readthedocs.io/en/latest/getting_started/configuration/prawini.html)
3) Create a scheduled task (e.g. `crontab` in Linux) running `synccompanion.py` with Python and using an argument of your subreddit name (e.g. `ffxiv`)


### Initialization

Create two wiki pages on your subreddit: `sidebar_sync` and `sidebar`. Set the edit permission to mods only and de-list the page from the wiki listing.

## Instructions for Moderators

### Adding new content

1) New content that you wish to be synced between old Reddit and the redesign should be added to the `sidebar_sync` wiki page under a new header (`####`). The header name should be concise and contain underscores instead of spaces; it represents the ID of this content section. Below that should **contain the content** which can be multiple lines. Example:

```
####Current_Shows
This could be a list of relevant TV shows. It appears on old Reddit and the redesign!
```

Note per above that only a single newline should follow the header, not two newlines.

2) On the `sidebar` *wiki* page, add a line that corresponds with the header name from above and surround it with `%%`. This page defines **where the content is located** on the sidebar for old Reddit (this makes it essentially structured data). Example:

```
%%Current_Shows%%
```

**This page acts as your sidebar**, so format it as you'd like. It can contain any typical sidebar content and include the IDs that'll sync between your sidebar and widgets.

3) Open the redesign and manually **create a new widget**. The title of the widget should be the header name from above, except replace the underscores with spaces. The widget text can be left blank, as it will be automatically updated. Example: `Current Shows` as a widget title.

### Editing existing content

If content exists that is being synced between old Reddit and the redesign, it is defined on the `sidebar_sync` wiki page. Simply edit your desired text on `sidebar_sync`, save the page, and wait for the next scheduled run of the bot. [Example gif.](https://i.imgur.com/aMGwVav.gifv)

### Deleting content

Simply delete the corresponding text on the `sidebar_sync` wiki page including the header, as well as the header ID section on the `sidebar` wiki page.

## Configuration

TBA
