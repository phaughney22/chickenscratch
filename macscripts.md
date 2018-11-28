# Useful MacOS Administration Scripts

Managing an entirely Apple based environment has been both a rewarding experience as well as challenging one. Windows has had years of enterprise focused development which is lightyears ahead of Apple when it comes to centralized management. That being said, third party software vendors have really stepped up their game to provide some great solutions. In the environment I manage I opted to go with Addigy for an asset management system for all of our devices. This was the first step in the building block for the organization's tech stack when I came in. It allows for cloud hosted management of all the devices in the organization so that we can set company wide policies, deploy software, assist remotely and also deploy shell scripts to the entire fleet.

The following scripts are a collection of of scripts I have collected from various sources and some I have modified or written myself. They are short scripts, but have been very useful and common enough for me to save them. Hopefully you might find them useful for your day to day tasks. Always remember to test any scripts before running them live in prod!

## Adds everyone to lpadmin group so that they can add printers without being a full admin. Still will not be able to unlock printing preferences but will be able to add printers.
> $ sudo dseditgroup -o edit -a "everyone" -t group lpadmin

## Hides the specified user. In this case the user is "adminninja" since this is the default admin user.
> $ sudo defaults write /Library/Preferences/com.apple.loginwindow HiddenUsersList -array-add adminninja

## Returns diagnostic info for the current wireless network the machine is connected to.
> $ /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I

## Forces restart of Coree Audio on the Mac if there are audio problems that seem un-resolvable
> $ sudo killall coreaudiod

## Searches for files within Documents folders for the requested text "essay".
> $ mdfind -onlyin ~/Documents essay

## Speaks whatever you put in quotes on the machine it is executed on
> $ say "Hello"

## Deletes all files in specified folder that have not been accessed in 365 days
> $ find ~/Downloads/Test -type f -atime +365 -exec rm {} \;
> $ mdfind -0 -onlyin /Users/$(stat -f %Su /dev/console)/Downloads 'kMDItemLastUsedDate <= $time.this_month(-4)' | xargs -0 -n1 rm

## This version moves the files to the trash instead of deleting
> $ find ~/Downloads/Test -type f ! -name '.*' -atime +90 -exec mv {} ~/.Trash \;
> $ mdfind -onlyin /Users/$loggedInUser/Downloads 'kMDItemLastUsedDate <= $time.this_month(-6)'
> $ mdfind -0 -onlyin /Users/$(stat -f %Su /dev/console)/Downloads 'kMDItemLastUsedDate <= $time.this_month(-1)' | xargs -n 1 -I '{}' mv {} /Users/$(stat -f %Su /dev/console)/.Trash -rf
