---
Title: Linux Useful Command
Description: >
  The useful command can let you use the command line more efficiently
---

+ [Convert linefeeds for all files in a folder | Bravehartk2's Blog"](https://www.ask-sheldon.com/convert-linefeeds-for-all-files-in-a-folder-crlf-to-lf/#:~:text=To%20just%20convert%20the%20CRLF%E2%80%99s%20in%20a%20single,%7C%20xargs%20-P%204%20-0%20-n%201%20dos2unix)

  ``` bash
  find . -type f -print0 | xargs -P 4 -0 -n 1  dos2unix 
  ```

+ [How to remove duplicates and sort entries in zsh history - Quora](https://www.quora.com/How-do-I-remove-duplicates-and-sort-entries-in-zsh-history)

  ``` bash
  cat -n .zsh_history | sort -t ';' -uk2 | sort -nk1 | cut -f2- > .zsh_short_history
  ```

+ [Linux Clear Journalctl Log](https://unix.stackexchange.com/questions/139513/how-to-clear-journalctl)

  ``` bash
  # remove all file
  sudo rm -rf /run/log/journal/*
  # or
  sudo journalctl --vacuum-time=1seconds
  sudo journalctl --vacuum-size=0M
  ```
