macos下cgo交叉编译cloudreve  
REPO=$(cd $(dirname $0); pwd)

cd $REPO
command -v brew || /bin/zsh -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/742481030/cnhomebrew@master/Homebrew.sh)"
command -v x86_64-linux-musl-gcc || brew install FiloSottile/musl-cross/musl-cross
command -v x86_64-w64-mingw32-gcc || brew install mingw-w64
command -v go ||brew install go
command -v node || brew install node
command -v yarn || brew install yarn 
command -v upx ||brew install uxp 




 

go build -x -v -ldflags "-s -w" -o cloudrev-macos && upx -9 cloudrev-macos ||echo "编译请检查runtime"

env CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc CXX=x86_64-w64-mingw32-g++ GOOS=windows GOARCH=amd64 go build  -v -ldflags "-s -w" -o cloudrev_x64.exe && upx -9 cloudrev_x64.exe ||echo "win64编译失败"

env CGO_ENABLED=1 CC=i686-w64-mingw32-gcc CXX=i686-w64w64-mingw32-g++ GOOS=windows GOARCH=386 go build  -v -ldflags "-s -w" -o cloudre_x86.exe && upx -9 cloudre_x86.exe ||echo "win32编译失败"

env CGO_ENABLED=1 CC=x86_64-linux-musl-gcc GOOS=linux GOARCH=amd64 go build -ldflags "-linkmode external -extldflags -static -s -w"   -o cloudreve_linux-64 && upx -9 cloudreve_linux-64 || echo "linux编译失败"

