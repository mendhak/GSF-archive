
## Prerequisites

Install Maven

    sudo apt-get install maven2


## Add to local Maven repo

Go to your new file and add it in:

    mvn install:install-file -Dfile=windows-live-sdk.aar -DgroupId=com.mendhak.gpsloggersupport -DartifactId=windows-live-sdk -Dversion=0.0.1 -Dpackaging=aar -DlocalRepositoryPath=/home/mendhak/Code/gpslogger-support-files

Make sure the folder was added under `com/mendhak/gpsloggersupport`

## Run Nexus indexer

    REPODIR=/home/mendhak/Code/gpslogger-support-files
    java -jar nexus-indexer-3.0.4-cli.jar -r $REPODIR -i $REPODIR/.index -d $REPODIR/.index -n localrepo

Look at the `.index` directory.  

## Prepare zip for upload

    zip -r repository0.0.1.zip .index com

Inspect the zip to make sure it just has `com` and `.index`

## Replace files on Bintray

Go to the [version page](https://bintray.com/mendhak/maven/gpslogger-support-files/0.0.1).

Upload repository0.0.1.zip and choose to 'Explode this archive'.  Publish.


## Use in Gradle project

Add to `build.gradle`:

    maven {
    url  "https://dl.bintray.com/mendhak/maven"
    }

You can then add packages like:

    compile 'com.mendhak.gpsloggersupport:mail:0.0.1'
    compile 'com.mendhak.gpsloggersupport:dropbox-android-sdk:1.6.3'
    compile 'com.mendhak.gpsloggersupport:windows-live-sdk:0.0.1'
