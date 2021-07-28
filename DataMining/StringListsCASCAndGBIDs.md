# What are String Lists?
\*.stl files (StringList Files) are files found in the `StringLists/` folder withing Diablos CASC Archives. These are binary files that contain the string names of different game objects, items, dialogue, etc. If you were to pop them open in a hex editor, or in notepad even, you would see in each of the files the string names.

# Whats CASC?
CASC Archives (Content Addressable Storage Container) are Blizzards proprietary storage containers for data and patch files.  
[CASCView](http://www.zezula.net/en/casc/main.html) - For downloading and extracting patch CASCs  
[Technical Information on CASCs](https://wowdev.wiki/CASC)

# What are GBIDs?
A GBID (Game Balance ID) is a 32bit hash of identifyer strings used by the game to resolve and identify items. The hash used is the DJB algorithm but with a base of 0. ActorCommonData objects have a GBID field which can be used to resolve in-world items to GameBalance SNO structures, and determine attributes such as item type, quality, etc.  
* **Credit:** [UnknownCheats Wiki](https://www.unknowncheats.me/wiki/Diablo:Diablo_3_Definitions)   

### Example hash implementations

(C++):
```cpp
int gbid(std::string input)
{
	std::transform(input.begin(), input.end(), input.begin(), ::tolower);
	int hash = 0;
	for (int i = 0; i < input.length(); i++)
	{
		hash = (hash << 5) + hash + (int)input[i];
	}
	return hash;
}
```
(PHP):
```php
function gbid($input) {
	$hash = 0;
	$input = strtolower($input);
	for ($i = 0; $i < strlen($input); $i++) {
		$hash = ($hash << 5) + $hash + ord($input[$i]);
		//A little magic here to emulate 32bit type wrapping since php likes to auto type cast
		while($hash > 2147483647) $hash -= 4294967296;
		while($hash < -2147483648) $hash += 4294967296;
	}
	return $hash;
}
```
(Power Shell)
```ps
Function gbid([string]$str) {
  $hash = 0
  $str = $str.ToLower()
  $array = [char[]]$str
  for ($i=0; $i -lt $array.length; $i++) {
    $hash = ($hash -shl 5) + $hash + [byte][char]$array[$i]
	while($hash -gt 2147483647) {
        $hash -= 4294967296
    }
	while($hash -lt -2147483648) {
        $hash += 4294967296
    }
  }
  Write-Output $hash
}
```

### Example Tools
[STLParser](https://github.com/Tonic-Box/STLParser/releases/) - Parses .STL files into both raw and hashed (gbid) lists  
[D3Parser](https://github.com/CaiMiao/D3Parser) - Takes STL/GAM Files and Parses them into Raw strings  
[D3 Hash Tool V2](https://github.com/ooCONTAGIONoo/D3HashTool/releases) - Contagions GBID hashing tool 

# Conclution
This is more than enough to get any one in the right direction in regards to pulling GBIDs and data mining the StringList files. For any other inqueries into the topic; Google, trial, and error are your friends. :)
