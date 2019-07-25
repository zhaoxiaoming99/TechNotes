# Mavan常用操作

## 运行调试
```bash
pushd "C:\cncdr-1.0\dev\backend\app"
mvn clean -Djetty.port=8888 jetty:run
```

## 打包编译
```bash
pushd "C:\cncdr-1.0\dev\backend"
mvn clean install -Dmaven.test.skip=true
```
