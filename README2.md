fork of [TwitchToPodcastRSS](https://github.com/lzeke0/TwitchRSS)

# LightTwitchPodcast

converts a twitch channel in a full-blown podcast that you can use on your Light Phone ii or Light Phone iii's podcast tool
(you can use this with a normal podcast app on a smartphone too)

<img width="500" padding="8px" alt="Screenshot 2025-05-18 at 6 47 52 PM" src="https://github.com/user-attachments/assets/fc99bc9d-fd9c-49f4-b858-42b9242430aa" />

## Usage

when you host this, just type the channel name into the text box and click the button and an RSS link will be generated and copied to your clipboard.
you can also just add `/vod/channelName` to your server path (like rss.yourdomain.com/**vod/channelName**).

example: `myserver.com/vod/channelName`


### transcoding
to enable transcoding just add `?transcode=true` to your url. to disable transcoding, either do nothing or add `?transcode=false`.

example: `myserver.com/vod/channelName?transcode=True`

### show currently streaming
unfinished streams are not included, but if you want them to just add `?include_streaming=True` to the feed URL

example: `myserver.com/vod/channelName?include_streaming=True`

### sorting
you can order the feed by any field suppored by twitch, the list of fields to sort by can be found [here](https://dev.twitch.tv/docs/api/reference#get-videos) in the response field section

by default it sorts by the `published_at` field (sorted by date published with most recent first), I don't have a need for anything else but if you do, you can.

to enable sorting just add `sort_by=[key]` or/and `desc=True` to the URL

some examples:

to sort by view count:

`myserver.com/vod/channelName?sort_by=view_count`

to sort by view count descending:

`myserver.com/vod/channelName?sort_by=view_count&desc=true`

### only links mode

if you don't use this for a Light Phone and only listen to the episodes in the Twitch app or website (meaning you're using this in an RSS reader) you can enable the `links_only=true` to skip the fetching of the audio stream, doing so will make the feed generation almost instant, so it's highly reccomended to enable this option if you don't actually want MP3s generated

example: `yourdomain.com/vod/channelName?links_only=True`

### mixing options

to mix options just add `&` beetween them

example: `myserver.com/vod/channelName` `?sort_by=view_count` `&desc=true` `&links_only=true` `&include_streaming=True`

## RSS Sifting
<img width="320" align="right" alt="Screenshot 2025-05-18 at 6 34 34 PM" src="https://github.com/user-attachments/assets/2c13a69d-9232-4aa8-96da-b95eaf9bc734" />

for the RSS to actually work with Light's podcast tool, take the link you generated and put it into this sifter: [siftrss.com](https://siftrss.com)

set the parameters to:
I want to **`include`** items where the **`title`** is **`exists`**.

This is necessary for the RSS to actually work with Light's podcast tool, it just changes the formatting slightly. I honestly have no idea why Light's podcast tool requires this, Android podcast tools don't, but this is a necessary step.

## vps instructions
go to somewhere like DigitalOcean and buy an Ubuntu VPS (or if you have a server just use that)

purchase the basic option, like 1gb memory normal CPU, should cost around $6

make sure that you set it to the marketplace Docker template

then get your IP (save it) from that and SSH into it from your terminal

## installation instructions
before doing anything be sure to get your `SECRET` and `CLIENT ID` from the [Twitch Dev Console](https://dev.twitch.tv/console).

precompiled images are [here](https://hub.docker.com/r/madiele/twitch_to_podcast_rss/) for linux machines with arm64, amd64, arm/v7, i386 architectures

images for raspberry pis are included  

installation is via [docker-compose](https://docs.docker.com/compose/install/) with precompiled image.

`git clone https://github.com/imnotklaus/TwitchToPodcastRSS.git`

`cd LightTwitchPodcast`

run `nano docker-compose.yml`

now edit `docker-compose.yml` with your `PORT` (should be `80:80` unless you have other stuff on that port), `TWITCH_SECRET` and `TWITCH_CLIENT_ID`
(in the file you will find also optional parameters like sub_folder for use with reverse proxies, define a unique server name, and so on)

save and quit out of nano: (press `ctrl + O`, press `enter`/`return`, press `ctrl + X`)

run + deploy (in `root/LightTwitchPodcast`): `sudo docker compose up -d`

#### when you want to update:

run this inside the folder with `docker-compose.yml`

`sudo docker compose pull && sudo docker compose up -d`

then run this to delete the old version from your system (note: this will also delete any other unused image you have)

`sudo docker system prune`

## issues
if you have any issues with this feel free to contact me on Discord, `@imnotklaus` or via email `cloud@gayfrog.xyz`.

you can also create an issue here on this repo.

## About
original [TwitchToPodcastRSS](https://github.com/madiele/TwitchToPodcastRSS) was developed by Mattia Di Eleuterio.

forked to [LightTwitchPodcast](https://github.com/imnotklaus/LightTwitchPodcast) by imnotklaus.

### Donations
support the original creator, not me!!

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/madiele)
