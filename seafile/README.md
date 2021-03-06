# b4t.to infra - Seafile

This is my [Seafile](https://www.seafile.com/en/home/) instance which acts as:

* Storage (My Dropbox replacement)
* Markdown notes database w/ Typora for local editting (Notion.so replacement)
* Sharing of files via links to friends
* "Drop point" ingest for files from devices I can't manage as easily (phone) via WebDAV syncing
* Syncing to all devices that need files locally via libraries

## Setup

* `docker-compose up --build -d`

You will also want to:

* Login to the admin account and
  * Copy `sf_dark_theme_7.1.3.css` into the custom CSS
  * Add the favicon and bg to brand the instance
* Copy the `seafile/` configs into the data directory
* Setup environment variables
  * `$SEAFILE_MYSQL_PASSWORD` - Strong and random, ties app to DB
  * `$SEAFILE_ADMIN_PASSWORD` - Admin account password
  * `$SEAFILE_BACKUP_B2_KEY_ID` - The key id for the Backblaze B2 access
  * `$SEAFILE_BACKUP_B2_KEY` - The actual applicationKey in Backblaze B2
  * `$SEAFILE_OBSCURED_PASSWORD` -  This needs to be the output of `docker container run rclone/rclone obscure [PASSWORD]`
  * `$BATTO_SVC_AUTH` - Strong and random, ties scripts together

### TODO

* WebDAV syncing does not support _setting_ mtime easily, meaning everything synced TO Seafile without the app will lose the proper mtime. Keep that in mind... Would be nice to get support for that but the WebDAV RFC doesn't really describe a good mechanism that's supported across the protocol
