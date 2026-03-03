Sometimes, external libs can be hurdles to javafx:jlink because everything must be in the module.
Instead, use jpackage + FAT JAR, it works for regular jar files (non-modular)

You can configure the jpackage plugin like this:
```xml
<configuration>
    <name>YourApp</name>
    <type>EXE</type> <!--EXE/MSI-->
    <mainJar>yourappname-1.0-SNAPSHOT.jar</mainJar>
    <mainClass>com.example.yourappname.Launcher</mainClass>

    <input>target/</input>

    <winShortcut>true</winShortcut>
    <winMenu>true</winMenu>
</configuration>
```

## congrats! you know how to export your javafx project!
