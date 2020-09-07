## 一、简介
> 本程序可将supervisord.exe运行于windows server。

## 二、编译
```shell
$ CGO_ENABLED=1 GOOS=windows GOARCH=amd64 go build -o supervisordBackground.exe
```

## 三、部署
> 在windows server中，将`supervisordBackground.exe`和`supervisordBackground.json`置于同一目录。

(1) 安装服务
```powershell
> .\supervisordBackground.exe install
```

(2) 卸载服务
```powershell
> .\supervisordBackground.exe uninstall
```

(3) 启动supervisord
```powershell
> net start supervisord
```

(4) 关闭supervisord
```powershell
> net stop supervisord
```

## 四、配置说明
supervisordBackground.json
```json
{
  "Name": "supervisord",
  "DisplayName": "supervisord for telegraf",
  "Description": "Run the telegraf",
  "Exec": "C:\\test\\supervisord.exe",
  "Args": ["-c","C:\\test\\supervisor.conf"],
  "Stderr": "C:\\test\\supervisordBackground_err.log",
  "Stdout": "C:\\test\\supervisordBackground_out.log"
}
```
说明：
- Exec：supervisord.exe程序绝对路径
- Args：填写supervisord.exe程序的配置文件绝对路径
- Stderr：错误输出日志路径
- Stdout：正确输出日志路径
