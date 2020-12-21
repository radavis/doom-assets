# doom-assets

Print OS info

```bash
$ cat /etc/os-release
NAME="Ubuntu"
VERSION="18.04.5 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.5 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=bionic
UBUNTU_CODENAME=bionic
```

Retrieve `doom1.wad` shareware wad and verify md5

```bash
$ curl -O http://distro.ibiblio.org/pub/linux/distributions/slitaz/sources/packages/d/doom1.wad
$ md5sum doom1.wad | grep f0cefca49926d00903cf57551d901abe # or
$ echo "f0cefca49926d00903cf57551d901abe doom1.wad" | md5sum -c -
```

Install `deutex` and extract assets

```bash
$ sudo apt install deutex
$ man deutex
$ mkdir doom1-wad && cd doom1-wad
$ deutex -doom ../doom1.wad -extract
```

Strangely, this gives a different output to the `./musics` folder

```
$ mkdir doom-wad && cd doom-wad
$ cp ../doom1.wad .
$ deutex -doom doom1.wad -extract
```

Convert `mus` format to `mid`

```bash
$ cd ~
$ git clone https://notabug.org/pgimeno/mmus2mid.git
$ cd mmus2mid
$ make
$ cd ~/bin  # a folder that is included in my $PATH
$ ln -s ~/mmus2mid/mmus2mid
$ cd ~/doom-assets
$ mmus2mid doom-wad/musics/*.mus
```

Play midi audio

Roland-SC-55.sf2 from [here](https://www.vogons.org/viewtopic.php?t=45600&start=120)

```
$ sudo apt install fluidsynth fluid-soundfont-gs
$ fluidsynth --audio-driver=alsa -o audio.alsa.device=hw:0 /usr/share/sounds/sf2/FluidR3_GM.sf2 doom1-wad/musics/d_e1m1.mid
$ fluidsynth --audio-driver alsa -o audio.alsa.device=hw:0 Roland-SC-55-Presets.sf2 doom-wad/musics/d_e1m1.mid
```
