macos下cgo交叉编译cloudreve
#安装brew
##安装gcc
brew install gcc
##安装mingw-w64
brew install mingw-w64

#编译
cd youproject
##win64
env CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc CXX=x86_64-w64-mingw32-g++ GOOS=windows GOARCH=amd64 go build -x -v -ldflags "-s -w" -o cloudrev_x64.exe
##win32
env CGO_ENABLED=1 CC=i686-w64-mingw32-gcc CXX=i686-w64w64-mingw32-g++ GOOS=windows GOARCH=386 go build -x -v -ldflags "-s -w" -o cloudre_x86.exe
