# repository



# How you can temporarily unlock the development process...

...if you have at least once built a project before on one of the machines

### TL;TR;

You have these dependencies in your local gradle cache. You can share these files. The steps are as follows:

- Convert your local Gradle cache to a local Maven repository
- Upload this cache to any static server
- Specify this path in your project

### Convert your local Gradle cache to a local Maven repository

- Find your gradle cache folder. If you are on macos or linux, the gradle cache is located at `~/.gradle/caches/modules-2/files-2.1/`.
- Next you should download the Python script from [here](https://github.com/sinsongdev/gradle-cash-to-maven-repo/blob/master/gradle_cache_to_repo.py).
- Then change lines 15 and 16. Replace line 15 with your path to the gradle cache. Replace line 16 with the full path to any folder.
- If you on Linux/MacOS delete lines 22-23 of the script (which are intended for Windows)
- Run the script using Python 3

### Upload local maven repo to static server

You have now obtained a folder with the local maven repo. These are just folders and have jar/pom/zip files in them. You need to upload them to any static server and give access to it. You can create a Github Static server for free. Just create a repository in your profile and enable Github Pages. You can also not use github pages, but just pushing your files and use this link:

- Create a GitHub repository
- Push all your files into the repository
- Then form a link: `https://github.com/YOUR_ORGANIZATION/YOUR_PROJECT/raw/BRANCH/path/to/root/folder`. Replace `YOUR_ORGANIZATION` on your organization/personal name. Replace `YOUR_PROJECT` on your repository name. Replace `BRANCH` on your branch name (`master` or `main` by default). Replace `path/to/root/folder` to your folders in the repository. The important thing is that it should be up to the folders with the beginning of the package name (`com` for example)

### Specify this path in your project

Wherever the jitpack.io repository is listed, specify the **HIGHER** link you received above. For example:

```
allprojects {
    repositories {
        ...
        maven { url `https://github.com/YOUR_ORGANIZATION/YOUR_PROJECT/raw/BRANCH/path/to/root/folder' }
        maven { url 'https://www.jitpack.io' }
    }
}
```

Or for `.kts` script:

```
repositories {
    ...
    maven("https://github.com/YOUR_ORGANIZATION/YOUR_PROJECT/raw/BRANCH/path/to/root/folder")
    maven("https://jitpack.io")
}
```

### Summary

If you don't have these files anywhere, you can't get them. But if you have these files in your local cache, with these instructions you can bring your CI back to life or run your colleagues' builds






https://github.com/jitpack/jitpack.io/issues/5337#issuecomment-1363329648