#CodeEnlightener
The CodeIgniter Framework "Enlightened" with the addition of the Smarty Template Engine

CodeIgniter is a decent lightweight engine. But it lacks one flaw that makes web design with the framework painful
and unflexible. Its current templating engine forces the user to clog thier controllers with extra logic for the view.
With the addition of the Smarty Template Engine this is now mostly avoided. Controller logic now contains more legible
code that shows better what is happening to the data before it is being sent to the view. It also allows for a more
flexible view with less ambiguous template terms used in the Smarty engine. The Smarty integration unleashes the full
power of Smarty with the ability to not only simply pass strings, but objects that can be iterated through thier
attribute content, as well as additional filtering objects for scenarios where data may or may not be available (eg.
error messages in the view)

Currently CodeEnlightener uses CodeIgniter v3.0-dev and Smarty v3.1.21 <br>
**CodeEnlightener has not updated to CodeIgniter v3.0rc3 due to a compatability bug with Smarty

#Setup
Setup of the project is the same as any other CodeIgniter project except for 1 extra step is needed for the Smarty
library. When publishing the project to your host, you need to ensure that the `templates_c` folder inside the 
`application/views` directory has read and write access. This is because Smarty caches previous pages to speed up
request times for pages that have not changed

####Configuration Locations
If you would like to apply some of your own custom configurations to the Smarty library. The smarty components are
located in the following directories:

* Smarty.php - main configuration file - `application/libraries/Smarty.php`
* Smarty core - `application/third_party/smarty`
* Smarty Default Template Directory - `application/views/templates`
* Smarty Default Template Cache Directory - `application/views/templates_c`

The project is preset up with the Smarty library autoloaded. in the `application/config/autoload.php` file

If you would like to swap out the current CodeIgniter engine with a different one, you can do so without effecting
any directory dependencies with Smarty as all dependencies are managed within the `application` folder. Changes to
the system folder other then possible core compatability issues will have no effect on Smarty

A tutorial to setup your own CodeIgniter with Smarty can be found here: <br>
[http://www.coolphptools.com/codeigniter-smarty](http://www.coolphptools.com/codeigniter-smarty)

#Usage
The project is still the CodeIgniter framework in the back, except with the Smarty engine for the front! Everything
except how data is passed from the controller to the view with smarty is the same! You can checkout the standard
codeigniter documents at [CodeIgniter.com](http://codeigniter.com) and the Smarty Template Engine docs at 
[Smarty.net](http://smarty.net). You can take a quick Smarty Crash Course at: 
["http://www.smarty.net/crash_course"]("http://www.smarty.net/crash_course")

####Introduction
Below is a general use introduction of how to interact with smarty in codeigniter. Please refer after to smarty docs
for more extensive details on all of the features in smarty

Within your controller you can access the smarty template engine within the `$this` reference. You can assign values
to be passed to your view as so: <br>
````php
$this->smarty->assign("<name_of_key>","<value>");

//example
$this->smarty->assign("title", "Welcome To CodeEnlightener");
````

Once you have finished assigning all values to be passed to the view. Call the template file to load. These template
files will replace your views in CodeIgniter as smarty will handle them and render them into appropriate html files
to be returned to the browser <br>
````php
$this->smarty->display("<name_of_template>.tpl");

//example
$this->smarty->display("welcome.tpl");
````

Additionaly, if you still have a preference for CodeIgniter's implementation of its parse method. There is an equivelent
function call available with the Smarty class.

Like the parse method, the first parameter takes the name of the template to apply the attributes to, the second
parameter is the data array which is an associative array of key and value pairs of the substitutions. If you
preferre to assign your key/value data the CodeIgniter way through the `$this->data` array you can do that aswell, and
then simply pass `$this->data` as the second parameter. Finally, pass TRUE or FALSE in the last parameter to return 
the view back instead of to the browser. <br>
````php
$this->smarty->view($template, $data=array(), TRUE/FALSE);

//example
$this->smarty->view("welcome.tpl", $this->data, FALSE);
````

