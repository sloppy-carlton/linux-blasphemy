# Xfce4 Windows 95 Anti-Rice
> [!NOTE]
> This is a very rough draft of what will eventually be instructions on how to rice your desktop to get it to look as close to Windows 95 as possible. It is still very much a work in progress that I can only pursue in my limited free time, so please be patient.

If you've ever thought to yourself, "Hey, what Linux needs is more Windows," I've got two things to say to you. The first is this:

![Image of a blushing Ultramarine Terminator Captain saying, "But Senpai... That's heresy!"](/assets/ultramarines-terminator-captain-v0-xxjdnj11avoc1.jpg)

The other is that your day has come!

I have spent time scouring the Internet for the themes, fonts, and other resources to use to replicate that Windows 95 aesthetic in Xfce, and I believe that I have succeeded. My instructions will mainly focus on Arch (btw) Linux, since that's the distro that I use, and that's the one I got this working on. I will be providing links to where I sourced my themes and fonts, so you should be able to find instructions there if mine are not relevant to your distro.

Prerequisites:
*Xfce
*LightDM
*Webkit or Webkit2 greeter for LightDM
*Plymouth
*Paru or Yay (Arch (btw))

Are you sitting comfortably? Good. Let's begin.

We're going to use the [Chicago95 theme created by grassmunk](https://github.com/grassmunk/Chicago95/tree/master).

We're also going to be using [these Core TTF Fonts from Microsoft](https://corefonts.sourceforge.net/)
```
yay -S chicago95-theme ttf-ms-fonts
```
or
```
paru -S chicago95-theme ttf-ms-fonts
```
you can also use the `chicago95-theme-git` package in the AUR.

You're still missing two fonts, <sup>link</sup>MS Sans Serif<sup>/link</sup> and <sup>link</sup>VGA 437<sup>/link</sup>. As luck would have it, I found those with the assistance of some helpful people on the r/linuxsucks subreddit. I've included them in this repo.

Download both of them, then do this:
```
sudo mkdir -p /usr/local/share/fonts
sudo cp ./Downloads/*.ttf /usr/local/share/fonts
```
If you already have `/usr/local/share/fonts`, you obviously don't need to do `mkdir -p /usr/local/share/fonts`.

Once you have those installed, you'll need to go into the Appearance settings to change your GTK+ and icon themes to Chicago95. You'll need to change your main system font to 'MS Sans Serif 1' and your monospace font to one of the 'VGA 437' fonts. You'll also need to go into your Mouse and Trackpad settings to change your cursor theme to one of the Chicago95 themes, and your Window Manager settings to change your Window Manager theme to Chicago95. Also change your window title font to 'MS Sans Serif 1.

If you're one of those types who just wants to watch the world burn, do this on an x86_64 Mac with Linux installed. I'm doing it on my 2015 MacBook Air.

Next: <sup>link</sup>Configuring the Webkit Greeter for LightDM<sup>/link</sup>.
