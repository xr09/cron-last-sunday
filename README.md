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

Since you're filtering by day of the week on cron you can just check for ocurrence on the script. For example:

    30 6 * * 6 root run-if-today 1 && /root/myfirstsaturdaybackup.sh

This checks for the first Saturday of the month. 

The script is also capable of checking day of the week in case you need to use it outside cron. See next section.

Standalone usage (verbose format)
=================================

run-if-today actually accepts two parameters, nth-day and day-of-week:

run-if-today 1 Sat # Checks for the first Saturday of the month

run-if-today 3 Mon # 3rd Monday

Keep in mind the day of week must have 3 letters starting with a capital letter. Check "date +%a" for today.

    Sun, Mon, Tue, Wed, Thu, Fri, Sat

Using this is rather simple, the script "run-if-today" evaluates its parameters and returns true or false 'a la bash' i.e. 0 or 1, then with the && operator we use it to execute tasks with cron, like this:

    30 6 * * 6 root run-if-today 1 Sat && /root/myfirstsaturdaybackup.sh


If run-if-today returns 1 (false in Bash) then the && (and) will stop the operation and nothing happens.
