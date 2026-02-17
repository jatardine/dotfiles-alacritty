# Yet Another Alacritty Theme (OUTDATED)

**[New repo on Codeberg!](https://codeberg.org/jevel/dotfiles-alacritty)**

![](https://github.com/jatardine/dotfiles-alacritty/blob/main/alacritty-xfce4-term-demo.png)

This is a default theme I use across all of my machines, including my Acer Aspire 5749Z.

### Dependencies

- Alacritty (duh)
- Iosevka Custom (**Please check the FAQ because there's a catch!**)
- zsh & [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) (for the arrows insead of `[USER]@[HOST]`)

## Potentially FAQ

**Q: Why does my font not match the one in the demo?**

Those may look like the regular Iosevka fonts, however Adi (Archcraft) edited them directly, instead of creating a separate TTF file:

```
fc-list | grep "Iosevka Custom"
/usr/share/fonts/iosevka/iosevka-regular.ttf: Iosevka Custom:style=Regular
/usr/share/fonts/iosevka/iosevka-oblique.ttf: Iosevka Custom,Iosevka Custom Oblique:style=Oblique,Regular
/usr/share/fonts/iosevka/iosevka-bold.ttf: Iosevka Custom:style=Bold
/usr/share/fonts/iosevka/iosevka-bolditalic.ttf: Iosevka Custom:style=Bold Italic
/usr/share/fonts/iosevka/iosevka-italic.ttf: Iosevka Custom:style=Italic
/usr/share/fonts/iosevka/iosevka-boldoblique.ttf: Iosevka Custom,Iosevka Custom Bold Oblique:style=Bold Oblique,Regular
```

I can't tell why he did that and I apologize for this odd configuration that will likely override existing Iosevka defaults. If you don't mind it, feel free to replace your defaults; if this messes the rest of your desktop up, you may want to choose a different font and edit `fonts.toml`. (Trust me, it frustrates me just as much and porting this config to a different machine only partially worked in one case.)

**Q: Where are the arrows?**

This is not set by any terminal emulator but by the shell (in this case zsh) itself. Oh My Zsh, the most popular framework for zsh, handles this and there are [tons of themes you can choose from](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes). Unfortunately, my config calls a custom theme called `Archcraft`, which came pre-installed with (you guessed it) [Archcraft](https://github.com/archcraft-os).

The theme can be copied and saved to `~/.oh-my-zsh/custom/themes/archcraft.zsh-theme`:

```
# Default OMZ theme for Archcraft

if [[ "$USER" == "root" ]]; then
  PROMPT="%(?:%{$fg_bold[red]%}%{$fg_bold[yellow]%}%{$fg_bold[red]%} :%{$fg_bold[red]%} )"
  PROMPT+='%{$fg[cyan]%}  %c%{$reset_color%} $(git_prompt_info)'
else
  PROMPT="%(?:%{$fg_bold[red]%}%{$fg_bold[green]%}%{$fg_bold[yellow]%} :%{$fg_bold[red]%} )"
  PROMPT+='%{$fg[cyan]%}  %c%{$reset_color%} $(git_prompt_info)'
fi

ZSH_THEME_GIT_PROMPT_PREFIX="%{$fg_bold[blue]%}  git:(%{$fg[red]%}"
ZSH_THEME_GIT_PROMPT_SUFFIX="%{$reset_color%} "
ZSH_THEME_GIT_PROMPT_DIRTY="%{$fg[blue]%}) %{$fg[yellow]%}✗"
ZSH_THEME_GIT_PROMPT_CLEAN="%{$fg[blue]%})"

```

Then go to your `~/.zshrc` and set `ZSH_THEME` (line 11) to `"archcraft"`. Of course, the name of the theme is up to you and you're free to replace "Archcraft" with a different name and further customize it to your liking. You may want to also edit `oh.my-zsh.sh` to allow initialization of custom themes.

If you don't see arrows and instead just the usual unicode blocks, you're missing fonts able to render this Unicode character. If overriding your default Iosevka fonts with the customized set provided by this repo is not a choice for you, you may rely on the default .ttf files for the Iosevka font family or switch to Noto Sans. However, keep in mind that those fonts are vastly different from the customized Iosevka fonts and Noto Sans in particular may load with improper spacing for certain letters.

**Q: Why does the demo screenshot show Xfce Terminal alongside Alacritty?**

A: My Xfce Terminal uses the same color scheme but always relies on bright colors (`colors.bright` in Alacritty). It's just a demo of what bright colors look like in practice. (Also my Vim still is calling Xfce Terminal and I can't be bothered to change that.

**Q: What's that toolbar / what WM are you using in the demo?**

It's a customized Fluxbox. You can find the configuration [here](https://github.com/jatardine/dotfiles-fluxbox-acer).
