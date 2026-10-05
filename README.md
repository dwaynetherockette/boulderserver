# Shared Minecraft Java world

This repository lets exactly one friend at a time host the same Minecraft Java world from their own PC.

## Tracked by Git

- `world/` — the actual Java world
- `HOSTING_LOCK.json` — exists only while somebody is hosting
- launcher/recovery scripts

## Kept local and NOT tracked

- `server.jar`
- `server.properties`
- `eula.txt`
- logs, crash reports, Java installation, RAM settings, whitelist/ops files, etc.

## Required local files

Each host puts these in the repository folder after cloning:

- `server.jar`
- `server.properties`
- `eula.txt`

Set `level-name=world` in `server.properties`.

## Normal use

Double-click `start-server.bat`.

The script:

1. refuses to overwrite unsaved local world changes;
2. fetches the newest GitHub state;
3. refuses to start if another host owns the lock;
4. atomically pushes its own hosting lock;
5. starts `server.jar`;
6. after you type `stop`, commits the changed `world/` folder;
7. pushes the world and removes the lock.

## After a crash / failed upload

On the same PC that was hosting, double-click `recover-after-crash.bat`.

Do not have another friend manually delete the lock unless you have first confirmed the hosting PC does not contain newer world data.
