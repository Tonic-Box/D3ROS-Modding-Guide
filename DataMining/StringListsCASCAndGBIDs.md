# What are String Lists?
\*.stl files (StringList Files) are files cound in the `StringLists/` folder withing Diablos CASC Archives. These are binary files that contain the string names of different game objects, items, dialogue, etc. If you were to pop them open in a hex editor, or in notepad even, you would see in each of the files the string names.

# Whats CASC?
CASC Archives (Content Addressable Storage Container) are Blizzards proprietary storage containers for data and patch files.  
[CASCView](http://www.zezula.net/en/casc/main.html) - For downloading and extracting patch CASCs  
[Technical Information on CASCs](https://wowdev.wiki/CASC)

# What are GBIDs?
A GBID (Game Balance ID) is a 32bit hash of identifyer strings used by the game to resolve and identify items. The hash used is the DJB algorithm but with a base of 0.  
* **Credit:** [UnknownCheats Wiki](https://www.unknowncheats.me/wiki/Diablo:Diablo_3_Definitions)  

### Example Tools
[STLParser - Parses .STL files into both raw and hashed (gbid) lists](https://github.com/Tonic-Box/STLParser/releases/)  
[STLParser](https://github.com/CaiMiao/D3Parser) - Takes STL Files and Parses them into Raw strings  
[D3 Hash Tool V2](https://github.com/ooCONTAGIONoo/D3HashTool/releases) - Contagions GBID hashing tool  

### Example implementations

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
		$hash = fix(($hash << 5) + $hash + ord($input[$i]));
		//A little magic here to emulate 32bit type wrapping since php likes to auto type cast
		while($hash > 2147483647) $hash -= 4294967296;
		while($hash < -2147483648) $hash += 4294967296;
	}
	return $hash;
}
```

# Conclution
This is more than enough to get any one in the right direction in regards to pulling GBIDs and data mining the StringList files. For any other inqueries into the topic; Google, trial, and error are your friends. :)
