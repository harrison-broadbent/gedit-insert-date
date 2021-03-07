# Gedit Insert Date

Insert the date using a keyboard shortcut in Gedit.

## **Installation**

### Simple (1 Minute)

- Download / clone this repository.

- Copy the "insert-date" file to the Gedit tools directory in your ~/home directory.

  - /home/username/.config/gedit/tools

- Open Gedit and press Menu (☰)>Preferences>Plugins and tick "External Tools".

Press F2 to insert a time/datestamp into your file in Gedit.

See "Customization" below for details on adjusting the behavior of the extension.

### Manual (3 Minutes)

- Open Gedit and press Menu (☰)>Preferences>Plugins and tick "External Tools".
- Press Menu (☰)>Manage External Tools...>+ (bottom left) to add a new tool.
- Give it a name, set a desired shortcut key (F2 works well), and change "Output" to "Insert at cursor position".
- Copy and paste the following script into the editor pane -

```bash

#!/bin/sh
echo "--- $(date +%c) ---\n"

```

Press F2 to insert a time/datestamp into your file in Gedit.

## **Customization**

Navigate to the Gedit entry for the tool.

- Menu (☰)>Manage External Tools...> select the name of the tool from the sidebar.
  - ("Add Date" if you followed the simple instructions)

### Change date format

- The _"$(date +%c)"_ part of the script is where the date is inserted, via the Bash _"date"_ command.
- Run _"date --help"_ in a terminal to get the full list of possible options.
- Some helpful ones (from: https://www.gnu.org/software/coreutils/date , _date --help_) -

  | Sequence | Description                                                |
  | -------- | ---------------------------------------------------------- |
  | %c       | locale's date and time (e.g., Thu Mar 3 23:05:25 2005)     |
  | %D       | date; same as %m/%d/%y                                     |
  | %F       | full date; same as %Y-%m-%d                                |
  | %T       | time; same as %H:%M:%S                                     |
  | %V       | ISO week number, with Monday as first day of week (01..53) |

- You can also use the following format modifiers -

  By default, date pads numeric fields with zeroes.
  The following optional flags may follow '%':

  | Sequence | Description                   |
  | -------- | ----------------------------- |
  | -        | (hyphen) do not pad the field |
  | \_       | (underscore) pad with spaces  |
  | 0 (zero) | (zero) pad with zeros         |
  | ^        | use upper case if possible    |
  | #        | use opposite case if possible |

### Change shortcut key

- Select "Shortcut key" from the Gedit tool pane, and then enter a new combination.

### Change padding text

- By default the date is wrapped as "--- $(date) ---\n"
  - This inserts "---", followed by the date, followed by "---", then 2 (**two**) trailing newlines.
  - Gedit automatically inserts a newline, then this script inserts a second.
- You can adjust the text around the "$(date)" -

  - Example: changing the line to -

  ```bash

  #!/bin/sh
  echo "--> DATE: $(date +%c) <--"

  ```

- would insert something like -
  - --> DATE: Sun 07 Mar 2021 17:08:00 <--
  - Followed by a single trailing newline

### Sources

- Date (Bash) reference document : https://www.gnu.org/software/coreutils/date
- AskUbuntu thread : https://askubuntu.com/questions/1168156/gedit-is-there-a-keyboard-shortcut-in-gedit-itself-to-insert-date-and-time
