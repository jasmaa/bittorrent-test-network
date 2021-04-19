# BitTorrent Test Network

Network setup for testing BitTorrent peers.

## Setup and Run

    docker-compose up --build

To check a peer:

    docker exec -it <CONTAINER ID> bash

## Network Configuration

Sample setup is comprised of:
  - `tracker`: Tracker web server
  - `peer_1`: Peer using Transmission client starting with full file/directory
  - `peer_2`: Peer using Transmission client that does not start full file/directory

To add additional peers, duplicate and rename the service you are interested in replicating
in `docker-compose.yml`.

## Changing Test Torrent

- Generate a new torrent in BitTorrent
  - Create a new torrent under `File->Create New Torrent`
  - Add target file/directory
  - Set trackers to `udp://tracker/announce` (This can also be changed to an external tracker if desired.)
  - Create and save torrent as `test.torrent`

- Copy `test.torrent` and target file/directory to `transmission`