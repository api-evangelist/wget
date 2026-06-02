---
title: 'Gary Benson: Docker images by age or size'
url: https://gbenson.net/docker-images-by-size-age/
date: '2026-05-19'
author: ''
feed_url: https://planet.gnu.org/rss20.xml
---
Files by age, newest first: ls -lt Docker images by age, newest first: docker images --format "{{.CreatedAt}}\t{{.Repository}}:{{.Tag}}" | sort -r Files by size, largest first: ls -lS Docker images by size, largest first: docker images --format "{{.Size}}\t{{.Repository}}:{{.Tag}}" | sort -rh Why why why??!
