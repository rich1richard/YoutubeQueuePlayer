# YoutubeQueuePlayer

This UiPath automation provides a way to build, store, and play curated queues of songs sourced from multiple locations, with YouTube as the primary playback endpoint. It offers several playlist-generation paths and utilities for managing and merging different types of inputs.

## Purpose

The workflow is designed to automate music queue creation by gathering tracks from various sources, processing them, and opening the final queue in YouTube. It centralizes common playlist workflows into a single automation with a simple menu-driven interface.

## Features

The automation currently supports:

* **Play file playlist**
  Uses a local file containing track names to construct a playable YouTube queue.

* **Play similar songs**
  Generates a queue of tracks that are musically related to a given seed song.

* **Play YouTube playlist**
  Takes an existing YouTube playlist and plays it, with the possibility to save it locally.

* **Play Discogs playlist**
  Builds a queue from a list of tracks originating from Discogs releases or collections.

* **[TOOL] Merge playlist**
  Utility mode for combining different playlist sources into a unified structure.

Each mode is selected through an on-screen dropdown form when the workflow starts.

## Requirements

* UiPath Studio
* Internet access for external lookups and YouTube playback
* Optional external data files depending on the playlist mode selected

Dependencies are restored automatically when the project is opened.

## How It Works

1. On launch, the workflow displays a selection dialog.
2. The user chooses a playlist source or tool.
3. A corresponding sequence processes the inputs:
   For example, if *8Play similar songs**:
   * Gets a seed song (or a semicolon-separated list of seeds song)
   * Fetches matches from Chosic
   * Constructs a playlist of similar songs
   * Saves the playlist (optional)
5. The workflow opens the resulting playlist as a queue in a browser (Edge as configured).

## Extending the Project

To add new playlist sources:

* Create a new sequence under `Sources/`
* Make it set its out argument named `out_Playlist` (to keep everything logical
* Add the option label to the variable named `Options` in the activity `Init parameters` of `Main.xaml`
* Add the call to that sequence in the corresponding `Case` in the activity `Build a playlist depending on the choice` of `Main.xaml`
* Pass the variable named `Playlist` to the previous out argument

  ⚠️ Hangle exception correctly to prevent unpredictable behaviors/crashes, and log important steps and situations correctly.
