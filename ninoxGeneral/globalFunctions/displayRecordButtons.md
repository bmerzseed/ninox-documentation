# displayRecordButtons(print: boolean, manip: boolean, nav: boolean)

This function takes 3 boolean arguments.

- 1 for whether or not the print icon should be shown on a record

- 1 for whether or not the create/ duplicate/ delete buttons should be shown on a record

- and for whether or not the first/ previous/ next/ last page navigation buttons should be shown.

The function works by declaring a variable called styleStr, this variable starts with just an opening html '''<style>''' tag.

Depending on the values of print/ manip/ nav, we either append styling which uses display: block to explicitly show the icons, or display: none to hide the icons.

The styling uses the class (.className) selector, we also use the .hud-menu-group selector in front of the icons classname throughout in order to only hide the icons which are a child of an element using the .hud-menu-group class.

finally, we append the '''</style>''' tag to close the stylesheet. And then return the styleStr inside the html() function.

This global function is called from a formula field called as ‘display record buttons’ inside almost all tables in the database, we use different print/ manip/ nav values as arguments depending on if isAdminMode() is true, if overrides are activated, and depending on the table itself. E.g. single record dashboard tables do not need navigation buttons.
