# Popup Notification (Door Hanger) Based Confirmation Library for Firefox 31 or later

## Usage:

    Components.utils.import('resource://my-modules/confirmWithPopup.js');
    
    confirmWithPopup({
      browser : gBrowser.selectedBrowser,            // the related browser
      label   : 'Ara you ready?',                    // the message
      value   : 'treestyletab-undo-close-tree',      // the internal key (optional)
      anchor  : '....',                              // the ID of the anchor element (optional)
      image   : 'chrome://....png',                  // the icon (optional)
      buttons : ['Yes', 'Yes forever', 'No forever], // button labels
      // Native options for PopupNotifications.show() :
      //   persistence (integer)
      //   timeout (integer)
      //   persistWhileVisible (boolean)
      //   dismissed (boolean)
      //   eventCallback (function)
      //   neverShow (boolean)
      //   popupIconURL (string) : will be used instead of "image" option.
    });

## ES6 Promise style

    confirmWithPopup(...)
     .then(function(aButtonIndex) {
       // the callback receives the index of the clicked button.
       switch (aButtonIndex) {
         case 0: return YesAction();
         case 1: return YesForeverAction();
         case 2: return NoForeverAction();
       }
     })
     .catch(function(aError) {
       // dismissed or removed (not called if any button is chosen)
       ...
     });

## without Promise

    confirmWithPopup({ ...,
      // Yes, Yes Forever, or No Forever
      callback : function(aButtonIndex) { ... },
      // dismissed or removed (not called if any button is chosen)
      onerror  : function(aError) { ... }
    });

