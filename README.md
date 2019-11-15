![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 更改所有数据库的恢复模型
#### Change Recovery Model For All Databases
**TIME STAMP**

![#](images/change-recovery-models-for-all-databases.png?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这里有一些逻辑用来更改所有数据库（不包括系统数据库）的恢复模型。这个问题很常见，并且有很多方法可以实现自动化，所以我想把它介绍给那些可能会感兴趣的人。

## English
Here’s some quick logic to change the recovery models of all databases (excluding system databases). This question comes up quite a bit and there are a number of ways to automate so thought I would throw it out there for anyone that might be interesting in doing it.

---
## Logic
```SQL

use master;
 
set nocount on
 
select 
	name
,	recovery_model_desc 
from 
	sys.databases 
where 
	database_id > 4 
order by 
	name asc -- check recovery model for all databases.
 
declare @set_full_recovery_all_databases varchar(max)
set 	@set_full_recovery_all_databases = ''
select 	@set_full_recovery_all_databases = @set_full_recovery_all_databases +
'alter database [' + name + '] set recoverty full;' + char(10)
from 
	sys.databases 
where 
	database_id > 4 
	and state_desc = 'online'
 
exec (@set_full_recovery_all_databases) -- change all databases to full recovery.
 
select 
	name
,	recovery_model_desc 
from
	sys.databases 
where 
	database_id > 4 
order by 
	name asc -- check recovery model again to confirm.

```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

