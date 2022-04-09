all: favicon.ico

favicon@16.png:
	inkscape -w 16 -h 16 -o favicon@16.png favicon.svg

favicon@32.png:
	inkscape -w 32 -h 32 -o favicon@32.png favicon.svg

favicon@48.png:
	inkscape -w 48 -h 48 -o favicon@48.png favicon.svg

favicon@64.png:
	inkscape -w 64 -h 64 -o favicon@64.png favicon.svg

favicon@128.png:
	inkscape -w 128 -h 128 -o favicon@128.png favicon.svg

favicon.ico: favicon@16.png favicon@32.png favicon@48.png favicon@64.png favicon@128.png
	convert favicon@16.png favicon@32.png favicon@48.png favicon@64.png favicon@128.png favicon.ico

