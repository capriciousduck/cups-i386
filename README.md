# cups-i386
Dockerized CUPS for 32-bit Docker Machines

## Usage
To allow access to a USB printer, execute the following run statement:

First create a volume using:
```bash
docker volume create cups_config
```
The run the cups container using:

```bash
docker run -d -p 631:631 --restart unless-stopped --privileged -v cups_config:/etc/cups -v /var/run/dbus:/var/run/dbus -v /dev/bus/usb:/dev/bus/usb --name cups capriciousduck/cups-i386
```
Access at `http://RPI.IP.ADDRESS:631`.  When asked for user and password, type `print` for both.

## Gotchas
Bonjour doesn't seem to play nice when the instance is encapsulated in a container.  Include `-v /var/run/dbus:/var/run/dbus` in your run statement to make your shared printer visible to Apple computers.
