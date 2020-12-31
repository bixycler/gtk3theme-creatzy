This theme is adapted from the GTK3's default theme "Adwaita".
This folder contains both source and SASS built out files. The files actually used as a theme are:

1. assets/
2. gtk.css

which are placed in `${ThemeBase}/${ThemeName}/gtk-3.0/`. And ${ThemeBase} can be `~/.themes` or `/usr/share/themes`.

Adaptation procedure
--------------------

1. Download source from https://gitlab.gnome.org/GNOME/gtk/tree/gtk-3-24/gtk/theme/Adwaita
2. Edit a suitable SCSS source file (_common.scss, etc.), see "How to tweak the theme" below
3. Compile: `sassc -M gtk.scss gtk.css` (To install SASSC: `sudo apt install sassc`)

This procedure is copied from: https://askubuntu.com/questions/1170151/help-creating-a-new-theme-based-on-adwaita

How to tweak the theme
----------------------

Adwaita is a complex theme, so to keep it maintainable it's written and
processed in SASS. The generated CSS is then transformed into a gresource file
during gtk build and used at runtime in a non-legible or editable form.

It is very likely your change will happen in the _common.scss file. That's where
all the widget selectors are defined. Here's a rundown of the "supporting"
stylesheets, that are unlikely to be the right place for a drive by stylesheet
fix:

_colors.scss        - global color definitions. We keep the number of defined
                      colors to a necessary minimum, most colors are derived
                      from a handful of basics. It covers both the light variant
                      and the dark variant.

_colors-public.scss - SCSS colors exported through gtk to allow for 3rd party
                      apps color mixing.

_drawing.scss       - drawing helper mixings/functions to allow easier
                      definition of widget drawing under specific context. This
                      is why Adwaita isn't 15000 LOC.

_common.scss        - actual definitions of style for each widget. This is
                      where you are likely to add/remove your changes.
                      
You can read about SASS at http://sass-lang.com/documentation/. Once you make
your changes to the _common.scss file, GTK will rebuild the CSS files.
