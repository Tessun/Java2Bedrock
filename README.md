## Usage
To run, simply:
```
./converter.sh MyResourcePack.zip
```
To run without settings prompts and use the defaults:
```
./converter.sh MyResourcePack.zip default
```

## About
The script has been updated to handle parent models and 2D items. It will generate a single sprite sheet for all textures used in 3D models, and copy over textures for 2D items individually.

Your script and resource pack zip file must be in the same directory. Ensure that this zip file is properly setup. It should not have a root directory. Your resource pack must also be formatted correctly, to vanilla specifications. By default, this script will download the default assets in order to generate texture atlases in cases in which you have utilized those. If you wish to use different default assets, you may specify this at the beginning. The default pack will then be downloaded after your specified assets, with your specified assets taking precedence. As long as you provide valid JSON, the script should output something you can use.

You may also specify an input bedrock pack to merge with the output assets produced by the converter. This should be in the same directory as the script and your input Java pack. Like the Java pack, ensure that it is compressed with no root folder. When prompted, type the file name of the input file, such as `example_rp.mcpack`. Merging of behavior packs is not currently supported.

The packs generated by this script can currently only be used in Bedrock Edition 1.16.210.59 and above. Please be sure to enable the experimental setting "Holiday Creator Features" on world generation. You'll probably also want to be in creative mode as that will be the only way to give yourself the blocks generated by the script. Here are the commands to obtain one of the items or place them in your head slot:
```
/give @p geysercmd:gmdl_####
/replaceitem entity @p slot.armor.head 0 geysercmd:gmdl_####
``` 
The \#### term corresponds to the numerical ID assigned to the model. These are written to config.json, which can be found in the target directory, along with packaged and non-packaged versions of the output assets. This will specify the corresponding item and nbt for each input predicate.

Also note that this script requires:
- [jq](https://stedolan.github.io/jq/download/) (1.6+)
- [sponge](https://joeyh.name/code/moreutils/)
- [imagemagick](https://imagemagick.org/script/download.php) (7+)
- [nodejs](https://nodejs.org/en/)
- [spritesheet-js](https://www.npmjs.com/package/spritesheet-js)

It will exit if you fail to meet these dependencies. While the ultimate intention here is to import these via Geyser, the script currently generates a behavior pack so that you may view your converted models in Bedrock Edition. It also generates a mappings file compliant with [@ImDaBigBoss](https://github.com/ImDaBigBoss)'s [PR](https://github.com/GeyserMC/Geyser/pull/2822) to add predicate support to Geyser.

Should you have any complaints about getting this to run because you "only use windows", do note that I was able to run this perfectly fine on a Mac running Parallels to run Windows to run WSL to run Ubuntu 20. Therefore, I am sure it is perfectly possible for you to get this working, regardless of your OS. I will gladly take such criticism only if you are willing to help develop this into a proper cross platform program. 

## Dependency Installation

### A note about ImageMagick

It seems many of the package repositories still install ImageMagick 6. If this occurs and the script fails for this reason, consider using [IMEI](https://github.com/SoftCreatR/imei/#one-step-automated-install) to build ImageMagick 7 from source.

### Debian, Ubuntu, & Mint
```sh
sudo apt-get install moreutils jq imagemagick unzip zip nodejs
npm i -g spritesheet-js
```

### MacOS
```sh
brew install moreutils jq imagemagick unzip zip nodejs
npm i -g spritesheet-js
```

### RHEL, Fedora, & Centos
```sh
sudo yum install moreutils jq imagemagick unzip zip nodejs
npm i -g spritesheet-js
```

### Arch Linux
```sh
sudo pacman -S moreutils jq imagemagick unzip zip nodejs
npm i -g spritesheet-js
```

### Windows
Impossible; consider [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

#### Special Notes for WSL
In general, packages on WSL seem to be a little wonky, and sometimes jq-1.5 will be installed, which will not work. To manually install jq-1.6 on WSL, at least for Ubuntu:
```sh
wget https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 && sudo chmod +x jq-linux64 && sudo mv jq-linux64 /usr/bin/jq
```
