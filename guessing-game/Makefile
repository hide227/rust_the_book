PKG_NAME := guessing-game
VERSION  := 0.1.0

DEBROOT := debroot

.PHONY: all
all: deb

.PHONY: build
build: target/release/$(PKG_NAME)

target/release/$(PKG_NAME): src/main.rs Cargo.toml
	cargo build --release

.PHONY: deb
deb: build
	rm -rf $(DEBROOT)
	mkdir -p $(DEBROOT)/usr/local/bin
	mkdir -p $(DEBROOT)/DEBIAN

	cp DEBIAN/control $(DEBROOT)/DEBIAN/control

	cp target/release/$(PKG_NAME) $(DEBROOT)/usr/local/bin/
	chmod 755 $(DEBROOT)/usr/local/bin/$(PKG_NAME)

	dpkg-deb --build $(DEBROOT) $(PKG_NAME)_$(VERSION).deb

.PHONY: clean
clean:
	cargo clean
	rm -rf $(DEBROOT) $(PKG_NAME)_*.deb
