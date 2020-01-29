![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Create Sequential Columns With Row_Number
**Post Date: February 1, 2018**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process


![SQL Row Number]( https://mikesdatawork.files.wordpress.com/2018/02/image001.png "Create Sequential Columns")
 
<p>Sometimes you find yourself needing to create massive columns for import tables, and here's a quick trick I use to create a variety of sequential rows in tables using the row_number() function. </p>      


## SQL-Logic
```SQL
use master;
set nocount on
 
declare @make_many_columns  table ([column_name] varchar(255))
insert into @make_many_columns
select
    case
        when row_number() over(order by [id] asc) < 100 then ',  [Column_00' + cast(row_number() over(order by [id] asc) as varchar(10)) + '] varchar(max)'
        else ', [Column_' + cast(row_number() over(order by [id] asc) as varchar(10)) + '] varchar(max)'
    end as 'Row'
from
    sysobjects
 
select top 200 * from @make_many_columns
 
create table [MyImport_01]
(
-- insert column names here
)
```
Hope you find it useful. 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

    
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

