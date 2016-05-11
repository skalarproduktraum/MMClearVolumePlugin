# MMClearVolumePlugin
[Micro-Manager](http://micro-manager.org) 2.0 plugin that opens datasets in the ClearVolume 3D viewer.  

[ClearVolume](http://fiji.sc/ClearVolume) is a volume rendering library tailored to microscopy developed at the MPI-CBG in Dresden.  The MMClearVolume plugin lets you open a ClearVolume viewer on a dataset in Micro-Manager.  It only works in Micro-Manager 2.0, not in Micro-Manager 1.4

![](http://valelab.ucsf.edu/~nstuurman/CV-MM-Desktop.png)


## Usage
Open a dataset in Micro-Manager.  Select `ClearVolume` from the plugins menu.  After a while, the 3D view will appear. Change brightness and contrast using the usual Micro-Manager controls (changing the gamma by changing the histogram line from straight to curved is especially useful).  Note the ClearVolume entry in the Inspector Window.  When you reduce the volume view by changing the x, y, or z slider, you can grab the active area in the slider and move it around (which will cause the visible volume area to change).  

## Usage in Live Mode

If using ClearVolume during a live, multi-D acquisition, please make sure that at least one full time point has been acquired. After this is the case, set the Z position in the viewer window to the maximum Z value, and only then open the ClearVolume plugin. After this you can use ClearVolume for all following time points.

## For Developers

MMClearVolumePlugin is set-up as a Maven project.  To build it, run `mvn install`. Copy the file  `target/MMClearVolumePlugin_-0.1-SNAPSHOT.jar`  to `Micro-Manager2.0/plugins`.  After this, you need to collect all the dependencies needed by ClearVolume by running `mvn dependency:copy-dependencies` which copies all dependent JARs into `target/cv_dependencies`. These files can then be copied in `jars/` dir of MM2.  Look for any duplicate jars by checking the contents of `plugins/` and ```mmplugins/` folders, and replace with the newest.

Launch Micro-Manager by running this command in the Micro-Manager 2.0 directory on Linux or OSX: 
```
java -cp “jars/*:ij.jar” ij.ImageJ
``` 
and this command under Windows: 
```
java -cp jars/*;ij.jar ij.ImageJ
``` 
The difference is the separator for the classpath: Linux/OSX use `:`, Windows uses `;`.

Make sure that you launch Java 1.8 (ClearVolume does not work in Java 1.6, which is usually used by Micro-Manager). Under Windows this is accomplished by installing Java 8 and removing the `jre/` directory from the Micro-Manager 2.0 distribution.

Hopefully, installation and deployment will be much simpler in the near future!

TODOs:
* Easy deployment
* Video capture


