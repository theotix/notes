CPP=g++
CFLAGS=-g -rdynamic -O0 -Wall `pkg-config sigc++-2.0 gtk+-3.0 gtkmm-3.0 gdkmm-3.0 webkitgtk-3.0 sqlite3 uuid --cflags`-Ilib/ -Ilibevernote/evernote-sdk -I. -Ilibevernote -Ilibevernote/evernote-sdk/thrift -Iinclude/ -lssl -lcrypto -lpthread -ldl

TGT=notes
OBJS= main.o notify.o utils.o windowbody.o maintoolbar.o leftpaneview.o notelistpaneview.o notepaneview.o databasemanager.o notedata.o evernoteSyncClient.o querygenerator.o webviewpopup.o evernotewebviewbox.o welcomewindow.o

all : ${OBJS}
ifdef WITHPDF
		@echo "Making with pdf"
		${CPP} ${CFLAGS} -o ${TGT} ${OBJS} `pkg-config sigc++-2.0 gtk+-3.0 gtkmm-3.0 webkitgtk-3.0 sqlite3 uuid --libs` -Ilib/ -Ilibevernote/evernote-sdk -Iwithpdf/ -I. -Ilibevernote -Ilibevernote/evernote-sdk/thrift -Iinclude/ -lssl -lcrypto -lpthread -lwkhtmltox -ldl
else
		@echo "Making without pdf"
		${CPP} ${CFLAGS} -o ${TGT} ${OBJS} `pkg-config sigc++-2.0 gtk+-3.0 gtkmm-3.0 webkitgtk-3.0 sqlite3 uuid --libs` -Ilib/ -Ilibevernote/evernote-sdk -Inormal/ -I. -Ilibevernote  -Ilibevernote/evernote-sdk/thrift -Iinclude/ -lssl -lcrypto -lpthread -ldl
endif

%.o : %.cc
ifdef WITHPDF
	${CPP} ${CFLAGS} -Iinclude/withpdf/ -c $<
else
	${CPP} ${CFLAGS} -Iinclude/normal/ -c $<
endif

.PHONY: clean
clean:
	rm -rf *.o notes

test: all
	LD_LIBRARY_PATH=libevernote/ ./notes

debug: all
	LD_LIBRARY_PATH=libevernote/ gdb --tui ./notes

clean-db:
	rm -f ~/.local/notify.db
