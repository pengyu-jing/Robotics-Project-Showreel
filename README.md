# Robotics Project Showreel

Demonstration and competition footage for the robotics projects in this account.
Each video is the working proof for a repository that holds the design files — the
CAD, firmware and PCB sources live there; the evidence that any of it ran lives
here.

All files are stored with **Git LFS**.

## Index

| Video | Project | Sources |
|---|---|---|
| `Competition Video-International Competition.mp4` | ABU Robocon 2023, *Casting Flowers over Angkor Wat* — international final | [`Robocon2023-Elephant-Robot`](https://github.com/pengyu-jing/Robocon2023-Elephant-Robot) |
| `Competition Video-Domestic competition.mp4` | Robocon 2023 — Chinese national competition | [`Robocon2023-Elephant-Robot`](https://github.com/pengyu-jing/Robocon2023-Elephant-Robot) |
| `Drone-Demostration Video.mp4` | Chiyu A-60 agricultural spraying quadcopter, 50 L tank, ~90 kg class | [`Chiyu-A60-Spray-Drone`](https://github.com/pengyu-jing/Chiyu-A60-Spray-Drone) |
| `A calligraphy robot-Domostration Video.mp4` | Brush calligraphy robot — 3R arm on a lead-screw linear stage | [`Calligraphy-Writing-Robot`](https://github.com/pengyu-jing/Calligraphy-Writing-Robot) |
| `A seesaw robot-Domostration Video.mp4` | Seesaw balancing robot — three-wheel differential drive, nine-axis IMU | [`Seesaw-Balancing-Robot`](https://github.com/pengyu-jing/Seesaw-Balancing-Robot) |
| `Flexible exoskeleton device-Demostration Video.mp4` | Flexible exoskeleton device | *no public repository* |

## Repository structure

```
Demostration Videos/           all six clips, MP4, Git LFS
.gitattributes                 LFS tracking rules
```

Flat by design: this is an index, not a project. Nothing here is built or run —
the directory exists so that each source repository can link to a stable URL for
its footage rather than embedding large binaries of its own.

## Getting the files (Git LFS)

This repository tracks its files with Git LFS, and `.gitattributes` itself was
committed *through* the LFS filter — the rule is `* filter=lfs diff=lfs merge=lfs
-text`, and `*` matches `.gitattributes` too. On clone, Git reads the pointer text
as attribute rules, prints

```
https://git-lfs.github.com/spec/v1 is not a valid attribute name: .gitattributes:1
```

and then skips the smudge filter entirely — so every file arrives as a pointer
stub even when `git-lfs` is installed. Recover the real content with:

```sh
git clone git@github.com:pengyu-jing/Robotics-Project-Showreel.git
cd Robotics-Project-Showreel
git lfs install --local
git lfs pull                       # or --include="<path>" for one file
```

To fetch a single clip instead of all six:

```sh
git lfs pull --include="Demostration Videos/Drone-Demostration Video.mp4"
```

A pointer stub is a short text file starting with
`version https://git-lfs.github.com/spec/v1`; if you see that where a source file
or a video should be, the pull has not run.

To fix this permanently, exclude `.gitattributes` from its own wildcard — add a
line such as `.gitattributes -filter -diff -merge text` after the `*` rule and
re-commit it as a plain file.

## Related repositories

- [`Robocon2023-Elephant-Robot`](https://github.com/pengyu-jing/Robocon2023-Elephant-Robot) — ABU Robocon 2023 R2 robot: swerve chassis, ring launchers, 17 in-house PCBs
- [`Chiyu-A60-Spray-Drone`](https://github.com/pengyu-jing/Chiyu-A60-Spray-Drone) — agricultural spraying UAV: airframe CAD and Pixhawk interface boards
- [`Calligraphy-Writing-Robot`](https://github.com/pengyu-jing/Calligraphy-Writing-Robot) — brush calligraphy robot: STM32F405, bus servos, linear stage
- [`Seesaw-Balancing-Robot`](https://github.com/pengyu-jing/Seesaw-Balancing-Robot) — seesaw balancing robot: STM32F401, GY-953 IMU

## Note on filenames

The directory and several files spell it *Demostration* / *Domostration* rather
than *Demonstration*. The names are left as they are because they are already
linked from elsewhere; renaming them would rewrite LFS pointers and break those
links.
