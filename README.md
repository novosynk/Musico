# Musico

### Listen Ad-Free. Enjoy High-Quality Music.

Musico is a modern, cross-platform music listening application built with Flutter. It is designed to provide a clean, fast, ad-free music experience with high-quality playback, powerful music discovery, offline listening, playlists, favorites, lyrics, downloads, and a modern music-player interface.

Musico focuses on giving users a simple experience: open the app, search for music, press play, and listen.

No complicated setup. No unnecessary account creation. No clutter.

---

## What is Musico?

Musico is a personal music player and music discovery application that brings music from multiple supported music sources into one unified experience.

Users can search for songs, discover new music, play tracks in high quality, create playlists, save favorites, download music for offline listening, view synchronized lyrics, and control everything through a modern player.

Musico is designed to work across:

- Android
- iOS
- Windows
- macOS
- Linux
- Web

The application uses a provider-based architecture so that different music sources can be integrated without changing the core player.

---

## Core Experience

The main goal of Musico is simple:

**Search → Play → Listen**

A user should be able to:

1. Open Musico.
2. Enter their name on first launch.
3. Enter the Home screen.
4. Search for a song.
5. Select the exact song they want.
6. See the player immediately.
7. Resolve a real playable audio stream.
8. Start listening.
9. Control playback from the Mini Player or Full Player.
10. Download the track when supported.
11. Listen to downloaded music without an internet connection.

The application must prioritize real functionality over fake UI states or placeholder data.

---

# Features

## Ad-Free Music Experience

Musico is designed around a clean listening experience without unnecessary advertising inside the application UI.

The interface should remain focused on music, discovery and playback.

---

## High-Quality Audio

Musico should prioritize high-quality playback.

The default preferred quality is:

**320 kbps**

when the selected source actually provides it.

If 320 kbps is not available for a specific track, Musico should automatically use the best available quality instead of failing playback.

For example:

320 kbps available  
→ Play 320 kbps

320 kbps unavailable  
→ Automatically use the highest available quality

The user can change their preferred playback quality from Settings.

The application must never falsely claim that a track is playing at 320 kbps when the actual source provides a lower quality.

---

# Multi-Source Music Discovery

Musico uses a provider-based architecture for music discovery.

Supported or planned providers include:

- YouTube Music
- Spotify
- JioSaavn
- Audius
- Jamendo
- Local device music

Each provider should be implemented independently through the common `MusicSource` architecture.

The UI and player should not depend directly on a specific provider.

---

# YouTube Music

YouTube Music is one of the primary music discovery sources for Musico.

Users should be able to:

- Search songs
- Search artists
- Search albums
- Search playlists
- View artwork
- View metadata
- Play the exact selected track
- Add tracks to playlists
- Favorite tracks
- Download supported tracks

### Exact Track Playback

When a user selects a YouTube Music result, Musico must preserve the exact YouTube track/video identity.

The application must not silently replace the selected song with another recording.

For example:

User searches:

`Artist - Song Name`

User selects a specific result.

Musico must resolve and play that exact selected result.

It must not randomly select another version, cover, remix or unrelated track.

---

# YouTube Playback Architecture

YouTube search and YouTube playback must be treated as separate operations.

Finding a song through search does not automatically mean that a playable audio stream is available.

Musico therefore uses a dedicated playback-resolution layer.

The playback flow should be:

```text
YouTube Music Search
        ↓
Selected Track
        ↓
Exact YouTube Track ID
        ↓
Playback Resolver
        ↓
Playable Audio Stream
        ↓
just_audio
        ↓
Actual Playback
