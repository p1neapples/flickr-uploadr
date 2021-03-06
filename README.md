flickr-uploadr
===============

Upload a directory of media to Flickr to use as a backup to your local storage.

Have a Raspberry Pi laying around that you got bored with after realizing that you have no use for RaspBMC?  Installing Raspbian + Bittorrent Sync + Flickr Uploadr makes a great mostly automatic backup solution.

## Features:
* Uploads images in full resolution to Flickr account (JPG, PNG, GIF)
* Stores image information locally using a simple SQLite database
* Automatically creates "Sets" based on the folder name the media is in
* Ignores ".picasabackup" directory (for Picasa users)
* Ability to remove images from Flickr when they are removed from your local hard drive (not enabled by default) 
* Ability to get start & completion status via Pushover.net

THIS SCRIPT IS PROVIDED WITH NO WARRANTY WHATSOEVER. PLEASE REVIEW THE SOURCE CODE TO MAKE SURE IT WILL WORK FOR YOUR NEEDS. IF YOU FIND A BUG, PLEASE REPORT IT.

## Requirements:
* Python 2.7+
* File write access (for the token and local database)
* Flickr API key (free)

## Optional:
* Pushover.net registration

## Setup:
Go to http://www.flickr.com/services/apps/create/apply and apply for an API key
Edit the following variables in the uploadr.ini:


* FILES_DIR = "files/"
* FLICKR = {
        "title"                 : "",
        "description"           : "",
        "tags"                  : "auto-upload",
        "is_public"             : "0",
        "is_friend"             : "0",
        "is_family"             : "0",
        "api_key"               : "Yourkey",
        "secret"                : "YourSecret"
        }
* SLEEP_TIME = 1 * 60
* DRIP_TIME = 1 * 60
* DB_PATH = os.path.join(FILES_DIR, "fickerdb")
* FLICKR["api_key"] = ""
* FLICKR["secret"] = ""
* PUSHOVER_TOKEN = "" (optional)
* PUSHOVER_USER = "" (optional)

## Usage
Clone repository and run (execution privs required):

$ ./uploadr.py

It will crawl through all the files from the 'FILES_DIR' directory and begin the upload process.

## Q&A
* Q: Who is this script designed for?
* A: Those people comfortable with the command line that want to backup their media on Flickr in full resolution.

* Q: Why don't you use OAuth?
* A: The older method is simpler to understand and works just as good. No need to fix what isn't broken.

* Q: Are you a python ninja?
* A: No, sorry. I just picked up the language to write this script because python can easily be installed on a Synology Diskstation.

* Q: Will this run on devices other than a Synology? Like a Raspberry Pi?
* A: Absolutely, see comments at the top of 'uploadr.py' to get some help with running in crontab.

* Q: Is this script feature complete and fully tested?
* A: Nope. It's a work in progress. I've tested it as needed for my needs, but it's possible to build additional features by contributing to the script.

* Q: Will it still work if I have subdirectories of 'FILES_DIR'?
* A: Yes. You can create multiple subs under 'FILES_DIR' and multiple sets will be created.
