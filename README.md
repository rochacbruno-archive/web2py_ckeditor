web2py_ckeditor (2014 fork, v1.0)
===============
v 1.0 Updated to ckeditor 4.4.6
      Merged cleanup and upload improvements from dmvieira


v 0.4 Updated to ckeditor 4.4.3 July 15 2014

v 0.3 The full version of the plugin is the default. The std version is included as well. 
Updated to ckeditor v4.3.4. March 25, 2014

This is a fork of Bruno Rocha's plugin.
It's updated to v4 ckeditor, and works better with recent web2py versions. Tested against web2py v2.9.x
The inline edit has been removed to simplify the code (and it seems that the javascript is no longer maintained upstream).


This web2py plugin is based on the original https://bitbucket.org/PhreeStyle/web2py_ckeditor/wiki/Home)

To upgrade to a newer version of ckeditor, replace the directory static/plugin\_ckeditor with the directory downloaded from the ckeditor site. The repository comes with a full version. To use that, rename the 'full' plugin to static/plugin_ckeditor


## CKEditor Plugin for web2py 

### Introduction 

Sometimes you just need a WYSIWYG editor. This plugin integrates CKEditor into web2py. It acts much like the Auth object in its usage. For example, in your model, you need to import and initialize it:

    from plugin_ckeditor import CKEditor
    ckeditor = CKEditor(db)
    ckeditor.define_tables()


### Basic Usage

It's most basic usage is to assign it to a Field widget:


      db.define_table('content',
            Field('title', length=255),
            Field('public', 'boolean', default=True),
            Field('text', 'text', widget=ckeditor.widget)
        )


The CKEditor now automatically becomes available every time SQLFORM is used.

It includes integrated upload and browse functionality for images. The plugin defines a table to store images.
This works using ckeditor's custom browser integration, which means web2py controls the display of contents when the user cliick browse.
Look at the file views/plugin_ckeditor/browse.html to alter the appearance of the uploaded file browser.

#### Image Properties

![Screenshot](https://lh4.googleusercontent.com/-XtkEW2sXXyU/Thcm-IwkZ8I/AAAAAAAAADU/uyPo2FTMob0/Screen%252520shot%2525202011-07-08%252520at%25252011.33.28%252520AM.png)

#### Image Info

![Screenshot](https://lh3.googleusercontent.com/-mBjk0bs_-Z8/ThcnEixpCDI/AAAAAAAAADc/_xH6sWwgs6o/Screen%252520shot%2525202011-07-08%252520at%25252011.35.29%252520AM.png)

#### Browse Images

![Screenshot](https://lh5.googleusercontent.com/-M4ddg9Dz9Kg/ThcnH0dubEI/AAAAAAAAADk/9WzdPj1ZiVE/Screen%2Bshot%2B2011-07-08%2Bat%2B11.35.06%2BAM.png)

#### Image Upload Result

![Screenshot](https://lh4.googleusercontent.com/-8DKGzp3qqbs/ThcnV3GNCOI/AAAAAAAAADs/A6_-CGOM8-g/Screen%252520shot%2525202011-07-08%252520at%25252011.35.42%252520AM.png)

The upload and browse functionality is all taken care of by the plugin and does not require you to do anything on your end once you have initialized the plugin in your model as demonstrated above.

##### References

Bruno used the following resources in developing this plugin, so a special thanks to the authors of these for providing the ground work required to make this possible:

http://www.web2pyslices.com/main/slices/take_slice/18

http://www.bitsntuts.com/jquery/ckeditor-edit-in-place-jquery-plugin


#### Tips

(From Leonel Câmara) When using it in a loaded component, there may be some routing issues. 
To solve: ...use the following code in your model before ckeditor.define_tables()

    # To avoid routing problems in case we're not the default app and in case we're in a LOAD and the extension for URLs isn't HTML
    ckeditor.settings.url_upload = URL(request.app, 'plugin_ckeditor', 'upload', extension='html')
    ckeditor.settings.url_browse = URL(request.app, 'plugin_ckeditor', 'browse', extension='html')


Q: "I was wondering how to preserve the formatting that's done for a field Using CKEditor when the field is serialized in a view."

Leonel Câmara: 	"You use the XML helper. For instance, let's suppose I have a table 'page' with a field 'body' which I have set with ckeditor. In the view I can do:
{{=XML(page.body, sanitize=False)}}

If you can trust the input "sanitize=False" is a good idea (for instance if it can only be changed in the backoffice by members of the administration), otherwise remove the sanitize=False."



