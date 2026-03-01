# JavaFX Packaging Tutorial

This guide explains how to take a JavaFX Maven project and turn it into a .msi file using `jlink` and `jpackage`.

## Prerequisites
* **JDK 21 or higher**
* **Maven** (via `mvn` or `.\mvnw`)
* **WiX Toolset v3.11** (Required by `jpackage` to build MSI files on Windows)

---

## Step 1: Clean and Prepare the Runtime
Before packaging, we need to create a custom Java Runtime Image (JRE). This ensures your app runs even if the user doesn't have Java installed.

Run this command in your terminal:
```powershell
.\mvnw clean javafx:jlink
```

## Step 2: Configure the JPackage Plugin
Add the following configuration to the <plugins> section of your pom.xml. This plugin automates the jpackage terminal command.
```xml
<plugin>
    <groupId>org.panteleyev</groupId>
    <artifactId>jpackage-maven-plugin</artifactId>
    <version>1.7.3</version> 
    <configuration>
        <name>AppName</name>
        <vendor>YourName</vendor>
        <appVersion>1.0.0</appVersion>

        <runtimeImage>target/app</runtimeImage>

        <module>com.example.demo/com.example.demo.HelloApplication</module>
        
        <destination>target/dist</destination> <!-- your app location -->
        <type>MSI</type> 
        
        <winDirChooser>true</winDirChooser> 
        <winShortcut>true</winShortcut> 
        <winMenu>true</winMenu> 
    </configuration>
</plugin>
```

## Step 3: Generate the Installer
Once your pom.xml is saved, trigger the packaging process with this command:
```powershell
.\mvnw jpackage:jpackage
```

## Step 4: Locate your App
After the process completes, you will find your installer here: target/dist
