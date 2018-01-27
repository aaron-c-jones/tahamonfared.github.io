---
excerpt: "Power Shell detour to exporting data from PowerBI Desktop to MSSQL."
---

Taha Monfared
January 27, 2018

If you are a PowerBI user and you are pedantic about database architecture, you will finally have the following problems:

1. You'll have so many steps in your data manipulations that it takes ages to be ready for reporting
2. You'll have big datasets residing in your PowerBI memory, who will eventually slow down your analysis
3. You'll have multiple R steps in your data manipulation that take even longer to process
4. You want to have an explicit version of your data in an RDBMS that you simply DirectQuery into, and voila!
5. RDBMS will also give you the freedom to link tables to your liking (aka multiple attributes linkages which are not possible in PBI)
6. You want to have SQL statement reports and views which you find hard, building in DAX or M. 

Once you reach the consensus that you are looking at the data in the right normalized way (believe me when I tell you, so many places 
don't care and don't know about the importance of database architecture. They just want flat files...) you can export your data directly to 
your MS SQL database. This process is not a thing you do every day, so if you are updating your data off of a poorly built database multiple times in a day may god be with you. You have two options (not counting using flat versions):

1- Keep nagging till they accept your database structure will give them better performance and keeps things tidy and right.
2- Keep a part of the data that you don't regularly update in MSSQL and the rest of your operations could be done in the PowerBI, 
so don't just discard all your steps in PBI. I recommend using the PBI version of all your data transformations somewhere and adding a reporting dashboard in another file. 

Now that you are ready to move, you have three options. You can find two of them in here:

[Two good ideas](http://biinsight.com/exporting-power-bi-data-to-sql-server/){: .btn .btn--inverse}

and "This Genius Tool" in Windows PowerShell in here:

[The Genius](https://ruiromanoblog.wordpress.com/2016/04/21/use-power-bi-desktop-as-an-etl-tool/){: .btn .btn--inverse}

Although there are steps to using it, it's so much easier and more accessible than the previous methods. Hope you have all the administrative power on your PC though. 

1. Run PowerShell as an administrator. (start menu search for power shell and then right click, run as administrator)
2. Check whether you have permission to run scripts. 

```PowerShell
Get-ExecutionPolicy -List
```

in Power Shell.

If you have undefined for your CurrentUser and LocalMachine Restricted set it to something else. Here are the restrictions you can use:

[PowerShell script running permissions](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-5.1&viewFallbackFrom=powershell-Microsoft.PowerShell.Core){: .btn .btn--inverse}

This is how I have set it up:

```PowerShell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser
```

Then as @RuiRomano describes, you'll need to run these:

```PowerShell
Install-Module PowerBIETL
Import-Module PowerBIETL
```

Then you can use the module!

```PowerShell
Export-PBIDesktopToSQL -pbiDesktopWindowName "*sample*" -sqlConnStr "Data Source=.\SQL2014; Initial Catalog=DestinationDB; Integrated Security=SSPI" -sqlSchema "stg" -verbose
```

Now you need to know how to connect to the database that you are using, whether local or on the network. These are some useful instructions:

![Connection String Instructions](https://www.connectionstrings.com/sql-server/){: .btn .btn--inverse}

If you want to use the Windows login, you can use "Trusted_Connection=True."

So the rest would be "Server=...;Database=...", for the -pbiDesktopWindowName the stars are wildcards. So whichever open instance of 
PBI you have you can just name it like "\*Iris\*".

And there you are.. your migration complete and you can direct query to your database and use all the perks that come with it!

Enjoy! Thanks Mr.Romano

 