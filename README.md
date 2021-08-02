# perfnotes
# Fonts
1.  Find out if there are any fonts that are not really used, stop loading those. (check out [this snippet](https://stackoverflow.com/questions/56316330/how-to-detect-if-css-font-face-is-not-used-on-a-page) + [What Font](https://chrome.google.com/webstore/detail/whatfont/jabopobgcpjmedljpbcaablpmlmfcogm?hl=en) + [Font Scanner](https://chrome.google.com/webstore/detail/fontscanner-scan-for-font/aodilhmhlmomokijchbkajpoibenmakn?hl=en))

2.  Where the fonts are hosted? Self-host everything that is possible (Adobe Fonts won't let you to self host for instance)

3.  Which format do they have? Use WOFF2 for speed and EOT as a fallback --- this will cover all browsers.

4.  Define which fonts are a part of the critical path (needed for the first screen). We need to load those as early as possible and delay the load of others. You might want to include them as inline CSS in head, for Google Fonts to load them via link, not separate CSS file. [Preload](https://web.dev/codelab-preload-web-fonts/) those critical fonts, [preconnect](https://web.dev/uses-rel-preconnect/) hosts if they are hosted elsewhere. You might also consider putting other fonts in a separate CSS and delay that file loading.

5.  Use swap as a [font-display property](https://developers.google.com/web/updates/2016/02/font-display)* value  to load system font before the actual font is loaded so that text stays visible while the custom font is loaded. Then use font-matcher to find and [tune](https://meowni.ca/font-style-matcher/) the system font kerning, spacing etc to look similar to the custom one. You might want to use [font face observe](https://dev.to/garybyrne/font-loading-with-fontface-observer-getting-started-3lgo)r after.\
    * If you don't host them locally: for Google Fonts ensure &display=swap in the link, for Adobe Fonts this is to be configured in the account 

6.  If there are quite a few variations of the font used on the site, check out if there is a variable option of that font available --- [variable](https://web.dev/variable-fonts/) font might be a perfect way to reduce the time spent on fonts.

7.  Icon fonts optimization highly depends on the situation: you might want to use block as font-display value; or/and make a subset font to load only used icons (make recommendation, don't trim during the audit); or even inline them as svg.
