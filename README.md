# Jellyfin Docker container

This is a docker container that runs my jellyfin server that I have on my debian mini PC.

It uses Caddy with cloudflare add-on,
Jellyfin (obviously) for media storage and access,
Cloudflare for DNS,
and Docker to keep it all in a container.

I followed this [YouTube guide](https://youtu.be/1Ejobytuh5s?si=71cIm1QTzprEzIZw), 
but then deviated to make it cloudflare friendly and then run in docker.

> [!Note]
> I am not affiliated with DemonWarriorTech.
> I just happened to stumble upon their videos and really enjoyed how in-depth and easily explained their tutorials were.
> It was the basis for the eventual set up that you see in this repo.

## Caddy

[Caddy](https://caddyserver.com/) is a server software that handles TLS certificates and more.
I use it since it's simple to use, FOSS, and extremely minimal.

It has such a little download size and is handled entirely in a single file which is
simple to understand and modify.

Love it.

## Jellyfin

[Jellyfin](https://jellyfin.org/) is a FOSS media server system.
It is an alternative to [Plex](https://www.plex.tv/your-media/) and 
[Emby](https://emby.media/).

It's a frontend that allows easy access to my media like Movies, Books, Anime, TV-Shows, etc.

I use it mainly for my music collection since I have a lot of CD's, but it also holds some of my favored movies, anime, and stuff.
I like it as an alternative to Spotify since it's ad-free, my music, and free.
Makes me happy.

### Why Jellyfin?

I decided on Jellyfin since it is FOSS, and has a dedicated set of apps and applets for end-user devices like smartphones and Smart TV's.
This means that I can make the Jellyfin server, expose it to the internet, then access it anywhere with internet access.

I found plex to be lame since you have to pay for it.
I have the capabilities to maintain my own server and not pay anyone else to do it.
Having to pay a MONTHLY subscription to access MY data? 
Especially when I can do it myself and customize it how I want it?
Hell nah fam.

Emby is cool, but I'd rather go for something with a bit more support for end-user
devices (like the Jellyfin app for mobile) as well as the dev docs.

If Jellyfin was not an option, I would say Emby is a good runner-up.

### How do you prepare your media for Jellyfin?

#### Music

For Music, I use:

- [EAC](https://www.exactaudiocopy.de/) - Exact Audio Copy - (A Windows OS Music CD Reader)
I used this since it had some great reviews from the internet and I can absolutely attest to that.
It ran well, handled just about any type of CD that I used, and has some cool customization should you want to use that.
I also really enjoyed the GUI. I would prefer a dark-mode option, but hey still super cool.
It also has integrations to tagging databases like MusicBrainz, and others.

- [abcde](https://abcde.einval.com/wiki/) - A Better CD Encoder - (A Linux-friendly Music CD Reader)
I enjoy this more compared to EAC since it's run via cmd line and I can edit it via nvim (text editor of choice).
It integrates with other plugins just like EAC such as Musicbrainz.

I store the Music in **16-bit 44.1 kHz quality FLAC**.
According to research online, namely 
[this source](https://www.tonestack.net/articles/digital-audio/high-resolution-audio-vs-16bit-44khz.html)
as well as other people's opinions on the internet,
I decided on this quality as a maximum limit for what I store my music as.
I also tested the other higher qualities and found them overkill which supported the findings from this article.

I also use the [FLAC](https://en.wikipedia.org/wiki/FLAC) filetype.
This filetype is useful since it's lossless and compressed too.
The name of FLAC is actually (Free Lossless Audio Codec) which is neat.
Compared to wav's it can take up to 50% less space, and also allows for metadata (i.e. tagging).

Speaking of Tagging, I utilize [MusicBrainz](https://musicbrainz.org/) for tagging.
It is basically an extremely large database of music metadata.
It has everything you would want to tag your CD's and digital music files.

I utilize their software [MusicBrainz Picard](https://picard.musicbrainz.org/) 
which is a FOSS that allows you to tag CD's or audio files with their system.
It integrates FLAWLESSLY between their website and software version.
You can copy the link for the exact CD release that you have in the URL and drag it into
Picard, and it is just THERE. 
ABSOLUTELY MENTAL.

I don't even think people realize how incredible that is given the VAST amount of
music information they have in their database.
Did I mention that it's *NIX and Windows compatible?

> [!Note]
> I am not affiliated with ANY of the software listed.
> I'm simply talking about them here in the README.md

#### Movies/TV-Shows/Anime/Comedy Specials/Anything that has Video and Audio

I utilize [.mkv](https://en.wikipedia.org/wiki/Matroska) files since they are lossless
and combine all information from the video into a single file.

For movies I use:

- [MakeMKV](https://www.makemkv.com/). It works flawlessly across OS in my experience.
Super simple GUI that get's the job done.
Works on encrypted DVD's and Blu-rays allegedly.

- [Handbrake](https://handbrake.fr/). 
Another cross-platform desktop FOSS tool that is awesome.
It extracts video from non-encrypted sources (home movies and stuff like that).
Has a GUI which is nice, but even more impressive are its many customization options
which makes it stand out for me.

I highly recommend these two software.

## Cloudflare

I already have a couple of domains on [Cloudflare](https://www.cloudflare.com/) so I
decided to make it route through another domain from them.
Makes the process for caddy super simple and in turn, jellyfin too.

It handles traffic and allows me to monitor it.
It also has high uptime compared to...

### DuckDNS

I actually used [DuckDNS](https://www.duckdns.org/) before Cloudflare as a free option.
I still support them and their mission.

HOWEVER!

The uptime was a big issue for me. 
I don't want to think about my connection not being active whenever
DuckDNS goes down, which was becoming an increasingly apparent problem.

I still highly recommend it to other people to use for other projects.
I simply opted for Cloudflare as a paid option since I valued the uptime highly.

## Docker

I run this inside a [Docker](https://www.docker.com/) container for portability and low resource usage.

Docker is a software that basically lets you create containers (NOT VIRTUAL MACHINES) to compartmentalize actively running pieces of software.
Envision a manager that tells their team leads to do separate tasks.
That's basically Docker in use.

Here, I have 3 containers being created:

- Caddy: caddy stuff (server)
- Jellyfin: handles the jellyfin instance (most of the heavy lifting - media reading, routing, auth, etc.)
- Cloudflare-ddns: ensures connection to cloudflare (TLS/DNS)

Check the 
[Dockerfile](https://github.com/EZRA-DVLPR/jellyfin/blob/main/Dockerfile)
and 
[docker-compose](https://github.com/EZRA-DVLPR/jellyfin/blob/main/docker-compose.yml.sample)
for info on how I set that up with my .env file.

> [!Important]
> I use a sample Caddyfile and docker-compose to hide the domain I actually use.
> I still include them as .sample's since it may prove helpful to others for an idea on how to set it up

> [!Note]
> No I will not be giving you access to my Jellyfin server
