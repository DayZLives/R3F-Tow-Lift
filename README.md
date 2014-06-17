R3F-Tow-Lift
============

This is a modified and preconfigured version of R3F's tow and lift script

1. Click ***[Download Zip](https://github.com/noxsicarius/R3F-Tow-Lift/archive/master.zip)*** on the right sidebar of this Github page.

	> Recommended PBO tool for all "pack", "repack", or "unpack" steps: ***[PBO Manager](http://www.armaholic.com/page.php?id=16369)***

1. Log into your server via FTP or your host's File Manager. Locate, download, and unpack (using PBO Manager or a similar PBO editor) your ***MPMissions/Your_Mission.pbo***, and open the resulting folder.
 
	> Note: "Your_Mission.pbo" is a placeholder name. Your mission might be called "DayZ_Epoch_11.Chernarus", "DayZ_Epoch_13.Tavi", or "dayz_mission" depending on hosting and chosen map.

1. Extract the downloaded folder and copy the ***R3F_ARTY_AND_LOG*** and ***custom*** from the folder into the root of your mission folder.
1. Open the ***init.sqf*** in the root of your mission folder and paste the following at the bottom:

	~~~~java
  //Tow and lift
  [] execVM “R3F_ARTY_AND_LOG\init.sqf”;
	~~~~

1. Find the following line:

  ~~~~java
  call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\compiles.sqf";
  ~~~~
  
  and replace it with:
  
  ~~~~java
  call compile preprocessFileLineNumbers "custom\compiles.sqf";
  ~~~~
  
1. You are now finished with the mission file portion. If necessary package and send it to your server.
1. Now unpack your ***dayz_server.pbo*** and open it.
1. Navigate to ***compile\server_publishVehilce2.sqf***, find this code:

  ~~~~java
  if(!_donotusekey) then {
    // Lock vehicle
    _object setvehiclelock "locked";
  };
  ~~~~
  
  and change it to this:
  
  ~~~~java
  if(!_donotusekey) then {
    // Lock vehicle
    _object setvehiclelock "locked";
    _object setVariable ["R3F_LOG_disabled",true,true];
  };
  ~~~~
  
  Save and close the file.
  
1. Navigate to ***system\server_monitor.sqf***, find this code:

  ~~~~java
    if(_ownerID != "0" and !(_object isKindOf "Bicycle")) then {
    	_object setvehiclelock "locked";
    };
  ~~~~
  
  and change it to this:
  
  ~~~~java
    if(_ownerID != "0" and !(_object isKindOf "Bicycle")) then {
    	_object setvehiclelock "locked";
    	_object setVariable ["R3F_LOG_disabled",true,true];
    };
  ~~~~
  
1. Package the PBO and send it to the server. Everything is finished.
