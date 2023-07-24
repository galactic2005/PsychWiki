# Haxe Functions
### addHaxeLibrary(libName:String, ?libPackage:String = '')
Imports haxe libraries into the interpreter. Basically an `import` statement in Haxe which imports specific packages into Haxe like sprites, text, tweens, etc.

- `libName` - The library name to be referenced.
- `libPackage` - An optional parameter, The library package to use.

Examples:
- Imports the sound library: `addHaxeLibrary('FlxSound', 'flixel.system')`
- Imports shader filters: `addHaxeLibrary('ShaderFilter', 'openfl.filters')`
- Imports CoolUtil: `addHaxeLibrary('CoolUtil')`

<details><summary><b>Import Haxe (Reference):</b></summary>
<p>

```haxe
package; // they are directories that contain modules, i dunno how it works; but very important to use.

// import library_package.library_name | <-- That's the syntax

import flixel.system.FlxSound; // Imports the sound package
import openfl.filters.ShaderFilter; // Imports the shader filter package
import CoolUtil; // Imports CoolUtil haxe file, i think

// Also the semi colon ';' character is very important when declaring functions, packages, variables, etc.
```

</p>
</details>

### runHaxeCode(codeToRun:String, ?varsToBring:Any = null, ?funcToRun:String = null, ?funcArgs:Array\<Dynamic\> = null)
<ins>Runs your haxe code</ins> for your Hscripts and stuff.

- `codeToRun` - The haxe code to be run, use double brackets `[[]]` for the string.
- `varsToBring` - An optional parameter, The Haxe variable(s) to import for string interpolation; Must be a table dictionary.
- `funcToRun` - An optional parameter, The Haxe function name to be referenced.
- `funcArgs` - An optional parameter, The argument(s) to be passed to the Haxe function.

Example:
```lua
function onCreate()
     runHaxeCode([[
          debugPrint(text, color); // will print > 'hi'
     ]], {text = 'hi', color = 0xFF0000})
end
```

### runHaxeFunction(funcToRun:String, ?funcArgs:Array\<Dynamic\> = null)
<ins>Executes the Haxe function</ins> from the `runHaxeCode()` function.

- `funcToRun` - The Haxe function name to be referenced.
- `funcArgs` - An optional parameter, The argument(s) to be passed to the Haxe function.

Example:
```lua
function onCreate()
     runHaxeCode([[
          function isBool(bool:String) { return bool == 'true' ? true : false; }
     ]])
     
     local proof = runHaxeFunction('isBool', {'true'})
     debugPrint(type(proof)) -- will print > 'boolean'
end
```

***

# Haxe Global Variable Functions
### setVar(varName:String, value:Dynamic)
Works exactly the same as `setVar()` function in Lua.

- `varName` - The variable to be referenced.
- `value` - The specified type of value for the variable to use or to over-write.

Example:
```lua
function onCreate()
     runHaxeCode([[
          setVar('globalVar', 'Hello Haxe!');
          setVar('globalYes', [34, 123, 4.20]);
     ]])
     runHaxeCode([[
          debugPrint(getVar('globalVar'), 0xf88700);    // will print > 'Hello Haxe!'
          debugPrint(getVar('globalYes')[2], 0xf88700); // will print > 4.20
     ]])

     -- Calling a Global Haxe Variable into Lua
     debugPrint(getProperty('globalYes')[1]) -- will print > 34
     debugPrint(getProperty('globalYes')[2]) -- will print > 123
end
```

### getVar(varName:String)
Works exactly the same as `getVar()` function in Lua.

- `varName` - The variable to be referenced.

### removeVar(varName:String)
Removes the global variable permanently, if not used anymore.

- `varName` - The variable to be referenced.

***

# Haxe In-Script Functions
### debugPrint(text:String, ?color:FlxColor = null)
Works exactly the same as the `debugPrint()` function.

- `text` - The text to be outputed to the top-left of the screen.
- `color` - An optional parameter, The color for the text to be displayed.

### getLuaObject(tag:String)
Gets the specified tag object outside the `runHaxeCode()` function.

- `tag` - The object tag name to be referenced.

Example:
```lua
function onCreate()
     makeLuaSprite('graphicThingy', nil, 0, 0)
     makeGraphic('graphicThingy', 1000, 1000, 'ff00ff')
     addLuaSprite('graphicThingy', true)

     runHaxeCode([[
          var theLuaTag = game.getLuaObject('graphicThingy'); // gets the lua tag
          theLuaTag.cameras = [game.camHUD]; // Sets it into 'camHUD'
          theLuaTag.alpha   = 0.5;           // Sets the opacity to '0.5'
          theLuaTag.angle   = 180;           // Sets the angle to '180'
     ]])
end
```