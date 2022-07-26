mkwgconf
===

Generates Wireguard configuration files. Designed for a
client/server-style Wireguard setup, but you can customize it however
you want.

How to use
===

1. Have Wireguard installed on your server and clients.

1. Make a copy of `example/example.json` and rename it to the name of your
Wireguard VPN server. In this example, we'll use `squirtle.conf`.

1. Edit `squirtle.conf` to include the names of all the clients you
want to be able to connect to your VPN.

1. Edit anything else in the conf file, such as the name of the
interface (it's usually wg0 in most Wireguard documentation), or the
intranet IP address ranges that you want your clients to be able to
access. *If your Wireguard server is a Raspberry Pi connected over
wifi, then you probably want to change `out_interface` to `wlan0`.*

1. `./mkwgconf --interface_conf=squirtle.json --server_template=server_conf.ini.tmpl --client_template=client_conf.ini.tmpl > squirtle-updated.json`

1. Notice that you now have a bunch of generated configuration files
in this directory. `wg0.conf` should be moved to your Wireguard server
at `/etc/wireguard/wg0.conf`. The other conf files are named according
to the names you used for your clients. The `-geo` conf is for VPN
usage where you want your client to appear to originate from a certain
IP address, and `-access` is for merely getting access to the intranet
ranges you specified in `intranet_ip_ranges`, without changing your
client's own IP address. Move those conf files to `/etc/wireguard` on
your client, or whatever you usually do to install those
configurations on your clients (e.g., `qrencode -t ansiutf8 <
wg0-pikachu-geo.conf` and then scanning the result on your phone).

1. Also notice that you piped the output to `squirtle-updated.json`,
which contains generated information that you probably want to keep,
such as the private Wireguard keys that the script generated for you
on the first run, and the IP addresses assigned to each client. After
inspecting this file, replace the original JSON file you created and
keep the new one, so that you'll be able to add new clients in the
future without regenerating all the prior clients' keys.
