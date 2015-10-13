# Order the laptop #

  * 2015-09-25: Ordered my yuna on [Ebay](http://www.ebay.com/itm/351398651121) for 412,13 EUR (444,30 USD delivery included).
  * 2015-10-08: My laptop arrived but I were not at home
  * 2015-10-09:
    * I picked up my laptop. I had to pay 31,31 € for commons (see [Costs](https://github.com/somenxavier/yuna/blob/master/Costs.md))
    * I login with my gmail username.
    * I write the specs of my model down (see [Model](https://github.com/somenxavier/yuna/blob/master/Specs.md) page). 

# Replacing hard disk #

  * 2015-10-09: I can't install the [Chrome Recover Utility](https://chrome.google.com/webstore/detail/chromebook-recovery-utili/jndclpdbaamdhonoechobihbbiimdgai) because of `Network_Failed` error. After [asking it](https://productforums.google.com/forum/#!msg/chromebook-central/KBUywqBgbOI/vr2KWLPgBgAJ;context-place=topicsearchin/chromebook-central/somenxavier), I knew it was the type of connection: the laptop was connected to a ad-blocking network. After connecting to my router directly, all was fine.
  * 2015-10-10: I used the Google Recovery Utility to make a backup. The important in this step is that the `ID` of the laptop is the same of the `chrome:system`, that is, `YUNA D25-A3B-L4A-A9C` (see [this](https://github.com/somenxavier/yuna/blob/master/figs/01-recovery/1-identifying.jpg)).
  * 2015-10-12: I [disassembled](https://github.com/somenxavier/yuna/tree/master/figs/02-disassemble) the chromebook:
    * removing the [18 screws](https://github.com/somenxavier/yuna/blob/master/figs/02-disassemble/1-screws.jpg) at the bottom
    * separate the [two parts](https://github.com/somenxavier/yuna/blob/master/figs/02-disassemble/2-separate-parts.jpg)
    * I deplug the battery cable and I substitute the 32 GB harddisk for my 128 GB (see the [motherboard connection details](https://github.com/somenxavier/yuna/blob/master/figs/02-disassemble/3-motherboard-details.JPG)).
    * Then I powered on the laptop and I recovered chromeos with the backup I made before (see this [folder](https://github.com/somenxavier/yuna/tree/master/figs/03-recovery)).
  * 2015-10-12: After so much effort, I discovered [this laptop](https://slimbook.es/). Slimbook has similar features but less price and has upgradable RAM and harddisk. 
  
# Installing linux: SeaBIOS part #

  * 2015-10-12:
    * I removed the two screws which could cause BIOS write protection. I do not really knew which is the screw which is reponsible of BIOS write protection, but there are only two left. So I decided to remove both (see [this pic](figs/04-chromeos-seabios-changes/1-removing-screws-for-writing-BIOS.JPG)).
    * I put the laptop in *developer mode*:
      * Press `ESC` + `F3` + `Power button`
      * `CTRL+D`
      * After [confirming](figs/04-chromeos-seabios-changes/2-confirmation.jpg) that, the system [rebooted](figs/04-chromeos-seabios-changes/3-rebooted.jpg) and [turned into](figs/04-chromeos-seabios-changes/4-transition.jpg) the Developer Mode. It takes about 8 minuts (see [5-awhile* series](figs/04-chromeos-seabios-changes/)). It rebooted [again](figs/04-chromeos-seabios-changes/6-reboot.jpg) and asking for the [config](figs/04-chromeos-seabios-changes/8-config.jpg). I recommend you to configurate the net, because you need for the next step.
   * Accessing the shell:
     * `CTRL+ALT+F2`: it opens a console window
     * I intered as a `chronos` user (no password)
     * Run [John Lewis](https://johnlewis.ie/custom-chromebook-firmware/rom-download/) script for writing BIOS in `RW_LEGACY` mode:
       ```
       cd; rm -f flash_chromebook_rom.sh; curl -L -O https://johnlewis.ie/flash_chromebook_rom.sh; sudo -E bash flash_chromebook_rom.sh
       ```
       Note: the ArchWiki says you have to enter as superuser, but John Lewis says the opposite. If you see the script it's clear than the second is right.
     * It asks you for [support](figs/05-johnlewis/1-support.jpg). It offers you options. In my case, [just one](figs/05-johnlewis/2-options.jpg): `RW_LEGACY`. Then it asks you for [confirmation](figs/05-johnlewis/3-confirmation.jpg). After that, it writes the BIOS (see [4-writing-*](figs/05-johnlewis/)).
   * Then I just set SeaBIOS as default (see [this folder](figs/06-setting-SeaBIOS-default/)):
     * In the shell (`chronos` user), I became superuser: `$ sudo bash`
     * `# sudo su`
     * `# flashrom --wp-disable`
     * `# flashrom --wp-status`
     * `# /usr/share/vboot/bin/set_gbb_flags.sh`
     * `# /usr/share/vboot/bin/set_gbb_flags.sh 0x489`
     * `# reboot`
   * Then you boot with SeaBIOS. The ChromeOS does not work in my case. You can boot with USB CD-ROM. In my case I use Arch boot CD iso and you could procede as normal intallation.