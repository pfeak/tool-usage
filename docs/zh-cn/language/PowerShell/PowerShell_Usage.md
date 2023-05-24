# PowerShell 常用操作

## 1. 系统操作

**获取所有盘符/C盘**

获取所有盘符 `[Environment]::GetLogicalDrives()`

获取 C 盘 `[Environment]::GetLogicalDrives()[0]`

**获取系统 CPU 架构**

利用 `systeminfo` 命令获取：`systeminfo | Where-Object { $_ -Match "^*based" }`

```powershell
PS C:\> systeminfo | Where-Object { $_ -Match "^*based" }
系统类型:         x64-based PC
```

**执行命令**

将字符串当做命令执行 `& 'calc'`

```powershell
# file: executor.ps1
echo $args[0]
echo $args[1]
echo $args[2]

# file: exe.ps1
$install = '.\executor.ps1'
$my_args = "1", "2", "3"
& $install $my_args
```

**脚本执行权限**

powershell 脚本 `.ps1` 出于安全考虑默认不能执行，需要通过指令赋予脚本执行权限

```powershell
# 参考
# https://www.fujieace.com/computer-practical/windows-powershell-ps1.html
# https://www.fujieace.com/jingyan/powershell.html

# 获取脚本执行权限
Get-ExecutionPolicy -List

# 设置允许所有脚本执行
Set-ExecutionPolicy Unrestricted

# 设置默认权限，用来需要执行权限
Set-ExecutionPolicy Undefined

# 一次性脚本执行权限
powershell.exe -ExecutionPolicy unrestricted -File "/path/to/you_script.ps1"
```

## 2. 文件目录操作

**删除指定文件**

`Remove-Item 'C:\123.txt'`

**远程下载文件**

在 try 中执行函数方便处理报错

```powershell
try {
    (new-object System.Net.WebClient).DownloadFile('https://www.baidu.com/robots.txt', 'C:\Users\test\Desktop\robots.txt')
} catch {
	// do something handle the error
}
```

文件下载可能遇到 `SSL` 和 `TLS` 报错，重写检测回调函数即可

```powershell
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = { $true }
try {
    (new-object System.Net.WebClient).DownloadFile('https://www.baidu.com/robots.txt', 'C:\Users\test\Desktop\robots.txt')
} catch {
	// do something handle the error
}
```

**遍历目录、文件**

```
Get-ChildItem ./
```

**遍历文件夹（倒序）获取最前文件夹**

```powershell
$dirs = @()
Get-ChildItem ./ | %{ if ($_ -is [System.IO.DirectoryInfo]) { $dirs += $_.FullName } }
if ($dirs.Count -eq 1) {
	$latest = ($dirs | Sort-Object -Descending)
} elseif ($dirs.Count -gt 1) {
	$latest = ($dirs | Sort-Object -Descending)[0]
} else {
	Write-Output "[!] Unzip agent failed and not found agent!"
}
```

**文件内容替换**

```powershell
$config = "config.json"
(Get-Content $config) | %{$_ -replace 'this is need to replace', 'new content'} | Set-Content $config
```

## 3. 输入输出

**文本输出**

常用输出函数 `Write-Host`、`Write-Output`，其中 `Write-Host` 可以输出颜色

```powershell
Write-Host "hello" -ForegroundColor Green -BackgroundColor Black
Write-Output "world"
```

**字符串文本格式化**

```powershell
Write-Output ('{0}:{1}' -f "姓名", "张三")
```

**读取文件**

```powershell
Get-Content './test.txt'
```

**写入文件**

```powershell
'hello world' | Set-Content './test.txt'
```

**文件文本替换**

```powershell
try {
    (Get-Content './test.txt') | %{$_ -replace 'will_be_replace', 'hello world'} | Set-Content './test.txt'
} catch {
    Write-Output "[!] Update file failed!"
}
```

## 4. 服务

管理员模式启动 `Powershell` 否则没有权限操作服务

**注册服务**

```powershell
# Delete and stop the service if it already exists.
if (Get-Service myService -ErrorAction SilentlyContinue) {
  $service = Get-WmiObject -Class Win32_Service -Filter "name='myService'"
  $service.StopService()
  Start-Sleep -s 1
  $service.delete()
}

$workdir = Split-Path $MyInvocation.MyCommand.Path

# Create the new service.
New-Service -name myService `
  -displayName myService `
  -binaryPathName "`"$workdir\myService.exe`" -c config.yml"

# Attempt to set the service to delayed start using sc config.
Try {
  Start-Process -FilePath sc.exe -ArgumentList 'config myService start= delayed-auto'
}
Catch { Write-Host -f red "An error occured setting the service to delayed start." }
```

**删除服务**

```powershell
# Delete and stop the service if it already exists.
if (Get-Service myService -ErrorAction SilentlyContinue) {
  $service = Get-WmiObject -Class Win32_Service -Filter "name='myService'"
  $service.StopService()
  Start-Sleep -s 1
  $service.delete()
}
```

**启动服务**

```powershell
try {
	Start-Service -Name myService
} catch {
	Write-Output "[!] Run myService Failed!"
}
```


