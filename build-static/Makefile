
# run from rtl-sdr/build-static
#
LIBUSBINCLUDEDIR = ../../libusb-1.0.26/libusb
LIBUSBSTATICDIRx86  = ../../libusb-1.0.26/build-static-x86_64
LIBUSBSTATICDIRARM  = ../../libusb-1.0.26/build-static-arm64

SRCDIR = ../src

SOURCE    =   $(SRCDIR)/rtl_tcp.c \
              $(SRCDIR)/librtlsdr.c \
							$(SRCDIR)/tuner_r82xx.c \
							$(SRCDIR)/tuner_e4k.c \
							$(SRCDIR)/tuner_fc0012.c \
							$(SRCDIR)/tuner_fc0013.c \
							$(SRCDIR)/tuner_fc2580.c \
							$(SRCDIR)/convenience/convenience.c

LIBx86 =      $(LIBUSBSTATICDIRx86)/libusb-1.0.a \
							$(LIBUSBSTATICDIRx86)/darwin_usb.o


LIBARM =      $(LIBUSBSTATICDIRARM)/libusb-1.0.a \
							$(LIBUSBSTATICDIRARM)/darwin_usb.o



rtl_tcp:			$(SRCDIR)/rtl_tcp.c

								clang $(SOURCE)  $(LIBx86) \
								    -framework Foundation  \
							      -framework IOKit  \
										-framework Security \
										-I. \
										-I$(SRCDIR)/../include \
										-L/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include \
							      -target x86_64-apple-macos13 -lm -o rtl_tcp-x86_64

								clang $(SOURCE)  $(LIBARM) \
										 -framework Foundation  \
										 -framework IOKit  \
										 -framework Security \
										 -I. \
										 -I$(SRCDIR)/../include \
										 -L/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include \
										 -target arm64-apple-macos13 -lm -o rtl_tcp-arm64

								lipo -create -output rtl_tcp rtl_tcp-x86_64 rtl_tcp-arm64
