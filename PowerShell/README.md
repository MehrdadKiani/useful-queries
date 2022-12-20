# PowerShell collection

## Theme

#### Orginal link
https://learn.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup#install-a-nerd-font

#### A quick setup
- Install Windows Terminal: https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=it-it&gl=it
- Install CaskaydiaCove Nerd Font from https://www.nerdfonts.com/font-downloads
- Install `winget install oh-my-posh`
- Install `winget install XP8K0HKJFRXGCK`
- Edit `notepad $PROFILE` and add `oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\paradox.omp.json" | Invoke-Expression` to the end of the file
- Change `paradox` with the one of the theme from here: https://ohmyposh.dev/docs/themes

## Rename Files

#### Remove from the beginning
```powershell
get-childitem *.txt | rename-item -newname { [string]($_.name).substring(1) }
```
