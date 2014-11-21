cron-last-sunday
================

Cron Last Sunday is the solution for those picky admins that always wanted to run a task the third Thursday of the Month, or maybe the first Monday, whatever.

Read a short [intro](http://xr09.github.io/cron-scheduling-for-the-fancy.html) at my blog.


Install
=======

Copy run-if-today to ~/bin for private use:

    cp -av run-if-today ~/bin/

Or /usr/local/bin/ for use by all system users:

    cp -av run-if-today /usr/local/bin/


Usage
=====

run-if-today accepts two parameters, nth-day and day-of-week:


run-if-today 1 Sat # Checks for the first Saturday of the month

run-if-today 3 Mon # 3rd Monday


Keep in mind the day of week must have 3 letters starting with a capital letter. Check "date +%a" for today.

Sun, Mon, Tue, Wed, Thu, Fri, Sat



Using this is rather simple, the script "run-if-today" evaluates its parameters and returns true or false 'a la bash' i.e. 0 or 1, then with the && operator we use it to execute tasks with cron, like this:

    30 6 * * 6 root run-if-today 1 Sat && /root/myfirstsaturdaybackup.sh


If run-if-today returns 1 (false in Bash) then the && (and) will stop the operation and nothing happens.

You could use a * instead of 6 for the day of week, the script checks if it's Saturday and within the date range of the desired week, but in order to execute this code as little as possible it's recommended to fix a weekday so it runs at most 4 or 5 times a month.
