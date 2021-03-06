# Using git with Unity

> https://thoughtbot.com/blog/how-to-git-with-unity

> The following is a copy paste from the link above, just in case it becomes available in the future for some reason.

### Add Unity-specific .gitignore Settings

```
# This .gitignore file should be placed at the root of your Unity project directory
#
# Get latest from https://github.com/github/gitignore/blob/master/Unity.gitignore
#
/[Ll]ibrary/
/[Tt]emp/
/[Oo]bj/
/[Bb]uild/
/[Bb]uilds/
/[Ll]ogs/
/[Uu]ser[Ss]ettings/

# MemoryCaptures can get excessive in size.
# They also could contain extremely sensitive data
/[Mm]emoryCaptures/

# Asset meta data should only be ignored when the corresponding asset is also ignored
!/[Aa]ssets/**/*.meta

# Uncomment this line if you wish to ignore the asset store tools plugin
# /[Aa]ssets/AssetStoreTools*

# Autogenerated Jetbrains Rider plugin
/[Aa]ssets/Plugins/Editor/JetBrains*

# Visual Studio cache directory
.vs/

# Gradle cache directory
.gradle/

# Autogenerated VS/MD/Consulo solution and project files
ExportedObj/
.consulo/
*.csproj
*.unityproj
*.sln
*.suo
*.tmp
*.user
*.userprefs
*.pidb
*.booproj
*.svd
*.pdb
*.mdb
*.opendb
*.VC.db

# Unity3D generated meta files
*.pidb.meta
*.pdb.meta
*.mdb.meta

# Unity3D generated file on crash reports
sysinfo.txt

# Builds
*.apk
*.aab
*.unitypackage

# Crashlytics generated file
crashlytics-build.properties

# Packed Addressables
/[Aa]ssets/[Aa]ddressable[Aa]ssets[Dd]ata/*/*.bin*

# Temporary auto-generated Android Assets
/[Aa]ssets/[Ss]treamingAssets/aa.meta
/[Aa]ssets/[Ss]treamingAssets/aa/*
```

In addition, depending on the platforms you intend to use for development, you should gitignore common files for macOS and/or Windows.

#### macOS .gitignore

```
# General
.DS_Store
.AppleDouble
.LSOverride

# Icon must end with two \r
Icon

# Thumbnails
._*

# Files that might appear in the root of a volume
.DocumentRevisions-V100
.fseventsd
.Spotlight-V100
.TemporaryItems
.Trashes
.VolumeIcon.icns
.com.apple.timemachine.donotpresent

# Directories potentially created on remote AFP share
.AppleDB
.AppleDesktop
Network Trash Folder
Temporary Items
.apdisk
```

#### Windows .gitignore

```
# Windows thumbnail cache files
Thumbs.db
Thumbs.db:encryptable
ehthumbs.db
ehthumbs_vista.db

# Dump file
*.stackdump

# Folder config file
[Dd]esktop.ini

# Recycle Bin used on file shares
$RECYCLE.BIN/

# Windows Installer files
*.cab
*.msi
*.msix
*.msm
*.msp

# Windows shortcuts
*.lnk
```

### Configure Unity For Version Control

With your project open in the Unity editor:

1. Open the editor settings window.
    - Edit > Project Settings > Editor
1. Make .meta files visible to avoid broken object references.
    - Version Control / Mode: ???Visible Meta Files???
1. Use plain text serialization to avoid unresolvable merge conflicts.
    - Asset Serialization / Mode: ???Force Text???
1. Save your changes.
    - File > Save Project

This will affect the following lines in your editor settings file:

-   `ProjectSettings/EditorSettings.asset`
    -   `m_ExternalVersionControlSupport: Visible Meta Files`
    -   `m_SerializationMode: 2`

If you???re curious, you can read more about Unity???s YAML scene format here: https://docs.unity3d.com/Manual/FormatDescription.html.

### Use Git Large File Storage

Git Large File Storage (LFS) uses Git attributes to track large files with Git, while keeping them out of your actual repository. Note that this will only work if you use GitHub or a server that supports the Git LFS API.

To set it up, download and install the Git LFS command line extension as documented on the Git LFS site: https://git-lfs.github.com/.

You can manually track the file types that you???d like Git LFS to manage, as described in the Git LFS docs. However, given the numerous file types that Unity supports, you are likely to miss a few.

Instead, feel free to use this sample `.gitattributes` file, which comprehensively accounts for all the file types that Unity currently supports (either natively or via conversion):

```
# 3D models

_.3dm filter=lfs diff=lfs merge=lfs -text
_.3ds filter=lfs diff=lfs merge=lfs -text
_.blend filter=lfs diff=lfs merge=lfs -text
_.c4d filter=lfs diff=lfs merge=lfs -text
_.collada filter=lfs diff=lfs merge=lfs -text
_.dae filter=lfs diff=lfs merge=lfs -text
_.dxf filter=lfs diff=lfs merge=lfs -text
_.fbx filter=lfs diff=lfs merge=lfs -text
_.jas filter=lfs diff=lfs merge=lfs -text
_.lws filter=lfs diff=lfs merge=lfs -text
_.lxo filter=lfs diff=lfs merge=lfs -text
_.ma filter=lfs diff=lfs merge=lfs -text
_.max filter=lfs diff=lfs merge=lfs -text
_.mb filter=lfs diff=lfs merge=lfs -text
_.obj filter=lfs diff=lfs merge=lfs -text
_.ply filter=lfs diff=lfs merge=lfs -text
_.skp filter=lfs diff=lfs merge=lfs -text
_.stl filter=lfs diff=lfs merge=lfs -text
\*.ztl filter=lfs diff=lfs merge=lfs -text

# Audio

_.aif filter=lfs diff=lfs merge=lfs -text
_.aiff filter=lfs diff=lfs merge=lfs -text
_.it filter=lfs diff=lfs merge=lfs -text
_.mod filter=lfs diff=lfs merge=lfs -text
_.mp3 filter=lfs diff=lfs merge=lfs -text
_.ogg filter=lfs diff=lfs merge=lfs -text
_.s3m filter=lfs diff=lfs merge=lfs -text
_.wav filter=lfs diff=lfs merge=lfs -text
\*.xm filter=lfs diff=lfs merge=lfs -text

# Fonts

_.otf filter=lfs diff=lfs merge=lfs -text
_.ttf filter=lfs diff=lfs merge=lfs -text

# Images

_.bmp filter=lfs diff=lfs merge=lfs -text
_.exr filter=lfs diff=lfs merge=lfs -text
_.gif filter=lfs diff=lfs merge=lfs -text
_.hdr filter=lfs diff=lfs merge=lfs -text
_.iff filter=lfs diff=lfs merge=lfs -text
_.jpeg filter=lfs diff=lfs merge=lfs -text
_.jpg filter=lfs diff=lfs merge=lfs -text
_.pict filter=lfs diff=lfs merge=lfs -text
_.png filter=lfs diff=lfs merge=lfs -text
_.psd filter=lfs diff=lfs merge=lfs -text
_.tga filter=lfs diff=lfs merge=lfs -text
_.tif filter=lfs diff=lfs merge=lfs -text
\*.tiff filter=lfs diff=lfs merge=lfs -text
```

### A Bonus For GitHub Users: Automatically Collapse Generated File Diffs

If you use GitHub to review diffs (ex., as part of a pull request workflow), you???ll notice that changes in Unity-generated YAML files are usually not actionable. You can reduce the clutter they introduce, while preserving the ability to review them as needed, by automatically collapsing the diffs on GitHub.

To do so, just append this to your `.gitattributes` file:

```
# Collapse Unity-generated files on GitHub

_.asset linguist-generated
_.mat linguist-generated
_.meta linguist-generated
_.prefab linguist-generated
\*.unity linguist-generated
```

You can read more about this feature here https://thoughtbot.com/blog/github-diff-supression.
