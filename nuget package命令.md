# nuget package mannage 命令

## 管理包

``` 
	# 安装包到当前项目
	install-package 包含 -version 版本号	
	
	PM> NuGet\Install-Package ClickHouse.Client -Version 7.0.0
	
	# 安装包到指定项目
	Install-Package Dapper -ProjectName MyProject
	

	# 卸载包	
	uninstall-package 包含 -version
	
	PM> NuGet\unInstall-Package ClickHouse.Client
	
	# 卸载包并同时移除未用的依赖
	Uninstall-Package Dapper -RemoveDependencies
	

	# 更新包到最新版本	
	Update-Package Newtonsoft.Json
	
	# 更新指定项目的所有包	
	Update-Package -ProjectName <项目名>	
	
	# 强制重新安装某个包及其依赖（修复引用损坏时很有用）
	Update-Package Newtonsoft.Json -reinstall
	
	# 强制重新安装所有包
	Update-Package -reinstall	
	
```

## 查看包 

``` 
	
	# 查看当前项目已安装的所有包	
	Get-Package

	# 查看指定项目中引用的包列表	
	Get-Package -ProjectName 项目名称
	
	PM> Get-Package -ProjectName ClickHouseDAL
	
	# 搜索远程源上的包	
	Find-Package Newtonsoft.Json

	# 当前解决方案中引用的包版本	
	Get-Package | ? { $_.Id -match "包名" }

	PM> Get-Package | ? { $_.Id -match "System.Net.Http" }
	
```