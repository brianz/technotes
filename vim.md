## Toggle case for words

`g~iw`
Toggle case of the current word (inner word – cursor anywhere in word)

http://vim.wikia.com/wiki/Switching_case_of_characters

## Guide on text objects

https://blog.carbonfive.com/2011/10/17/vim-text-objects-the-definitive-guide/

## Docs on vim-surround

https://github.com/tpope/vim-surround/blob/master/doc/surround.txt

## Text object essentials

- `cit` -> Change inner HTML tag
- `cstt` -> Change the HTML tag itself, [preserving attributes](https://stackoverflow.com/questions/16340037/change-html-tag-in-vim-but-keeping-the-attributes-surround).
- `cis` -> Change inner sentence
- `cip` -> Change inner paragraph

- `ci'` -> Change inner single quoted content (same applies for any surround-type text like `"` or `(`
- `di"` -> Delete inner double quoted content
- `dt"` -> Delete from cursor position until next double quote, non-inclusive [(see this answer)](https://askubuntu.com/questions/64833/vi-shortcut-to-delete-until-the-next-x-character)

- `dst` -> Delete surrounding tag
- `cs'"` -> Change surrounding single quote to double quote

## Change text with yanked text

Go to the word you want to replace and do `cw`. Do `Ctrl+r` followed by `0` to paste the `0` register.

https://unix.stackexchange.com/questions/88714/vim-how-can-i-do-a-change-word-using-the-current-paste-buffer

## Change tag

`cstt`

https://stackoverflow.com/a/35915468/87858
