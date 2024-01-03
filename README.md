# Environmental Automations in OS X
This is a collection of guides and scripts for environmental automations in OS X

Disclaimer: I tested what follows for my system only. Please modify the steps as you see fit. Also, I'm not an expert and I just figured this out on my own by reading online and piecing together what works for me. The guides here are mainly for people who don't have much coding experience but want to implement environmental automations to help them with productivity and other stuff.

## Schedule your calendar/task list/whatever URL to open in full screen mode via your default browser

### Write a bash script

Note: the following steps assumes you'd like to do stuff via command line, but you can create a script using a GUI text editor as well.

1. Open **Terminal**.

2. (Optional) Navigate to a location where you'd like to store your scripts via `cd` (e.g., `cd ~/bash` just because I have a bash folder for scripts).

3. Create a bash script using vim (or nano - whatever you prefer): 

    ```console
    vim filename
    ```

    The above works nicely if you want to execute your script from anywhere (i.e., not needing to navigate to its location) by typing an extensionless name, much like a regular command. This involves making the script executable with `chmod +x filename` and adding the folder containing the script to your `PATH` variable (if you'll do this, make sure to not mess up your `PATH` by mistake!).

    You can also name it with the .sh extension, but this is optional and just adds clarity:

    ```console
    vim filename.sh
    ```

5. **(If you're using vim)** Press `i` for insert mode, then input something like: (this opens GCal in day view in full screen mode via Arc, my default browser)

    ```bash
    #!/bin/bash

    open "https://calendar.google.com/calendar/u/0/r/day";
    /usr/bin/osascript -e 'tell application "System Events"' -e 'keystroke "f" using {control down, command down}' -e 'end tell' -e EOF
    ```

    You scan skip adding the second line if you don't want full screen mode. Feel free to modify this part however you like!

6. **(If you're using vim)** Press <kbd>Esc</kbd> to go back to normal mode, then type `:wq` to save what you wrote (w) and exit (q). Use `q!` if you don't want to save what you wrote and just want to exit instead.

### Schedule a cron job

5. Type `crontab -e` to schedule a cron job. Apparently, there are other ways to schedule a script, but this is the simplest I've found that works for me.
   
6. Press `i` again to enter insert mode, then schedule a job by adding the appropriate line in cron syntax. You can use [Crontab](https://crontab.guru/) to help you write the first part of the expression. In my case, I wanted my Google Calendar to open at the start of every hour, so I used:

    ```
    0 * * * * /Users/[my_username]/bash/gcal
    ```

    I have another script that opens Amazing Marvin in the same way. I scheduled that to run every 9:30 pm in my time zone by adding:

    ```
    30 21 * * * /Users/[my_username]/bash/marvin
    ```

7. Press <kbd>Esc</kbd> then type `:wq` to save and exit. Afterwards, you'll be prompted to allow Terminal to administer your computer - choose OK so that it works properly.

### Final notes

8. You're done! Feel free to test this out by using a time that's like a minute or two away from your current time, just so that you'd see that it works as intended.

    P.S. After this, when you open Terminal, you might get notification saying "You have mail." If you want to clear that, just input `mail` to read the mail, keep on pressing <kbd>Enter</kbd> until you've read all the mail (if there are multiple), then input `q` to exit.
