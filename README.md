# OS Concept - A Plan for an Operating System i wish to make.
As a mac user i cannot get used to linux, The messy file systems and the way programs are installed for me is a big no. I've always wanted to make my own OS for things to work the way I want it.
One of the main goals I have in mind is to make a user friendly system for people who want it, while also being able to flip a switch and instantly allow for the advanced users to do whatever they want.

## Feedback is very much welcome! 
If you have anything you would like to see or don't particularly like, i urge you to submit an issue as I want everyones views on how they prefer their system.
## Help is also very much welcome!
I'm a horrible programmer, so if any mega brains wanna help me with bringing this system to life, please do :). I will forever be in your dept.
(I can't get a kernel with a libc going for the life of me, like how is that possible?)

## The File System.
The plan is for the File system to be clean and friendly to packages.
### The Root.
I might make some hidden symlink folders for /bin /usr /tmp and /etc for unix compatibility, but that might get messy in the long run.
- Applications      - For Applications, Obviously.
- System            - For System Files, Obviously.
- Users             - For Users Home folders. 
- Libraries         - For Development and Runtime Dependencies. These should be bundled with the application for user friendliness.
- Drives            - For Filesystem Mounts, the name of the mount folder being the Volume label.
- Config            - For Default Settings, these can be overritten (if allowed) by another Config folder in the users Home folder.
- Other             - For Everything else, basically the etc folder.

### Home Folder
The idea is to be as friendly as possible. hopefully a setting for the user to setup their own directory structure instead of pre-creating folders such as documents, pictures, videos, etc. Here is a decent default excluding those folders.
- Other             - For Everything that the user doesn't make, This is where previously said Config folder will be.
- Desktop           - Hopefully a Desktop, in the unlikely event that i can port or make a desktop enviroment. 
##### Optional Folders
- Documents         - A place to keep all your documents in.
- Videos            - So you can keep all your memories and shrek movie edits in one place.
- Pictures          - For all those lovely photos, drawings and shitposts.
- Audio             - To keep your music and clips of your friends saying regrettable stuff in a call all sorted.

## Bundles and Bundle Types
A Bundle is a folder with an extension to disguise itself as a file, Bundles will be used to neatly package things like Applications, Libraries and other Compiled Binary Types in an architechture friendly way.
### Basic Bundle Root
Doesn't derive from another bundle.
- Dependencies      - Dependencies that this bundle might use. I'll go into more detail later about how dependencies work to save disk space.
- Binary            - For any binary files, with subdirectories for architechture.
- Assets            - Any assets that the binary files use, things like images, etc.
- info.json         - Basically the information about this bundle, like the type of bundle, bundle name, main executable + icon (if an application bundle) and dependencies.

### Application Bundle Root
Derives from the basic bundle.
- icon.png          - An icon for the application.
- codesignature     - Some kind of file for potentionally signing code.

### System Extension Bundle Root
Doesn't derive from another bundle.
- Dependencies      - Dependencies that this bundle might use. I'll go into more detail later about how dependencies work to save disk space.
- Overrides         - Contains subfolders for architechture, Files in the current architechtures subfolder will add new files or override existing files in the user's Home, or with enough privledges, in the root.
- info.json         - Basically the information about this bundle, like the type of bundle, bundle name, main executable (if an application bundle) and dependencies.

## Dependencies 
A way for an application or a bundle to call a library shared by other applications and bundles.
### Bundled Dependencies
If an Application or Bundle comes pre packaged with a Dependency the system does not have, the system will move the Dependency over to the libraries folder.
If an Application or Bundle comes pre packaged with a Dependency the system already has, the system will delete the one packaged with the app and use the already installed Dependency.

### External Dependencies
If an Application or Bundle specifies a Dependency in the info.json that isn't packaged with it, the system will check to see if a Download URL is specified in the info.json for that Dependency.

### Cleaning Dependencies.
Once a week, a script will be run to check every Application and used Bundles to find Dependencies that are no longer needed by any of those Applications or Dependencies.

# This is all the plans for now, future ideas are to be added.
