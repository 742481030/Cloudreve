macos下cgo交叉编译cloudreve  
#安装brew  


/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

/bin/zsh -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/742481030/cnhomebrew@master/Homebrew.sh)"

##安装gcc  
brew install gcc  
##安装mingw-w64  编译win需要
brew install mingw-w64  
#安装linux 工具链 文件较多建议梯子
brew install FiloSottile/musl-cross/musl-cross
#编译  windows
cd 项目目录  
##win64  

env CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc CXX=x86_64-w64-mingw32-g++ GOOS=windows GOARCH=amd64 go build -x -v -ldflags "-s -w" -o cloudrev_x64.exe
##win32

env CGO_ENABLED=1 CC=i686-w64-mingw32-gcc CXX=i686-w64w64-mingw32-g++ GOOS=windows GOARCH=386 go build -x -v -ldflags "-s -w" -o cloudre_x86.exe


#编译linux64
 env CGO_ENABLED=1 CC=x86_64-linux-musl-gcc GOOS=linux GOARCH=amd64 go build -ldflags "-linkmode external -extldflags -static" -x -a -o cloudreve_linux-64
 
 
 env CGO_ENABLED=1 CC=x86_64-linux-musl-gcc GOOS=linux GOARCH=amd64 go build -ldflags "-linkmode external -extldflags -static -s -w" -x -a -o cloudreve_linux-64-ws

#压缩可执行程序
brew install upx
使用方法 upx -9 可执行文件路径

