
mkwgconf
===

Generates Wireguard configuration files. Designed for a
client/server-style Wireguard setup, but you can customize it however
you want.

Requirements
===
1. Python 2.7
1. pystache (pip module)

How to use
===

Have Wireguard installed on your server and clients.

Edit `wireguard.conf` to include the names of all the clients you
want to be able to connect to your VPN.

Edit anything else in the conf file, such as the name of the
interface (it's usually wg0 in most Wireguard documentation), or the
intranet IP address ranges that you want your clients to be able to
access.

run `./mkwgconf`

You will now have everything generated in `output` directory. Replace current wireguard config at `/etc/wireguard` with `wg0.conf`.

The specific client files specified as following:

``wg0-*client*-full.conf``
> Handles all traffic over VPN
> 
``wg0-*client*.conf``
> ONLY internal subnets

(Optional) Generate QR code
`qrencode -t ansiutf8 < wg0-*client*-full.conf`

Config should be updated everytime you run `./mkwgconf` to guarantee you do not regenerate private keys or public keys.
