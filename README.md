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

### Why Jellfin?

I decided on Jellyfin since it is FOSS, and has a dedicated set of apps and applets for end-user devices like phones and Smart TV's.
This means that I can make the Jellyfin server, expose it up to the internet, then access it anywhere with internet access.

I found plex to be lame since you have to pay for it.
I have the capabilities to maintain my own server and not pay anyone else to do it.
Monthly subscription to access my data? When I can do it myself and customize it how it want it?
Hell nah fam.

Emby is cool, but I'd rather go for something with a tiny bit more support for end-user devices as well as the dev docs.

If Jellyfin was not an option, I would say Emby is a good runner-up.

## Cloudflare

I already have a couple of domains on [Cloudflare](https://www.cloudflare.com/) so I decided to make it route through them.
Makes the process for caddy super simple and the same for the jellyfin too.

It handles traffic and I can monitor that stuff.
It also has high uptime compared to...

### DuckDNS

I actually used [DuckDNS](https://www.duckdns.org/) before Cloudflare as a free option.
I also support them and their mission.

HOWEVER!

The uptime was a big issue for me. 
I don't want to think about my connection not being active whenever
DuckDNS goes down, which was becoming an increasingly apparent problem.

I still highly recommend it to other people to use for other projects.
I simply opted for Cloudflare as a paid option since I valued the uptime highly.

## Docker

I run this inside a [Docker](https://www.docker.com/) container for portability and low resource usage.

Docker is a software that basically lets you create containers (NOT VIRTUAL MACHINES) to compartmentalize actively running pieces of software.
Envision a manager that tells it's team leads to do stuff.
That's basically Docker in use.

Here, I have 3 containers being created:

- Caddy: caddy stuff (server)
- Jellyfin: handles the jellyfin server (most of the heavy lifting - media reading, routing, auth, etc.)
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
