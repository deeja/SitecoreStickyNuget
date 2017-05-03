# SitecoreStickyNuget
"In Sitecore" NuGet installer 


The problem

We have multiple updates of js and css to support a component that is on our website. 
The component is lightweight, and is hardly worth having a seperate deployment for. 

Possible solutions

Have a nuget feed that can be accessed by the CMS
Save in the media library or similar, which is distributed out to the CD servers. 
When delivered to the CD servers, then it's manually installed via an install command from the CMS


# NUGET INSTALLER

0. Set Nuget feed
1. Acquire package / insert into media library (maybe the core database?)
2. Publish package (from master to web or target - if not using the core database) 
3. Install package to all servers
4. Reinstall package to all servers

# Issues 

- Display currently installed versions of packages on 

- Storage of the currently installed package (configuration xml / database item) - combination of the two?
<nugetpackages>
	<package name="Something" version="3.0.2" />	
</nugetpackages>


compare the package info in the db
if older version, then update to one in DB
if newer version, then update DB to be newer version
if same then do nothing. 

## Set nuget feed
Settings -> NugetPackage

## Verify files installed are the same as in the package (MD5?)
There may a case where they are overwritten on install
<nugetpackages>
		<package name="Something" version="3.0.2">
			<file verify="1092348321094813283">/somefile/is/here.txt</file>
		</package>
</nugetpackages>

If a package is installed on the server, and a deployment happens, then the package may be overwritten. 
This includes the config file that contains the currently installed package version. 

Might be better to use the core database for the installation of the nuget packages. 


CD servers will need some sort of connection to the CM server to allow monitoring of the package 
