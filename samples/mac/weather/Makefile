all: clean build

MONO=/Library/Frameworks/Mono.framework/Versions/Current/Commands/mono
MONOMSBUILD=/Library/Frameworks/Mono.framework/Versions/Current/Commands/msbuild
OBJC_GEN_DIR=../../../objcgen
OBJC_GEN=$(OBJC_GEN_DIR)/bin/Debug/objcgen.exe
$(OBJC_GEN): $(wildcard $(OBJC_GEN_DIR)/*.cs) $(wildcard ../../support/*)
	$(MAKE) -C $(OBJC_GEN_DIR)

prepare: $(OBJC_GEN)
	$(MONOMSBUILD) /p:Configuration=Debug MyManagedStuff/MyManagedStuff.sln
	$(MONO) $(OBJC_GEN) --debug -c MyManagedStuff/MyManagedStuff/bin/Debug/MyManagedStuff.dll -o theweather/MyManagedStuff
	cp MyManagedStuff/MyManagedStuff/bin/Debug/MyManagedStuff.dll theweather/MyManagedStuff/MyManagedStuff.dll

build: prepare
	xcodebuild -project theweather/theweather.xcodeproj -target theweather -configuration Debug

clean:
	rm -rf theweather/MyManagedStuff theweather/build MyManagedStuff/MyManagedStuff/bin MyManagedStuff/MyManagedStuff/obj