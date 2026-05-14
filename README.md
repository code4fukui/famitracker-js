# FamiTracker CX

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

> A discontinued cross-platform port of the FamiTracker NES/Famicom music tracker.

> **Note:** The repository is named "famitracker-js", but this is a C++ project. The name is a historical artifact.

> **Project Status: Discontinued**
> This is an archived project, preserved for historical reasons. It is no longer maintained.

FamiTracker CX is a free, cross-platform fork of the popular [FamiTracker](http://famitracker.com/), created to bring the NES/Famicom music tracker to Linux. The core code is based on the original work by Jonathan Liss (jsr), with the porting effort and new components written by Dan Spencer.

## Features

*   **Cross-Platform GUI:** The original Windows-based UI was rewritten from scratch using the Qt 4 library to run natively on Linux.
*   **Multiple Interfaces:** Includes a full graphical editor (Qt), a terminal-based player (ncurses), and a simple command-line player.
*   **Linux Audio Support:** Natively supports ALSA and JACK audio backends.
*   **Modular Architecture:** The original codebase was refactored into reusable components to support different frontends.
*   **Expansion Chip Support:** Emulates various sound chips, including VRC6, MMC5, FDS, and VRC7.

## Building from Source

### Dependencies
*   CMake
*   A C++ compiler (e.g., g++)
*   Qt 4 development libraries
*   ALSA development libraries (`libasound2-dev`)
*   JACK development libraries (`libjack-dev`)
*   ncurses development libraries (`libncurses5-dev`)
*   Boost Thread library (`libboost-thread-dev`)

### Instructions
```bash
# Clone the repository
git clone https://github.com/your-user/famitracker-js.git
cd famitracker-js

# Configure the build
cmake .

# Compile the project
make
```

## Usage

After building, you can run the different interfaces using the provided shell scripts, which set the correct library paths.

*   **Qt GUI:** `./src/qt-gui/install/famitracker-qt.sh`
*   **ncurses Player:** `./src/ncurses-ui/install/famitracker-nc.sh`
*   **Console Player:** `./src/console-play-ui/install/famitracker-play.sh`

## Project Post-Mortem

This section is preserved from the original author's notes on the project's challenges and lessons learned.

#### Challenges
*   Porting the MFC/Win32 codebase to Qt.
*   Modularizing the original code into reusable components to allow for multiple UI frontends (the original kept all `.cpp` files in a single directory).
*   Lingering undefined behavior in the original code created bugs in the Linux version.

#### Coding Mistakes in FamiTracker CX
*   The "thread pool" was implemented as a message queue, not a true thread pool.
*   Using the `type_t` notation on structs instead of `typedefs`.
*   Using global state to manage document data for the Qt GUI.
*   The sound sink implementations abused inheritance, leading to many audio bugs.

#### If This Project Were Attempted Again
Closer coordination with the original author (jsr) would have been key. Organizing the code base to be reusable from the start and keeping a development branch available via a DVCS like Git would have solved many of the problems this fork aimed to address.

## Credits and Attribution

*   **Original FamiTracker:** Jonathan Liss (jsr) and other contributors. Project page: [http://famitracker.com/](http://famitracker.com/)
*   **FamiTracker CX Port:** Dan Spencer (nukethepotato)
*   **Icon:** Kuhneghetz
*   **Toolbar Icons:** ilkke
*   **Export Plugin Support:** Gradualore
*   **DPCM Import Resampler:** Jahrmander
*   **Third-Party Libraries:**
    *   `blip_buffer` by blargg
    *   YM2413 & YM2149 emulators by Mitsutaka Okazaki
    *   FDS sound emulator from nezplug

## License

MIT License — see [LICENSE](LICENSE).