---
layout: home
title: Create a Plug-in for Eclipse Tutorial
permalink: /wiki/eclipse-plugin
tag: programming
---

## Create a Plug-in for Eclipse Tutorial

The Eclipse IDE is highly extendable and can be customized through the creation of plug-ins.  With all of its features, one thing it doesn't have is a simple and quick way to change the font size in the editor without going through a complex preferences screen.  This functionality is particularly useful when reviewing your code with others during a code review.  Follow these tutorial steps, and you will be able to build such a plug-in allowing you to share your code with people sitting anywhere in the room.

### Tutorial Steps
The following steps can be followed in order to build this feature into a plug-in that you can use in your projects.

  * Create a new plug-in project
  * Run the new plugin project 
  * Update the icon to a new 16 x 16 pixel image
  * Update the plug-in tooltip and name
  * Add a variable in the Action class
  * Edit the plugin.xml to add the preference dependencies (org.eclipse.core.runtime)
  * Integrate font change size methods (for org.eclipse.jface.textfont & org.eclipse.jdt.ui.editors.textfont)
  * Export the completed plug-in as a jar

### Additional Features to Add
  * Change the icon when pressed to reflect the font size state
  * Change the wrapping from 120 to 80 characters per line

<code>
public void run(IAction action) {
    IPreferencesService srv = Platform.getPreferencesService();
    String value = srv.getString("org.eclipse.ui.workbench","org.eclipse.jdt.ui.editors.textfont", null, null);
		
    Preferences preference = srv.getRootNode().node("/instance/org.eclipse.ui.workbench");
    preference.put("org.eclipse.jdt.ui.editors.textfont",getFontDataOfSize(value,size).toString());
		
    try {
	preference.flush();
    }catch(BackingStoreException e){ /* Do nothing */ }
}
        
private int getFontSize(String info,int fontSize) {
    return PreferenceConverter.basicGetFontData(info)[0].getHeight();
}
	
private FontData getFontDataOfSize(String info, int size){
    FontData fd = PreferenceConverter.basicGetFontData(info)[0];
    fd.setHeight(size);
    return fd;
}
</code>

### Troubleshooting
When running a new instance of Eclipse to test your plug-in from Eclipse, you may receive an MaxPermGen exception.  This can be fixed by adding the following arguments to your run configuration. 

<code>
    vm args: -XX:MaxPermSize=512M
    program args: --launcher.XXMaxPermSize=512m
</code>