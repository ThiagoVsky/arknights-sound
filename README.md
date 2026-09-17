# Arknights sound effects and music

Game assets from Arknights, extracted from the **EN** game server. This repository is
generated and refreshed by machine; do not edit its contents by hand.

## What is here

Source: `audio/**` on the EN game server, excluding every voice set.

Grouped by the game's own layout:

- `music/<event>/<track>.mp3`: the soundtrack, including event and battle themes.
- `player/`: player character and interface sounds.
- `avg_se_<n>/`: story and cutscene effects.
- `enmy_snd_<type>_<n>/`: enemy sounds.
- `ambience/`, `general_<n>/`, `vox/`, `cnstrct_snd_<n>/`: ambience and assorted effect banks.
- `custom_se/`: effects belonging to specific game modes.

Each directory holds the individual clips of that bank.

## Format

MP3, 96 kbps mono for effects and 160 kbps for stereo music

The split from the voice repositories is by path, not by filename: there are music tracks with `voice` in the name, such as `m_bat_failed_intro_voice`, which belong here rather than in a voice repository.

## Updating

`.github/workflows/update.yml` runs once a day. Incremental state lives in
`.state/sound.json`, so only bundles that are new or whose hash changed are downloaded
and extracted again; a rerun with nothing new is a no-op.

Run it locally:

```bash
python -m pip install "arkprts[all]" lameenc
python tools/assets_sync.py --out . --flat --state .state
python tools/assets_sync.py --verify --out . --flat
```

`tools/assets_sync.py` in this repository is a self-contained copy whose default group is
`sound`. The canonical copy lives in [ArknightsGameDataEN](https://github.com/ThiagoVsky/ArknightsGameDataEN) under
`tools/assets_sync.py`; the download uses
[arkprts](https://github.com/thesadru/arkprts) and the extraction uses
[UnityPy](https://github.com/K0lb3/UnityPy) with the LZ4AK decompressor that arkprts
registers in place of the LZHAM that UnityPy does not implement.

