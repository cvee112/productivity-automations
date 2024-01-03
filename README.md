# Environmental Automations in OS X
This is a collection of guides and scripts for environmental automations in OS X

Disclaimer: I tested what follows for my system only. Please modify the steps as you see fit. Also, I'm not an expert and I just figured this out on my own by reading online and piecing together what works for me. The guides here are mainly for people who don't have much coding experience but want to implement environmental automations to help them with productivity and other stuff.

## Schedule your calendar/task list/whatever URL to open in full screen mode via your default browser

1. Open Terminal.

2. Create a bash script in a location you see fit. In my case, I did the following after navigating via `cd` (e.g., `cd ~/bash` just because I have a bash folder that I added to my `PATH` so all the executable scripts there can be executed from anywhere by typing the name - but that's not necessary for you):

    ```console
    vim filename
    ```

    You can also do:

    ```console
    vim filename.sh
    ```

3. (If you're using vim) Press `i` for insert mode, then input something like the following (this opens GCal in day view in full screen via my default browser, Arc):

    ```
    #!/bin/bash

    open "https://calendar.google.com/calendar/u/0/r/day";
    /usr/bin/osascript -e 'tell application "System Events"' -e 'keystroke "f" using {control down, command down}' -e 'end tell' -e EOF
    ```

4. (If you're using vim) Press <kbd>Esc</kbd> to go back to normal mode, then type `:wq` to save what you wrote (w) and exit (q). Use `q!` if you don't want to save what you wrote and just want to exit instead.

5. Type and enter `crontab -e` to schedule a cron job. Apparently, there are other ways to schedule a script, but this is the simplest I've found.
   
6. Press `i` again to enter insert mode, then schedule a job by adding the appropriate line in cron syntax. You can use [Crontab](https://crontab.guru/) to help you devise the first part of the expression that fits your needs. In my case, I wanted my Google Calendar to open at the start of every hour, so I used:

    ```
    0 * * * * /Users/[my_username]/bash/gcal
    ```

    I have this other script that opens Amazing Marvin in full screen mode via my browser, and I wanted to schedule that to run every 9:30 pm in my time zone, so I also added:

    ```
    30 21 * * * /Users/[my_username]/bash/marvin
    ```

7. Press <kbd>Esc</kbd> then type `:wq` to save and exit. You'll be prompted to allow Terminal to administer your computer afterwards - choose OK so that it works properly.

8. And you're done! Feel free to test this out by adding a time that's like a minute or two away from your current time, just so that you'd see that it works as intended.

    P.S. After this, when you open Terminal, you might get notification saying "You have mail." If you want to clear that, just input `mail` to read the mail, keep on pressing <kbd>Enter</kbd> until you've read all the mail (if there are multiple), then input `q` to exit.
