# Icons

All the icons can be transferred over the bus by a particular serialization of their data, capabe of representing multiple resolutions of the same image or a brief aimation of images of the same size.

Icons are transferred in an array of raw image data structures of signature `a(iiay)` with each one describing the width, height, and image data respectively. The data is represented in ARGB32 format and is in the network byte order, to make easy the communication over the network between little and big endian machines.
