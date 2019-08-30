mkwgconf
===

Generates Wireguard configuration files. Designed for a
client/server-style Wireguard setup, but you can customize it however
you want.

Requirements
===
Python 2.7
pystache (pip module)

How to use
===

1. Have Wireguard installed on your server and clients.

1. Edit `wireguard.conf` to include the names of all the clients you
want to be able to connect to your VPN.

1. Edit anything else in the conf file, such as the name of the
interface (it's usually wg0 in most Wireguard documentation), or the
intranet IP address ranges that you want your clients to be able to
access.

1. run `./mkwgconf`

1. You will now have everything generated in `output` directory. Replace current wireguard config at `/etc/wireguard` with `wg0.conf`.
The specific client files specified as following:

wg0-*client*-full.conf # Handles all traffic over VPN
wg0-*client*.conf # ONLY internal subnets + DNS (make sure this is within subnet range also for one of the internal subnets)

1. (Optional) Generate QR code
`qrencode -t ansiutf8 < wg0-*client*-full.conf`

1. Config should be updated everytime you run `./mkwgconf` to guarantee you do not regenerate private keys or public keys.


