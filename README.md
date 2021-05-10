# BitTorrent Test Network

Network setup for testing BitTorrent peers.

## Setup and Run

Start containers with:

    docker-compose up --build

Interface with a peer with:

    docker exec -it <CONTAINER ID> bash

Containers need to be brought down to reset files:

    docker-compose down

## Network Configuration

The default setup consists of a tracker and 2 peers where
1 peer starts by seeding a torrent for an image to the
other peer.

The network is comprised of:
  - `tracker`: Tracker web server
  - `peer_1`: Peer using Transmission client starting with full file/directory
  - `peer_2`: Peer using Transmission client that does not start full file/directory

To add additional peers, duplicate and rename the service you are interested in replicating
in `docker-compose.yml`.

## Changing Test Torrent

- Generate a new torrent in BitTorrent
  - Create a new torrent under `File->Create New Torrent`
  - Add target file/directory
  - Set trackers to `http://tracker/announce` (This can also be changed to an external tracker if desired.)
  - Create and save torrent as `test.torrent`

- Copy `test.torrent` and target file/directory to `transmission`

- Change `cp networking_03.png ./downloads` to `cp -r <TARGET FILE/DIRECTORY> ./downloads` in `docker-compose.yml`
for peers with the initial target file/directory.

## Adding Other Clients

Custom BitTorrent client implementations can be added to the network by adding a folder containing the new client's code and a `Dockerfile`
specifying how to build the image for the client. `docker-compose.yml` can then be updated to include the new folder
as well as a run command for the client. `custom_client` contains a skeleton for adding new clients.

When adding a new client, make sure:

- Executables have execution permission before building in Docker Compose
- Your client has a copy of the `.torrent` you are working with
- `docker-compose.yml` is configured to expose the port your client is advertising itself on
