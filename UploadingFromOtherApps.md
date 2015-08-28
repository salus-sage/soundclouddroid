# Introduction #

If SoundCloud Droid is installed, any app can easily upload files to the user's SoundCloud account by issuing an appropriate [Intent](http://developer.android.com/reference/android/content/Intent.html), which will then allow the user to complete the upload process with SoundCloud Droid.  Moreover, since SoundCloud Droid responds to the standard [ACTION\_SEND](http://developer.android.com/reference/android/content/Intent.html#ACTION_SEND) Intent, many apps already do this.

If your app doesn't, here's what you can do:

# Uploading a Track using an Intent #

The following example will attempt to send a specific file using an [Intent](http://developer.android.com/reference/android/content/Intent.html). It will present the user with an activity chooser, where the user can choose the app used to send the file.  If SoundCloud Droid is installed, it will be one of the choices.

```

// this code assumes being in an Activity

Intent sendFile = new Intent(Intent.ACTION_SEND);

sendFile.putExtra(Intent.EXTRA_STREAM, Uri.parse ("file://somePathTo/file.3gp"));
sendFile.setType("audio/3gpp"); // the MIME type has to be an audio type for SoundCloud Droid to pick up the intent

Intent intentChooser = Intent.createChooser(sendFile, "Send the file using:");
      	
try
{
   startActivity(intentChooser);
}
catch (ActivityNotFoundException e)
{
    Toast.makeText(this, "No apps can send the file.").show();
}

```

# What if SoundCloud Droid is not Installed? #

If SoundCloud Droid is not installed, the user can be taken to the Market app to download it.  The following code sample will check to see whether SoundCloud Droid is installed, and if not, take the user to its Market page:

```

// this code assumes being in an Activity

try
{
    // if the package doesn't exist, this will throw an exception
    getPackageManager().getPackageInfo("org.urbanstew.soundclouddroid", 0);
}
catch (PackageManager.NameNotFoundException e)
{
    // SoundCloud Droid is not installed
    try
    {
        // take the user to the SoundCloud Droid page in the Market
        startActivity (
            new Intent (
                Intent.ACTION_VIEW,
                Uri.parse("market://search?q=pname:org.urbanstew.soundclouddroid")
	    ).addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
        );
    } catch (ActivityNotFoundException e)
    {
        // Market is not installed either
    }
}

```