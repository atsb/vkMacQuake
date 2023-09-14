# 🌋 vkMacQuake
vkMacQuake is a port of id Software's [Quake](https://en.wikipedia.org/wiki/Quake_(video_game)) using Vulkan instead of OpenGL for rendering. It is based on the popular [QuakeSpasm](http://quakespasm.sourceforge.net/) and [QuakeSpasm-Spiked](https://triptohell.info/moodles/qss/) ports and runs all mods compatible with QuakeSpasm like [Arcane Dimensions](http://www.moddb.com/mods/arcane-dimensions).

vkMacQuake is strictly for macOS users.  If this port breaks things for systems other than macOS, then that is a feature not a bug.

Improvements over QuakeSpasm include:
* Much better performance with multithreaded rendering and loading
* The game can run at higher frame rates than 72Hz without breaking physics
* A software Quake like underwater effect
* Support for remastered models if using data from the 2021 rerelease
* Dynamic shadows (requires a GPU with ray tracing support)
* Better color precision reducing banding in dark areas
* Native support for anti aliasing and anisotropic filtering
* 8-bit color emulation
* Scaling for pixelated look
* Mods menu for easy mod loading
* More modern protocol to avoid certain movement issues (from QSS)
* Support for custom mod HUDs (from QSS)
* Support for scriptable particles (from QSS)

# Installation

> **Note**\
> Make sure all data files are lowercase, e.g. "id1", not "ID1" and "pak0.pak", not "PAK0.PAK". Some distributions of the game have upper case file names, e.g. from GOG.com.

## Quake '2021 re-release'

vkMacQuake has initial support for playing the 2021 re-release content. Follow installation instructions as above but copy the files into the rerelease folder.

# Vulkan
vkMacQuake shows basic usage of the API. For example it demonstrates render passes & sub passes, pipeline barriers & synchronization, compute shaders, push & specialization constants, CPU/GPU parallelism and memory pooling.

# Building
> **Note**\
> You will need at least Vulkan SDK version 1.2.162 or newer. When building for Linux this is not always the case for the SDK provided by the distribution. Install the latest LunarG SDK if necessary.

## MacOS

To compile vkMacQuake, first install the build dependencies with Homebrew:

~~~
brew install molten-vk vulkan-headers glslang spirv-tools sdl2 libvorbis flac opus opusfile mad meson pkgconfig zopfli
~~~

Then clone the vkMacQuake repo:

~~~
git clone https://github.com/atsb/vkMacQuake.git
~~~

Now go to the Quake directory and compile the executable:

~~~
cd vkMacQuake
meson build && ninja -C build
~~~

> **Note**\
> The Meson version needs to be 0.47.0 or newer.

# Optional - Music / Soundtrack

> **Note**\
> This section only applies to older releases. For the 2021 re-release music will work out of the box.

The original Quake had a great soundtrack by Nine Inch Nails. Unfortunately, the Steam version does not come with the soundtrack files. The GOG-provided files need to be converted before they are ready for use. In general, you'll just need to move a "music" folder to the correct location within your vkMacQuake installation (.e.g `/usr/share/quake/id1/music`). Most Quake engines play nicest with soundtracks placed in the `id1/music` subfolder vs. `sound\cdtracks`

QuakeSpasm, the engine vkMacQuake is derived from, supports OGG, MP3, FLAC, and WAV audio formats. The Linux version of QuakeSpasm/vkMacQuake requires external libraries: libogg or libvorbis for OGG support, libmad or libmpg123 for MP3, and libflac for FLAC. If you already have a setup that works for the engine you're currently using, then you don't necessarily have to change it. 

Generally, the below setup works for multiple engines, including Quakespasm/vkMacQuake:

* The music files are loose files, NOT inside a pak or pk3 archive.
* The files are placed inside a "music" subfolder of the "id1" folder. For missionpack or mod soundtracks, the files are placed in a "music" subfolder of the appropriate game folder. So the original Quake soundtrack files go inside "id1\music", Mission Pack 1 soundtrack files go inside "hipnotic\music", and Mission Pack 2 soundtrack files go inside "rogue\music".
* The files are named in the pattern "tracknn", where "nn" is the CD track number that the file was ripped from. Since the soundtrack starts at the second CD track, MP3 soundtrack files are named "track02.mp3", "track03.mp3", etc. OGG soundtrack files are named "track02.ogg", "track03.ogg", etc. FLAC soundtrack files are named "track02.flac", "track03.flac", etc. WAV soundtrack files are named "track02.wav", "track03.wav", etc.

**See more:** [Quake Soundtrack Solutions (Steam Community)](http://steamcommunity.com/sharedfiles/filedetails/?id=119489135)
