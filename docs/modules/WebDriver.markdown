---
layout: doc
title: WebDriver Module - Codeception - Documentation
---

# WebDriver Module
**For additional reference, please review the [source](https://github.com/Codeception/Codeception/tree/master/src/Codeception/Module/WebDriver.php)**


New generation Selenium2 module.
*Included in Codeception 1.7.0*

### Installation

Download [Selenium2 WebDriver](http://code.google.com/p/selenium/downloads/list?q=selenium-server-standalone-2)
Launch the daemon: `java -jar selenium-server-standalone-2.xx.xxx.jar`

### Migration Guide (Selenium2 -> WebDriver)

* `wait` method accepts seconds instead of milliseconds. All waits use second as parameter.



### Status

* Maintainer: **davert**
* Stability: **beta**
* Contact: davert.codecept@mailican.com
* Based on [facebook php-webdriver](https://github.com/facebook/php-webdriver)

### Configuration

* url *required* - start url for your app
* browser *required* - browser that would be launched
* host  - Selenium server host (localhost by default)
* port - Selenium server port (4444 by default)
* restart - set to false to share browser sesssion between tests (by default), or set to true to create a session per test
* wait - set the implicit wait (5 secs) by default.
* capabilities - sets Selenium2 [desired capabilities](http://code.google.com/p/selenium/wiki/DesiredCapabilities). Should be a key-value array.

#### Example (`acceptance.suite.yml`)

    modules:
       enabled: [WebDriver]
       config:
          WebDriver:
             url: 'http://localhost/'
             browser: firefox
             wait: 10
             capabilities:
                 unexpectedAlertBehaviour: 'accept'


Class WebDriver
 * package Codeception\Module

### Actions


#### acceptPopup


Accepts JavaScript native popup window created by `window.alert`|`window.confirm`|`window.prompt`.
Don't confuse it with modal windows, created by [various libraries](http://jster.net/category/windows-modals-popups).



#### amOnPage


Opens the page.
Requires relative uri as parameter

Example:

{% highlight php %}

<?php
// opens front page
$I->amOnPage('/');
// opens /register page
$I->amOnPage('/register');
?>

{% endhighlight %}

 * param $page


#### amOnSubdomain


Sets 'url' configuration parameter to hosts subdomain.
It does not open a page on subdomain. Use `amOnPage` for that

{% highlight php %}

<?php
// If config is: 'http://mysite.com'
// or config is: 'http://www.mysite.com'
// or config is: 'http://company.mysite.com'

$I->amOnSubdomain('user');
$I->amOnPage('/');
// moves to http://user.mysite.com/
?>

{% endhighlight %}
 * param $subdomain
 * return mixed


#### appendField


Append text to an element
Can add another selection to a select box

{% highlight php %}

<?php
$I->appendField('#mySelectbox', 'SelectValue');
$I->appendField('#myTextField', 'appended');
?>

{% endhighlight %}

 * param string $field
 * param string $value


#### attachFile


Attaches file from Codeception data directory to upload field.

Example:

{% highlight php %}

<?php
// file is stored in 'tests/_data/prices.xls'
$I->attachFile('input[@type="file"]', 'prices.xls');
?>

{% endhighlight %}

 * param $field
 * param $filename


#### cancelPopup


Dismisses active JavaScript popup created by `window.alert`|`window.confirm`|`window.prompt`.


#### checkOption


Ticks a checkbox.
For radio buttons use `selectOption` method.

Example:

{% highlight php %}

<?php
$I->checkOption('#agree');
?>

{% endhighlight %}

 * param $option


#### click


Perform a click on link or button.
Link or button are found by their names or CSS selector.
Submits a form if button is a submit type.

If link is an image it's found by alt attribute value of image.
If button is image button is found by it's value
If link or button can't be found by name they are searched by CSS selector.

The second parameter is a context: CSS or XPath locator to narrow the search.

Examples:

{% highlight php %}

<?php
// simple link
$I->click('Logout');
// button of form
$I->click('Submit');
// CSS button
$I->click('#form input[type=submit]');
// XPath
$I->click('//form/*[@type=submit]')
// link in context
$I->click('Logout', '#nav');
?>

{% endhighlight %}
 * param $link
 * param $context


#### clickWithRightButton


Performs contextual click with right mouse button on element matched by CSS or XPath.

 * param $cssOrXPath
 * throws \Codeception\Exception\ElementNotFound


#### dontSee


Check if current page doesn't contain the text specified.
Specify the css selector to match only specific region.

Examples:

{% highlight php %}

<?php
$I->dontSee('Login'); // I can suppose user is already logged in
$I->dontSee('Sign Up','h1'); // I can suppose it's not a signup page
$I->dontSee('Sign Up','//body/h1'); // with XPath
?>

{% endhighlight %}

 * param $text
 * param null $selector


#### dontSeeCheckboxIsChecked


Assert if the specified checkbox is unchecked.
Use css selector or xpath to match.

Example:

{% highlight php %}

<?php
$I->dontSeeCheckboxIsChecked('#agree'); // I suppose user didn't agree to terms
$I->seeCheckboxIsChecked('#signup_form input[type=checkbox]'); // I suppose user didn't check the first checkbox in form.
?>

{% endhighlight %}

 * param $checkbox


#### dontSeeCookie


Checks that cookie doesn't exist

 * param $cookie
 * return mixed


#### dontSeeCurrentUrlEquals


Checks that current url is not equal to value.
Unlike `dontSeeInCurrentUrl` performs a strict check.

{% highlight php %}

<?php
// current url is not root
$I->dontSeeCurrentUrlEquals('/');
?>

{% endhighlight %}

 * param $uri


#### dontSeeCurrentUrlMatches


Checks that current url does not match a RegEx value

{% highlight php %}

<?php
// to match root url
$I->dontSeeCurrentUrlMatches('~$/users/(\d+)~');
?>

{% endhighlight %}

 * param $uri


#### dontSeeElement


Checks that element is invisible or not present on page.

{% highlight php %}

<?php
$I->dontSeeElement('.error');
$I->dontSeeElement('//form/input[1]');
?>

{% endhighlight %}

 * param $selector


#### dontSeeElementInDOM


Opposite to `seeElementInDOM`.

 * param $selector


#### dontSeeInCurrentUrl


Checks that current uri does not contain a value

{% highlight php %}

<?php
$I->dontSeeInCurrentUrl('/users/');
?>

{% endhighlight %}

 * param $uri


#### dontSeeInField


Checks that an input field or textarea doesn't contain value.
Field is matched either by label or CSS or Xpath
Example:

{% highlight php %}

<?php
$I->dontSeeInField('Body','Type your comment here');
$I->dontSeeInField('form textarea[name=body]','Type your comment here');
$I->dontSeeInField('form input[type=hidden]','hidden_value');
$I->dontSeeInField('#searchform input','Search');
$I->dontSeeInField('//form/*[@name=search]','Search');
?>

{% endhighlight %}

 * param $field
 * param $value


#### dontSeeInTitle


Checks that page title does not contain text.

 * param $title
 * return mixed


#### dontSeeLink


Checks if page doesn't contain the link with text specified.
Specify url to narrow the results.

Examples:

{% highlight php %}

<?php
$I->dontSeeLink('Logout'); // I suppose user is not logged in
?>

{% endhighlight %}

 * param $text
 * param null $url


#### dontSeeOptionIsSelected


Checks if option is not selected in select field.

{% highlight php %}

<?php
$I->dontSeeOptionIsSelected('#form input[name=payment]', 'Visa');
?>

{% endhighlight %}

 * param $selector
 * param $optionText
 * return mixed


#### doubleClick


Performs a double click on element matched by CSS or XPath.

 * param $cssOrXPath
 * throws \Codeception\Exception\ElementNotFound


#### dragAndDrop


Performs a simple mouse drag and drop operation.

{% highlight php %}

<?php
$I->dragAndDrop('#drag', '#drop');
?>

{% endhighlight %}

 * param string $source (CSS ID or XPath)
 * param string $target (CSS ID or XPath)


#### executeInSelenium


Low-level API method.
If Codeception commands are not enough, use Selenium WebDriver methods directly

{% highlight php %}

$I->executeInSelenium(function(\WebDriver $webdriver) {
  $webdriver->get('http://google.com');
});

{% endhighlight %}

Use [WebDriver Session API](https://github.com/facebook/php-webdriver)
Not recommended this command too be used on regular basis.
If Codeception lacks important Selenium methods implement then and submit patches.

 * param callable $function


#### executeJS


Executes custom JavaScript

 * param $script
 * return mixed


#### fillField


Fills a text field or textarea with value.

Example:

{% highlight php %}

<?php
$I->fillField("//input[@type='text']", "Hello World!");
?>

{% endhighlight %}

 * param $field
 * param $value


#### getName

__not documented__


#### grabCookie


Grabs a cookie value.

 * param $cookie
 * return mixed


#### grabFromCurrentUrl


Takes a parameters from current URI by RegEx.
If no url provided returns full URI.

{% highlight php %}

<?php
$user_id = $I->grabFromCurrentUrl('~$/user/(\d+)/~');
$uri = $I->grabFromCurrentUrl();
?>

{% endhighlight %}

 * param null $uri
 * internal param $url
 * return mixed


#### grabTextFrom


Finds and returns text contents of element.
Element is searched by CSS selector, XPath or matcher by regex.

Example:

{% highlight php %}

<?php
$heading = $I->grabTextFrom('h1');
$heading = $I->grabTextFrom('descendant-or-self::h1');
$value = $I->grabTextFrom('~<input value=(.*?)]~sgi');
?>

{% endhighlight %}

 * param $cssOrXPathOrRegex
 * return mixed


#### grabValueFrom


Finds and returns field and returns it's value.
Searches by field name, then by CSS, then by XPath

Example:

{% highlight php %}

<?php
$name = $I->grabValueFrom('Name');
$name = $I->grabValueFrom('input[name=username]');
$name = $I->grabValueFrom('descendant-or-self::form/descendant::input[@name = 'username']');
?>

{% endhighlight %}

 * param $field
 * return mixed


#### makeScreenshot


Makes a screenshot of current window and saves it to `tests/_log/debug`.

{% highlight php %}

<?php
$I->amOnPage('/user/edit');
$I->makeScreenshot('edit page');
// saved to: tests/_log/debug/UserEdit - edit page.png
?>

{% endhighlight %}

 * param $name


#### maximizeWindow


Maximizes current window


#### moveBack


Moves back in history


#### moveForward


Moves forward in history


#### moveMouseOver


Move mouse over the first element matched by css or xPath on page

https://code.google.com/p/selenium/wiki/JsonWireProtocol#/session/:sessionId/moveto

 * param string $cssOrXPath css or xpath of the web element
 * param int $offsetX
 * param int $offsetY

 * throws \Codeception\Exception\ElementNotFound
 * return null


#### pauseExecution


Pauses test execution in debug mode.
To proceed test press "ENTER" in console.

This method is recommended to use in test development, for additional page analysis, locator searing, etc.


#### pressKey


Presses key on element found by css, xpath is focused
A char and modifier (ctrl, alt, shift, meta) can be provided.
For special keys use key constants from \WebDriverKeys class.

Example:

{% highlight php %}

<?php
// <input id="page" value="old" />
$I->pressKey('#page','a'); // => olda
$I->pressKey('#page',array('ctrl','a'),'new'); //=> new
$I->pressKey('#page',array('shift','111'),'1','x'); //=> old!!!1x
$I->pressKey('descendant-or-self::*[@id='page']','u'); //=> oldu
$I->pressKey('#name', array('ctrl', 'a'), WebDriverKeys::DELETE); //=>''
?>

{% endhighlight %}

 * param $element
 * param $char can be char or array with modifier. You can provide several chars.
 * throws \Codeception\Exception\ElementNotFound


#### reloadPage


Reloads current page


#### resetCookie


Unsets cookie

 * param $cookie
 * return mixed


#### resizeWindow


Resize current window

Example:
{% highlight php %}

<?php
$I->resizeWindow(800, 600);


{% endhighlight %}

 * param int    $width
 * param int    $height


#### see


Check if current page contains the text specified.
Specify the css selector to match only specific region.

Examples:

{% highlight php %}

<?php
$I->see('Logout'); // I can suppose user is logged in
$I->see('Sign Up','h1'); // I can suppose it's a signup page
$I->see('Sign Up','//body/h1'); // with XPath
?>

{% endhighlight %}

 * param $text
 * param null $selector


#### seeCheckboxIsChecked


Assert if the specified checkbox is checked.
Use css selector or xpath to match.

Example:

{% highlight php %}

<?php
$I->seeCheckboxIsChecked('#agree'); // I suppose user agreed to terms
$I->seeCheckboxIsChecked('#signup_form input[type=checkbox]'); // I suppose user agreed to terms, If there is only one checkbox in form.
$I->seeCheckboxIsChecked('//form/input[@type=checkbox and  * name=agree]');
?>

{% endhighlight %}

 * param $checkbox


#### seeCookie


Checks that cookie is set.

 * param $cookie
 * return mixed


#### seeCurrentUrlEquals


Checks that current url is equal to value.
Unlike `seeInCurrentUrl` performs a strict check.

{% highlight php %}

<?php
// to match root url
$I->seeCurrentUrlEquals('/');
?>

{% endhighlight %}

 * param $uri


#### seeCurrentUrlMatches


Checks that current url is matches a RegEx value

{% highlight php %}

<?php
// to match root url
$I->seeCurrentUrlMatches('~$/users/(\d+)~');
?>

{% endhighlight %}

 * param $uri


#### seeElement


Checks for a visible element on a page, matching it by CSS or XPath

{% highlight php %}

<?php
$I->seeElement('.error');
$I->seeElement('//form/input[1]');
?>

{% endhighlight %}
 * param $selector


#### seeElementInDOM


Checks if element exists on a page even it is invisible.

{% highlight php %}

<?php
$I->seeElementInDOM('//form/input[type=hidden]');
?>

{% endhighlight %}

 * param $selector


#### seeInCurrentUrl


Checks that current uri contains a value

{% highlight php %}

<?php
// to match: /home/dashboard
$I->seeInCurrentUrl('home');
// to match: /users/1
$I->seeInCurrentUrl('/users/');
?>

{% endhighlight %}

 * param $uri


#### seeInField


Checks that an input field or textarea contains value.
Field is matched either by label or CSS or Xpath

Example:

{% highlight php %}

<?php
$I->seeInField('Body','Type your comment here');
$I->seeInField('form textarea[name=body]','Type your comment here');
$I->seeInField('form input[type=hidden]','hidden_value');
$I->seeInField('#searchform input','Search');
$I->seeInField('//form/*[@name=search]','Search');
?>

{% endhighlight %}

 * param $field
 * param $value


#### seeInPopup


Checks that active JavaScript popup created by `window.alert`|`window.confirm`|`window.prompt` contain text.

 * param $text


#### seeInTitle


Checks that page title contains text.

{% highlight php %}

<?php
$I->seeInTitle('Blog - Post #1');
?>

{% endhighlight %}

 * param $title
 * return mixed


#### seeLink


Checks if there is a link with text specified.
Specify url to match link with exact this url.

Examples:

{% highlight php %}

<?php
$I->seeLink('Logout'); // matches <a href="#">Logout</a>
$I->seeLink('Logout','/logout'); // matches <a href="/logout">Logout</a>
?>

{% endhighlight %}

 * param $text
 * param null $url


#### seeOptionIsSelected


Checks if option is selected in select field.

{% highlight php %}

<?php
$I->seeOptionIsSelected('#form input[name=payment]', 'Visa');
?>

{% endhighlight %}

 * param $selector
 * param $optionText
 * return mixed


#### selectOption


Selects an option in select tag or in radio button group.

Example:

{% highlight php %}

<?php
$I->selectOption('form select[name=account]', 'Premium');
$I->selectOption('form input[name=payment]', 'Monthly');
$I->selectOption('//form/select[@name=account]', 'Monthly');
?>

{% endhighlight %}

Can select multiple options if second argument is array:

{% highlight php %}

<?php
$I->selectOption('Which OS do you use?', array('Windows','Linux'));
?>

{% endhighlight %}

 * param $select
 * param $option


#### setCookie


Sets a cookie.

 * param $cookie
 * param $value
 * return mixed


#### submitForm


Submits a form located on page.
Specify the form by it's css or xpath selector.
Fill the form fields values as array. Hidden fields can't be accessed.

This command itself triggers the request to form's action.

Examples:

{% highlight php %}

<?php
$I->submitForm('#login', array('login' => 'davert', 'password' => '123456'));


{% endhighlight %}

For sample Sign Up form:

{% highlight html %}

<form action="/sign_up">
    Login: <input type="text" name="user[login]" /><br/>
    Password: <input type="password" name="user[password]" /><br/>
    Do you agree to out terms? <input type="checkbox" name="user[agree]" /><br/>
    Select pricing plan <select name="plan"><option value="1">Free</option><option value="2" selected="selected">Paid</option></select>
    <input type="submit" value="Submit" />
</form>

{% endhighlight %}
You can write this:

{% highlight php %}

<?php
$I->submitForm('#userForm', array('user' => array('login' => 'Davert', 'password' => '123456', 'agree' => true)));


{% endhighlight %}

 * param $selector
 * param $params
 * throws \Codeception\Exception\ElementNotFound


#### switchToIFrame


Switch to another frame

Example:
{% highlight html %}

<iframe name="another_frame" src="http://example.com">


{% endhighlight %}

{% highlight php %}

<?php
# switch to iframe
$I->switchToIFrame("another_frame");
# switch to parent page
$I->switchToIFrame();


{% endhighlight %}

 * param string|null $name


#### switchToWindow


Switch to another window identified by its name.

The window can only be identified by its name. If the $name parameter is blank it will switch to the parent window.

Example:
{% highlight html %}

<input type="button" value="Open window" onclick="window.open('http://example.com', 'another_window')">

{% endhighlight %}

{% highlight php %}

<?php
$I->click("Open window");
# switch to another window
$I->switchToWindow("another_window");
# switch to parent window
$I->switchToWindow();
?>

{% endhighlight %}

If the window has no name, the only way to access it is via the `executeInSelenium()` method like so:

{% highlight yaml %}

<?php
$I->executeInSelenium(function (\Webdriver $webdriver) {
     $handles=$webDriver->getWindowHandles();
     $last_window = end($handles);
     $webDriver->switchTo()->window($name);
});
?>

{% endhighlight %}

 * param string|null $name


#### typeInPopup


Enters text into native JavaScript prompt popup created by `window.prompt`.

 * param $keys


#### uncheckOption


Unticks a checkbox.

Example:

{% highlight php %}

<?php
$I->uncheckOption('#notify');
?>

{% endhighlight %}

 * param $option


#### unselectOption

__not documented__


#### wait


Explicit wait.

 * param $timeout secs


#### waitForElement


Waits for element to appear on page for $timeout seconds to pass.
If element not appears, timeout exception is thrown.

{% highlight php %}

<?php
$I->waitForElement('#agree_button', 30); // secs
$I->click('#agree_button');
?>

{% endhighlight %}

 * param $element
 * param int $timeout seconds
 * throws \Exception


#### waitForElementChange


Waits for element to change or for $timeout seconds to pass. Element "change" is determined
by a callback function which is called repeatedly until the return value evaluates to true.

{% highlight php %}

<?php
$I->waitForElementChange('#menu', function(\WebDriverElement $el) {
    return $el->isDisplayed();
}, 100);
?>

{% endhighlight %}

 * param $element
 * param \Closure $callback
 * param int $timeout seconds
 * throws \Codeception\Exception\ElementNotFound


#### waitForElementNotVisible


Waits for element to not be visible on the page for $timeout seconds to pass.
If element stays visible, timeout exception is thrown.

{% highlight php %}

<?php
$I->waitForElementNotVisible('#agree_button', 30); // secs
?>

{% endhighlight %}

 * param $element
 * param int $timeout seconds
 * throws \Exception


#### waitForElementVisible


Waits for element to be visible on the page for $timeout seconds to pass.
If element doesn't appear, timeout exception is thrown.

{% highlight php %}

<?php
$I->waitForElementVisible('#agree_button', 30); // secs
$I->click('#agree_button');
?>

{% endhighlight %}

 * param $element
 * param int $timeout seconds
 * throws \Exception


#### waitForJS


Executes JavaScript and waits for it to return true or for the timeout.

In this example we will wait for all jQuery ajax requests are finished or 60 secs otherwise.

{% highlight php %}

<?php
$I->waitForJS("return $.active == 0;", 60);
?>

{% endhighlight %}

 * param $script
 * param $timeout int seconds


#### waitForText


Waits for text to appear on the page for a specific amount of time.
Can also be passed a selector to search in.
If text does not appear, timeout exception is thrown.

{% highlight php %}

<?php
$I->waitForText('foo', 30); // secs
$I->waitForText('foo', 30, '.title'); // secs
?>

{% endhighlight %}

 * param string $text
 * param int $timeout seconds
 * param null $selector
 * throws \Exception
 * internal param string $element
