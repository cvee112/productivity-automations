# Productivity Automations in macOS
This is a collection of step-by-step guides for app-free (script-based) productivity automations in macOS.

**Who this is for:** People who don't have much coding experience but want to implement basic productivity automations without downloading an app. While I wrote what follows with macOS in mind, modifying parts should make things work in Linux as well.

**Disclaimer:** These work for my system, but modify the steps as you see fit! I'm not an expert and I just figured things out by reading online and piecing together what works for me. 

## Navigation
1. [Automation 1: Schedule a URL to open every X o'clock](#automation-1)
2. [Automation X: Under construction](#tbc)
3. [Questions?](#questions)

## Automation 1: Schedule a URL to open every X o'clock <a name="automation-1"></a>

This schedules your calendar/task list/whatever URL to open in full screen mode via your default browser. It involves (1) [writing a bash script](#bash-1) then (2) [scheduling a cron job](#cron-2) that runs the script every X time.

### Write a bash script <a name="bash-1"></a>

Note: the following steps assume you'd like to do stuff via command line, but you can create a script using a GUI text editor as well.

1. Open **Terminal**.

2. (_Optional)_ Navigate to a location where you'd like to store your scripts via `cd` (e.g., `cd ~/bash` just because I have a bash folder for scripts).

3. Create a bash script using vim (or nano - whatever you prefer): 

    ```console
    vim filename
    ```

    The above works nicely if you want to execute your script from anywhere (i.e., not needing to navigate to its location) by typing an extensionless name, much like a regular command. This involves making the script executable with `chmod +x filename` and adding the folder containing the script to your `PATH` variable (if you'll do this, make sure to not mess up your `PATH` by mistake!).

    You can also name it with the .sh extension, but this is _optional_ and just adds clarity:

    ```console
    vim filename.sh
    ```

4. **(If you're using vim)** Press `i` for insert mode, then input something like:

    ```bash
    #!/bin/bash

    open "https://calendar.google.com/calendar/u/0/r/day";
    /usr/bin/osascript -e 'tell application "System Events"' -e 'keystroke "f" using {control down, command down}' -e 'end tell' -e EOF
    ```

    When run, this opens GCal in day view in full screen mode via Arc, my default browser. 

    Feel free to modify this part however you like! For example:
    - You can use a different browser via `open -a browsername URL` as in `open -a firefox https://google.com`.
    - You can remove the second line if you don't want to go full screen.

5. **(If you're using vim)** Press <kbd>Esc</kbd> to go back to normal mode, then type `:wq` to save what you wrote (w) and exit (q). Use `q!` if you don't want to save what you wrote and just want to exit instead.
   
6. _(Optional)_ Test the script by typing the script name (if you're still in the directory that contains it) or typing out the path to the script (if you're now in a different directory). For example, the script above is named _gcal_, so I can execute it by just entering:

    ```console
    gcal
    ```

### Schedule a cron job <a name="cron-2"></a>

7. Type `crontab -e` to schedule a cron job. Apparently, there are other ways to schedule a script, but this is the simplest I've found that works for me.
   
8. Press `i` to enter insert mode, then schedule a job by adding the appropriate line in cron syntax. You can use [Crontab](https://crontab.guru/) to help you write the first part of the expression. In my case, I wanted my Google Calendar to open at the start of every hour, so I used:

    ```
    0 * * * * /Users/[my_username]/bash/gcal
    ```

    I have another script that opens Amazing Marvin in the same way. I scheduled that to run every 9:30 pm in my time zone by adding:

    ```
    30 21 * * * /Users/[my_username]/bash/marvin
    ```

9. Press <kbd>Esc</kbd> then type `:wq` to save and exit. Afterwards, you'll be prompted to allow Terminal to administer your computer - choose OK so that it works properly.

### Final notes <a name="final-notes-3"></a>

10. You're done! Feel free to test this out by using a time that's like a minute or two away from your current time, just so that you'd see that it works as intended. P.S. After this, when you open Terminal, you might get notification saying "You have mail." If you want to clear that, just input `mail` to read the mail, keep on pressing <kbd>Enter</kbd> until you've read all the mail (if there are multiple), then input `q` to exit.

## Automation X: Under construction

I'll add to this as I create more automations for myself!

## Questions? <a name="questions"></a>

Feel free to message me (@cvee) through Discord!
