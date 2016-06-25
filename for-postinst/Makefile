PKG_NAME:=m2repository
PKG_VERSION:=33

PKG_SOURCE:=android_${PKG_NAME}_r${PKG_VERSION}.zip
PKG_SOURCE_URL:=https://dl.google.com/android/repository/${PKG_SOURCE}

DL_DIR=/var/cache/google-android-m2repository-installer
UNPACK_DIR=$(DL_DIR)/m2repository
INSTALL_DIR=/usr/lib/android-sdk/extras/android
DOC_DIR=/usr/share/doc/google-android-m2repository

all: $(DL_DIR)/$(UNPACK_DIR)/source.properties

install: all
	install -d -m0755 $(DOC_DIR)
	gzip -9 --stdout $(UNPACK_DIR)/NOTICE.txt > $(DOC_DIR)/copyright.gz
	install -m0644 $(UNPACK_DIR)/source.properties $(DOC_DIR)/
	install -d -m0755 $(INSTALL_DIR)
	mv $(UNPACK_DIR) $(INSTALL_DIR)/

$(DL_DIR)/$(UNPACK_DIR)/source.properties: $(DL_DIR)/$(PKG_SOURCE)
	cd $(DL_DIR) && unzip -ou $(PKG_SOURCE)

$(DL_DIR)/$(PKG_SOURCE): $(DL_DIR)
	cd $(DL_DIR) && \
		wget --continue $(PKG_SOURCE_URL)
	sha1sum -c $(PKG_SOURCE).sha1

$(DL_DIR):
	install -d -m0700 $(DL_DIR)

clean:
	-rm -rf -- $(UNPACK_DIR)

distclean: clean
	-rm -rf -- $(DL_DIR)

.PHONY: install clean

