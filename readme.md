# TextformatterFunkyFunctions

Textformatter which is inspired by the TextformatterHannaCode module.

Allows you to add tags (“Funky Functions”) to your text fields which will be replaced by markup. The markup will be generated from script files either from a configurable path below `site/` or from the `site/templates/fields/` folder. In contrast to TextformatterHannaCode it does not come with a backend code editor interface. All scripts must be available as files in the mentioned paths.

Other characteristic are:

- That it allows to directly pull data from fields on the same page
- It allows to select items from array-like data by given ranges and/or indexes: `images=1,3,6-9,12`
- It allows to select items from WireData derived data by given selector: `images="description*=nice"`
- It allows to pull data from another page field into a tag attribute: `[[nice-script field="selector"]]`
- It will render available scripts in `templates/fields/` automatically as fallback and provide the value as `$value`
- It will search for scripts in this order similar to `$page->render()`
    1. `$givenPath/$funkyName/$pageTemplateName.php`
    2. `$givenPath/$funkyName.$pageTemplateName.php`
    3. `$givenPath/$pageTemplateName/$funkyName.php`
    4. `$givenPath/$funkyName.php`
- It is hookable to override rendering with own engine stuff

It is not (yet?) in the modules directory. Thus, I don't provide any support, but you can report bugs and errors anyway. That would be nice :)

## Examples

```
[[nice-gallery images=1,2,3,6- type=special-kind]]
```
This will render the script `nice-gallery.php` with the variables `$images` and `$type`.  
Value of `$type` will be `"special-kind"`, value of `$images` will be items 1, 2, 3 and all the rest from item 6 up to the end of the images field of that name of the page.
A variable `$arguments` is also provided with all “arguments”/variables bundled.

```
[[hero-image pictures="description*=nice"]]
```
This will render the script `hero-image.php` from the detected scripts folder and pull the image its description contains "nice".

```
[[images="description*=nice"]]
```
This will render the script `images.php` from the detected scripts folder and pull all images which have the "nice" in their description from images field.


## Installation

[The Processwire way.](http://modules.processwire.com/install-uninstall/)

Then, add this Textformatter in the details tab of the desired Textfield.

## Changelog

#### 1.2.0 - 2017/11/13, fixes

added: Also matches field references inside unquoted attribute values.  
fix: Fetch correct values if attribute name and attriute values field reference are the same (Always fetch value field reference).  

#### 1.1.0 - 2017/11/3, added render function

added: A render function.

#### 1.0.1 - 2017/10/31, fixed bug in regex

fixed: Greedy bug in regex.

#### 1.0 - 2017/10/30, refactoring, added ability to filter by processwie selectors, pull data from

added: Ability to filter field values by processwire selectors  
added: Ability to pull data from page fields into attributes  
other: Refactoring

#### 0.x - 2017/10/23, Initial release