# hideCreateRecordOnPopup()

This function works very similarly to the displayRecordButtons() function.

It returns css inside the html() function, which is called from a formula field wherever we want to hide the ‘create record’ button inside the popup relationship select form.

The selector takes children of elements with the ‘popupeditor’ class, which have both the ‘nx-button-text’ classname, and also the ‘blue’ classname.

This function is setup to only hide the buttons if the user is not in admin mode, it is this way as otherwise it was removing the ability to submit on the 'filter columns' interface.
