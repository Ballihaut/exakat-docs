Real Code Cases {#Cases}
===============

Introduction
------------

All the examples in this section are real code, extracted from major PHP
applications.

Examples
--------

### Adding Zero

#### Thelia {#thelia-structures-addzero}

`adding-zero`{.interpreted-text role="ref"}, in
core/lib/Thelia/Model/Map/ProfileResourceTableMap.php:250.

This return statement is doing quite a lot, including a buried \'0 +
\$offset\'. This call is probably an echo to \'1 + \$offset\', which is
a little later in the expression.

``` {.php}
return serialize(array((string) $row[TableMap::TYPE_NUM == $indexType ? 0 + $offset : static::translateFieldName('ProfileId', TableMap::TYPE_PHPNAME, $indexType)], (string) $row[TableMap::TYPE_NUM == $indexType ? 1 + $offset : static::translateFieldName('ResourceId', TableMap::TYPE_PHPNAME, $indexType)]));
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-structures-addzero}

`adding-zero`{.interpreted-text role="ref"}, in
interface/forms/fee\_sheet/new.php:466:534.

\$main\_provid is filtered as an integer. \$main\_supid is then filtered
twice : one with the sufficent (int) and then, added with 0.

``` {.php}
if (!$alertmsg && ($_POST['bn_save'] || $_POST['bn_save_close'] || $_POST['bn_save_stay'])) {
    $main_provid = 0 + $_POST['ProviderID'];
    $main_supid  = 0 + (int)$_POST['SupervisorID'];
    //.....
```

### Ambiguous Array Index

#### PrestaShop {#prestashop-arrays-ambiguouskeys}

`ambiguous-array-index`{.interpreted-text role="ref"}, in
src/PrestaShopBundle/Install/Install.php:532.

Null, as a key, is actually the empty string.

``` {.php}
$list = array(
            'products' => _PS_PROD_IMG_DIR_,
            'categories' => _PS_CAT_IMG_DIR_,
            'manufacturers' => _PS_MANU_IMG_DIR_,
            'suppliers' => _PS_SUPP_IMG_DIR_,
            'stores' => _PS_STORE_IMG_DIR_,
            null => _PS_IMG_DIR_.'l/', // Little trick to copy images in img/l/ path with all types
        );
```

------------------------------------------------------------------------

#### Mautic {#mautic-arrays-ambiguouskeys}

`ambiguous-array-index`{.interpreted-text role="ref"}, in
app/bundles/CoreBundle/Entity/CommonRepository.php:314.

True is turned into 1 (integer), and false is turned into 0 (integer).

``` {.php}
foreach ($metadata->getAssociationMappings() as $field => $association) {
                    if (in_array($association['type'], [ClassMetadataInfo::ONE_TO_ONE, ClassMetadataInfo::MANY_TO_ONE])) {
                        $baseCols[true][$entityClass][]  = $association['joinColumns'][0]['name'];
                        $baseCols[false][$entityClass][] = $field;
                    }
                }
```

### error\_reporting() With Integers

#### SugarCrm {#sugarcrm-structures-errorreportingwithinteger}

`error\_reporting()-with-integers`{.interpreted-text role="ref"}, in
modules/UpgradeWizard/silentUpgrade\_step1.php:436.

This only displays E\_ERROR, the highest level of error reporting. It
should be checked, as it happens in the \'silentUpgrade\' script.

``` {.php}
ini_set('error_reporting', 1);
```

### Eval() Usage

#### XOOPS {#xoops-structures-evalusage}

`eval()-usage`{.interpreted-text role="ref"}, in
htdocs/modules/system/class/block.php:266.

eval() execute code that was arbitrarily stored in \$this, in one of the
properties. Then, it is sent to output, but collected before reaching
the browser, and put again in \$content. May be the
echo/ob\_get\_contents() could have been skipped.

``` {.php}
ob_start();
                    echo eval($this->getVar('content', 'n'));
                    $content = ob_get_contents();
                    ob_end_clean();
```

------------------------------------------------------------------------

#### Mautic {#mautic-structures-evalusage}

`eval()-usage`{.interpreted-text role="ref"}, in
app/bundles/InstallBundle/Configurator/Step/CheckStep.php:238.

create\_function() is actually an eval() in disguise : replace it with a
closure for code modernization

``` {.php}
create_function('$cfgValue', 'return $cfgValue > 100;')
```

### Exit() Usage

#### Traq {#traq-structures-exitusage}

`exit()-usage`{.interpreted-text role="ref"}, in
src/Controllers/attachments.php:75.

This acts as a view. The final \'exit\' is meant to ensure that no other
piece of data is emitted, potentially polluting the view. This also
prevent any code cleaning to happen.

``` {.php}
/**
     * View attachment page
     *
     * @param integer $attachment_id
     */
    public function action_view($attachment_id)
    {
        // Don't try to load a view
        $this->render['view'] = false;

        header(Content-type: {$this->attachment->type});
        $content_type = explode('/', $this->attachment->type);

        // Check what type of file we're dealing with.
        if($content_type[0] == 'text' or $content_type[0] == 'image') {
            // If the mime-type is text, we can just display it
            // as plain text. I hate having to download files.
            if ($content_type[0] == 'text') {
                header(Content-type: text/plain);
            }
            header("Content-Disposition: filename=\"{$this->attachment->name}\"");
        }
        // Anything else should be downloaded
        else {
            header("Content-Disposition: attachment; filename=\"{$this->attachment->name}\"");
        }

        // Decode the contents and display it
        print(base64_decode($this->attachment->contents));
        exit;
    }
```

------------------------------------------------------------------------

#### ThinkPHP {#thinkphp-structures-exitusage}

`exit()-usage`{.interpreted-text role="ref"}, in
ThinkPHP/Library/Vendor/EaseTemplate/template.core.php:60.

Here, exit is used as a rudimentary error management. When the version
is not correctly provided via EaseTemplateVer, the application stop
totally.

``` {.php}
$this->version      = (trim($_GET['EaseTemplateVer']))?die('Ease Templae E3!'):'';
```

### Multiply By One

#### SugarCrm {#sugarcrm-structures-multiplybyone}

`multiply-by-one`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/modules/Relationships/views/view.editfields.php:74.

Here, \'\$count % 1\' is always true, after the first loop of the
foreach. There is no need for % usage.

``` {.php}
$count = 0;
        foreach($this->fields as $def)
        {
            if (!empty($def['relationship_field'])) {
                $label = !empty($def['vname']) ? $def['vname'] : $def['name'];
                echo <td> . translate($label, $this->module) . :</td>
                   . <td><input id='{$def['name']}' name='{$def['name']}'>  ;

                if ($count%1)
                    echo </tr><tr>;
                $count++;
            }
        }
        echo </tr></table></form>;
```

------------------------------------------------------------------------

#### Edusoho {#edusoho-structures-multiplybyone}

`multiply-by-one`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

1 is useless here, since 24 \* 3600 is already an integer. And, of
course, a day is not 24 \* 3600\... at least every day.

``` {.php}
'yesterdayStart' => date('Y-m-d', strtotime(date('Y-m-d', time())) - 1 * 24 * 3600),
```

### Not Not

#### Cleverstyle {#cleverstyle-structures-notnot}

`not-not`{.interpreted-text role="ref"}, in
modules/OAuth2/OAuth2.php:190.

This double-call returns `$results` as a boolean, preventing a spill of
data to the calling method. The `(bool)` operator would be clearer here.

``` {.php}
$result = $this->db_prime()->q(
            [
                DELETE FROM `[prefix]oauth2_clients`
                WHERE `id` = '%s',
                DELETE FROM `[prefix]oauth2_clients_grant_access`
                WHERE `id`  = '%s',
                DELETE FROM `[prefix]oauth2_clients_sessions`
                WHERE `id`  = '%s'
            ],
            $id
        );
        unset($this->cache->{'/'});
        return !!$result;
```

------------------------------------------------------------------------

#### Tine20 {#tine20-structures-notnot}

`not-not`{.interpreted-text role="ref"}, in
tine20/Calendar/Controller/MSEventFacade.php:392.

It seems that !! is almost superfluous, as a property called
\'is\_deleted\' should already be a boolean.

``` {.php}
foreach ($exceptions as $exception) {
                $exception->assertAttendee($this->getCalendarUser());
                $this->_prepareException($savedEvent, $exception);
                $this->_preserveMetaData($savedEvent, $exception, true);
                $this->_eventController->createRecurException($exception, !!$exception->is_deleted);
            }
```

### include\_once() Usage

#### XOOPS {#xoops-structures-onceusage}

`include\_once()-usage`{.interpreted-text role="ref"}, in
/htdocs/xoops\_lib/modules/protector/admin/center.php:5.

Loading() classes should be down with autoload(). autload() may be build
in several distinct functions, using spl\_autoload\_register().

``` {.php}
require_once dirname(__DIR__) . 'class/gtickets.php'
```

------------------------------------------------------------------------

#### Tikiwiki {#tikiwiki-structures-onceusage}

`include\_once()-usage`{.interpreted-text role="ref"}, in
tiki-mytiki\_shared.php :140.

Turn the code from tiki-mytiki\_shared.php into a function or a method,
and call it when needed.

``` {.php}
include_once('tiki-mytiki_shared.php');
```

### Strpos()-like Comparison

#### Piwigo {#piwigo-structures-strposcompare}

`strpos()-like-comparison`{.interpreted-text role="ref"}, in
admin/include/functions.php:2585.

preg\_match may return 0 if not found, and null if the \$pattern is
erroneous. While hardcoded regex may be checked at compile time,
dynamically built regex may fail at execution time. This is particularly
important here, since the function may be called with incoming data for
maintenance : \'clear\_derivative\_cache(\$\_GET\[\'type\'\]);\' is in
the /admin/maintenance.php.

``` {.php}
function clear_derivative_cache_rec($path, $pattern)
{
  $rmdir = true;
  $rm_index = false;

  if ($contents = opendir($path))
  {
    while (($node = readdir($contents)) !== false)
    {
      if ($node == '.' or $node == '..')
        continue;
      if (is_dir($path.'/'.$node))
      {
        $rmdir &= clear_derivative_cache_rec($path.'/'.$node, $pattern);
      }
      else
      {
        if (preg_match($pattern, $node))
```

------------------------------------------------------------------------

#### Thelia {#thelia-structures-strposcompare}

`strpos()-like-comparison`{.interpreted-text role="ref"}, in
core/lib/Thelia/Controller/Admin/FileController.php:198.

preg\_match is used here to identify files with a forbidden extension.
The actual list of extension is provided to the method via the parameter
\$extBlackList, which is an array. In case of mis-configuration by the
user of this array, preg\_match may fail : for example, when regex
special characters are provided. At that point, the whole filter becomes
invalid, and can\'t distinguish good files (returning false) and other
files (returning NULL). It is safe to use === false in this situation.

``` {.php}
if (!empty($extBlackList)) {
            $regex = "#^(.+)\.(".implode("|", $extBlackList).")$#i";

            if (preg_match($regex, $realFileName)) {
                $message = $this->getTranslator()
                    ->trans(
                        'Files with the following extension are not allowed: %extension, please do an archive of the file if you want to upload it',
                        [
                            '%extension' => $fileBeingUploaded->getClientOriginalExtension(),
                        ]
                    );
            }
        }
```

### var\_dump()\... Usage

#### Tine20 {#tine20-structures-vardumpusage}

`var\_dump()...-usage`{.interpreted-text role="ref"}, in
tine20/library/Ajam/Connection.php:122.

Two usage of var\_dump(). They are protected by configuration, since the
debug property must be set to \'true\'. Yet, it is safer to avoid them
altogether, and log the information to an external file.

``` {.php}
if($this->debug === true) {
            var_dump($this->getLastRequest());
            var_dump($response);
        }
```

------------------------------------------------------------------------

#### Piwigo {#piwigo-structures-vardumpusage}

`var\_dump()...-usage`{.interpreted-text role="ref"}, in
include/ws\_core.inc.php:273.

This is a hidden debug system : when the response format is not
available, the whole object is dumped in the output.

``` {.php}
function run()
  {
    if ( is_null($this->_responseEncoder) )
    {
      set_status_header(400);
      @header("Content-Type: text/plain");
      echo ("Cannot process your request. Unknown response format.
Request format: ".@$this->_requestFormat." Response format: ".@$this->_responseFormat."\n");
      var_export($this);
      die(0);
    }
```

### Empty Function

#### Contao {#contao-functions-emptyfunction}

`empty-function`{.interpreted-text role="ref"}, in
core-bundle/src/Resources/contao/modules/ModuleQuicklink.php:91.

The closure used with array\_map() is empty : this means that the keys
are all set to the returned value of the empty closure, which is null.
The actual effect is to reset the values to NULL. A better solution,
without using the empty closure, is to rely on array\_fill\_keys() to
create an array with default values.

``` {.php}
if (!empty($tmp) && \is_array($tmp))
            {
                $arrPages = array_map(function () {}, array_flip($tmp));
            }
```

### Used Once Variables

#### shopware {#shopware-variables-variableusedonce}

`used-once-variables`{.interpreted-text role="ref"}, in
\_sql/migrations/438-add-email-template-header-footer-fields.php:115.

In the updateEmailTemplate method, \$generatedQueries collects all the
generated SQL queries. \$generatedQueries is not initialized, and never
used after initialization.

``` {.php}
private function updateEmailTemplate($name, $content, $contentHtml = null)
    {
        $sql = <<<SQL
UPDATE `s_core_config_mails` SET `content` = "$content" WHERE `name` = "$name" AND dirty = 0
SQL;
        $this->addSql($sql);

        if ($contentHtml != null) {
            $sql = <<<SQL
UPDATE `s_core_config_mails` SET `content` = "$content", `contentHTML` = "$contentHtml" WHERE `name` = "$name" AND dirty = 0
SQL;
            $generatedQueries[] = $sql;
        }

        $this->addSql($sql);
    }
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-variables-variableusedonce}

`used-once-variables`{.interpreted-text role="ref"}, in
library/core/class.configuration.php:1461.

In this code, \$cachedConfigData is collected after storing date in the
cache. Gdn::cache()-\>store() does actual work, so its calling is
necessary. The result, collected after execution, is not reused in the
rest of the method (long method, not all is shown here). Removing such
variable is a needed clean up after development and debug, but also
prevents pollution of the variable namespace.

``` {.php}
// Save to cache if we're into that sort of thing
                $fileKey = sprintf(Gdn_Configuration::CONFIG_FILE_CACHE_KEY, $this->Source);
                if ($this->Configuration && $this->Configuration->caching() && Gdn::cache()->type() == Gdn_Cache::CACHE_TYPE_MEMORY && Gdn::cache()->activeEnabled()) {
                    $cachedConfigData = Gdn::cache()->store($fileKey, $data, [
                        Gdn_Cache::FEATURE_NOPREFIX => true,
                        Gdn_Cache::FEATURE_EXPIRY => 3600
                    ]);
                }
```

### Empty Classes

#### WordPress {#wordpress-classes-emptyclass}

`empty-classes`{.interpreted-text role="ref"}, in
wp-includes/SimplePie/Core.php:54.

Empty class, but documented as backward compatibility.

``` {.php}
/**
 * SimplePie class.
 *
 * Class for backward compatibility.
 *
 * @deprecated Use {@see SimplePie} directly
 * @package SimplePie
 * @subpackage API
 */
class SimplePie_Core extends SimplePie
{

}
```

### Non Ascii Variables

#### Magento {#magento-variables-variablenonascii}

`non-ascii-variables`{.interpreted-text role="ref"}, in
dev/tests/functional/tests/app/Mage/Checkout/Test/Constraint/AssertOrderWithMultishippingSuccessPlacedMessage.php:52.

The initial C is actually a russian C.

``` {.php}
$сheckoutMultishippingSuccess
```

### Non Static Methods Called In A Static

#### Dolphin {#dolphin-classes-nonstaticmethodscalledstatic}

`non-static-methods-called-in-a-static`{.interpreted-text role="ref"},
in Dolphin-v.7.3.5/xmlrpc/BxDolXMLRPCFriends.php:11.

getIdByNickname() is indeed defined in the class \'BxDolXMLRPCUtil\' and
it calls the database. The class relies on functions (not methods) to
query the database with the correct connexion.

``` {.php}
class BxDolXMLRPCFriends
{
    function getFriends($sUser, $sPwd, $sNick, $sLang)
    {
        $iIdProfile = BxDolXMLRPCUtil::getIdByNickname ($sNick);
```

------------------------------------------------------------------------

#### Magento {#magento-classes-nonstaticmethodscalledstatic}

`non-static-methods-called-in-a-static`{.interpreted-text role="ref"},
in app/code/core/Mage/Paypal/Model/Payflowlink.php:143.

Mage\_Payment\_Model\_Method\_Abstract is an abstract class : this way,
it is not possible to instantiate it and then, access its methods. The
class is extended, so it could be called from one of the objects.
Although, the troubling part is that isAvailable() uses \$this, so it
can\'t be static.

``` {.php}
Mage_Payment_Model_Method_Abstract::isAvailable($quote)
```

### Forgotten Visibility

#### FuelCMS {#fuelcms-classes-nonppp}

`forgotten-visibility`{.interpreted-text role="ref"}, in
/fuel/modules/fuel/controllers/Module.php:713.

Missing visibility for the index() method,and all the methods in the
Module class.

``` {.php}
class Module extends Fuel_base_controller {

    // --------------------------------------------------------------------

    /**
     * Displays the list (table) view
     *
     * @access  public
     * @return  void
     */ 
    function index()
    {
        $this->items();
    }
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-classes-nonppp}

`forgotten-visibility`{.interpreted-text role="ref"}, in
livezilla/\_lib/objects.global.users.inc.php:2516.

Static method that could be public.

``` {.php}
class Visitor extends BaseUser 
{
// Lots of code

    static function CreateSPAMFilter($_userId,$_base64=true)
    {
        if(!empty(Server::$Configuration->File[gl_sfa]))
        {
```

### Multiple Index Definition

#### Magento {#magento-arrays-multipleidenticalkeys}

`multiple-index-definition`{.interpreted-text role="ref"}, in
app/code/core/Mage/Adminhtml/Block/System/Convert/Gui/Grid.php:80.

\'type\' is defined twice. The first one, \'options\' is overwritten.

``` {.php}
$this->addColumn('store_id', array(
            'header'    => Mage::helper('adminhtml')->__('Store'),
            'type'      => 'options',
            'align'     => 'center',
            'index'     => 'store_id',
            'type'      => 'store',
            'width'     => '200px',
        ));
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-arrays-multipleidenticalkeys}

`multiple-index-definition`{.interpreted-text role="ref"}, in
resources/Resources.php:223.

\'target\' is repeated, though with the same values. This is just dead
code.

``` {.php}
// inside a big array
    'jquery.getAttrs' => [
        'targets' => [ 'desktop', 'mobile' ],
        'scripts' => 'resources/src/jquery/jquery.getAttrs.js',
        'targets' => [ 'desktop', 'mobile' ],
    ],
    // big array continues
```

### Incompilable Files

#### xataface {#xataface-php-incompilable}

`incompilable-files`{.interpreted-text role="ref"}, in
lib/XML/Tree.php:289.

Compilation error with PHP 7.2 version.

``` {.php}
syntax error, unexpected 'new' (T_NEW)
```

### Multiple Constant Definition

#### Dolibarr {#dolibarr-constants-multipleconstantdefinition}

`multiple-constant-definition`{.interpreted-text role="ref"}, in
htdocs/main.inc.php:914.

All is documented here : \'Constants used to defined number of lines in
textarea\'. Constants are not changing during an execution, and this
allows the script to set values early in the process, and have them used
later, in the templates. Yet, building constants dynamically may lead to
confusion, when developpers are not aware of the change.

``` {.php}
// Constants used to defined number of lines in textarea
if (empty($conf->browser->firefox))
{
    define('ROWS_1',1);
    define('ROWS_2',2);
    define('ROWS_3',3);
    define('ROWS_4',4);
    define('ROWS_5',5);
    define('ROWS_6',6);
    define('ROWS_7',7);
    define('ROWS_8',8);
    define('ROWS_9',9);
}
else
{
    define('ROWS_1',0);
    define('ROWS_2',1);
    define('ROWS_3',2);
    define('ROWS_4',3);
    define('ROWS_5',4);
    define('ROWS_6',5);
    define('ROWS_7',6);
    define('ROWS_8',7);
    define('ROWS_9',8);
}
```

------------------------------------------------------------------------

#### OpenConf {#openconf-constants-multipleconstantdefinition}

`multiple-constant-definition`{.interpreted-text role="ref"}, in
modules/request.php:71.

The constant is build according to the situation, in the part of the
script (file request.php). This hides the actual origin of the value,
but keeps the rest of the code simple. Just keep in mind that this
constant may have different values.

``` {.php}
if (isset($_GET['ocparams']) && !empty($_GET['ocparams'])) {
        $params = '';
        if (preg_match_all("/(\w+)--(\w+)_-/", $_GET['ocparams'], $matches)) {
            foreach ($matches[1] as $idx => $m) {
                if (($m != 'module') && ($m != 'action') && preg_match("/^[\w-]+$/", $m)) {
                    $params .= '&' . $m . '=' . urlencode($matches[2][$idx]);
                    $_GET[$m] = $matches[2][$idx];
                }
            }
        }
        unset($_GET['ocparams']);
        define('OCC_SELF', $_SERVER['PHP_SELF'] . '?module=' . $_REQUEST['module'] . '&action=' . $_GET['action'] . $params);
    } elseif (isset($_SERVER['REQUEST_URI']) && strstr($_SERVER['REQUEST_URI'], '?')) {
        define('OCC_SELF', htmlspecialchars($_SERVER['REQUEST_URI']));
    } elseif (isset($_SERVER['QUERY_STRING']) && strstr($_SERVER['QUERY_STRING'], '&')) {
        define('OCC_SELF', $_SERVER['PHP_SELF'] . '?' . htmlspecialchars($_SERVER['QUERY_STRING']));
    } else {
        err('This server does not support REQUEST_URI or QUERY_STRING','Error');
    }
```

### Invalid Constant Name

#### OpenEMR {#openemr-constants-invalidname}

`invalid-constant-name`{.interpreted-text role="ref"}, in
library/classes/InsuranceCompany.class.php:20.

Either a copy/paste, or a generated definition file : the file contains
25 constants definition. The constant is not found in the rest of the
code.

``` {.php}
define("INS_TYPE_OTHER_NON-FEDERAL_PROGRAMS", 10);
```

### Wrong Optional Parameter

#### FuelCMS {#fuelcms-functions-wrongoptionalparameter}

`wrong-optional-parameter`{.interpreted-text role="ref"}, in
fuel/modules/fuel/helpers/validator\_helper.php:78.

The \$regex parameter should really be first, as it is compulsory.
Though, if this is a legacy function, it may be better to give regex a
default value, such as empty string or null, and test it before using
it.

``` {.php}
if (!function_exists('regex'))
{
    function regex($var = null, $regex)
    {
        return preg_match('#'.$regex.'#', $var);
    } 
}
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-functions-wrongoptionalparameter}

`wrong-optional-parameter`{.interpreted-text role="ref"}, in
applications/dashboard/modules/class.navmodule.php:99.

Note the second parameter, \$dropdown, which has no default value. It is
relayed to the addDropdown method, which as no default value too. Since
both methods are documented, we can see that they should be an
addDropdown : null is probably a good idea, coupled with an explicit
check on the actual value.

``` {.php}
/**
     * Add a dropdown to the items array if it satisfies the $isAllowed condition.
     *
     * @param bool|string|array $isAllowed Either a boolean to indicate whether to actually add the item
     * or a permission string or array of permission strings (full match) to check.
     * @param DropdownModule $dropdown The dropdown menu to add.
     * @param string $key The item's key (for sorting and CSS targeting).
     * @param string $cssClass The dropdown wrapper's CSS class.
     * @param array|int $sort Either a numeric sort position or and array in the style: array('before|after', 'key').
     * @return NavModule $this The calling object.
     */
    public function addDropdownIf($isAllowed = true, $dropdown, $key = '', $cssClass = '', $sort = []) {
        if (!$this->isAllowed($isAllowed)) {
            return $this;
        } else {
            return $this->addDropdown($dropdown, $key, $cssClass, $sort);
        }
    }
```

### One Variable String

#### Tikiwiki {#tikiwiki-type-onevariablestrings}

`one-variable-string`{.interpreted-text role="ref"}, in
lib/wiki-plugins/wikiplugin\_addtocart.php:228.

Double-quotes are not needed here. If casting to string is important,
the (string) would be more explicit.

``` {.php}
foreach ($plugininfo['params'] as $key => $param) {
        $default["$key"] = $param['default'];
    }
```

------------------------------------------------------------------------

#### NextCloud {#nextcloud-type-onevariablestrings}

`one-variable-string`{.interpreted-text role="ref"}, in
build/integration/features/bootstrap/BasicStructure.php:349.

Both concatenations could be merged, independantly. If readability is
important, why not put them inside curly brackets?

``` {.php}
public static function removeFile($path, $filename) {
        if (file_exists("$path" . "$filename")) {
            unlink("$path" . "$filename");
        }
    }
```

### Static Methods Can\'t Contain \$this

#### xataface {#xataface-classes-staticcontainsthis}

`static-methods-can't-contain-$this`{.interpreted-text role="ref"}, in
Dataface/LanguageTool.php:48.

\$this is hidden in the arguments of the static call to the method.

``` {.php}
public static function loadRealm($name){
        return self::getInstance($this->app->_conf['default_language'])->loadRealm($name);
    }
```

------------------------------------------------------------------------

#### SugarCrm {#sugarcrm-classes-staticcontainsthis}

`static-methods-can't-contain-$this`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/modules/ACLActions/ACLAction.php:332.

Notice how \$this is tested for existence before using it. It seems
strange, at first, but we have to remember that if \$this is never set
when calling a static method, a static method may be called with \$this.
Confusingly, this static method may be called in two ways.

``` {.php}
static function hasAccess($is_owner=false, $access = 0){

        if($access != 0 && $access == ACL_ALLOW_ALL || ($is_owner && $access == ACL_ALLOW_OWNER))return true;
       //if this exists, then this function is not static, so check the aclaccess parameter
        if(isset($this) && isset($this->aclaccess)){
            if($this->aclaccess == ACL_ALLOW_ALL || ($is_owner && $this->aclaccess == ACL_ALLOW_OWNER))
            return true;
        }
        return false;
    }
```

### While(List() = Each())

#### OpenEMR {#openemr-structures-whilelisteach}

`while(list()-=-each())`{.interpreted-text role="ref"}, in
library/report.inc:153.

The first while() is needed, to read the arbitrary long list returned by
the SQL query. The second list may be upgraded with a foreach, to read
both the key and the value. This is certainly faster to execute and to
read.

``` {.php}
function getInsuranceReport($pid, $type = primary)
{
    $sql = select * from insurance_data where pid=? and type=? order by date ASC;
    $res = sqlStatement($sql, array($pid, $type));
    while ($list = sqlFetchArray($res)) {
        while (list($key, $value) = each($list)) {
            if ($ret[$key]['content'] != $value && $ret[$key]['date'] < $list['date']) {
                $ret[$key]['content'] = $value;
                $ret[$key]['date'] = $list['date'];
            }
        }
    }

    return $ret;
}
```

------------------------------------------------------------------------

#### Dolphin {#dolphin-structures-whilelisteach}

`while(list()-=-each())`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/modules/boonex/forum/classes/Forum.php:1875.

This clever use of while() and list() is actually a foreach(\$a as \$r)
(the keys are ignored)

``` {.php}
function getRssUpdatedTopics ()
    {
        global $gConf;

        $this->_rssPrepareConf ();

        $a = $this->fdb->getRecentTopics (0);

        $items = '';
        $lastBuildDate = '';
        $ui = array();
        reset ($a);
        while ( list (,$r) = each ($a) ) {
            // acquire user info
            if (!isset($ui[$r['last_post_user']]) && ($aa = $this->_getUserInfoReadyArray ($r['last_post_user'], false)))
                $ui[$r['last_post_user']] = $aa;

            $td = orca_mb_replace('/#/', $r['count_posts'], '[L[# posts]]') . ' &#183; ' . orca_mb_replace('/#/', $ui[$r['last_post_user']]['title'], '[L[last reply by #]]') . ' &#183; ' . $r['cat_name'] . ' &#187; ' . $r['forum_title'];
```

### Several Instructions On The Same Line

#### Piwigo {#piwigo-structures-onelinetwoinstructions}

`several-instructions-on-the-same-line`{.interpreted-text role="ref"},
in tools/triggers\_list.php:993.

There are two instructions on the line with the if(). Note that the
condition is not followed by a bracketed block. When reviewing, it
really seems that echo \'\<br\>\' and \$f=0; are on the same block, but
the second is indeed an unconditional expression. This is very difficult
to spot.

``` {.php}
foreach ($trigger['files'] as $file)
      {
        if (!$f) echo '<br>'; $f=0;
        echo preg_replace('#\((.+)\)#', '(<i>$1</i>)', $file);
      }
```

------------------------------------------------------------------------

#### Tine20 {#tine20-structures-onelinetwoinstructions}

`several-instructions-on-the-same-line`{.interpreted-text role="ref"},
in tine20/Calendar/Controller/Event.php:1594.

Here, \$\_event-\>attendee is saved in a local variable, then the
property is destroyed. Same for \$\_event-\>notes; Strangely, a few
lines above, the properties are unset on their own line. Unsetting
properties leads to surprise bugs, and hidding the unset after ; makes
it harder to spot.

``` {.php}
$futurePersistentExceptionEvents->setRecurId($_event->getId());
                unset($_event->recurid);
                unset($_event->base_event_id);
                foreach(array('attendee', 'notes', 'alarms') as $prop) {
                    if ($_event->{$prop} instanceof Tinebase_Record_RecordSet) {
                        $_event->{$prop}->setId(NULL);
                    }
                }
                $_event->exdate = $futureExdates;

                $attendees = $_event->attendee; unset($_event->attendee);
                $note = $_event->notes; unset($_event->notes);
                $persistentExceptionEvent = $this->create($_event, $_checkBusyConflicts && $dtStartHasDiff);
```

### Multiples Identical Case

#### SugarCrm {#sugarcrm-structures-multipledefinedcase}

`multiples-identical-case`{.interpreted-text role="ref"}, in
modules/ModuleBuilder/MB/MBPackage.php:439.

It takes a while to find the double \'required\' case, but the executed
code is actually the same, so this is dead code at worst.

``` {.php}
switch ($col) {
    case 'custom_module':
        $installdefs['custom_fields'][$name]['module'] = $res;
        break;
    case 'required':
        $installdefs['custom_fields'][$name]['require_option'] = $res;
        break;
    case 'vname':
        $installdefs['custom_fields'][$name]['label'] = $res;
        break;
    case 'required':
        $installdefs['custom_fields'][$name]['require_option'] = $res;
        break;
    case 'massupdate':
        $installdefs['custom_fields'][$name]['mass_update'] = $res;
        break;
    case 'comments':
        $installdefs['custom_fields'][$name]['comments'] = $res;
        break;
    case 'help':
        $installdefs['custom_fields'][$name]['help'] = $res;
        break;
    case 'len':
        $installdefs['custom_fields'][$name]['max_size'] = $res;
        break;
    default:
        $installdefs['custom_fields'][$name][$col] = $res;
}//switch
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-structures-multipledefinedcase}

`multiples-identical-case`{.interpreted-text role="ref"}, in
ExpressionEngine\_Core2.9.2/system/expressionengine/controllers/cp/admin\_content.php:577.

\'deft\_status\' is doubled, with a fallthrough. This looks like some
forgotten copy/paste.

``` {.php}
switch ($key){
                                case 'cat_group':
                                    //PHP code
                                    break;
                                case 'status_group':
                                case 'field_group':
                                    //PHP code
                                    break;
                                case 'deft_status':
                                case 'deft_status':
                                    //PHP code
                                    break;
                                case 'search_excerpt':
                                    //PHP code
                                    break;
                                case 'deft_category':
                                    //PHP code
                                    break;
                                case 'blog_url':
                                case 'comment_url':
                                case 'search_results_url':
                                case 'rss_url':
                                    //PHP code
                                    break;
                                default :
                                    //PHP code
                                    break;
                            }
```

### Switch Without Default

#### Zencart {#zencart-structures-switchwithoutdefault}

`switch-without-default`{.interpreted-text role="ref"}, in
admin/tax\_rates.php:15.

The \'action\' is collected from \$\_GET and then, compared with various
strings to handle the different actions to be taken. The default
behavior is implicit here : if no \'action\', display the initial form
for taxes to be changed. This has to be understood as a general
philosophy of ZenCart project, or by reading the rest of the HTML code.
Adding a \'default\' case here would help understand what happens in
case \'action\' is absent or unrecognized.

``` {.php}
$action = (isset($_GET['action']) ? $_GET['action'] : '');

  if (zen_not_null($action)) {
    switch ($action) {
      case 'insert':
        // PHP code 
        break;
      case 'save':
        // PHP code 
        break;
      case 'deleteconfirm':
        // PHP code
        break;
    }
  }
?> .... HTML code
```

------------------------------------------------------------------------

#### Traq {#traq-structures-switchwithoutdefault}

`switch-without-default`{.interpreted-text role="ref"}, in
src/Helpers/Ticketlist.php:311.

The default case is actually processed after the switch, by the next
if/then structure. The structure deals with the customFields, while the
else deals with any unknown situations. This if/then could be wrapped in
the \'default\' case of switch, for consistent processing. The if/then
condition would be hard to use as a \'case\' (possible, though).

``` {.php}
public static function dataFor($column, $ticket)
    {
        switch ($column) {
            // Ticket ID column
            case 'ticket_id':
                return $ticket['ticket_id'];
                break;

            // Status column
            case 'status':
            case 'type':
            case 'component':
            case 'priority':
            case 'severity':
                return $ticket[{$column}_name];
                break;

            // Votes
            case 'votes':
                return $ticket['votes'];
                break;
        }

        // If we're still here, it may be a custom field
        if ($value = $ticket->customFieldValue($column)) {
            return $value->value;
        }

        // Nothing!
        return '';
    }
```

### \$this Belongs To Classes Or Traits

#### OpenEMR {#openemr-classes-thisisforclasses}

`$this-belongs-to-classes-or-traits`{.interpreted-text role="ref"}, in
ccr/display.php:24.

\$this is used to call the document\_upload\_download\_log() method,
although this piece of code is not part of a class, nor is included in a
class.

``` {.php}
<?php 
require_once(dirname(__FILE__) . "/../interface/globals.php");

$type = $_GET['type'];
$document_id = $_GET['doc_id'];
$d = new Document($document_id);
$url =  $d->get_url();
$storagemethod = $d->get_storagemethod();
$couch_docid = $d->get_couch_docid();
$couch_revid = $d->get_couch_revid();

if ($couch_docid && $couch_revid) {
    $couch = new CouchDB();
    $data = array($GLOBALS['couchdb_dbase'],$couch_docid);
    $resp = $couch->retrieve_doc($data);
    $xml = base64_decode($resp->data);
    if ($content=='' && $GLOBALS['couchdb_log']==1) {
        $log_content = date('Y-m-d H:i:s')." ==> Retrieving document\r\n";
        $log_content = date('Y-m-d H:i:s')." ==> URL: ".$url."\r\n";
        $log_content .= date('Y-m-d H:i:s')." ==> CouchDB Document Id: ".$couch_docid."\r\n";
        $log_content .= date('Y-m-d H:i:s')." ==> CouchDB Revision Id: ".$couch_revid."\r\n";
        $log_content .= date('Y-m-d H:i:s')." ==> Failed to fetch document content from CouchDB.\r\n";
        //$log_content .= date('Y-m-d H:i:s')." ==> Will try to download file from HardDisk if exists.\r\n\r\n";
        $this->document_upload_download_log($d->get_foreign_id(), $log_content);
        die(xlt("File retrieval from CouchDB failed"));
    }
```

### Nested Ternary

#### SPIP {#spip-structures-nestedternary}

`nested-ternary`{.interpreted-text role="ref"}, in
ecrire/inc/utils.php:2648.

Interesting usage of both if/then, for the flow control, and ternary,
for data process. Even on multiple lines, nested ternaries are quite
hard to read.

``` {.php}
// le script de l'espace prive
    // Mettre a "index.php" si DirectoryIndex ne le fait pas ou pb connexes:
    // les anciens IIS n'acceptent pas les POST sur ecrire/ (#419)
    // meme pb sur thttpd cf. http://forum.spip.net/fr_184153.html
    if (!defined('_SPIP_ECRIRE_SCRIPT')) {
        define('_SPIP_ECRIRE_SCRIPT', (empty($_SERVER['SERVER_SOFTWARE']) ? '' :
            preg_match(',IIS|thttpd,', $_SERVER['SERVER_SOFTWARE']) ?
                'index.php' : ''));
    }
```

------------------------------------------------------------------------

#### Zencart {#zencart-structures-nestedternary}

`nested-ternary`{.interpreted-text role="ref"}, in
app/library/zencart/ListingQueryAndOutput/src/formatters/TabularProduct.php:143.

No more than one level of nesting for this ternary call, yet it feels a
lot more, thanks to the usage of arrayed properties, constants, and
functioncalls.

``` {.php}
$lc_text .= '<br />' . (zen_get_show_product_switch($listing->fields['products_id'], 'ALWAYS_FREE_SHIPPING_IMAGE_SWITCH') ? (zen_get_product_is_always_free_shipping($listing->fields['products_id']) ? TEXT_PRODUCT_FREE_SHIPPING_ICON . '<br />' : '') : '');
```

### Non-constant Index In Array

#### Dolibarr {#dolibarr-arrays-nonconstantarray}

`non-constant-index-in-array`{.interpreted-text role="ref"}, in
htdocs/includes/OAuth/Common/Storage/DoliStorage.php:245.

The [state]{.title-ref} constant in the [\$result]{.title-ref} array is
coming from the SQL query. There is no need to make this a constant :
making it a string will remove some warnings in the logs.

``` {.php}
public function hasAuthorizationState($service)
    {
        // get state from db
        dol_syslog("get state from db");
        $sql = "SELECT state FROM ".MAIN_DB_PREFIX."oauth_state";
        $sql.= " WHERE service='".$this->db->escape($service)."'";
        $resql = $this->db->query($sql);
        $result = $this->db->fetch_array($resql);
        $states[$service] = $result[state];
        $this->states[$service] = $states[$service];

        return is_array($states)
        && isset($states[$service])
        && null !== $states[$service];
    }
```

------------------------------------------------------------------------

#### Zencart {#zencart-arrays-nonconstantarray}

`non-constant-index-in-array`{.interpreted-text role="ref"}, in
app/library/zencart/Services/src/LeadLanguagesRoutes.php:112.

The [fields]{.title-ref} constant in the [\$tableEntry]{.title-ref}
which holds a list of tables. It seems to be a SQL result, but it is
conveniently abstracted with
[\$this-\>listener-\>getTableList()]{.title-ref}, so we can\'t be sure.

``` {.php}
public function updateLanguageTables($insertId)
    {
        $tableList = $this->listener->getTableList();
        if (count($tableList) == 0) {
            return;
        }
        foreach ($tableList as $tableEntry) {
            $languageKeyField = issetorArray($tableEntry, 'languageKeyField', 'language_id');
            $sql = " INSERT IGNORE INTO :table: (";
            $sql = $this->dbConn->bindVars($sql, ':table:', $tableEntry ['table'], 'noquotestring');
            $sql .= $languageKeyField. ", ";
            $fieldNames = "";
            foreach ($tableEntry[fields] as $fieldName => $fieldType) {
                $fieldNames .= $fieldName . ", ";
            }
```

### Class, Interface Or Trait With Identical Names

#### shopware {#shopware-classes-citsamename}

`class,-interface-or-trait-with-identical-names`{.interpreted-text
role="ref"}, in
engine/Shopware/Components/Form/Interfaces/Element.php:30.

Most Element classes extends ModelEntity, which is an abstract class.
There is also an interface, called Element, for forms. And, last, one of
the class Element extends JsonSerializable, which is a PHP native
interface. Namespaces are definitely crucial to understand which Element
is which.

``` {.php}
interface Element { /**/ } // in engine/Shopware/Components/Form/Interfaces/Element.php:30

class Element implements \JsonSerializable { /**/ }     // in engine/Shopware/Bundle/EmotionBundle/Struct/Element.php:29

class Element extends ModelEntity { /**/ }  // in /engine/Shopware/Models/Document/Element.php:37
```

------------------------------------------------------------------------

#### NextCloud {#nextcloud-classes-citsamename}

`class,-interface-or-trait-with-identical-names`{.interpreted-text
role="ref"}, in lib/private/Files/Storage/Storage.php:33.

Interface Storage extends another Storage class. Here, the fully
qualified name is used, so we can understand which storage is which at
read time : a \'use\' alias would make this line more confusing.

``` {.php}
interface Storage extends \OCP\Files\Storage { /**/ }
```

### Empty Try Catch

#### LiveZilla {#livezilla-structures-emptytrycatch}

`empty-try-catch`{.interpreted-text role="ref"}, in
livezilla/\_lib/trdp/Zend/Mail/Protocol/Pop3.php:237.

This is an aptly commented empty try/catch : the emited exception is
extra check for a Zend Mail Protocol Exception. Hopefully, the
Zend\_Mail\_Protocol\_Exception only covers a already-closed situation.
Anyhow, this should be logged for later diagnostic.

``` {.php}
public function logout()
    {
        if (!$this->_socket) {
            return;
        }

        try {
            $this->request('QUIT');
        } catch (Zend_Mail_Protocol_Exception $e) {
            // ignore error - we're closing the socket anyway
        }

        fclose($this->_socket);
        $this->_socket = null;
    }
```

------------------------------------------------------------------------

#### Mautic {#mautic-structures-emptytrycatch}

`empty-try-catch`{.interpreted-text role="ref"}, in
app/bundles/ReportBundle/Model/ExportHandler.php:66.

Removing a file : if the file is not \'deleted\' by the method call, but
raises an error, it is hidden. When file destruction is impossible
because the file is already destroyed (or missing), this is well. If the
file couldn\'t be destroyed because of missing writing privileges,
hiding this error will have serious consequences.

``` {.php}
/**
     * @param string $fileName
     */
    public function removeFile($fileName)
    {
        try {
            $path = $this->getPath($fileName);
            $this->filePathResolver->delete($path);
        } catch (FileIOException $e) {
        }
    }
```

### Used Once Variables (In Scope)

#### shopware {#shopware-variables-variableusedoncebycontext}

`used-once-variables-(in-scope)`{.interpreted-text role="ref"}, in
\_sql/migrations/438-add-email-template-header-footer-fields.php:115.

In the updateEmailTemplate method, \$generatedQueries collects all the
generated SQL queries. \$generatedQueries is not initialized, and never
used after initialization.

``` {.php}
private function updateEmailTemplate($name, $content, $contentHtml = null)
    {
        $sql = <<<SQL
UPDATE `s_core_config_mails` SET `content` = "$content" WHERE `name` = "$name" AND dirty = 0
SQL;
        $this->addSql($sql);

        if ($contentHtml != null) {
            $sql = <<<SQL
UPDATE `s_core_config_mails` SET `content` = "$content", `contentHTML` = "$contentHtml" WHERE `name` = "$name" AND dirty = 0
SQL;
            $generatedQueries[] = $sql;
        }

        $this->addSql($sql);
    }
```

### Deprecated PHP Functions

#### Dolphin {#dolphin-php-deprecated}

`deprecated-php-functions`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/inc/classes/BxDolAdminSettings.php:270.

Split() was abandonned in PHP 7.0

``` {.php}
split(',', $aItem['extra']);
```

### Dangling Array References

#### Typo3 {#typo3-structures-danglingarrayreferences}

`dangling-array-references`{.interpreted-text role="ref"}, in
typo3/sysext/impexp/Classes/ImportExport.php:322.

foreach() reads \$lines into \$r, and augment those lines. By the end,
the \$r variable is not unset. Yet, several lines later, in the same
method but with different conditions, another loop reuse the variable
\$r. If is\_array(\$this-\>dat\[\'header\'\]\[\'pagetree\'\] and
is\_array(\$this-\>remainHeader\[\'records\'\]) are arrays at the same
moment, then both loops are called, and they share the same reference.
Values of the latter array will end up in the formar.

``` {.php}
if (is_array($this->dat['header']['pagetree'])) {
    reset($this->dat['header']['pagetree']);
    $lines = [];
    $this->traversePageTree($this->dat['header']['pagetree'], $lines);

    $viewData['dat'] = $this->dat;
    $viewData['update'] = $this->update;
    $viewData['showDiff'] = $this->showDiff;
    if (!empty($lines)) {
        foreach ($lines as &$r) {
            $r['controls'] = $this->renderControls($r);
            $r['fileSize'] = GeneralUtility::formatSize($r['size']);
            $r['message'] = ($r['msg'] && !$this->doesImport ? '<span class=text-danger>' . htmlspecialchars($r['msg']) . '</span>' : '');
        }
        $viewData['pagetreeLines'] = $lines;
    } else {
        $viewData['pagetreeLines'] = [];
    }
}
// Print remaining records that were not contained inside the page tree:
if (is_array($this->remainHeader['records'])) {
    $lines = [];
    if (is_array($this->remainHeader['records']['pages'])) {
        $this->traversePageRecords($this->remainHeader['records']['pages'], $lines);
    }
    $this->traverseAllRecords($this->remainHeader['records'], $lines);
    if (!empty($lines)) {
        foreach ($lines as &$r) {
            $r['controls'] = $this->renderControls($r);
            $r['fileSize'] = GeneralUtility::formatSize($r['size']);
            $r['message'] = ($r['msg'] && !$this->doesImport ? '<span class=text-danger>' . htmlspecialchars($r['msg']) . '</span>' : '');
        }
        $viewData['remainingRecords'] = $lines;
    }
}
```

------------------------------------------------------------------------

#### SugarCrm {#sugarcrm-structures-danglingarrayreferences}

`dangling-array-references`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/modules/Import/CsvAutoDetect.php:165.

There are two nested foreach here : they both have referenced blind
variables. The second one uses \$data, but never changes it. Yet, it is
reused the next round in the first loop, leading to pollution from the
first rows of \$this-\>\_parser-\>data into the lasts. This may happen
even if \$data is not modified explicitely : in fact, it will be
modified the next call to foreach(\$row as \...), for each element in
\$row.

``` {.php}
foreach ($this->_parser->data as &$row) {
    foreach ($row as &$data) {
        $len = strlen($data);
        // check if it begins and ends with single quotes
        // if it does, then it double quotes may not be the enclosure
        if ($len>=2 && $data[0] == " && $data[$len-1] == ") {
            $beginEndWithSingle = true;
            break;
        }
    }
    if ($beginEndWithSingle) {
        break;
    }
    $depth++;
    if ($depth > $this->_max_depth) {
        break;
    }
}
```

### Queries In Loops

#### TeamPass {#teampass-structures-queriesinloop}

`queries-in-loops`{.interpreted-text role="ref"}, in
install/install.queries.php:551.

The value is SELECTed first in the database, and it is INSERTed if not.
This may be done in one call in most databases.

``` {.php}
foreach ($aMiscVal as $elem) {
    //Check if exists before inserting
    $tmp = mysqli_num_rows(
        mysqli_query(
            $dbTmp,
            SELECT * FROM `.$var['tbl_prefix'].misc`
            WHERE type='.$elem[0].' AND intitule='.$elem[1].'
        )
    );
    if (intval($tmp) === 0) {
        $queryRes = mysqli_query(
            $dbTmp,
            INSERT INTO `.$var['tbl_prefix'].misc`
            (`type`, `intitule`, `valeur`) VALUES
            ('.$elem[0].', '.$elem[1].', '.
            str_replace(', , $elem[2]).');
        ); // or die(mysqli_error($dbTmp))
    }

    // append new setting in config file
    $config_text .= '.$elem[1].' => '.str_replace(', , $elem[2]).',;
                        }
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-structures-queriesinloop}

`queries-in-loops`{.interpreted-text role="ref"}, in
contrib/util/deidentification/deidentification.php:287.

The value is SELECTed first in the database, and it is INSERTed if not.
This may be done in one call in most databases.

``` {.php}
$query = select * from facility;
$result = mysqli_query($con, $query);
while ($row = mysqli_fetch_array($result)) {
    $string = update facility set 

          `name`    = 'Facility_{$row['id']}',
          `phone`   = '(000) 000-0000'

        where `id` = {$row['id']};

    mysqli_query($con, $string) or print Error altering facility table \n;
    $string = '';
}
```

### Aliases Usage

#### Cleverstyle {#cleverstyle-functions-aliasesusage}

`aliases-usage`{.interpreted-text role="ref"}, in
modules/HybridAuth/Hybrid/thirdparty/Vimeo/Vimeo.php:422.

is\_writeable() should be written is\_writable(). No extra \'e\'.

``` {.php}
is_writeable($chunk_temp_dir)
```

------------------------------------------------------------------------

#### phpMyAdmin {#phpmyadmin-functions-aliasesusage}

`aliases-usage`{.interpreted-text role="ref"}, in
libraries/classes/Server/Privileges.php:5064.

join() should be written implode()

``` {.php}
join('`, `', $tmp_privs2['Update'])
```

### Var Keyword

#### xataface {#xataface-classes-oldstylevar}

`var-keyword`{.interpreted-text role="ref"}, in
SQL/Parser/wrapper.php:24.

With the usage of var and a first method bearing the name of the class,
this is PHP 4 code that is still in use.

``` {.php}
class SQL_Parser_wrapper {

    var $_data;
    var $_tableLookup;
    var $_parser;

    function SQL_Parser_wrapper(&$data, $dialect='MySQL'){
```

### Wrong Number Of Arguments

#### xataface {#xataface-functions-wrongnumberofarguments}

`wrong-number-of-arguments`{.interpreted-text role="ref"}, in
actions/existing\_related\_record.php:130.

df\_display() actually requires only 2 arguments, while three are
provided. The last argument is completely ignored. df\_display() is
called in a total of 9 places : this now looks like an API change that
left many calls untouched.

``` {.php}
df_display($context, $template, true);

// in public-api.php :
function df_display($context, $template_name){
    import( 'Dataface/SkinTool.php');
    $st = Dataface_SkinTool::getInstance();

    return $st->display($context, $template_name);
}
```

### Undefined static:: Or self::

#### xataface {#xataface-classes-undefinedstaticmp}

`undefined-static\:\:-or-self\:\:`{.interpreted-text role="ref"}, in
actions/forgot\_password.php:194.

This is probably a typo, since the property called public static
\$EX\_NO\_USERS\_WITH\_EMAIL = 501; is defined in that class.

``` {.php}
if ( !$user ) throw new Exception(df_translate('actions.forgot_password.null_user',"Cannot send email for null user"), self::$EX_NO_USERS_FOUND_WITH_EMAIL);
```

------------------------------------------------------------------------

#### SugarCrm {#sugarcrm-classes-undefinedstaticmp}

`undefined-static\:\:-or-self\:\:`{.interpreted-text role="ref"}, in
code/SugarCE-Full-6.5.26/include/SugarDateTime.php:574.

self::\$sugar\_strptime\_long\_mon refers to the current class, which
extends DateTime. No static property was defined at either of them, with
the name \'\$sugar\_strptime\_long\_mon\'. This has been a Fatal error
at execution time since PHP 5.3, at least.

``` {.php}
if ( isset($regexp['positions']['F']) && !empty($dateparts[$regexp['positions']['F']])) {
               // FIXME: locale?
    $mon = $dateparts[$regexp['positions']['F']];
    if(isset(self::$sugar_strptime_long_mon[$mon])) {
        $data["tm_mon"] = self::$sugar_strptime_long_mon[$mon];
    } else {
        return false;
    }
}
```

### list() May Omit Variables

#### OpenConf {#openconf-structures-listomissions}

`list()-may-omit-variables`{.interpreted-text role="ref"}, in
openconf/author/privacy.php:29.

The first variable in the list(), \$none, isn\'t reused anywhere in the
script. In fact, its name convey the meaning that is it useless, but is
in the array nonetheless.

``` {.php}
list($none, $OC_privacy_policy) = oc_getTemplate('privacy_policy');
```

------------------------------------------------------------------------

#### FuelCMS {#fuelcms-structures-listomissions}

`list()-may-omit-variables`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

\$a is never reused again. \$b, on the other hand is. Not assigning any
value to \$a saves some memory, and avoid polluting the local variable
space.

``` {.php}
list($b, $a) = array(reset($params->me), key($params->me));
```

### Or Die

#### Tine20 {#tine20-structures-ordie}

`or-die`{.interpreted-text role="ref"}, in scripts/addgrant.php:34.

Typical error handling, which also displays the MySQL error message, and
leaks informations about the system. One may also note that
mysql\_connect is not supported anymore, and was replaced with mysqli
and pdo : this may be a backward compatibile file.

``` {.php}
$link = mysql_connect($host, $user, $pass) or die("No connection: " . mysql_error( ))
```

------------------------------------------------------------------------

#### OpenConf {#openconf-structures-ordie}

`or-die`{.interpreted-text role="ref"}, in
openconf/chair/export.inc:143.

or die() is also applied to many situations, where a blocking situation
arise. Here, with the creation of a temporary file.

``` {.php}
$coreFile = tempnam('/tmp/', 'ocexport') or die('could not generate Excel file (6)')
```

### Use const

#### phpMyAdmin {#phpmyadmin-constants-constrecommended}

`use-const`{.interpreted-text role="ref"}, in error\_report.php:17.

This may be turned into a [const]{.title-ref} call, with a static
expression.

``` {.php}
define('ROOT_PATH', __DIR__ . DIRECTORY_SEPARATOR)
```

------------------------------------------------------------------------

#### Piwigo {#piwigo-constants-constrecommended}

`use-const`{.interpreted-text role="ref"}, in
include/functions\_plugins.inc.php:32.

Const works efficiently with literal

``` {.php}
define('EVENT_HANDLER_PRIORITY_NEUTRAL', 50)
```

### Written Only Variables

#### Dolibarr {#dolibarr-variables-writtenonlyvariable}

`written-only-variables`{.interpreted-text role="ref"}, in
htdocs/ecm/class/ecmdirectory.class.php:692.

\$val is only written, as only the keys are used. \$val may be skipped
by applying the foreach to array\_keys(\$this-\>cats), instead of the
whole array.

``` {.php}
// We add properties fullxxx to all elements
        foreach($this->cats as $key => $val)
        {
            if (isset($motherof[$key])) continue;
            $this->build_path_from_id_categ($key, 0);
        }
```

------------------------------------------------------------------------

#### SuiteCrm {#suitecrm-variables-writtenonlyvariable}

`written-only-variables`{.interpreted-text role="ref"}, in
modules/Campaigns/utils.php:820.

\$email\_health is used later in the method; while \$email\_components
is only set, and never used.

``` {.php}
//run query for mail boxes of type 'bounce'
        $email_health = 0;
        $email_components = 2;
        $mbox_qry = "select * from inbound_email where deleted ='0' and mailbox_type = 'bounce'";
        $mbox_res = $focus->db->query($mbox_qry);

        $mbox = array();
        while ($mbox_row = $focus->db->fetchByAssoc($mbox_res)) {
            $mbox[] = $mbox_row;
        }
```

### Foreach Reference Is Not Modified

#### Dolibarr {#dolibarr-structures-foreachreferenceisnotmodified}

`foreach-reference-is-not-modified`{.interpreted-text role="ref"}, in
htdocs/product/reassort.php:364.

\$wh is an array, and is read for its index \'id\', but it is not
modified. The reference sign is too much.

``` {.php}
if($nb_warehouse>1) {
    foreach($warehouses_list as &$wh) {

        print '<td class=right>';
        print empty($product->stock_warehouse[$wh['id']]->real) ? '0' : $product->stock_warehouse[$wh['id']]->real;
        print '</td>';
    }
}
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-structures-foreachreferenceisnotmodified}

`foreach-reference-is-not-modified`{.interpreted-text role="ref"}, in
applications/vanilla/models/class.discussionmodel.php:944.

\$discussion is also an object : it doesn\'t need any reference to be
modified. And, it is not modified, but only read.

``` {.php}
foreach ($result as $key => &$discussion) {
    if (isset($this->_AnnouncementIDs)) {
        if (in_array($discussion->DiscussionID, $this->_AnnouncementIDs)) {
            unset($result[$key]);
            $unset = true;
        }
    } elseif ($discussion->Announce && $discussion->Dismissed == 0) {
        // Unset discussions that are announced and not dismissed
        unset($result[$key]);
        $unset = true;
    }
}
```

### Useless Return

#### ThinkPHP {#thinkphp-functions-uselessreturn}

`useless-return`{.interpreted-text role="ref"}, in
library/think/Request.php:2121.

``` {.php}
public function __set($name, $value)
    {
        return $this->param[$name] = $value;
    }
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-functions-uselessreturn}

`useless-return`{.interpreted-text role="ref"}, in
applications/dashboard/views/attachments/attachment.php:14.

The final \'return\' is useless : return void (here, return without
argument), is the same as returning null, unless the \'void\' return
type is used. The other return, is in the two conditions, is important
to skip the end of the functioncall.

``` {.php}
function writeAttachment($attachment) {

        $customMethod = AttachmentModel::getWriteAttachmentMethodName($attachment['Type']);
        if (function_exists($customMethod)) {
            if (val('Error', $attachment)) {
                writeErrorAttachment($attachment);
                return;
            }
            $customMethod($attachment);
        } else {
            trace($customMethod, 'Write Attachment method not found');
            trace($attachment, 'Attachment');
        }
        return;
    }
```

### Unpreprocessed Values

#### Zurmo {#zurmo-structures-unpreprocessed}

`unpreprocessed-values`{.interpreted-text role="ref"}, in
app/protected/core/utils/ZurmoTranslationServerUtil.php:79.

It seems that a simple concatenation could be used here. There is
another call to this expression in the code, and a third that uses
\'PATCH\_VERSION\' on top of the two others.

``` {.php}
join('.', array(MAJOR_VERSION, MINOR_VERSION))
```

------------------------------------------------------------------------

#### Piwigo {#piwigo-structures-unpreprocessed}

`unpreprocessed-values`{.interpreted-text role="ref"}, in
include/random\_compat/random.php:34.

PHP\_VERSION is actually build with PHP\_MAJOR\_VERSION,
PHP\_MINOR\_VERSION and PHP\_RELEASE\_VERSION. There is also a compact
version : PHP\_VERSION\_ID

``` {.php}
explode('.', PHP_VERSION);
```

### Undefined Properties

#### WordPress {#wordpress-classes-undefinedproperty}

`undefined-properties`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

Properties are not defined, but they are thoroughly initialized when the
XML document is parsed. All those definition should be in a property
definition, for clear documentation.

``` {.php}
$this->DeliveryLine1 = '';
        $this->DeliveryLine2 = '';
        $this->City = '';
        $this->State = '';
        $this->ZipAddon = '';
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-classes-undefinedproperty}

`undefined-properties`{.interpreted-text role="ref"}, in
includes/logging/LogFormatter.php:561.

parsedParametersDeleteLog is an undefined property. Defining the
property with a null default value is important here, to keep the code
running.

``` {.php}
protected function getMessageParameters() {
        if ( isset( $this->parsedParametersDeleteLog ) ) {
            return $this->parsedParametersDeleteLog;
        }
```

### Strict Comparison With Booleans

#### Phinx {#phinx-structures-booleanstrictcomparison}

`strict-comparison-with-booleans`{.interpreted-text role="ref"}, in
src/Phinx/Db/Adapter/MysqlAdapter.php:1131.

[ìsNull( )]{.title-ref}[ always returns a boolean : it may be only be
]{.title-ref}[true]{.title-ref}[ or ]{.title-ref}[false]{.title-ref}\`.
Until typehinted properties or return typehint are used, isNull() may
return anything else.

``` {.php}
$column->isNull( ) == false
```

------------------------------------------------------------------------

#### Typo3 {#typo3-structures-booleanstrictcomparison}

`strict-comparison-with-booleans`{.interpreted-text role="ref"}, in
typo3/sysext/lowlevel/Classes/Command/FilesWithMultipleReferencesCommand.php:90.

When `dry-run` is not defined, the getOption() method actually returns a
`null` value. So, comparing the result of getOption() to false is
actually wrong : using a constant to prevent values to be inconsistent
is recommended here.

``` {.php}
$input->getOption('dry-run') != false
```

### Lone Blocks

#### ThinkPHP {#thinkphp-structures-loneblock}

`lone-blocks`{.interpreted-text role="ref"}, in
ThinkPHP/Library/Vendor/Hprose/HproseReader.php:163.

There is no need for block in a case/default clause. PHP executes all
command in order, until a break or the end of the switch. There is
another occurrence of that situation in this code : it seems to be a
coding convention, while only applied to a few switch statements.

``` {.php}
for ($i = 0; $i < $len; ++$i) {
            switch (ord($this->stream->getc()) >> 4) {
                case 0:
                case 1:
                case 2:
                case 3:
                case 4:
                case 5:
                case 6:
                case 7: {
                    // 0xxx xxxx
                    $utf8len++;
                    break;
                }
                case 12:
                case 13: {
                    // 110x xxxx   10xx xxxx
                    $this->stream->skip(1);
                    $utf8len += 2;
                    break;
                }
```

------------------------------------------------------------------------

#### Tine20 {#tine20-structures-loneblock}

`lone-blocks`{.interpreted-text role="ref"}, in
tine20/Addressbook/Convert/Contact/VCard/Abstract.php:199.

A case of empty case, with empty blocks. This is useless code. Event the
curly brackets with the final case are useless.

``` {.php}
switch ( $property['TYPE'] ) {
                        case 'JPG' : {}
                        case 'jpg' : {}
                        case 'Jpg' : {}
                        case 'Jpeg' : {}
                        case 'jpeg' : {}
                        case 'PNG' : {}
                        case 'png' : {}
                        case 'JPEG' : {
                            if (Tinebase_Core::isLogLevel(Zend_Log::DEBUG)) 
                                Tinebase_Core::getLogger()->warn(__METHOD__ . '::' . __LINE__ . ' Photo: passing on invalid ' . $property['TYPE'] . ' image as is (' . strlen($property->getValue()) .')' );
                            $jpegphoto = $property->getValue();
                            break;
                        }
```

### PHP Keywords As Names

#### ChurchCRM {#churchcrm-php-reservednames}

`php-keywords-as-names`{.interpreted-text role="ref"}, in
src/kiosk/index.php:42.

\$false may be true or false (or else\...). In fact, the variable is not
even defined in this file, and the file do a lot of inclusion.

``` {.php}
if (!isset($_COOKIE['kioskCookie'])) {
    if ($windowOpen) {
        $guid = uniqid();
        setcookie("kioskCookie", $guid, 2147483647);
        $Kiosk = new \ChurchCRM\KioskDevice();
        $Kiosk->setGUIDHash(hash('sha256', $guid));
        $Kiosk->setAccepted($false);
        $Kiosk->save();
    } else {
        header("HTTP/1.1 401 Unauthorized");
        exit;
    }
}
```

------------------------------------------------------------------------

#### xataface {#xataface-php-reservednames}

`php-keywords-as-names`{.interpreted-text role="ref"}, in
Dataface/Record.php:1278.

This one is documented, and in the end, makes a lot of sense.

``` {.php}
function &getRelatedRecord($relationshipName, $index=0, $where=0, $sort=0){
        if ( isset($this->cache[__FUNCTION__][$relationshipName][$index][$where][$sort]) ){
            return $this->cache[__FUNCTION__][$relationshipName][$index][$where][$sort];
        }
        $it = $this->getRelationshipIterator($relationshipName, $index, 1, $where, $sort);
        if ( $it->hasNext() ){
            $rec =& $it->next();
            $this->cache[__FUNCTION__][$relationshipName][$index][$where][$sort] =& $rec;
            return $rec;
        } else {
            $null = null;   // stupid hack because literal 'null' can't be returned by ref.
            return $null;
        }
    }
```

### Could Use self

#### WordPress {#wordpress-classes-shoulduseself}

`could-use-self`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

Securimage could be called self.

``` {.php}
class Securimage 
{
// Lots of code
            Securimage::$_captchaId = $id;
}
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-classes-shoulduseself}

`could-use-self`{.interpreted-text role="ref"}, in
livezilla/\_lib/objects.global.users.inc.php:1599.

Using self makes it obvious that Operator::GetSystemId() is a local
call, while Communication::GetParameter() is external.

``` {.php}
class Operator extends BaseUser 
{
    static function ReadParams()
    {
        if(!empty($_POST[POST_EXTERN_REQUESTED_INTERNID]))
            return Communication::GetParameter(POST_EXTERN_REQUESTED_INTERNID,,$c,FILTER_SANITIZE_SPECIAL_CHARS,null,32);
        else if(!empty($_GET[operator]))
        {
            $userid = Communication::GetParameter(operator,,$c,FILTER_SANITIZE_SPECIAL_CHARS,null,32,false,false);
            $sysid = Operator::GetSystemId($userid);
}
```

### Logical Should Use Symbolic Operators

#### Cleverstyle {#cleverstyle-php-logicalinletters}

`logical-should-use-symbolic-operators`{.interpreted-text role="ref"},
in modules/Uploader/Mime/Mime.php:171.

\$extension is assigned with the results of pathinfo(\$reference\_name,
PATHINFO\_EXTENSION) and ignores static::hasExtension(\$extension). The
same expression, placed in a condition (like an if), would assign a
value to \$extension and use another for the condition itself. Here,
this code is only an expression in the flow.

``` {.php}
$extension = pathinfo($reference_name, PATHINFO_EXTENSION) and static::hasExtension($extension);
```

------------------------------------------------------------------------

#### OpenConf {#openconf-php-logicalinletters}

`logical-should-use-symbolic-operators`{.interpreted-text role="ref"},
in chair/export.inc:143.

In this context, the priority of execution is used on purpose;
\$coreFile only collect the temporary name of the export file, and when
this name is empty, then the second operand of OR is executed, though
never collected. Since this second argument is a \'die\', its return
value is lost, but the initial assignation is never used anyway.

``` {.php}
$coreFile = tempnam('/tmp/', 'ocexport') or die('could not generate Excel file (6)')
```

### Catch Overwrite Variable

#### PhpIPAM {#phpipam-structures-catchshadowsvariable}

`catch-overwrite-variable`{.interpreted-text role="ref"}, in
app/subnets/scan/subnet-scan-snmp-route.php:58.

\$e is used both as \'local\' variable : it is local to the catch
clause, and it is a blind variable in a foreach(). There is little
overlap between the two occurrences, but one reader may wonder why the
caught exception is shown later on.

``` {.php}
try {
        $res = $Snmp->get_query(get_routing_table);
        // remove those not in subnet
        if (sizeof($res)>0) {
           // save for debug
           $debug[$d->hostname][$q] = $res;

           // save result
           $found[$d->id][$q] = $res;
        }
    } catch (Exception $e) {
       // save for debug
       $debug[$d->hostname][$q] = $res;
       $errors[] = $e->getMessage();
    }

// lots of code
// on line 132
    // print errors
    if (isset($errors)) {
        print <hr>;
        foreach ($errors as $e) {
            print $Result->show (warning, $e, false, false, true);
        }
    }
```

------------------------------------------------------------------------

#### SuiteCrm {#suitecrm-structures-catchshadowsvariable}

`catch-overwrite-variable`{.interpreted-text role="ref"}, in
modules/Emails/EmailUIAjax.php:1082.

\$e starts as an Email(), in the \'getMultipleMessagesFromSugar\' case,
while a few lines later, in \'refreshSugarFolders\', \$e is now an
exception. Breaks are in place, so both occurrences are separated, yet,
one may wonder why an email is a warning, or a mail is a warning.

``` {.php}
// On line 900, $e is a Email
        case getMultipleMessagesFromSugar:
            $GLOBALS['log']->debug(********** EMAIL 2.0 - Asynchronous - at: getMultipleMessagesFromSugar);
            if (isset($_REQUEST['uid']) && !empty($_REQUEST['uid'])) {
                $exIds = explode(,, $_REQUEST['uid']);
                $out = array();

                foreach ($exIds as $id) {
                    $e = new Email();
                    $e->retrieve($id);
                    $e->description_html = from_html($e->description_html);
                    $ie->email = $e;
                    $out[] = $ie->displayOneEmail($id, $_REQUEST['mbox']);
                }

                echo $json->encode($out);
            }

            break;


// lots of code
// on line 1082
        case refreshSugarFolders:
            try {
                $GLOBALS['log']->debug(********** EMAIL 2.0 - Asynchronous - at: refreshSugarFolders);
                $rootNode = new ExtNode('', '');
                $folderOpenState = $current_user->getPreference('folderOpenState', 'Emails');
                $folderOpenState = (empty($folderOpenState)) ?  : $folderOpenState;
                $ret = $email->et->folder->getUserFolders(
                    $rootNode,
                    sugar_unserialize($folderOpenState),
                    $current_user,
                    true
                );
                $out = $json->encode($ret);
                echo $out;
            } catch (SugarFolderEmptyException $e) {
                $GLOBALS['log']->warn($e);
                $out = $json->encode(array(
                    'message' => 'No folder selected warning message here...',
                ));
                echo $out;
            }
            break;
```

### Deep Definitions

#### Dolphin {#dolphin-functions-deepdefinitions}

`deep-definitions`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

The ConstructHiddenValues function builds the ConstructHiddenSubValues
function. Thus, ConstructHiddenValues can only be called once.

``` {.php}
function ConstructHiddenValues($Values)
{
    /**
     *    Recursive function, processes multidimensional arrays
     *
     * @param string $Name  Full name of array, including all subarrays' names
     *
     * @param array  $Value Array of values, can be multidimensional
     *
     * @return string    Properly consctructed <input type="hidden"...> tags
     */
    function ConstructHiddenSubValues($Name, $Value)
    {
        if (is_array($Value)) {
            $Result = "";
            foreach ($Value as $KeyName => $SubValue) {
                $Result .= ConstructHiddenSubValues("{$Name}[{$KeyName}]", $SubValue);
            }
        } else // Exit recurse
        {
            $Result = "<input type=\"hidden\" name=\"" . htmlspecialchars($Name) . "\" value=\"" . htmlspecialchars($Value) . "\" />\n";
        }

        return $Result;
    }

    /* End of ConstructHiddenSubValues function */

    $Result = '';
    if (is_array($Values)) {
        foreach ($Values as $KeyName => $Value) {
            $Result .= ConstructHiddenSubValues($KeyName, $Value);
        }
    }

    return $Result;
}
```

### Repeated print()

#### Edusoho {#edusoho-structures-repeatedprint}

`repeated-print()`{.interpreted-text role="ref"}, in app/check.php:71.

All echo may be merged into one : do this by turning the ; and . into
\',\', and removing the superfluous echo. Also, echo\_style may be
turned into a non-display function, returning the build style, rather
than echoing it to the output.

``` {.php}
echo PHP_EOL;
echo_style('title', 'Note');
echo '  The command console could use a different php.ini file'.PHP_EOL;
echo_style('title', '~~~~');
echo '  than the one used with your web server. To be on the'.PHP_EOL;
echo '      safe side, please check the requirements from your web'.PHP_EOL;
echo '      server using the ';
echo_style('yellow', 'web/config.php');
echo ' script.'.PHP_EOL;
echo PHP_EOL;
```

------------------------------------------------------------------------

#### HuMo-Gen {#humo-gen-structures-repeatedprint}

`repeated-print()`{.interpreted-text role="ref"}, in menu.php:71.

Simply calling print once is better than three times. Here too, echo
usage would reduce the amount of memory allocation due to concatenation
prior display.

``` {.php}
print '<input type=text name=quicksearch value=.$quicksearch. size=10 '.$pattern.' title=.__(Minimum:).$min_chars.__(characters).>';
            print ' <input type=submit value=.__(Search).>';
        print </form>;
```

### Objects Don\'t Need References

#### Zencart {#zencart-structures-objectreferences}

`objects-don't-need-references`{.interpreted-text role="ref"}, in
includes/library/illuminate/support/helpers.php:484.

No need for & operator when \$class is only used for a method call.

``` {.php}
/**
     * @param $class
     * @param $eventID
     * @param array $paramsArray
     */
    public function updateNotifyCheckoutflowFinishedManageSuccessOrderLinkEnd(&$class, $eventID, $paramsArray = array())
    {
        $class->getView()->getTplVarManager()->se('flag_show_order_link', false);
    }
```

------------------------------------------------------------------------

#### XOOPS {#xoops-structures-objectreferences}

`objects-don't-need-references`{.interpreted-text role="ref"}, in
htdocs/class/theme\_blocks.phps:221.

Here, \$template is modified, when its properties are modified. When
only the properties are modified, or read, then & is not necessary.

``` {.php}
public function buildBlock($xobject, &$template)
    {
        // The lame type workaround will change
        // bid is added temporarily as workaround for specific block manipulation
        $block = array(
            'id'      => $xobject->getVar('bid'),
            'module'  => $xobject->getVar('dirname'),
            'title'   => $xobject->getVar('title'),
            // 'name'        => strtolower( preg_replace( '/[^0-9a-zA-Z_]/', '', str_replace( ' ', '_', $xobject->getVar( 'name' ) ) ) ),
            'weight'  => $xobject->getVar('weight'),
            'lastmod' => $xobject->getVar('last_modified'));

        $bcachetime = (int)$xobject->getVar('bcachetime');
        if (empty($bcachetime)) {
            $template->caching = 0;
        } else {
            $template->caching        = 2;
            $template->cache_lifetime = $bcachetime;
        }
        $template->setCompileId($xobject->getVar('dirname', 'n'));
        $tplName = ($tplName = $xobject->getVar('template')) ? db:$tplName : 'db:system_block_dummy.tpl';
        $cacheid = $this->generateCacheId('blk_' . $xobject->getVar('bid'));
// more code to the end of the method
```

### Lost References

#### WordPress {#wordpress-variables-lostreferences}

`lost-references`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### Never Used Properties

#### WordPress {#wordpress-classes-propertyneverused}

`never-used-properties`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### No Real Comparison

#### Magento {#magento-type-norealcomparison}

`no-real-comparison`{.interpreted-text role="ref"}, in
app/code/core/Mage/XmlConnect/Block/Catalog/Product/Options/Configurable.php:74.

Compare prices and physical quantities with a difference, so as to avoid
rounding errors.

``` {.php}
if ((float)$option['price'] != 0.00) {
                        $valueNode->addAttribute('price', $option['price']);
                        $valueNode->addAttribute('formated_price', $option['formated_price']);
                    }
```

------------------------------------------------------------------------

#### SPIP {#spip-type-norealcomparison}

`no-real-comparison`{.interpreted-text role="ref"}, in
ecrire/maj/v017.php:37.

Here, the current version number is stored as a real number. With a
string, though a longer value, it may be compared using the
version\_compare() function.

``` {.php}
$version_installee == 1.701
```

### Unused Global

#### Dolphin {#dolphin-structures-unusedglobal}

`unused-global`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/modules/boonex/forum/classes/DbForum.php:548.

\$gConf is not used in this method, and may be safely avoided.

``` {.php}
function getUserPostsList ($user, $sort, $limit = 10)
    {
        global $gConf;

        switch ($sort) {
            case 'top':
                $order_by = " t1.`votes` DESC ";
                break;
            case 'rnd':
                $order_by = " RAND() ";
                break;
            default:
                $order_by = " t1.`when` DESC ";
        }

        $sql =  " 
        SELECT t1.`forum_id`, t1.`topic_id`, t2.`topic_uri`, t2.`topic_title`, t1.`post_id`, t1.`user`, `post_text`, t1.`when`
            FROM " . TF_FORUM_POST . " AS t1
        INNER JOIN " . TF_FORUM_TOPIC . " AS t2
            ON (t1.`topic_id` = t2.`topic_id`)
        WHERE  t1.`user` = '$user' AND `t2`.`topic_hidden` = '0'
        ORDER BY " . $order_by . " 
        LIMIT $limit";

        $a = $this->getAll ($sql);
        $this->_cutPostText($a);
        return $a;
    }
```

### Useless Global

#### Zencart {#zencart-structures-uselessglobal}

`useless-global`{.interpreted-text role="ref"}, in
admin/includes/modules/newsletters/newsletter.php:25.

\$\_GET is always a global variable. There is no need to declare it
global in any scope.

``` {.php}
function choose_audience() {
        global $_GET;
```

------------------------------------------------------------------------

#### HuMo-Gen {#humo-gen-structures-uselessglobal}

`useless-global`{.interpreted-text role="ref"}, in relations.php:332.

It is hard to spot that \$generY is useless, but this is the only
occurrence where \$generY is refered to as a global. It is not accessed
anywhere else as a global (there are occurrences of \$generY being an
argument), and it is not even assigned within that function.

``` {.php}
function calculate_ancestor($pers) {
    global $db_functions, $reltext, $sexe, $sexe2, $spouse, $special_spouseY, $language, $ancestortext, $dutchtext, $selected_language, $spantext, $generY, $foundY_nr, $rel_arrayY;
```

### Preprocessable

#### phpadsnew {#phpadsnew-structures-shouldpreprocess}

`preprocessable`{.interpreted-text role="ref"}, in
phpAdsNew-2.0/adview.php:302.

Each call to chr() may be done before. First, chr() may be replace with
the hexadecimal sequence \"0x3B\"; Secondly, 0x3b is a rather long
replacement for a simple semi-colon. The whole pragraph could be stored
in a separate file, for easier modifications.

``` {.php}
echo chr(0x47).chr(0x49).chr(0x46).chr(0x38).chr(0x39).chr(0x61).chr(0x01).chr(0x00).
             chr(0x01).chr(0x00).chr(0x80).chr(0x00).chr(0x00).chr(0x04).chr(0x02).chr(0x04).
             chr(0x00).chr(0x00).chr(0x00).chr(0x21).chr(0xF9).chr(0x04).chr(0x01).chr(0x00).
             chr(0x00).chr(0x00).chr(0x00).chr(0x2C).chr(0x00).chr(0x00).chr(0x00).chr(0x00).
             chr(0x01).chr(0x00).chr(0x01).chr(0x00).chr(0x00).chr(0x02).chr(0x02).chr(0x44).
             chr(0x01).chr(0x00).chr(0x3B);
```

### Useless Unset

#### Tine20 {#tine20-structures-uselessunset}

`useless-unset`{.interpreted-text role="ref"}, in
tine20/Felamimail/Controller/Message.php:542.

\$\_rawContent is unset after being sent to the stream. The variable is
a parameter, and will be freed at the end of the call of the method. No
need to do it explicitly.

``` {.php}
protected function _createMimePart($_rawContent, $_partStructure)
    {
        if (Tinebase_Core::isLogLevel(Zend_Log::TRACE)) Tinebase_Core::getLogger()->trace(__METHOD__ . '::' . __LINE__ . ' Content: ' . $_rawContent);

        $stream = fopen(php://temp, 'r+');
        fputs($stream, $_rawContent);
        rewind($stream);

        unset($_rawContent);
        //..... More code, no usage of $_rawContent
    }
```

------------------------------------------------------------------------

#### Typo3 {#typo3-structures-uselessunset}

`useless-unset`{.interpreted-text role="ref"}, in
typo3/sysext/frontend/Classes/Page/PageRepository.php:708.

\$row is unset under certain conditions : here, we can read it in the
comments. Eventually, the \$row will be returned, and turned into a
NULL, by default. This will also create a notice in the logs. Here, the
best would be to set a null value, instead of unsetting the variable.

``` {.php}
public function getRecordOverlay($table, $row, $sys_language_content, $OLmode = '')
    {
//....  a lot more code, with usage of $row, and several unset($row)
//...... Reduced for simplicity
                    } else {
                        // When default language is displayed, we never want to return a record carrying
                        // another language!
                        if ($row[$GLOBALS['TCA'][$table]['ctrl']['languageField']] > 0) {
                            unset($row);
                        }
                    }
                }
            }
        }
        foreach ($GLOBALS['TYPO3_CONF_VARS']['SC_OPTIONS']['t3lib/class.t3lib_page.php']['getRecordOverlay'] ?? [] as $className) {
            $hookObject = GeneralUtility::makeInstance($className);
            if (!$hookObject instanceof PageRepositoryGetRecordOverlayHookInterface) {
                throw new \UnexpectedValueException($className . ' must implement interface ' . PageRepositoryGetRecordOverlayHookInterface::class, 1269881659);
            }
            $hookObject->getRecordOverlay_postProcess($table, $row, $sys_language_content, $OLmode, $this);
        }
        return $row;
    }
```

### Buried Assignation

#### XOOPS {#xoops-structures-buriedassignation}

`buried-assignation`{.interpreted-text role="ref"}, in
htdocs/image.php:170.

Classic iffectation : the condition also collects the needed value to
process the drawing. This is very common in PHP, and the Yoda condition,
with its constant on the left, shows that extra steps were taken to
strengthen that piece of code.

``` {.php}
if (0 < ($radius = $radii[2] * $q)) { // left bottom
        imagearc($workingImage, $radius - 1, $workingHeight - $radius, $radius * 2, $radius * 2, 90, 180, $alphaColor);
        imagefilltoborder($workingImage, 0, $workingHeight - 1, $alphaColor, $alphaColor);
    }
```

------------------------------------------------------------------------

#### Mautic {#mautic-structures-buriedassignation}

`buried-assignation`{.interpreted-text role="ref"}, in
app/bundles/CoreBundle/Controller/ThemeController.php:47.

The setting of the variable \$cancelled is fairly hidden here, with its
extra operator !. The operator is here for the condition, as \$cancelled
needs the \'cancellation\' state, while the condition needs the
contrary. Note also that isset() could be moved out of this condition,
and made the result easier to read.

``` {.php}
$form        = $this->get('form.factory')->create('theme_upload', [], ['action' => $action]);

        if ($this->request->getMethod() == 'POST') {
            if (isset($form) && !$cancelled = $this->isFormCancelled($form)) {
                if ($this->isFormValid($form)) {
                    $fileData = $form['file']->getData();
```

### No array\_merge() In Loops

#### Tine20 {#tine20-performances-arraymergeinloops}

`no-array\_merge()-in-loops`{.interpreted-text role="ref"}, in
tine20/Tinebase/User/Ldap.php:670.

Classic example of array\_merge() in loop : here, the attributures
should be collected in a local variable, and then merged in one
operation, at the end. That includes the attributes provided before the
loop, and the array provided after the loop. Note that the order of
merge will be the same when merging than when collecting the arrays.

``` {.php}
$attributes = array_values($this->_rowNameMapping);
        foreach ($this->_ldapPlugins as $plugin) {
            $attributes = array_merge($attributes, $plugin->getSupportedAttributes());
        }

        $attributes = array_merge($attributes, $this->_additionalLdapAttributesToFetch);
```

### Useless Parenthesis

#### Mautic {#mautic-structures-uselessparenthesis}

`useless-parenthesis`{.interpreted-text role="ref"}, in
code/app/bundles/EmailBundle/Controller/AjaxController.php:85.

Parenthesis are useless around \$progress\[1\], and around the division
too.

``` {.php}
$dataArray['percent'] = ($progress[1]) ? ceil(($progress[0] / $progress[1]) * 100) : 100;
```

------------------------------------------------------------------------

#### Woocommerce {#woocommerce-structures-uselessparenthesis}

`useless-parenthesis`{.interpreted-text role="ref"}, in
includes/class-wc-coupon.php:437.

Parenthesis are useless for calculating \$discount\_percent, as it is a
divisition. Moreover, it is not needed with \$discount, (float) applies
to the next element, but it does make the expression more readable.

``` {.php}
if ( wc_prices_include_tax() ) {
    $discount_percent = ( wc_get_price_including_tax( $cart_item['data'] ) * $cart_item_qty ) / WC()->cart->subtotal;
} else {
    $discount_percent = ( wc_get_price_excluding_tax( $cart_item['data'] ) * $cart_item_qty ) / WC()->cart->subtotal_ex_tax;
}
$discount = ( (float) $this->get_amount() * $discount_percent ) / $cart_item_qty;
```

### Unresolved Instanceof

#### WordPress {#wordpress-classes-unresolvedinstanceof}

`unresolved-instanceof`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
private function resolveTag($match)
    {
        $tagReflector = $this->createLinkOrSeeTagFromRegexMatch($match);
        if (!$tagReflector instanceof Tag\SeeTag && !$tagReflector instanceof Tag\LinkTag) {
            return $match;
        }
```

### Use PHP Object API

#### WordPress {#wordpress-php-useobjectapi}

`use-php-object-api`{.interpreted-text role="ref"}, in
wp-includes/functions.php:2558.

Finfo has also a class, with the same name.

``` {.php}
finfo_open(FILEINFO_MIME_TYPE)
```

------------------------------------------------------------------------

#### PrestaShop {#prestashop-php-useobjectapi}

`use-php-object-api`{.interpreted-text role="ref"}, in
admin-dev/filemanager/include/utils.php:174.

transliterator\_transliterate() has also a class named Transliterator

``` {.php}
transliterator_transliterate('Accents-Any', $str)
```

------------------------------------------------------------------------

#### SugarCrm {#sugarcrm-php-useobjectapi}

`use-php-object-api`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/include/database/MysqliManager.php:222.

Mysqli has also a class, with the same name.

``` {.php}
mysqli_fetch_field_direct($result, $i)
```

### Altering Foreach Without Reference

#### Contao {#contao-structures-alteringforeachwithoutreference}

`altering-foreach-without-reference`{.interpreted-text role="ref"}, in
core-bundle/src/Resources/contao/classes/Theme.php:613.

\$tmp\[\$kk\] is &\$vv.

``` {.php}
foreach ($tmp as $kk=>$vv)
                                {
                                    // Do not use the FilesModel here – tables are locked!
                                    $objFile = $this->Database->prepare(SELECT uuid FROM tl_files WHERE path=?)
                                                              ->limit(1)
                                                              ->execute($this->customizeUploadPath($vv));

                                    $tmp[$kk] = $objFile->uuid;
                                }
```

------------------------------------------------------------------------

#### WordPress {#wordpress-structures-alteringforeachwithoutreference}

`altering-foreach-without-reference`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

\$ids\[\$index\] is &\$rrid.

``` {.php}
foreach($ids as $index => $rrid)
                {
                    if($rrid == $this->Id)
                    {
                        $ids[$index] = $_id;
                        $write = true;
                        break;
                    }
                }
```

### Old Style \_\_autoload()

#### Piwigo {#piwigo-php-oldautoloadusage}

`old-style-\_\_autoload()`{.interpreted-text role="ref"}, in
include/phpmailer/PHPMailerAutoload.php:45.

This code handles situations for PHP after 5.1.0 and older. Rare are the
applications that are still using those versions in 2019.

``` {.php}
if (version_compare(PHP_VERSION, '5.1.2', '>=')) {
    //SPL autoloading was introduced in PHP 5.1.2
    if (version_compare(PHP_VERSION, '5.3.0', '>=')) {
        spl_autoload_register('PHPMailerAutoload', true, true);
    } else {
        spl_autoload_register('PHPMailerAutoload');
    }
} else {
    /**
     * Fall back to traditional autoload for old PHP versions
     * @param string $classname The name of the class to load
     */
    function __autoload($classname)
    {
        PHPMailerAutoload($classname);
    }
}
```

### Empty Instructions

#### Zurmo {#zurmo-structures-emptylines}

`empty-instructions`{.interpreted-text role="ref"}, in
app/protected/core/widgets/MentionInput.php:84.

There is no need for a semi-colon after a if/then structure.

``` {.php}
public function run()
        {
            $id = $this->getId();
            $additionalSettingsJs = showAvatars: . var_export($this->showAvatars, true) . ,;
            if ($this->classes)
            {
                $additionalSettingsJs .=  $this->classes . ',';
            };
            if ($this->templates)
            {
                $additionalSettingsJs .=  $this->templates;
            };
```

------------------------------------------------------------------------

#### ThinkPHP {#thinkphp-structures-emptylines}

`empty-instructions`{.interpreted-text role="ref"}, in
ThinkPHP/Library/Vendor/Smarty/sysplugins/smarty\_internal\_configfileparser.php:83.

There is no need for a semi-colon after a class structure, unless it is
an anonymous class.

``` {.php}
class TPC_yyStackEntry
{
    public $stateno;       /* The state-number */
    public $major;         /* The major token value.  This is the code
                     ** number for the token at this stack level */
    public $minor; /* The user-supplied minor token value.  This
                     ** is the value of the token  */
};
```

### Use Pathinfo

#### SuiteCrm {#suitecrm-php-usepathinfo}

`use-pathinfo`{.interpreted-text role="ref"}, in
include/utils/file\_utils.php:441.

Looking for the extension ? Use pathinfo() and PATHINFO\_EXTENSION

``` {.php}
$exp = explode('.', $filename);
```

### Should Use Constants

#### Tine20 {#tine20-functions-shoulduseconstants}

`should-use-constants`{.interpreted-text role="ref"}, in
tine20/Sales/Controller/Invoice.php:560.

True should be replaced by COUNT\_RECURSIVE. The default one is
COUNT\_NORMAL.

``` {.php}
count($billables, true)
```

### No Parenthesis For Language Construct

#### Phpdocumentor {#phpdocumentor-structures-noparenthesisforlanguageconstruct}

`no-parenthesis-for-language-construct`{.interpreted-text role="ref"},
in src/Application/Renderer/Router/StandardRouter.php:55.

No need for parenthesis with require(). instanceof has a higher
precedence than return anyway.

``` {.php}
$this[] = new Rule(function ($node) { return ($node instanceof NamespaceDescriptor); }, $namespaceGenerator);
```

------------------------------------------------------------------------

#### phpMyAdmin {#phpmyadmin-structures-noparenthesisforlanguageconstruct}

`no-parenthesis-for-language-construct`{.interpreted-text role="ref"},
in db\_datadict.php:170.

Not only echo() doesn\'t use any parenthesis, but this syntax gives the
illusion that echo() only accepts one argument, while it actually
accepts an arbitrary number of argument.

``` {.php}
echo (($row['Null'] == 'NO') ? __('No') : __('Yes'))
```

### No Hardcoded Path

#### Tine20 {#tine20-structures-nohardcodedpath}

`no-hardcoded-path`{.interpreted-text role="ref"}, in
tine20/Tinebase/DummyController.php:28.

When this script is not run on a Linux system, the file save will fail.

``` {.php}
file_put_contents('/var/run/tine20/DummyController.txt', 'success ' . $n)
```

------------------------------------------------------------------------

#### Thelia {#thelia-structures-nohardcodedpath}

`no-hardcoded-path`{.interpreted-text role="ref"}, in
local/modules/Tinymce/Resources/js/tinymce/filemanager/include/php\_image\_magician.php:2317.

The [iptc.jpg]{.title-ref} file is written. It looks like the file may
be written next to the php\_image\_magician.php file, but this is deep
in the source code and is unlikely. This means that the working
directory has been set to some other place, though we don\'t read it
immediately.

``` {.php}
private function writeIPTC($dat, $value)
    {

        # LIMIT TO JPG

        $caption_block = $this->iptc_maketag(2, $dat, $value);
        $image_string = iptcembed($caption_block, $this->fileName);
        file_put_contents('iptc.jpg', $image_string);
    }
```

### No Hardcoded Port

#### WordPress {#wordpress-structures-nohardcodedport}

`no-hardcoded-port`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### Use Constant As Arguments

#### Tikiwiki {#tikiwiki-functions-useconstantasarguments}

`use-constant-as-arguments`{.interpreted-text role="ref"}, in
lib/language/Language.php:112.

E\_WARNING is a valid value, but PHP documentation for trigger\_error()
explains that E\_USER constants should be used.

``` {.php}
trigger_error("Octal or hexadecimal string '" . $match[1] . "' not supported", E_WARNING)
```

------------------------------------------------------------------------

#### shopware {#shopware-functions-useconstantasarguments}

`use-constant-as-arguments`{.interpreted-text role="ref"}, in
engine/Shopware/Plugins/Default/Core/Debug/Components/EventCollector.php:106.

One example where code review reports errors where unit tests don\'t :
array\_multisort actually requires sort order first (SORT\_ASC or
SORT\_DESC), then sort flags (such as SORT\_NUMERIC). Here, with
SORT\_DESC = 3 and SORT\_NUMERIC = 1, PHP understands it as the coders
expects it. The same error is repeated six times in the code.

``` {.php}
array_multisort($order, SORT_NUMERIC, SORT_DESC, $this->results)
```

### Assign Default To Properties

#### LiveZilla {#livezilla-classes-makedefault}

`assign-default-to-properties`{.interpreted-text role="ref"}, in
livezilla/\_lib/functions.external.inc.php:174.

Flags may default to array() in the class definition. Filled array(),
with keys and values, are also possible.

``` {.php}
class OverlayChat
{
    public $Botmode;
    public $Human;
    public $HumanGeneral;
    public $RepollRequired;
    public $OperatorCount;
    public $Flags;
    public $LastMessageReceived;
    public $LastPostReceived;
    public $IsHumanChatAvailable;
    public $IsChatAvailable;
    public $ChatHTML;
    public $OverlayHTML;
    public $PostHTML;
    public $FullLoad;
    public $LanguageRequired = false;
    public $LastPoster;
    public $EyeCatcher;
    public $GroupBuilder;
    public $CurrentOperatorId;
    public $BotTitle;
    public $OperatorPostCount;
    public $PlaySound;
    public $SpeakingToHTML;
    public $SpeakingToAdded;
    public $Version = 1;

    public static $MaxPosts = 50;
    public static $Response;

    function __construct()
    {
        $this->Flags = array();
        VisitorChat::$Router = new ChatRouter();
    }
```

------------------------------------------------------------------------

#### phpMyAdmin {#phpmyadmin-classes-makedefault}

`assign-default-to-properties`{.interpreted-text role="ref"}, in
libraries/classes/Console.ph:55.

\_isEnabled may default to true. It could also default to a class
constant.

``` {.php}
class Console
{
    /**
     * Whether to display anything
     *
     * @access private
     * @var bool
     */
    private $_isEnabled;

// some code ignored here
    /**
     * Creates a new class instance
     */
    public function __construct()
    {
        $this->_isEnabled = true;
```

### Should Chain Exception

#### Magento {#magento-structures-shouldchainexception}

`should-chain-exception`{.interpreted-text role="ref"}, in
lib/Mage/Backup/Filesystem/Rollback/Ftp.php:81.

Instead of using the exception message as an argument, chaining the
exception would send the whole exception, including the message, and
other interesting information like file and line.

``` {.php}
protected function _initFtpClient()
    {
        try {
            $this->_ftpClient = new Mage_System_Ftp();
            $this->_ftpClient->connect($this->_snapshot->getFtpConnectString());
        } catch (Exception $e) {
            throw new Mage_Backup_Exception_FtpConnectionFailed($e->getMessage());
        }
    }
```

------------------------------------------------------------------------

#### Tine20 {#tine20-structures-shouldchainexception}

`should-chain-exception`{.interpreted-text role="ref"}, in
tine20/Setup/Controller.php:81.

Here, the new exception gets an hardcoded message. More details about
the reasons are already available in the \$e exception, but they are not
logged, not chained for later processing.

``` {.php}
try {
            $dirIterator = new DirectoryIterator($this->_baseDir);
        } catch (Exception $e) {
            Setup_Core::getLogger()->warn(__METHOD__ . '::' . __LINE__ . ' Could not open base dir: ' . $this->_baseDir);
            throw new Tinebase_Exception_AccessDenied('Could not open Tine 2.0 root directory.');
        }
```

### Undefined Interfaces

#### xataface {#xataface-interfaces-undefinedinterfaces}

`undefined-interfaces`{.interpreted-text role="ref"}, in
Dataface/Error.php:112.

Exception seems to be a typo, and leads to an always-true expression.

``` {.php}
public static function isError($obj){
        if ( !PEAR::isError($obj) and !($obj instanceof Exception_) ) return false;
        return ($obj->getCode() >= DATAFACE_E_ERROR);
    }
```

### Useless Interfaces

#### Woocommerce {#woocommerce-interfaces-uselessinterfaces}

`useless-interfaces`{.interpreted-text role="ref"}, in
includes/interfaces/class-wc-order-item-data-store-interface.php:20.

WC\_Order\_Item\_Data\_Store\_Interface is used to structure the class
WC\_Order\_Item\_Data\_Store. It is not used anywhere else.

``` {.php}
interface WC_Order_Item_Data_Store_Interface {


//////// 
//includes/data-stores/class-wc-order-item-data-store.php

class WC_Order_Item_Data_Store implements WC_Order_Item_Data_Store_Interface {
```

### Should Use Prepared Statement

#### Dolibarr {#dolibarr-security-shouldusepreparedstatement}

`should-use-prepared-statement`{.interpreted-text role="ref"}, in
htdocs/product/admin/price\_rules.php:76.

This code is well escaped, as the integer type cast will prevent any
special chars to be used. Here, a prepared statement would apply a
modern approach to securing this query.

``` {.php}
$db->query("DELETE FROM " . MAIN_DB_PREFIX . "product_pricerules WHERE level = " . (int) $i)
```

### No Hardcoded Ip

#### OpenEMR {#openemr-structures-nohardcodedip}

`no-hardcoded-ip`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

Although they are commented just above, the values provided here are
suspicious.

``` {.php}
// FTP parameters that you must customize.  If you are not sending
 // then set $FTP_SERVER to an empty string.
 //
 $FTP_SERVER = 192.168.0.30;
 $FTP_USER   = openemr;
 $FTP_PASS   = secret;
 $FTP_DIR    = ;
```

------------------------------------------------------------------------

#### NextCloud {#nextcloud-structures-nohardcodedip}

`no-hardcoded-ip`{.interpreted-text role="ref"}, in
config/config.sample.php:1561.

Although they are documented as empty array, 3 values are provided as
examples. They do not responds, at the time of writing, but they may.

``` {.php}
/**
 * List of trusted proxy servers
 *
 * You may set this to an array containing a combination of
 * - IPv4 addresses, e.g. `192.168.2.123`
 * - IPv4 ranges in CIDR notation, e.g. `192.168.2.0/24`
 * - IPv6 addresses, e.g. `fd9e:21a7:a92c:2323::1`
 *
 * _(CIDR notation for IPv6 is currently work in progress and thus not
 * available as of yet)_
 *
 * When an incoming request's `REMOTE_ADDR` matches any of the IP addresses
 * specified here, it is assumed to be a proxy instead of a client. Thus, the
 * client IP will be read from the HTTP header specified in
 * `forwarded_for_headers` instead of from `REMOTE_ADDR`.
 *
 * So if you configure `trusted_proxies`, also consider setting
 * `forwarded_for_headers` which otherwise defaults to `HTTP_X_FORWARDED_FOR`
 * (the `X-Forwarded-For` header).
 *
 * Defaults to an empty array.
 */
'trusted_proxies' => array('203.0.113.45', '198.51.100.128', '192.168.2.0/24'),
```

### Echo With Concat

#### Phpdocumentor {#phpdocumentor-structures-echowithconcat}

`echo-with-concat`{.interpreted-text role="ref"}, in
src/phpDocumentor/Bootstrap.php:76.

Simply replace the dot by a comma.

``` {.php}
echo 'PROFILING ENABLED' . PHP_EOL
```

------------------------------------------------------------------------

#### TeamPass {#teampass-structures-echowithconcat}

`echo-with-concat`{.interpreted-text role="ref"}, in
includes/libraries/Authentication/Yubico/PEAR.php:162.

This is less obvious, but turning print to echo, and the double-quoted
string to single quoted string will yield the same optimisation.

``` {.php}
print "PEAR constructor called, class=$classname\n";
```

### Else If Versus Elseif

#### TeamPass {#teampass-structures-elseifelseif}

`else-if-versus-elseif`{.interpreted-text role="ref"}, in items.php:819.

This code could be turned into a switch() structure.

``` {.php}
if ($field[3] === 'text') {
                echo '
                        <input type=text id=edit_field_.$field[0]._.$elem[0]. class=edit_item_field input_text text ui-widget-content ui-corner-all size=40 data-field-type=.$field[3]. data-field-masked=.$field[4]. data-field-is-mandatory=.$field[5]. data-template-id=.$templateID.>';
            } else if ($field[3] === 'textarea') {
                echo '
                        <textarea id=edit_field_.$field[0]._.$elem[0]. class=edit_item_field input_text text ui-widget-content ui-corner-all colums=40 rows=5 data-field-type=.$field["3"]. data-field-masked=.$field[4]. data-field-is-mandatory=.$field[5]. data-template-id=.$templateID.></textarea>';
            }
```

------------------------------------------------------------------------

#### Phpdocumentor {#phpdocumentor-structures-elseifelseif}

`else-if-versus-elseif`{.interpreted-text role="ref"}, in
src/phpDocumentor/Plugin/Core/Transformer/Writer/Xsl.php:112.

The first then block is long and complex. The else block, on the other
hand, only contains a single if/then/else. Both conditions are distinct
at first sight, so a if / elseif / then structure would be the best.

``` {.php}
if ($transformation->getQuery() !== '') {
/** Long then block **/
        } else {
            if (substr($transformation->getArtifact(), 0, 1) == '$') {
                // not a file, it must become a variable!
                $variable_name = substr($transformation->getArtifact(), 1);
                $this->xsl_variables[$variable_name] = $proc->transformToXml($structure);
            } else {
                $relativeFileName = substr($artifact, strlen($transformation->getTransformer()->getTarget()) + 1);
                $proc->setParameter('', 'root', str_repeat('../', substr_count($relativeFileName, '/')));

                $this->writeToFile($artifact, $proc, $structure);
            }
        }
```

### Could Be Static

#### Dolphin {#dolphin-structures-couldbestatic}

`could-be-static`{.interpreted-text role="ref"}, in
inc/utils.inc.php:673.

Dolphin pro relies on HTMLPurifier to handle cleaning of values : it is
used to prevent xss threat. In this method, oHtmlPurifier is first
checked, and if needed, created. Since creation is long and costly, it
is only created once. Once the object is created, it is stored as a
global to be accessible at the next call of the method. In fact,
oHtmlPurifier is never used outside this method, so it could be turned
into a \'static\' variable, and prevent other methods to modify it. This
is a typical example of variable that could be static instead of global.

``` {.php}
function clear_xss($val)
{
    // HTML Purifier plugin
    global $oHtmlPurifier;
    if (!isset($oHtmlPurifier) && !$GLOBALS['logged']['admin']) {

        require_once(BX_DIRECTORY_PATH_PLUGINS . 'htmlpurifier/HTMLPurifier.standalone.php');

/..../

        $oHtmlPurifier = new HTMLPurifier($oConfig);
    }

    if (!$GLOBALS['logged']['admin']) {
        $val = $oHtmlPurifier->purify($val);
    }

    $oZ = new BxDolAlerts('system', 'clear_xss', 0, 0,
        array('oHtmlPurifier' => $oHtmlPurifier, 'return_data' => &$val));
    $oZ->alert();

    return $val;
}
```

------------------------------------------------------------------------

#### Contao {#contao-structures-couldbestatic}

`could-be-static`{.interpreted-text role="ref"}, in
system/helper/functions.php:184.

\$arrScanCache is a typical cache variables. It is set as global for
persistence between calls. If it contains an already stored answer, it
is returned immediately. If it is not set yet, it is then filled with a
value, and later reused. This global could be turned into static, and
avoid pollution of global space.

``` {.php}
function scan($strFolder, $blnUncached=false)
{
    global $arrScanCache;

    // Add a trailing slash
    if (substr($strFolder, -1, 1) != '/')
    {
        $strFolder .= '/';
    }

    // Load from cache
    if (!$blnUncached && isset($arrScanCache[$strFolder]))
    {
        return $arrScanCache[$strFolder];
    }
    $arrReturn = array();

    // Scan directory
    foreach (scandir($strFolder) as $strFile)
    {
        if ($strFile == '.' || $strFile == '..')
        {
            continue;
        }

        $arrReturn[] = $strFile;
    }

    // Cache the result
    if (!$blnUncached)
    {
        $arrScanCache[$strFolder] = $arrReturn;
    }

    return $arrReturn;
}
```

### Could Use Short Assignation

#### ChurchCRM {#churchcrm-structures-coulduseshortassignation}

`could-use-short-assignation`{.interpreted-text role="ref"}, in
src/ChurchCRM/utils/GeoUtils.php:74.

Sometimes, the variable is on the other side of the operator.

``` {.php}
$distance = 0.6213712 * $distance;
```

------------------------------------------------------------------------

#### Thelia {#thelia-structures-coulduseshortassignation}

`could-use-short-assignation`{.interpreted-text role="ref"}, in
local/modules/Tinymce/Resources/js/tinymce/filemanager/include/utils.php:70.

/= is rare, but it definitely could be used here.

``` {.php}
$size = $size / 1024;
```

### Pre-increment

#### ExpressionEngine {#expressionengine-performances-prepostincrement}

`pre-increment`{.interpreted-text role="ref"}, in
system/ee/EllisLab/ExpressionEngine/Controller/Utilities/Communicate.php:650.

Using preincrement in for() loops is safe and straightforward.

``` {.php}
for ($x = 0; $x < $number_to_send; $x++)
        {
            $email_address = array_shift($recipient_array);

            if ( ! $this->deliverEmail($email, $email_address))
            {
                $email->delete();

                $debug_msg = ee()->email->print_debugger(array());

                show_error(lang('error_sending_email').BR.BR.$debug_msg);
            }
            $email->total_sent++;
        }
```

------------------------------------------------------------------------

#### Traq {#traq-performances-prepostincrement}

`pre-increment`{.interpreted-text role="ref"}, in
src/Controllers/Tickets.php:84.

\$this-\>currentProject-\>next\_ticket\_id value is ignored by the code.
It may be turned into a preincrement.

``` {.php}
TimelineModel::newTicketEvent($this->currentUser, $ticket)->save();

            $this->currentProject->next_ticket_id++;
            $this->currentProject->save();
```

### Indices Are Int Or String

#### Zencart {#zencart-structures-indicesareintorstring}

`indices-are-int-or-string`{.interpreted-text role="ref"}, in
includes/modules/payment/paypaldp.php:2523.

All those strings ends up as integers.

``` {.php}
// Build Currency format table
    $curFormat = Array();
    $curFormat[036]=2;
    $curFormat[124]=2;
    $curFormat[203]=2;
    $curFormat[208]=2;
    $curFormat[348]=2;
    $curFormat[392]=0;
    $curFormat[554]=2;
    $curFormat[578]=2;
    $curFormat[702]=2;
    $curFormat[752]=2;
    $curFormat[756]=2;
    $curFormat[826]=2;
    $curFormat[840]=2;
    $curFormat[978]=2;
    $curFormat[985]=2;
```

------------------------------------------------------------------------

#### Mautic {#mautic-structures-indicesareintorstring}

`indices-are-int-or-string`{.interpreted-text role="ref"}, in
app/bundles/CoreBundle/Entity/CommonRepository.php:315.

\$baseCols has 1 and 0 (respectively) for index.

``` {.php}
foreach ($metadata->getAssociationMappings() as $field => $association) {
                    if (in_array($association['type'], [ClassMetadataInfo::ONE_TO_ONE, ClassMetadataInfo::MANY_TO_ONE])) {
                        $baseCols[true][$entityClass][]  = $association['joinColumns'][0]['name'];
                        $baseCols[false][$entityClass][] = $field;
                    }
                }
```

### Should Typecast

#### xataface {#xataface-type-shouldtypecast}

`should-typecast`{.interpreted-text role="ref"}, in
Dataface/Relationship.php:1612.

This is an exact example. A little further, the same applies to
intval(\$max))

``` {.php}
intval($min);
```

------------------------------------------------------------------------

#### OpenConf {#openconf-type-shouldtypecast}

`should-typecast`{.interpreted-text role="ref"}, in
author/upload.php:62.

This is another exact example.

``` {.php}
intval($_POST['pid']);
```

### No Direct Usage

#### Edusoho {#edusoho-structures-nodirectusage}

`no-direct-usage`{.interpreted-text role="ref"}, in
edusoho/src/AppBundle/Controller/Admin/FinanceSettingController.php:107.

Glob() returns false, in case of error. It returns an empty array in
case everything is fine, but nothing was found. In case of error,
array\_map() will stop the script.

``` {.php}
array_map('unlink', glob($dir.'/MP_verify_*.txt'));
```

------------------------------------------------------------------------

#### XOOPS {#xoops-structures-nodirectusage}

`no-direct-usage`{.interpreted-text role="ref"}, in
htdocs/Frameworks/moduleclasses/moduleadmin/moduleadmin.php:585.

Although the file is readable, file() may return false in case of
failure. On the other hand, implode doesn\'t accept boolean values.

``` {.php}
$file = XOOPS_ROOT_PATH . /modules/{$module_dir}/docs/changelog.txt;
            if ( is_readable( $file ) ) {
                $ret .= implode( '<br>', file( $file ) ) . \n;
            }
```

### Avoid Substr() One

#### ChurchCRM {#churchcrm-structures-nosubstrone}

`avoid-substr()-one`{.interpreted-text role="ref"}, in
src/Login.php:141.

No need to call substr() to get only one char.

``` {.php}
if (substr($LocationFromGet, 0, 1) == "/") {
    $LocationFromGet = substr($LocationFromGet, 1);
}
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-structures-nosubstrone}

`avoid-substr()-one`{.interpreted-text role="ref"}, in
livezilla/\_lib/objects.global.inc.php:2243.

No need to call substr() to get only one char.

``` {.php}
$_hex = str_replace("#", "", $_hex);
            if(strlen($_hex) == 3) {
            $r = hexdec(substr($_hex,0,1).substr($_hex,0,1));
            $g = hexdec(substr($_hex,1,1).substr($_hex,1,1));
            $b = hexdec(substr($_hex,2,1).substr($_hex,2,1));
        } else {
            $r = hexdec(substr($_hex,0,2));
            $g = hexdec(substr($_hex,2,2));
            $b = hexdec(substr($_hex,4,2));
        }
        $rgb = array($r, $g, $b);
        return $rgb;
```

### Useless Brackets

#### ChurchCRM {#churchcrm-structures-uselessbrackets}

`useless-brackets`{.interpreted-text role="ref"}, in src/Menu.php:72.

Difficut to guess what was before the block here. It doesn\'t have any
usage for control flow.

``` {.php}
$new_row = false;
        $count_people = 0;

        {
            foreach ($peopleWithBirthDays as $peopleWithBirthDay) {
                if ($new_row == false) {
                    ?>

                    <div class=row>
                <?php
                    $new_row = true;
                } ?>
                <div class=col-sm-3>
```

------------------------------------------------------------------------

#### Piwigo {#piwigo-structures-uselessbrackets}

`useless-brackets`{.interpreted-text role="ref"}, in picture.php:342.

There is no need for block braces with case. In fact, it does give a
false sense of break, while the case will still fall over to the next
one.

``` {.php}
case 'rate' :
    {
      include_once(PHPWG_ROOT_PATH.'include/functions_rate.inc.php');
      rate_picture($page['image_id'], $_POST['rate']);
      redirect($url_self);
    }
```

### preg\_replace With Option e

#### Edusoho {#edusoho-structures-pregoptione}

`preg\_replace-with-option-e`{.interpreted-text role="ref"}, in
vendor\_user/uc\_client/lib/uccode.class.php:32.

This call extract text between \[code\] tags, then process it with
\$this-\>codedisp() and nest it again in the original string.
preg\_replace\_callback() is a drop-in replacement for this piece of
code.

``` {.php}
$message = preg_replace("/\s*\[code\](.+?)\[\/code\]\s*/ies", "$this->codedisp('\1')", $message);
```

### eval() Without Try

#### FuelCMS {#fuelcms-structures-evalwithouttry}

`eval()-without-try`{.interpreted-text role="ref"}, in
fuel/modules/fuel/controllers/Blocks.php:268.

The @ will prevent any error, while the try/catch allows the processing
of certain types of error, namely the Fatal ones.

``` {.php}
@eval($_name_var_eval)
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-structures-evalwithouttry}

`eval()-without-try`{.interpreted-text role="ref"}, in
system/ee/EllisLab/Addons/member/mod.member\_memberlist.php:637.

\$cond is build from values extracted from the \$fields array. Although
it is probably reasonably safe, a try/catch here will collect any
unexpected situation cleaningly.

``` {.php}
elseif (isset($fields[$val['3']]))
                    {
                        if (array_key_exists('m_field_id_'.$fields[$val['3']], $row))
                        {
                            $v = $row['m_field_id_'.$fields[$val['3']]];

                            $lcond = str_replace($val['3'], "$v", $lcond);
                            $cond = $lcond.' '.$rcond;
                            $cond = str_replace("\|", "|", $cond);

                            eval("$result = ".$cond.";");
```

### Relay Function

#### TeamPass {#teampass-functions-relayfunction}

`relay-function`{.interpreted-text role="ref"}, in
includes/libraries/Goodby/CSV/Import/Standard/Interpreter.php:88.

This example puts actually a name on the events : this method
\'delegate\' and it does it in the smallest amount of possible work,
being given all the arguments.

``` {.php}
/**
     * delegate to observer
     *
     * @param $observer
     * @param $line
     */
    private function delegate($observer, $line)
    {
        call_user_func($observer, $line);
    }
```

------------------------------------------------------------------------

#### SPIP {#spip-functions-relayfunction}

`relay-function`{.interpreted-text role="ref"}, in
ecrire/inc/json.php:73.

var2js() acts as an alternative for json\_encode(). Yet, it used to be
directly called by the framework\'s code and difficult to change. With
the advent of json\_encode, the native function has been used, and even,
a compatibility tool was set up. Thus, the relay function.

``` {.php}
if (!function_exists('json_encode')) {
    function json_encode($v) {
        return var2js($v);
    }
}
```

### Silently Cast Integer

#### MediaWiki {#mediawiki-type-silentlycastinteger}

`silently-cast-integer`{.interpreted-text role="ref"}, in
includes/debug/logger/monolog/AvroFormatter.php:167.

Too many ff in the masks.

``` {.php}
private function encodeLong( $id ) {
        $high   = ( $id & 0xffffffff00000000 ) >> 32;
        $low    = $id & 0x00000000ffffffff;
        return pack( 'NN', $high, $low );
    }
```

### Timestamp Difference

#### Zurmo {#zurmo-structures-timestampdifference}

`timestamp-difference`{.interpreted-text role="ref"}, in
app/protected/modules/import/jobs/ImportCleanupJob.php:73.

This is wrong twice a year, in countries that has day-ligth saving time.
One of the weeks will be too short, and the other will be too long.

``` {.php}
/**
         * Get all imports where the modifiedDateTime was more than 1 week ago.  Then
         * delete the imports.
         * (non-PHPdoc)
         * @see BaseJob::run()
         */
        public function run()
        {
            $oneWeekAgoTimeStamp = DateTimeUtil::convertTimestampToDbFormatDateTime(time() - 60 * 60 *24 * 7);
```

------------------------------------------------------------------------

#### shopware {#shopware-structures-timestampdifference}

`timestamp-difference`{.interpreted-text role="ref"}, in
engine/Shopware/Controllers/Backend/Newsletter.php:150.

When daylight saving strike, the email may suddenly be locked for 1 hour
minus 30 seconds ago. The lock will be set for the rest of the hour,
until the server catch up.

``` {.php}
// Check lock time. Add a buffer of 30 seconds to the lock time (default request time)
            if (!empty($mailing['locked']) && strtotime($mailing['locked']) > time() - 30) {
                echo "Current mail: '" . $subjectCurrentMailing . "'\n";
                echo "Wait " . (strtotime($mailing['locked']) + 30 - time()) . " seconds ...\n";
                return;
            }
```

### Unused Arguments

#### ThinkPHP {#thinkphp-functions-unusedarguments}

`unused-arguments`{.interpreted-text role="ref"}, in
ThinkPHP/Library/Behavior/AgentCheckBehavior.class.php:18.

\$params are requested, but never used. The method is not overloading
another one, as the class doesn\'t extends anything. \$params is unused.

``` {.php}
class AgentCheckBehavior
{
    public function run(&$params)
    {
        // 代理访问检测
        $limitProxyVisit = C('LIMIT_PROXY_VISIT', null, true);
        if ($limitProxyVisit && ($_SERVER['HTTP_X_FORWARDED_FOR'] || $_SERVER['HTTP_VIA'] || $_SERVER['HTTP_PROXY_CONNECTION'] || $_SERVER['HTTP_USER_AGENT_VIA'])) {
            // 禁止代理访问
            exit('Access Denied');
        }
    }
}
```

------------------------------------------------------------------------

#### phpMyAdmin {#phpmyadmin-functions-unusedarguments}

`unused-arguments`{.interpreted-text role="ref"}, in
libraries/classes/Display/Results.php:1985.

Although \$column\_index is documented, it is not found in the rest of
the (long) body of the function. It might have been refactored into
\$sorted\_column\_index.

``` {.php}
/**
     * Prepare parameters and html for sorted table header fields
     *
     * @param array    $sort_expression             sort expression
     * @param array    $sort_expression_nodirection sort expression without direction
     * @param string   $sort_tbl                    The name of the table to which
     *                                             the current column belongs to
     * @param string   $name_to_use_in_sort         The current column under
     *                                             consideration
     * @param array    $sort_direction              sort direction
     * @param stdClass $fields_meta                 set of field properties
     * @param integer  $column_index                The index number to current column
     *
     * @return  array   3 element array - $single_sort_order, $sort_order, $order_img
     *
     * @access  private
     *
     * @see     _getOrderLinkAndSortedHeaderHtml()
     */
    private function _getSingleAndMultiSortUrls(
        array $sort_expression,
        array $sort_expression_nodirection,
        $sort_tbl,
        $name_to_use_in_sort,
        array $sort_direction,
        $fields_meta,
        $column_index
    ) {
    /**/
        // find the sorted column index in row result
        // (this might be a multi-table query)
        $sorted_column_index = false;
    /**/
    }
```

### Switch To Switch

#### Thelia {#thelia-structures-switchtoswitch}

`switch-to-switch`{.interpreted-text role="ref"}, in
core/lib/Thelia/Controller/Admin/TranslationsController.php:100.

The two first comparison may be turned into a case, and the last one
could be default, or default with a check on empty().

``` {.php}
if($modulePart == 'core') { /**/ } elseif($modulePart == 'admin-includes') { /**/ } elseif(!empty($modulePart)) { /**/ }
```

------------------------------------------------------------------------

#### XOOPS {#xoops-structures-switchtoswitch}

`switch-to-switch`{.interpreted-text role="ref"}, in
htdocs/search.php:74.

Here, converting this structure to switch requires to drop the ===
usage. Also, no default usage here.

``` {.php}
if($action === 'results') { /**/ } elseif($action === 'showall') { /**/ } elseif($action === 'showallbyuser') { /**/ }
```

### Wrong Parameter Type

#### Zencart {#zencart-php-internalparametertype}

`wrong-parameter-type`{.interpreted-text role="ref"}, in
admin/includes/header.php:180.

setlocale() may be called with null or \'\' (empty string), and will set
values from the environment. When called with \"0\" (the string), it
only reports the current setting. Using an integer is probably
undocumented behavior, and falls back to the zero string.

``` {.php}
$loc = setlocale(LC_TIME, 0);
        if ($loc !== FALSE) echo ' - ' . $loc; //what is the locale in use?
```

### Redefined Default

#### Piwigo {#piwigo-classes-redefineddefault}

`redefined-default`{.interpreted-text role="ref"}, in
admin/include/updates.class.php:34.

default\_themes is defined as an empty array, then filled with new
values. Same for default\_plugins. Both may be defined as declaration
time, and not during the constructor.

``` {.php}
class updates
{
  var $types = array();
  var $plugins;
  var $themes;
  var $languages;
  var $missing = array();
  var $default_plugins = array();
  var $default_themes = array();
  var $default_languages = array();
  var $merged_extensions = array();
  var $merged_extension_url = 'http://piwigo.org/download/merged_extensions.txt';

  function __construct($page='updates')
  {
    $this->types = array('plugins', 'themes', 'languages');

    if (in_array($page, $this->types))
    {
      $this->types = array($page);
    }
    $this->default_themes = array('clear', 'dark', 'Sylvia', 'elegant', 'smartpocket');
    $this->default_plugins = array('AdminTools', 'TakeATour', 'language_switch', 'LocalFilesEditor');
```

### Wrong fopen() Mode

#### Tikiwiki {#tikiwiki-php-fopenmode}

`wrong-fopen()-mode`{.interpreted-text role="ref"}, in
lib/tikilib.php:6777.

This fopen() mode doesn\'t exists. Use \'w\' instead.

``` {.php}
fopen('php://temp', 'rw');
```

------------------------------------------------------------------------

#### HuMo-Gen {#humo-gen-php-fopenmode}

`wrong-fopen()-mode`{.interpreted-text role="ref"}, in
include/phprtflite/lib/PHPRtfLite/StreamOutput.php:77.

This fopen() mode doesn\'t exists. Use \'w\' instead.

``` {.php}
fopen($this->_filename, 'wr', false)
```

### Use random\_int()

#### Thelia {#thelia-php-betterrand}

`use-random\_int()`{.interpreted-text role="ref"}, in
core/lib/Thelia/Tools/TokenProvider.php:151.

The whole function may be replaced by random\_int(), as it generates
random tokens. This needs an extra layer of hashing, to get a long and
string results.

``` {.php}
/**
     * @return string
     */
    protected static function getComplexRandom()
    {
        $firstValue = (float) (mt_rand(1, 0xFFFF) * rand(1, 0x10001));
        $secondValues = (float) (rand(1, 0xFFFF) * mt_rand(1, 0x10001));

        return microtime() . ceil($firstValue / $secondValues) . uniqid();
    }
```

------------------------------------------------------------------------

#### FuelCMS {#fuelcms-php-betterrand}

`use-random\_int()`{.interpreted-text role="ref"}, in
fuel/modules/fuel/libraries/Fuel.php:235.

Security tokens should be build with a CSPRNG source. uniqid() is based
on time, and though it changes anytime (sic), it is easy to guess. Those
days, it looks like \'5b1262e74dbb9\';

``` {.php}
$this->installer->change_config('config', '$config[\'encryption_key\'] = \'\';', '$config[\'encryption_key\'] = \''.md5(uniqid()).'\';');
```

### Already Parents Interface

#### WordPress {#wordpress-interfaces-alreadyparentsinterface}

`already-parents-interface`{.interpreted-text role="ref"}, in
src/Phinx/Db/Adapter/AbstractAdapter.php:41.

SqlServerAdapter extends PdoAdapter, PdoAdapter extends AbstractAdapter.
The first and the last both implements AdapterInterface. Only one is
needed.

``` {.php}
/**
 * Base Abstract Database Adapter.
 */
abstract class AbstractAdapter implements AdapterInterface
{

/// In the src/src/Phinx/Db/Adapter/SqlServerAdapter.php, line 45
/**
 * Phinx SqlServer Adapter.
 *
 */
class SqlServerAdapter extends PdoAdapter implements AdapterInterface
{
```

------------------------------------------------------------------------

#### Thelia {#thelia-interfaces-alreadyparentsinterface}

`already-parents-interface`{.interpreted-text role="ref"}, in
core/lib/Thelia/Core/Template/Loop/BaseSpecificModule.php:35.

PropelSearchLoopInterface is implemented by both BaseSpecificModule and
Payment

``` {.php}
abstract class BaseSpecificModule extends BaseI18nLoop implements PropelSearchLoopInterface

/* in file  core/lib/Thelia/Core/Template/Loop/Payment.php, line 28 */

class Payment extends BaseSpecificModule implements PropelSearchLoopInterface
```

### Ternary In Concat

#### TeamPass {#teampass-structures-ternaryinconcat}

`ternary-in-concat`{.interpreted-text role="ref"}, in
includes/libraries/protect/AntiXSS/UTF8.php:5409.

The concatenations in the initial comparison are disguised casting. When
\$str2 is empty too, the ternary operator yields a 0, leading to a
systematic failure.

``` {.php}
$str1 . '' === $str2 . '' ? 0 : strnatcmp(self::strtonatfold($str1), self::strtonatfold($str2))
```

### No Hardcoded Hash

#### shopware {#shopware-structures-nohardcodedhash}

`no-hardcoded-hash`{.interpreted-text role="ref"}, in
engine/Shopware/Models/Document/Data/OrderData.php:254.

This is actually a hashed hardcoded password. As the file explains, this
is a demo order, for populating the database when in demo mode, so this
is fine. We also learn that the password are securily sorted here. It
may also be advised to avoid hardcoding this password, as any demo shop
has the same user credential : it is the first to be tried when a demo
installation is found.

``` {.php}
'_userID' => '3',
    '_user' => new ArrayObject([
            'id' => '3',
            'password' => '$2y$10$GAGAC6.1kMRvN4RRcLrYleDx.EfWhHcW./cmoOQg11sjFUY73SO.C',
            'encoder' => 'bcrypt',
            'email' => 'demo@shopware.com',
            'customernumber' => '20005',
```

------------------------------------------------------------------------

#### SugarCrm {#sugarcrm-structures-nohardcodedhash}

`no-hardcoded-hash`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/include/Smarty/Smarty.class.php:460.

The MD5(\'Smarty\') is hardcoded in the properties. This property is not
used in the class, but in parts of the code, when a unique delimiter is
needed.

``` {.php}
/**
     * md5 checksum of the string 'Smarty'
     *
     * @var string
     */
    var $_smarty_md5           = 'f8d698aea36fcbead2b9d5359ffca76f';
```

### Identical Conditions

#### WordPress {#wordpress-structures-identicalconditions}

`identical-conditions`{.interpreted-text role="ref"}, in
wp-admin/theme-editor.php:247.

The condition checks first if \$has\_templates or \$theme-\>parent(),
and one of the two is sufficient to be valid. Then, it checks again that
\$theme-\>parent() is activated with &&. This condition may be reduced
by calling \$theme-\>parent(), as \$has\_template is unused here.

``` {.php}
<?php if ( ( $has_templates || $theme->parent() ) && $theme->parent() ) : ?>
```

------------------------------------------------------------------------

#### Dolibarr {#dolibarr-structures-identicalconditions}

`identical-conditions`{.interpreted-text role="ref"}, in
htdocs/core/lib/files.lib.php:2052.

Better check twice that \$modulepart is really
\'apercusupplier\_invoice\'.

``` {.php}
$modulepart == 'apercusupplier_invoice' || $modulepart == 'apercusupplier_invoice'
```

------------------------------------------------------------------------

#### Mautic {#mautic-structures-identicalconditions}

`identical-conditions`{.interpreted-text role="ref"}, in
app/bundles/CoreBundle/Views/Standard/list.html.php:47.

When the line is long, it tends to be more and more difficult to review
the values. Here, one of the two first is too many.

``` {.php}
!empty($permissions[$permissionBase . ':deleteown']) || !empty($permissions[$permissionBase . ':deleteown']) || !empty($permissions[$permissionBase . ':delete'])
```

### No Choice

#### NextCloud {#nextcloud-structures-nochoice}

`no-choice`{.interpreted-text role="ref"}, in
build/integration/features/bootstrap/FilesDropContext.php:71.

Token is checked, but processed in the same way each time. This actual
check is done twice, in the same class, in the method
droppingFileWith().

``` {.php}
public function creatingFolderInDrop($folder) {
        $client = new Client();
        $options = [];
        if (count($this->lastShareData->data->element) > 0){
            $token = $this->lastShareData->data[0]->token;
        } else {
            $token = $this->lastShareData->data[0]->token;
        }
        $base = substr($this->baseUrl, 0, -4);
        $fullUrl = $base . '/public.php/webdav/' . $folder;

        $options['auth'] = [$token, ''];
```

------------------------------------------------------------------------

#### Zencart {#zencart-structures-nochoice}

`no-choice`{.interpreted-text role="ref"}, in
admin/includes/functions/html\_output.php:179.

At least, it always choose the most secure way : use SSL.

``` {.php}
if ($usessl) {
        $form .= zen_href_link($action, $parameters, 'NONSSL');
      } else {
        $form .= zen_href_link($action, $parameters, 'NONSSL');
      }
```

### Common Alternatives

#### Dolibarr {#dolibarr-structures-commonalternatives}

`common-alternatives`{.interpreted-text role="ref"}, in
htdocs/admin/facture.php:531.

The opening an closing tag couldd be moved outside the if condition :
they are compulsory in both cases.

``` {.php}
// Active
                                if (in_array($name, $def))
                                {
                                    print '<td class="center">'."\n";
                                    print '<a href="'.$_SERVER["PHP_SELF"].'?action=del&value='.$name.'">';
                                    print img_picto($langs->trans("Enabled"), 'switch_on');
                                    print '</a>';
                                    print '</td>';
                                }
                                else
                                {
                                    print '<td class=center\>'."\n";
                                    print '<a href="'.$_SERVER["PHP_SELF"].'?action=set&value='.$name.'&scan_dir='.$module->scandir.'&label='.urlencode($module->name).'">'.img_picto($langs->trans("SetAsDefault"), 'switch_off').'</a>';
                                    print "</td>";
                                }
```

------------------------------------------------------------------------

#### NextCloud {#nextcloud-structures-commonalternatives}

`common-alternatives`{.interpreted-text role="ref"}, in
apps/encryption/lib/KeyManager.php:436.

[\$shareKey = \$this-\>getShareKey(\$path, \$uid);]{.title-ref} is
common to all three alternatives. In fact, [\$uid =
\$this-\>getPublicShareKeyId();]{.title-ref} is not common, and that
shoul de reviewed, as [\$uid]{.title-ref} will be undefined.

``` {.php}
if ($this->util->isMasterKeyEnabled()) {
            $uid = $this->getMasterKeyId();
            $shareKey = $this->getShareKey($path, $uid);
            if ($publicAccess) {
                $privateKey = $this->getSystemPrivateKey($uid);
                $privateKey = $this->crypt->decryptPrivateKey($privateKey, $this->getMasterKeyPassword(), $uid);
            } else {
                // when logged in, the master key is already decrypted in the session
                $privateKey = $this->session->getPrivateKey();
            }
        } else if ($publicAccess) {
            // use public share key for public links
            $uid = $this->getPublicShareKeyId();
            $shareKey = $this->getShareKey($path, $uid);
            $privateKey = $this->keyStorage->getSystemUserKey($this->publicShareKeyId . '.privateKey', Encryption::ID);
            $privateKey = $this->crypt->decryptPrivateKey($privateKey);
        } else {
            $shareKey = $this->getShareKey($path, $uid);
            $privateKey = $this->session->getPrivateKey();
        }
```

### Logical Mistakes

#### Dolibarr {#dolibarr-structures-logicalmistakes}

`logical-mistakes`{.interpreted-text role="ref"}, in
htdocs/core/lib/admin.lib.php:1165.

This expression is always true. When [\$nbtabsql]{.title-ref} is
[\$nbtablib]{.title-ref}, the left part is true; When
[\$nbtabsql]{.title-ref} is [\$nbtabsqlsort]{.title-ref}, the right part
is true; When any other value is provided, both operands are true.

``` {.php}
$nbtablib != $nbtabsql || $nbtabsql != $nbtabsqlsort
```

------------------------------------------------------------------------

#### Cleverstyle {#cleverstyle-structures-logicalmistakes}

`logical-mistakes`{.interpreted-text role="ref"}, in
modules/HybridAuth/Hybrid/Providers/DigitalOcean.php:123.

This expression is always false. When
[\$data-\>account-\>email\_verified]{.title-ref} is [true]{.title-ref},
the right part is false; When
[\$data-\>account-\>email\_verified]{.title-ref} is
[\$data-\>account-\>email]{.title-ref}, the right part is false; The
only viable solution is to have \` \$data-\>account-\>email\`true : this
is may be the intend it, though it is not easy to understand.

``` {.php}
TRUE == $data->account->email_verified and $data->account->email == $data->account->email_verified
```

### Same Conditions In Condition

#### TeamPass {#teampass-structures-sameconditions}

`same-conditions-in-condition`{.interpreted-text role="ref"}, in
sources/identify.php:1096.

[\$result == 1]{.title-ref} is use once in the main if/then, then again
the second if/then/elseif structure. Both are incompatible, since, in
the else, [\$result]{.title-ref} will be different from 1.

``` {.php}
if ($result == 1) {
                $return = "";
                $logError = "";
                $proceedIdentification = true;
                $userPasswordVerified = false;
                unset($_SESSION['hedgeId']);
                unset($_SESSION['flickercode']);
            } else {
                if ($result < -10) {
                    $logError = "ERROR: ".$result;
                } elseif ($result == -4) {
                    $logError = "Wrong response code, no more tries left.";
                } elseif ($result == -3) {
                    $logError = "Wrong response code, try to reenter.";
                } elseif ($result == -2) {
                    $logError = "Timeout. The response code is not valid anymore.";
                } elseif ($result == -1) {
                    $logError = "Security Error. Did you try to verify the response from a different computer?";
                } elseif ($result == 1) {
                    $logError = "Authentication successful, response code correct.
                          <br /><br />Authentification Method for SecureBrowser updated!";
                    // Add necessary code here for accessing your Business Application
                }
                $return = "agses_error";
                echo '[{"value" : "'.$return.'", "user_admin":"',
                isset($_SESSION['user_admin']) ? $_SESSION['user_admin'] : "",
                '", "initial_url" : "'.@$_SESSION['initial_url'].'",
                "error" : "'.$logError.'"}]';

                exit();
            }
```

------------------------------------------------------------------------

#### Typo3 {#typo3-structures-sameconditions}

`same-conditions-in-condition`{.interpreted-text role="ref"}, in
typo3/sysext/recordlist/Classes/RecordList/DatabaseRecordList.php:1696.

[\$table == \'pages]{.title-ref} is caught initially, and if it fails,
it is tested again in the final else. This won\'t happen.

``` {.php}
} elseif ($table === 'pages') {
                                $parameters = ['id' => $this->id, 'pagesOnly' => 1, 'returnUrl' => GeneralUtility::getIndpEnv('REQUEST_URI')];
                                $href = (string)$uriBuilder->buildUriFromRoute('db_new', $parameters);
                                $icon = '<a class="btn btn-default" href="' . htmlspecialchars($href) . '" title="' . htmlspecialchars($lang->getLL('new')) . '">'
                                    . $spriteIcon->render() . '</a>';
                            } else {
                                $params = '&edit[' . $table . '][' . $this->id . ']=new';
                                if ($table === 'pages') {
                                    $params .= '&overrideVals[pages][doktype]=' . (int)$this->pageRow['doktype'];
                                }
                                $icon = '<a class="btn btn-default" href="#" onclick="' . htmlspecialchars(BackendUtility::editOnClick($params, '', -1))
                                    . '" title="' . htmlspecialchars($lang->getLL('new')) . '">' . $spriteIcon->render() . '</a>';
                            }
```

### Return True False

#### Mautic {#mautic-structures-returntruefalse}

`return-true-false`{.interpreted-text role="ref"}, in
app/bundles/LeadBundle/Model/ListModel.php:125.

\$isNew could be a typecast.

``` {.php}
$isNew = ($entity->getId()) ? false : true;
```

------------------------------------------------------------------------

#### FuelCMS {#fuelcms-structures-returntruefalse}

`return-true-false`{.interpreted-text role="ref"}, in
fuel/modules/fuel/helpers/validator\_helper.php:254.

If/then is a lot of code to produce a boolean.

``` {.php}
function length_min($str, $limit = 1)
    {
        if (strlen(strval($str)) < $limit)
        {
            return FALSE;
        }
        else
        {
            return TRUE;
        }
    }
```

### Useless Switch

#### Phpdocumentor {#phpdocumentor-structures-uselessswitch}

`useless-switch`{.interpreted-text role="ref"}, in
fuel/modules/fuel/libraries/Inspection.php:349.

This method parses comments. In fact, comments are represented by other
tokens, which may be added or removed at time while coding.

``` {.php}
public function parse_comments($code)
    {
        $comments = array();
        $tokens = token_get_all($code);

        foreach($tokens as $token)
        {
            switch($token[0])
            {
                case T_DOC_COMMENT:
                    $comments[] = $token[1];
                    break;
            }
        }
        return $comments;

    }
```

------------------------------------------------------------------------

#### Dolphin {#dolphin-structures-uselessswitch}

`useless-switch`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/inc/classes/BxDolModuleDb.php:34.

\$aParams is an argument : this code looks like the switch is reserved
for future use.

``` {.php}
function getModulesBy($aParams = array())
    {
        $sMethod = 'getAll';
        $sPostfix = $sWhereClause = "";

        $sOrderClause = "ORDER BY `title`";
        switch($aParams['type']) {
            case 'path':
                $sMethod = 'getRow';
                $sPostfix .= '_path';
                $sWhereClause .= "AND `path`='" . $aParams['value'] . "'";
                break;
        }
```

### Could Use \_\_[DIR](getBaseUrl%20and%20__setBaseUrl%20shouldn't%20be%20named%20like%20that.)

#### Woocommerce {#woocommerce-structures-couldusedir}

`could-use-\_\_dir\_\_`{.interpreted-text role="ref"}, in
includes/class-wc-api.php:162.

All the 120 occurrences use [dirname( \_\_FILE\_\_ )]{.title-ref}, and
could be upgraded to \_\_[DIR](DIR__%20Then%20Slash) if backward
compatibility to PHP 5.2 is not critical.

``` {.php}
private function rest_api_includes() {
        // Exception handler.
        include_once dirname( __FILE__ ) . '/api/class-wc-rest-exception.php';

        // Authentication.
        include_once dirname( __FILE__ ) . '/api/class-wc-rest-authentication.php';
```

------------------------------------------------------------------------

#### Piwigo {#piwigo-structures-couldusedir}

`could-use-\_\_dir\_\_`{.interpreted-text role="ref"}, in
include/random\_compat/random.php:50.

[dirname( \_\_FILE\_\_ )]{.title-ref} is cached into \$RandomCompatDIR,
then reused three times. Using \_\_[DIR](debugInfo()%20Usage) would save
that detour.

``` {.php}
$RandomCompatDIR = dirname(__FILE__);

    require_once $RandomCompatDIR.'/byte_safe_strings.php';
    require_once $RandomCompatDIR.'/cast_to_int.php';
    require_once $RandomCompatDIR.'/error_polyfill.php';
```

### Should Use Coalesce

#### ChurchCRM {#churchcrm-php-shouldusecoalesce}

`should-use-coalesce`{.interpreted-text role="ref"}, in
src/ChurchCRM/Service/FinancialService.php:597.

ChurchCRM features 5 old style ternary operators, which are all in this
SQL query. ChurchCRM requires PHP 7.0, so a simple code review could
remove them all.

``` {.php}
$sSQL = "INSERT INTO pledge_plg
                    (plg_famID,
                    plg_FYID, 
                    plg_date, 
                    plg_amount,
                    plg_schedule, 
                    plg_method, 
                    plg_comment, 
                    plg_DateLastEdited, 
                    plg_EditedBy, 
                    plg_PledgeOrPayment, 
                    plg_fundID, 
                    plg_depID, 
                    plg_CheckNo, 
                    plg_scanString, 
                    plg_aut_ID, 
                    plg_NonDeductible, 
                    plg_GroupKey)
                    VALUES ('".
          $payment->FamilyID."','".
          $payment->FYID."','".
          $payment->Date."','".
          $Fund->Amount."','".
          (isset($payment->schedule) ? $payment->schedule : 'NULL')."','".
          $payment->iMethod."','".
          $Fund->Comment."','".
          date('YmdHis')."',".
          $_SESSION['user']->getId().",'".
          $payment->type."',".
          $Fund->FundID.','.
          $payment->DepositID.','.
          (isset($payment->iCheckNo) ? $payment->iCheckNo : 'NULL').",'".
          (isset($payment->tScanString) ? $payment->tScanString : 'NULL')."','".
          (isset($payment->iAutID) ? $payment->iAutID : 'NULL')."','".
          (isset($Fund->NonDeductible) ? $Fund->NonDeductible : 'NULL')."','".
          $sGroupKey."')";
```

------------------------------------------------------------------------

#### Cleverstyle {#cleverstyle-php-shouldusecoalesce}

`should-use-coalesce`{.interpreted-text role="ref"}, in
modules/Feedback/index.php:37.

Cleverstyle nests ternary operators when selecting default values. Here,
moving some of them to ?? will reduce the code complexity and make it
more readable. Cleverstyle requires PHP 7.0 or more recent.

``` {.php}
$Page->content(
    h::{'cs-form form'}(
        h::{'section.cs-feedback-form article'}(
            h::{'header h2.cs-text-center'}($L->Feedback).
            h::{'table.cs-table[center] tr| td'}(
                [
                    h::{'cs-input-text input[name=name][required]'}(
                        [
                            'placeholder' => $L->feedback_name,
                            'value'       => $User->user() ? $User->username() : (isset($_POST['name']) ? $_POST['name'] : '')
                        ]
                    ),
                    h::{'cs-input-text input[type=email][name=email][required]'}(
                        [
                            'placeholder' => $L->feedback_email,
                            'value'       => $User->user() ? $User->email : (isset($_POST['email']) ? $_POST['email'] : '')
                        ]
                    ),
                    h::{'cs-textarea[autosize] textarea[name=text][required]'}(
                        [
                            'placeholder' => $L->feedback_text,
                            'value'       => isset($_POST['text']) ? $_POST['text'] : ''
                        ]
                    ),
                    h::{'cs-button button[type=submit]'}($L->feedback_send)
                ]
            )
        )
    )
);
```

### If With Same Conditions

#### phpMyAdmin {#phpmyadmin-structures-ifwithsameconditions}

`if-with-same-conditions`{.interpreted-text role="ref"}, in
libraries/classes/Response.php:345.

The first test on \$this-\>\_isSuccess settles the situation with
\_JSON. Then, a second check is made. Both could be merged, also the
second one is fairly long (not shown).

``` {.php}
if ($this->_isSuccess) {
            $this->_JSON['success'] = true;
        } else {
            $this->_JSON['success'] = false;
            $this->_JSON['error']   = $this->_JSON['message'];
            unset($this->_JSON['message']);
        }

        if ($this->_isSuccess) {
```

------------------------------------------------------------------------

#### Phpdocumentor {#phpdocumentor-structures-ifwithsameconditions}

`if-with-same-conditions`{.interpreted-text role="ref"}, in
src/phpDocumentor/Transformer/Command/Project/TransformCommand.php:239.

\$templates is extracted from \$input. If it is empty, a second source
is polled. Finally, if nothing has worked, a default value is used
(\'clean\'). In this case, each attempt is an alternative solution to
the previous failing call. The second test could be reported on
\$templatesFromConfig, and not \$templates.

``` {.php}
$templates = $input->getOption('template');
        if (!$templates) {
            /** @var Template[] $templatesFromConfig */
            $templatesFromConfig = $configurationHelper->getConfigValueFromPath('transformations/templates');
            foreach ($templatesFromConfig as $template) {
                $templates[] = $template->getName();
            }
        }

        if (!$templates) {
            $templates = array('clean');
        }
```

### Throw Functioncall

#### SugarCrm {#sugarcrm-exceptions-throwfunctioncall}

`throw-functioncall`{.interpreted-text role="ref"}, in
include/externalAPI/cmis\_repository\_wrapper.php:918.

SugarCRM uses exceptions to fill work in progress. Here, we recognize a
forgotten \'new\' that makes throw call a function named \'Exception\'.
This fails with a Fatal Error, and doesn\'t issue the right messsage.
The same error had propgated in the code by copy and paste : it is
available 17 times in that same file.

``` {.php}
function getContentChanges()
    {
        throw Exception("Not Implemented");
    }
```

------------------------------------------------------------------------

#### Zurmo {#zurmo-exceptions-throwfunctioncall}

`throw-functioncall`{.interpreted-text role="ref"}, in
app/protected/modules/gamification/rules/collections/GameCollectionRules.php:66.

Other part of the code actually instantiate the exception before
throwing it.

``` {.php}
abstract class GameCollectionRules
    {
        /**
         * @return string
         * @throws NotImplementedException - Implement in children classes
         */
        public static function getType()
        {
            throw NotImplementedException();
        }
```

### Use Instanceof

#### TeamPass {#teampass-classes-useinstanceof}

`use-instanceof`{.interpreted-text role="ref"}, in
includes/libraries/Database/Meekrodb/db.class.php:506.

In this code, `is_object()` and `instanceof` have the same basic : they
both check that \$ts is an object. In fact, `instanceof` is more
precise, and give more information about the variable.

``` {.php}
protected function parseTS($ts) {
    if (is_string($ts)) return date('Y-m-d H:i:s', strtotime($ts));
    else if (is_object($ts) && ($ts instanceof DateTime)) return $ts->format('Y-m-d H:i:s');
  }
```

------------------------------------------------------------------------

#### Zencart {#zencart-classes-useinstanceof}

`use-instanceof`{.interpreted-text role="ref"}, in
includes/modules/payment/firstdata\_hco.php:104.

In this code, `is_object()` is used to check the status of the order.
Possibly, \$order is false or null in case of incompatible status. Yet,
when \$object is an object, and in particular being a global that may be
assigned anywhere else in the code, it seems that the method
\'update\_status\' is magically always available. Here, using instance
of to make sure that \$order is an \'paypal\' class, or a
\'storepickup\' or any of the payment class.

``` {.php}
function __construct() {
    global $order;

    // more lines, no mention of $order
    if (is_object($order)) $this->update_status();

    // more code
}
```

### Always Positive Comparison

#### Magento {#magento-structures-nevernegative}

`always-positive-comparison`{.interpreted-text role="ref"}, in
app/code/core/Mage/Dataflow/Model/Profile.php:85.

strlen((\$actiosXML) will never be negative, and hence, is always false.
This exception is never thrown.

``` {.php}
if (strlen($actionsXML) < 0 &&
        @simplexml_load_string('<data>' . $actionsXML . '</data>', null, LIBXML_NOERROR) === false) {
            Mage::throwException(Mage::helper('dataflow')->__("Actions XML is not valid."));
        }
```

### Empty Blocks

#### Cleverstyle {#cleverstyle-structures-emptyblocks}

`empty-blocks`{.interpreted-text role="ref"}, in
modules/Blogs/api/Controller.php:44.

Else is empty, but commented.

``` {.php}
public static function posts_get ($Request) {
        $id = $Request->route_ids(0);
        if ($id) {
            $post = Posts::instance()->get($id);
            if (!$post) {
                throw new ExitException(404);
            }
            return $post;
        } else {
            // TODO: implement latest posts
        }
    }
```

------------------------------------------------------------------------

#### PhpIPAM {#phpipam-structures-emptyblocks}

`empty-blocks`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

The `then` block is empty and commented : yet, it may have been clearer
to make the condition != and omitted the whole empty block.

``` {.php}
/* checks */
if($_POST['action'] == delete) {
    # no cecks
}
else {
    # remove spaces
    $_POST['name'] = trim($_POST['name']);

    # length > 4 and < 12
    if( (mb_strlen($_POST['name']) < 2) || (mb_strlen($_POST['name']) > 24) )   { $errors[] = _('Name must be between 4 and 24 characters'); }
```

### Dependant Trait

#### Zencart {#zencart-traits-dependanttrait}

`dependant-trait`{.interpreted-text role="ref"}, in
app/library/zencart/CheckoutFlow/src/AccountFormValidator.php:14.

Note that addressEntries is used, and is also expected to be an array or
an object with ArrayAccess. \$addressEntries is only defined in a class
called \'Guest\' which is also the only one using that trait. Any other
class using the AccountFormValidator trait must define addressEntries.

``` {.php}
trait AccountFormValidator
{

    abstract protected function getAddressFieldValue($fieldName);

    /**
     * @return bool|int
     */
    protected function errorProcessing()
    {
        $error = false;
        foreach ($this->addressEntries as $fieldName => $fieldDetails) {
            $this->addressEntries[$fieldName]['value'] = $this->getAddressFieldValue($fieldName);
            $fieldError = $this->processFieldValidator($fieldName, $fieldDetails);
            $this->addressEntries[$fieldName]['error'] = $fieldError;
            $error = $error | $fieldError;
        }
        return $error;
    }
```

### Hidden Use Expression

#### Tikiwiki {#tikiwiki-namespaces-hiddenuse}

`hidden-use-expression`{.interpreted-text role="ref"}, in
lib/core/Tiki/Command/DailyReportSendCommand.php:17.

Sneaky error\_reporting, hidden among the use calls.

``` {.php}
namespace Tiki\Command;

use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputArgument;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Input\InputOption;
use Symfony\Component\Console\Output\OutputInterface;
error_reporting(E_ALL);
use TikiLib;
use Reports_Factory;
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-namespaces-hiddenuse}

`hidden-use-expression`{.interpreted-text role="ref"}, in
interface/patient\_file/summary/browse.php:23.

Use expression is only reached when the csrf token is checked. This
probably save some CPU when no csrf is available, but it breaks the
readability of the file.

``` {.php}
<?php
/**
 * Patient selector for insurance gui
 *
 * @package   OpenEMR
 * @link      http://www.open-emr.org
 * @author    Brady Miller <brady.g.miller@gmail.com>
 * @copyright Copyright (c) 2018 Brady Miller <brady.g.miller@gmail.com>
 * @license   https://github.com/openemr/openemr/blob/master/LICENSE GNU General Public License 3
 */


require_once(../../globals.php);
require_once($srcdir/patient.inc);
require_once($srcdir/options.inc.php);

if (!empty($_POST)) {
    if (!verifyCsrfToken($_POST[csrf_token_form])) {
        csrfNotVerified();
    }
}

use OpenEMR\Core\Header;
```

### Multiple Alias Definitions

#### ChurchCRM {#churchcrm-namespaces-multiplealiasdefinitions}

`multiple-alias-definitions`{.interpreted-text role="ref"}, in Various
files:\--.

It is actually surprising to find FamilyQuery defined as
ChurchCRMBaseFamilyQuery only once, while all other reference are for
ChurchCRMFamilyQuery. That lone use is actually useful in the code, so
it is not a forgotten refactorisation.

``` {.php}
use ChurchCRM\Base\FamilyQuery  // in /src/MapUsingGoogle.php:7

use ChurchCRM\FamilyQuery   // in /src/ChurchCRM/Dashboard/EventsDashboardItem.php:8
                            // and 29 other files
```

------------------------------------------------------------------------

#### Phinx {#phinx-namespaces-multiplealiasdefinitions}

`multiple-alias-definitions`{.interpreted-text role="ref"}, in Various
files:\--.

One \'Command\' is refering to a local Command class, while the other is
refering to an imported class. They are all in a similar name space
ConsoleCommand.

``` {.php}
use Phinx\Console\Command                       //in file /src/Phinx/Console/PhinxApplication.php:34
use Symfony\Component\Console\Command\Command   //in file /src/Phinx/Console/Command/Init.php:31
use Symfony\Component\Console\Command\Command   //in file /src/Phinx/Console/Command/AbstractCommand.php:32
```

### Nested Ifthen

#### LiveZilla {#livezilla-structures-nestedifthen}

`nested-ifthen`{.interpreted-text role="ref"}, in
livezilla/\_lib/objects.global.inc.php:847.

The first condition is fairly complex, and could also return early.
Then, the second nested if could be merged into one : this would reduce
the number of nesting, but make the condition higher.

``` {.php}
if(isset(Server::$Configuration->File["gl_url_detect"]) && !Server::$Configuration->File["gl_url_detect"] && isset(Server::$Configuration->File["gl_url"]) && !empty(Server::$Configuration->File["gl_url"]))
        {
            $url = Server::$Configuration->File["gl_url"];
        }
        else if(isset($_SERVER["HTTP_HOST"]) && !empty($_SERVER["HTTP_HOST"]))
        {
            $host = $_SERVER["HTTP_HOST"];
            $path = $_SERVER["PHP_SELF"];

            if(!empty($path) && !Str::EndsWith(strtolower($path),strtolower($_file)) && strpos(strtolower($path),strtolower($_file)) !== false)
            {
                if(empty(Server::$Configuration->File["gl_kbmr"]))
                {
                    Logging::DebugLog(serialize($_SERVER));
                    exit("err 888383; can't read $_SERVER[\"HTTP_HOST\"] and $_SERVER[\"PHP_SELF\"]");
                }
            }

            define("LIVEZILLA_DOMAIN",Communication::GetScheme() . $host);
            $url = LIVEZILLA_DOMAIN . str_replace($_file,"",htmlentities($path,ENT_QUOTES,"UTF-8"));
        }
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-structures-nestedifthen}

`nested-ifthen`{.interpreted-text role="ref"}, in
includes/Linker.php:1493.

There are 5 level of nesting here, from the beginning of the method,
down to the last condition. All work on local variables, as it is a
static method. May be breaking this into smaller functions would help
readability.

``` {.php}
public static function normalizeSubpageLink( $contextTitle, $target, &$text ) {
        $ret = $target; # default return value is no change

        # Some namespaces don't allow subpages,
        # so only perform processing if subpages are allowed
        if (
            $contextTitle && MediaWikiServices::getInstance()->getNamespaceInfo()->
            hasSubpages( $contextTitle->getNamespace() )
        ) {
            $hash = strpos( $target, '#' );
            if ( $hash !== false ) {
                $suffix = substr( $target, $hash );
                $target = substr( $target, 0, $hash );
            } else {
                $suffix = '';
            }
            # T9425
            $target = trim( $target );
            $contextPrefixedText = MediaWikiServices::getInstance()->getTitleFormatter()->
                getPrefixedText( $contextTitle );
            # Look at the first character
            if ( $target != '' && $target[0] === '/' ) {
                # / at end means we don't want the slash to be shown
                $m = [];
                $trailingSlashes = preg_match_all( '%(/+)$%', $target, $m );
                if ( $trailingSlashes ) {
                    $noslash = $target = substr( $target, 1, -strlen( $m[0][0] ) );
                } else {
                    $noslash = substr( $target, 1 );
                }

                $ret = $contextPrefixedText . '/' . trim( $noslash ) . $suffix;
                if ( $text === '' ) {
                    $text = $target . $suffix;
                } # this might be changed for ugliness reasons
            } else {
                # check for .. subpage backlinks
                $dotdotcount = 0;
                $nodotdot = $target;
                while ( strncmp( $nodotdot, "../", 3 ) == 0 ) {
                    ++$dotdotcount;
                    $nodotdot = substr( $nodotdot, 3 );
                }
                if ( $dotdotcount > 0 ) {
                    $exploded = explode( '/', $contextPrefixedText );
                    if ( count( $exploded ) > $dotdotcount ) { # not allowed to go below top level page
                        $ret = implode( '/', array_slice( $exploded, 0, -$dotdotcount ) );
                        # / at the end means don't show full path
                        if ( substr( $nodotdot, -1, 1 ) === '/' ) {
                            $nodotdot = rtrim( $nodotdot, '/' );
                            if ( $text === '' ) {
                                $text = $nodotdot . $suffix;
                            }
                        }
                        $nodotdot = trim( $nodotdot );
                        if ( $nodotdot != '' ) {
                            $ret .= '/' . $nodotdot;
                        }
                        $ret .= $suffix;
                    }
                }
            }
        }

        return $ret;
    }
```

### Cast To Boolean

#### MediaWiki {#mediawiki-structures-casttoboolean}

`cast-to-boolean`{.interpreted-text role="ref"}, in
includes/page/WikiPage.php:2274.

\$options\[\'changed\'\] and \$options\[\'created\'\] are documented and
used as boolean. Yet, SiteStatsUpdate may require integers, for correct
storage in the database, hence the type casting. `(int) (bool)` may be
an alternative here.

``` {.php}
$edits = $options['changed'] ? 1 : 0;
        $pages = $options['created'] ? 1 : 0;


        DeferredUpdates::addUpdate( SiteStatsUpdate::factory(
            [ 'edits' => $edits, 'articles' => $good, 'pages' => $pages ]
        ) );
```

------------------------------------------------------------------------

#### Dolibarr {#dolibarr-structures-casttoboolean}

`cast-to-boolean`{.interpreted-text role="ref"}, in
htdocs/societe/class/societe.class.php:2777.

Several cases are built on the same pattern there. Each of the
expression may be replaced by a cast to `(bool)`.

``` {.php}
case 3:
                $ret=(!$conf->global->SOCIETE_IDPROF3_UNIQUE?false:true);
                break;
```

### Failed Substr Comparison

#### Zurmo {#zurmo-structures-failingsubstrcomparison}

`failed-substr-comparison`{.interpreted-text role="ref"}, in
app/protected/modules/zurmo/modules/SecurableModule.php:117.

filterAuditEvent compares a six char string with \'AUDIT\_EVENT\_\'
which contains 10 chars. This method returns only FALSE. Although it is
used only once, the whole block that calls this method is now dead code.

``` {.php}
private static function filterAuditEvent($s)
        {
            return substr($s, 0, 6) == 'AUDIT_EVENT_';
        }
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-structures-failingsubstrcomparison}

`failed-substr-comparison`{.interpreted-text role="ref"}, in
includes/media/DjVu.php:263.

\$metadata contains data that may be in different formats. When it is a
pure XML file, it is \'Old style\'. The comment helps understanding that
this is not the modern way to go : the Old Style is actually never
called, due to a failing condition.

``` {.php}
private function getUnserializedMetadata( File $file ) {
        $metadata = $file->getMetadata();
        if ( substr( $metadata, 0, 3 ) === '<?xml' ) {
            // Old style. Not serialized but instead just a raw string of XML.
            return $metadata;
        }
```

### Should Make Ternary

#### ChurchCRM {#churchcrm-structures-shouldmaketernary}

`should-make-ternary`{.interpreted-text role="ref"}, in
src/CartToFamily.php:57.

\$sState could be the receiving part of a ternary operator.

``` {.php}
if ($sCountry == 'United States' || $sCountry == 'Canada') {
            $sState = InputUtils::LegacyFilterInput($_POST['State']);
        } else {
            $sState = InputUtils::LegacyFilterInput($_POST['StateTextbox']);
        }
```

### Use Positive Condition

#### SPIP {#spip-structures-usepositivecondition}

`use-positive-condition`{.interpreted-text role="ref"}, in
ecrire/inc/utils.php:925.

if (isset(\$time\[\$t\])) { } else { } would put the important case in
first place, and be more readable.

``` {.php}
if (!isset($time[$t])) {
        $time[$t] = $a + $b;
    } else {
        $p = ($a + $b - $time[$t]) * 1000;
        unset($time[$t]);
#           echo "'$p'";exit;
        if ($raw) {
            return $p;
        }
        if ($p < 1000) {
            $s = '';
        } else {
            $s = sprintf("%d ", $x = floor($p / 1000));
            $p -= ($x * 1000);
        }

        return $s . sprintf($s ? "%07.3f ms" : "%.3f ms", $p);
    }
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-structures-usepositivecondition}

`use-positive-condition`{.interpreted-text role="ref"}, in
system/ee/EllisLab/Addons/forum/mod.forum\_core.php:9138.

Let\'s be positive, and start processing the presence of \$topic first.
And let\'s call it empty(), not == \'\'.

``` {.php}
if ($topic != '')
                        {
                            $sql .= '('.substr($topic, 0, -3).') OR ';
                            $sql .= '('.substr($tbody, 0, -3).') ';
                        }
                        else
                        {
                            $sql = substr($sql, 0, -3);
                        }
```

### Use ::Class Operator

#### Typo3 {#typo3-classes-useclassoperator}

`use-\:\:class-operator`{.interpreted-text role="ref"}, in
typo3/sysext/install/Configuration/ExtensionScanner/Php/ConstructorArgumentMatcher.php:4.

`TYPO3\CMS\Core\Package\PackageManager` could be
`TYPO3\CMS\Core\Package\PackageManager::class`.

``` {.php}
return [
    'TYPO3\CMS\Core\Package\PackageManager' => [
        'required' => [
            'numberOfMandatoryArguments' => 1,
            'maximumNumberOfArguments' => 1,
```

### Don\'t Echo Error

#### ChurchCRM {#churchcrm-security-dontechoerror}

`don't-echo-error`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This is classic debugging code that should never reach production.
mysqli\_error() and mysqli\_errno() provide valuable information is case
of an error, and may be exploited by intruders.

``` {.php}
if (mysqli_error($cnInfoCentral) != '') {
        echo gettext('An error occured: ').mysqli_errno($cnInfoCentral).'--'.mysqli_error($cnInfoCentral);
    } else {
```

------------------------------------------------------------------------

#### Phpdocumentor {#phpdocumentor-security-dontechoerror}

`don't-echo-error`{.interpreted-text role="ref"}, in
src/phpDocumentor/Plugin/Graphs/Writer/Graph.php:77.

Default development behavior : display the caught exception. Production
behavior should not display that message, but log it for later review.
Also, the return in the catch should be moved to the main code sequence.

``` {.php}
public function processClass(ProjectDescriptor $project, Transformation $transformation)
    {
        try {
            $this->checkIfGraphVizIsInstalled();
        } catch (\Exception $e) {
            echo $e->getMessage();

            return;
        }
```

### Useless Type Casting

#### FuelCMS {#fuelcms-structures-uselesscasting}

`useless-type-casting`{.interpreted-text role="ref"}, in
fuel/codeigniter/core/URI.php:214.

substr() always returns a string, so there is no need to enforce this.

``` {.php}
if (isset($_SERVER['SCRIPT_NAME'][0]))
        {
            if (strpos($uri, $_SERVER['SCRIPT_NAME']) === 0)
            {
                $uri = (string) substr($uri, strlen($_SERVER['SCRIPT_NAME']));
            }
            elseif (strpos($uri, dirname($_SERVER['SCRIPT_NAME'])) === 0)
            {
                $uri = (string) substr($uri, strlen(dirname($_SERVER['SCRIPT_NAME'])));
            }
        }
```

------------------------------------------------------------------------

#### ThinkPHP {#thinkphp-structures-uselesscasting}

`useless-type-casting`{.interpreted-text role="ref"}, in
ThinkPHP/Library/Think/Db/Driver/Sqlsrv.class.php:67.

A comparison always returns a boolean, except for the spaceship
operator.

``` {.php}
foreach ($result as $key => $val) {
                $info[$val['column_name']] = array(
                    'name'    => $val['column_name'],
                    'type'    => $val['data_type'],
                    'notnull' => (bool) ('' === $val['is_nullable']), // not null is empty, null is yes
                    'default' => $val['column_default'],
                    'primary' => false,
                    'autoinc' => false,
                );
            }
```

### No isset() With empty()

#### XOOPS {#xoops-structures-noissetwithempty}

`no-isset()-with-empty()`{.interpreted-text role="ref"}, in
htdocs/class/tree.php:297.

Too much vlaidation

``` {.php}
isset($this->tree[$key]['child']) && !empty($this->tree[$key]['child']);
```

### Useless Check

#### Magento {#magento-structures-uselesscheck}

`useless-check`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code assumes that \$delete is an array, then checks if it empty.
Foreach will take care of the empty check.

``` {.php}
if (!empty($delete)) {
            foreach ($delete as $categoryId) {
                $where = array(
                    'product_id = ?'  => (int)$object->getId(),
                    'category_id = ?' => (int)$categoryId,
                );

                $write->delete($this->_productCategoryTable, $where);
            }
        }
```

------------------------------------------------------------------------

#### Phinx {#phinx-structures-uselesscheck}

`useless-check`{.interpreted-text role="ref"}, in
src/Phinx/Migration/Manager.php:828.

If \$dependencies is not empty, foreach() skips the loops.

``` {.php}
private function getSeedDependenciesInstances(AbstractSeed $seed)
    {
        $dependenciesInstances = [];
        $dependencies = $seed->getDependencies();
        if (!empty($dependencies)) {
            foreach ($dependencies as $dependency) {
                foreach ($this->seeds as $seed) {
                    if (get_class($seed) === $dependency) {
                        $dependenciesInstances[get_class($seed)] = $seed;
                    }
                }
            }
        }

        return $dependenciesInstances;
    }
```

### Bail Out Early

#### OpenEMR {#openemr-structures-bailoutearly}

`bail-out-early`{.interpreted-text role="ref"}, in
interface/modules/zend\_modules/module/Carecoordination/src/Carecoordination/Controller/EncounterccdadispatchController.php:69.

This is a typical example of a function mostly controlled by one
condition. It could be rewrite as \'if(\$validResult !=
\'existingpatient\')\' then return. The \'else\' clause is not used
anymore, and the whole block of code is now the main sequence of the
method.

``` {.php}
public function ccdaFetching($parameterArray = array())
    {
        $validResult = $this->getEncounterccdadispatchTable()->valid($parameterArray[0]);
        // validate credentials
        if ($validResult == 'existingpatient') {
/// Long bloc of code
        } else {
            return '<?xml version=1.0 encoding=UTF-8?>
            <!-- Edited by XMLSpy -->
            <note>

                <heading>Authetication Failure</heading>
                <body></body>
            </note>
            ';
        }
```

------------------------------------------------------------------------

#### opencfp {#opencfp-structures-bailoutearly}

`bail-out-early`{.interpreted-text role="ref"}, in
chair/assign\_auto\_reviewers\_weighted\_topic\_match.inc:105.

This long example illustrates two aspects : first, the shortcut to the
end of the method may be the \'then\' clause, not necessarily the
\'else\'. \'!in\_array(\$pid.\'-\'.\$rid, \$conflictAR)\' leads to
return, and the \'else\' should be removed, while keeping its content.
Secondly, we can see 3 conditions that all lead to a premature end to
the method. After refactoring all of them, the method would end up with
1 level of indentation, instead of 3.

``` {.php}
function oc_inConflict(&$conflictAR, $pid, $rid=null) {
    if ($rid == null) {
        $rid = $_SESSION[OCC_SESSION_VAR_NAME]['acreviewerid'];
    }
    if (!in_array($pid.'-'.$rid, $conflictAR)) {
        return false; // not in conflict
    } else {
        $tempr = ocsql_query("SELECT COUNT(*) AS `count` FROM `" . OCC_TABLE_PAPERREVIEWER . "` WHERE `paperid`='" . safeSQLstr($pid) . "' AND `reviewerid`='" . safeSQLstr($rid) . "'");
        if ((ocsql_num_rows($tempr) == 1)
            && ($templ = ocsql_fetch_assoc($tempr))
            && ($templ['count'] == 1)
        ) {
            return false; // assigned as reviewer
        } else {
            $tempr = ocsql_query("SELECT COUNT(*) AS `count` FROM `" . OCC_TABLE_PAPERADVOCATE . "` WHERE `paperid`='" . safeSQLstr($pid) . "' AND `advocateid`='" . safeSQLstr($rid) . "'");
            if ((ocsql_num_rows($tempr) == 1)
                && ($templ = ocsql_fetch_assoc($tempr))
                && ($templ['count'] == 1)
            ) {
                return false; // assigned as advocate
            }
        }
    }
    return true;
}
```

### Too Many Local Variables

#### HuMo-Gen {#humo-gen-functions-toomanylocalvariables}

`too-many-local-variables`{.interpreted-text role="ref"}, in
relations.php:813.

15 local variables pieces of code are hard to find in a compact form.
This function shows one classic trait of such issue : a large ifthen is
at the core of the function, and each time, it collects some values and
build a larger string. This should probably be split between different
methods in a class.

``` {.php}
function calculate_nephews($generX) { // handed generations x is removed from common ancestor
global $db_functions, $reltext, $sexe, $sexe2, $language, $spantext, $selected_language, $foundX_nr, $rel_arrayX, $rel_arrayspouseX, $spouse;
global $reltext_nor, $reltext_nor2; // for Norwegian and Danish

    if($selected_language=="es"){
        if($sexe=="m") { $neph=__('nephew'); $span_postfix="o "; $grson='nieto'; }
        else { $neph=__('niece'); $span_postfix="a "; $grson='nieta'; }
        //$gendiff = abs($generX - $generY); // FOUT
        $gendiff = abs($generX - $generY) - 1;
        $gennr=$gendiff-1;
        $degree=$grson." ".$gennr.$span_postfix;
        if($gendiff ==1) { $reltext=$neph.__(' of ');}
        elseif($gendiff > 1 AND $gendiff < 27) {
            spanish_degrees($gendiff,$grson);
            $reltext=$neph." ".$spantext.__(' of ');
        }
        else { $reltext=$neph." ".$degree; }
    } elseif ($selected_language==he){
        if($sexe=='m') { $nephniece = __('nephew'); }
///............
```

### Illegal Name For Method

#### PrestaShop {#prestashop-classes-wrongname}

`illegal-name-for-method`{.interpreted-text role="ref"}, in
admin-dev/ajaxfilemanager/inc/class.pagination.php:200.

``` {.php}
/**
     * get base url for pagination links aftr excluded those key
     * identified on excluded query strings
     *
     */
    function __getBaseUrl()
    {

        if(empty($this->baseUrl))
        {

            $this->__setBaseUrl();
        }
        return $this->baseUrl;
    }
```

------------------------------------------------------------------------

#### Magento {#magento-classes-wrongname}

`illegal-name-for-method`{.interpreted-text role="ref"}, in
app/code/core/Mage/Core/Block/Abstract.php:1139.

public method, called \'\_\_\'. Example : \$this-\>\_\_();

``` {.php}
public function __()
    {
        $args = func_get_args();
        $expr = new Mage_Core_Model_Translate_Expr(array_shift($args), $this->getModuleName());
        array_unshift($args, $expr);
        return $this->_getApp()->getTranslator()->translate($args);
    }
```

### Long Arguments

#### Cleverstyle {#cleverstyle-structures-longarguments}

`long-arguments`{.interpreted-text role="ref"}, in
core/drivers/DB/MySQLi.php:40.

This query is not complex, but its length tend to push the end out of
the view in the IDE. It could be rewritten as a variable, on the
previous line, with some formatting. The same formatting would help
without the variable too, yet, mixing the SQL syntax with the PHP
methodcall adds a layer of confusion.

``` {.php}
$this->instance->query("SET SESSION sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION'")
```

------------------------------------------------------------------------

#### Contao {#contao-structures-longarguments}

`long-arguments`{.interpreted-text role="ref"}, in
core-bundle/src/Resources/contao/widgets/CheckBoxWizard.php:145.

This one-liner includes 9 members and 6 variables : some are formatted
by sprintf, some are directly concatenated in the string. Breaking this
into two lines improves readbility and code review.

``` {.php}
sprintf('<span><input type="checkbox" name="%s" id="opt_%s" class="tl_checkbox" value="%s"%s%s onfocus="Backend.getScrollOffset()"> %s<label for="opt_%s">%s</label></span>', $this->strName . ($this->multiple ? '[]' : ''), $this->strId . '_' . $i, ($this->multiple ? \StringUtil::specialchars($arrOption['value']) : 1), (((\is_array($this->varValue) && \in_array($arrOption['value'], $this->varValue)) || $this->varValue == $arrOption['value']) ? ' checked="checked"' : ''), $this->getAttributes( ), $strButtons, $this->strId . '_' . $i, $arrOption['label'])
```

### No Boolean As Default

#### OpenConf {#openconf-functions-nobooleanasdefault}

`no-boolean-as-default`{.interpreted-text role="ref"}, in
openconf/include.php:1264.

Why do we need a [chair]{.title-ref} when printing a cell\'s file ?

``` {.php}
function oc_printFileCells(&$sub, $chair = false) { /**/ }
```

### Property Used In One Method Only

#### Contao {#contao-classes-propertyusedinonemethodonly}

`property-used-in-one-method-only`{.interpreted-text role="ref"}, in
calendar-bundle/src/Resources/contao/modules/ModuleEventlist.php:38.

Date is protected property. It is used only in the compile() method, and
it is not used by the parent class. As such, it may be turned into a
local variable.

``` {.php}
class ModuleEventlist extends Events
{

    /**
     * Current date object
     * @var Date
     */
    protected $Date;

// Date is used in function compile() only
```

------------------------------------------------------------------------

#### Traq {#traq-structures-dirthenslash}

`\_\_dir\_\_-then-slash`{.interpreted-text role="ref"}, in
src/Kernel.php:60.

When executed in a path \'/a/b/c\', this code will require
\'/a../../vendor/autoload.php.

``` {.php}
static::$loader = require __DIR__.'../../vendor/autoload.php';
```

### No Need For Else

#### Thelia {#thelia-structures-noneedforelse}

`no-need-for-else`{.interpreted-text role="ref"}, in
core/lib/Thelia/Core/Template/Loop/Address.php:92.

After checking that \$currentCustomer is null, the method returns. The
block with Else may be removed and its code may be moved one level up.

``` {.php}
if ($customer === 'current') {
            $currentCustomer = $this->securityContext->getCustomerUser();
            if ($currentCustomer === null) {
                return null;
            } else {
                $search->filterByCustomerId($currentCustomer->getId(), Criteria::EQUAL);
            }
        } else {
            $search->filterByCustomerId($customer, Criteria::EQUAL);
        }
```

------------------------------------------------------------------------

#### ThinkPHP {#thinkphp-structures-noneedforelse}

`no-need-for-else`{.interpreted-text role="ref"}, in
projects/thinkphp/code//ThinkPHP/Library/Org/Util/Rbac.class.php:187.

This code has both good and bad example. Good : no use of else, after
\$\_SESSION\[\$accessGuid\] check. Issue : else usage after usage of
!isset(\$accessList\[strtoupper(\$appName)\]\[strtoupper(CONTROLLER\_NAME)\]\[strtoupper(ACTION\_NAME)\])

``` {.php}
if (empty($_SESSION[C('ADMIN_AUTH_KEY')])) {
                if (C('USER_AUTH_TYPE') == 2) {
                    //加强验证和即时验证模式 更加安全 后台权限修改可以即时生效
                    //通过数据库进行访问检查
                    $accessList = self::getAccessList($_SESSION[C('USER_AUTH_KEY')]);
                } else {
                    // 如果是管理员或者当前操作已经认证过，无需再次认证
                    if ($_SESSION[$accessGuid]) {
                        return true;
                    }
                    //登录验证模式，比较登录后保存的权限访问列表
                    $accessList = $_SESSION['_ACCESS_LIST'];
                }
                //判断是否为组件化模式，如果是，验证其全模块名
                if (!isset($accessList[strtoupper($appName)][strtoupper(CONTROLLER_NAME)][strtoupper(ACTION_NAME)])) {
                    $_SESSION[$accessGuid] = false;
                    return false;
                } else {
                    $_SESSION[$accessGuid] = true;
                }
```

### Strange Name For Variables

#### FuelCMS {#fuelcms-variables-strangename}

`strange-name-for-variables`{.interpreted-text role="ref"}, in
fuel/modules/fuel/libraries/parser/dwoo/Dwoo/Adapters/CakePHP/dwoo.php:86.

Three \_ is quite a lot for variables. Would they not be parameters but
global variables, that would still be quite a lot.

``` {.php}
public function _render($___viewFn, $___data_for_view, $___play_safe = true, $loadHelpers = true) {
    /**/
}
```

------------------------------------------------------------------------

#### PhpIPAM {#phpipam-variables-strangename}

`strange-name-for-variables`{.interpreted-text role="ref"}, in
app/admin/sections/edit-result.php:56.

\$sss is the end-result of a progression, from \$subsections (3s) to
\$ss to \$sss. Although it is understandable from the code, a fuller
name, like \$subsection\_subnet or \$one\_subsection\_subnet would make
this more readable.

``` {.php}
//fetch subsection subnets
        foreach($subsections as $ss) {
            $subsection_subnets = $Subnets->fetch_section_subnets($ss->id); //fetch all subnets in subsection
            if(sizeof($subsection_subnets)>0) {
                foreach($subsection_subnets as $sss) {
                    $out[] = $sss;
                }
            }
            $num_subnets = $num_subnets + sizeof($subsection_subnets);
            //count all addresses that will be deleted!
            $ipcnt = $Addresses->count_addresses_in_multiple_subnets($out);
        }
```

### Check All Types

#### Zend-Config {#zend-config-structures-checkalltypes}

`check-all-types`{.interpreted-text role="ref"}, in
src/Writer/Ini.php:122.

\$value must be an array or a string here.

``` {.php}
foreach ($config as $key => $value) {
            $group = array_merge($parents, [$key]);

            if (is_array($value)) {
                $iniString .= $this->addBranch($value, $group);
            } else {
                $iniString .= implode($this->nestSeparator, $group)
                           .  ' = '
                           .  $this->prepareValue($value)
                           .  \n;
            }
        }
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-structures-checkalltypes}

`check-all-types`{.interpreted-text role="ref"}, in
library/core/class.form.php:2488.

When \$this-\>\_FormValues is not null, then it is an array or an
object, as it may be used immediately with foreach(). A check with
is\_array() would be a stronger option here.

``` {.php}
public function formDataSet() {
        if (is_null($this->_FormValues)) {
            $this->formValues();
        }

        $result = [[]];
        foreach ($this->_FormValues as $key => $value) {
```

### Missing Cases In Switch

#### Tikiwiki {#tikiwiki-structures-missingcases}

`missing-cases-in-switch`{.interpreted-text role="ref"}, in
lib/articles/artlib.php:1075.

This switch handles 3 cases, plus the default for all others. There are
other switch structures which also handle the \'\' case. There may be a
missing case here. In particular,
projects/tikiwiki/code//article\_image.php host another switch with the
same case, plus another \'topic\' case.

``` {.php}
switch ($image_type) {
            case 'article':
                $image_cache_prefix = 'article';
                break;
            case 'submission':
                $image_cache_prefix = 'article_submission';
                break;
            case 'preview':
                $image_cache_prefix = 'article_preview';
                break;
            default:
                return false;
        }
```

### Repeated Regex

#### Vanilla {#vanilla-structures-repeatedregex}

`repeated-regex`{.interpreted-text role="ref"}, in
library/core/class.pluginmanager.php:1200.

This regex is actually repeated 4 times across the Vanilla database,
including this variation : \'\#\^(https?:)?//\#i\'.

``` {.php}
'`^https?://`'
```

------------------------------------------------------------------------

#### Tikiwiki {#tikiwiki-structures-repeatedregex}

`repeated-regex`{.interpreted-text role="ref"}, in tiki-login.php:369.

This regex is use twice, identically, in the same file, with a few line
of distance. It may be federated at the file level.

``` {.php}
preg_match('/(tiki-register|tiki-login_validate|tiki-login_scr)\.php/', $url)
```

### No Class In Global

#### Dolphin {#dolphin-php-noclassinglobal}

`no-class-in-global`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/inc/classes/BxDolXml.php:10.

This class should be put away in a \'dolphin\' or \'boonex\' namespace.

``` {.php}
class BxDolXml { 
    /* class BxDolXML code */ 
}
```

### Could Use str\_repeat()

#### Zencart {#zencart-structures-couldusestrrepeat}

`could-use-str\_repeat()`{.interpreted-text role="ref"}, in
includes/functions/functions\_general.php:1234.

That\'s a 45 repeat of &nbsp;

``` {.php}
if ( (!zen_browser_detect('MSIE')) && (zen_browser_detect('Mozilla/4')) ) {
      for ($i=0; $i<45; $i++) $pre .= '&nbsp;';
    }
```

### Suspicious Comparison

#### PhpIPAM {#phpipam-structures-suspiciouscomparison}

`suspicious-comparison`{.interpreted-text role="ref"}, in
app/tools/vrf/index.php:110.

if \$subnet\[\'description\'\] is a string, the comparison with 0 turn
it into a boolean. false\'s length is 0, and true length is 1. PHP saves
the day.

``` {.php}
$subnet['description'] = strlen($subnet['description']==0) ? "/" : $subnet['description'];
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-structures-suspiciouscomparison}

`suspicious-comparison`{.interpreted-text role="ref"}, in
ExpressionEngine\_Core2.9.2/system/expressionengine/libraries/simplepie/SimplePie/Misc.php:1925.

If trim(\$attribs\[\'\'\]\[\'mode\'\]) === \'base64\', then it is set to
lowercase (although it is already), and added to the && logical test. If
it is \'BASE64\', this fails.

``` {.php}
if (isset($attribs['']['mode']) && strtolower(trim($attribs['']['mode']) === 'base64'))
```

### Strings With Strange Space

#### OpenEMR {#openemr-type-stringwithstrangespace}

`strings-with-strange-space`{.interpreted-text role="ref"}, in
library/globals.inc.php:3270.

The name of the contry contains both an unsecable space (the first,
after Tonga), and a normal space (between Tonga and Islands).
Translations are stored in a database, which preserves the unbreakable
spaces. This also means that fixing the translation must be applied to
every piece of data at the same time. The xl() function, which handles
the translations, is also a good place to clean the spaces before
searching for the right translation.

``` {.php}
'to' => xl('Tonga (Tonga Islands)'),
```

------------------------------------------------------------------------

#### Thelia {#thelia-type-stringwithstrangespace}

`strings-with-strange-space`{.interpreted-text role="ref"}, in
templates/backOffice/default/I18n/fr\_FR.php:647.

This is another example with a translation sentence. Here, the
unbreakable space is before the question mark : this is a typography
rule, that is common to many language. This would be a false positive,
unless typography is handled by another part of the software.

``` {.php}
'Mot de passe oublié ?'
```

### No Empty Regex

#### Tikiwiki {#tikiwiki-structures-noemptyregex}

`no-empty-regex`{.interpreted-text role="ref"}, in
lib/sheet/excel/writer/worksheet.php:1925.

The initial \'s\' seems to be too much. May be a typo ?

``` {.php}
// Strip URL type
        $url = preg_replace('s[^internal:]', '', $url);
```

### Randomly Sorted Arrays

#### Contao {#contao-arrays-randomlysortedliterals}

`randomly-sorted-arrays`{.interpreted-text role="ref"}, in
system/modules/core/dca/tl\_module.php:259.

The array array(\'maxlength\', \'decodeEntities\', \'tl\_class\') is
configured multiple times in this file. Most of them is in the second
form, but some are in the first form. (Multiple occurrences in this
file).

``` {.php}
array('maxlength' => 255, 'decodeEntities' => true, 'tl_class' => 'w50') // Line 246
array('decodeEntities' => true, 'maxlength' => 255, 'tl_class' => 'w50'); // ligne 378
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-arrays-randomlysortedliterals}

`randomly-sorted-arrays`{.interpreted-text role="ref"}, in
applications/dashboard/models/class.activitymodel.php:308.

\'Photo\' moved from last to second. This array is used with a \'Join\'
key, and is the base for a SQL table JOIN. As such, order is important.
If this is the case, it seems unusual that the order is not the same for
a join using the same tables. If it is not the case, arrays may be
reordered.

``` {.php}
/* L 305 */        Gdn::userModel()->joinUsers(
            $result->resultArray(),
            ['ActivityUserID', 'RegardingUserID'],
            ['Join' => ['Name', 'Email', 'Gender', 'Photo']]
        );

// L 385
        Gdn::userModel()->joinUsers($result, ['ActivityUserID', 'RegardingUserID'], ['Join' => ['Name', 'Photo', 'Email', 'Gender']]);
```

### Only Variable Passed By Reference

#### Dolphin {#dolphin-functions-onlyvariablepassedbyreference}

`only-variable-passed-by-reference`{.interpreted-text role="ref"}, in
administration/charts.json.php:89.

This is not possible, as array\_slice() returns a new array, and not a
reference. Minimally, the intermediate result must be saved in a
variable, then popped. Actually, this code extracts the element at key 1
in the \$aData array, although this also works with hash (non-numeric
keys).

``` {.php}
array_pop(array_slice($aData, 0, 1))
```

------------------------------------------------------------------------

#### PhpIPAM {#phpipam-functions-onlyvariablepassedbyreference}

`only-variable-passed-by-reference`{.interpreted-text role="ref"}, in
functions/classes/class.Thread.php:243.

This is sneaky bug : the assignation \$status = 0 returns a value, and
not a variable. This leads PHP to mistake the initialized 0 with the
variable \$status and fails. It is not possible to initialize variable
AND use them as argument.

``` {.php}
pcntl_waitpid($this->pid, $status = 0)
```

### No Return Used

#### SPIP {#spip-functions-noreturnused}

`no-return-used`{.interpreted-text role="ref"}, in
ecrire/inc/utils.php:1067.

job\_queue\_remove() is called as an administration order, and the
result is not checked. It is considered as a fire-and-forget command.

``` {.php}
function job_queue_remove($id_job) {
    include_spip('inc/queue');

    return queue_remove_job($id_job);
}
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-functions-noreturnused}

`no-return-used`{.interpreted-text role="ref"}, in
livezilla/\_lib/trdp/Zend/Loader.php:114.

The loadFile method tries to load a file, aka as include. If the
inclusion fails, a PHP error is emitted (an exception would do the
same), and there is not error management. Hence, the \'return true;\',
which is not tested later. It may be dropped.

``` {.php}
public static function loadFile($filename, $dirs = null, $once = false)
    {
// A lot of code to check and include files

        return true;
    }
```

### Mixed Concat And Interpolation

#### SuiteCrm {#suitecrm-structures-mixedconcatinterpolation}

`mixed-concat-and-interpolation`{.interpreted-text role="ref"}, in
modules/AOW\_Actions/actions/actionSendEmail.php:89.

How long did it take to spot the hidden \$checked variable in this long
concatenation ? Using a consistent method of interpolation would help
readability here.

``` {.php}
"<input type='checkbox' id='aow_actions_param[" . $line . "][individual_email]' name='aow_actions_param[" . $line . "][individual_email]' value='1' $checked></td>"
```

------------------------------------------------------------------------

#### Edusoho {#edusoho-structures-mixedconcatinterpolation}

`mixed-concat-and-interpolation`{.interpreted-text role="ref"}, in
src/AppBundle/Controller/Admin/SiteSettingController.php:168.

Calling a method from a property of an object is possible inside a
string, though it is rare. Setting the method outside the string make it
more readable.

``` {.php}
"{$this->container->getParameter('topxia.upload.public_url_path')}/" . $parsed['path']
```

### Too Many Injections

#### NextCloud {#nextcloud-classes-toomanyinjections}

`too-many-injections`{.interpreted-text role="ref"}, in
lib/private/Share20/Manager.php:130.

Well documented Manager class. Quite a lot of injections though, it must
take a long time to prepare it.

``` {.php}
/**
     * Manager constructor.
     *
     * @param ILogger $logger
     * @param IConfig $config
     * @param ISecureRandom $secureRandom
     * @param IHasher $hasher
     * @param IMountManager $mountManager
     * @param IGroupManager $groupManager
     * @param IL10N $l
     * @param IFactory $l10nFactory
     * @param IProviderFactory $factory
     * @param IUserManager $userManager
     * @param IRootFolder $rootFolder
     * @param EventDispatcher $eventDispatcher
     * @param IMailer $mailer
     * @param IURLGenerator $urlGenerator
     * @param \OC_Defaults $defaults
     */
    public function __construct(
            ILogger $logger,
            IConfig $config,
            ISecureRandom $secureRandom,
            IHasher $hasher,
            IMountManager $mountManager,
            IGroupManager $groupManager,
            IL10N $l,
            IFactory $l10nFactory,
            IProviderFactory $factory,
            IUserManager $userManager,
            IRootFolder $rootFolder,
            EventDispatcher $eventDispatcher,
            IMailer $mailer,
            IURLGenerator $urlGenerator,
            \OC_Defaults $defaults
    ) {
        $this->logger = $logger;
        $this->config = $config;
        $this->secureRandom = $secureRandom;
        $this->hasher = $hasher;
        $this->mountManager = $mountManager;
        $this->groupManager = $groupManager;
        $this->l = $l;
        $this->l10nFactory = $l10nFactory;
        $this->factory = $factory;
        $this->userManager = $userManager;
        $this->rootFolder = $rootFolder;
        $this->eventDispatcher = $eventDispatcher;
        $this->sharingDisabledForUsersCache = new CappedMemoryCache();
        $this->legacyHooks = new LegacyHooks($this->eventDispatcher);
        $this->mailer = $mailer;
        $this->urlGenerator = $urlGenerator;
        $this->defaults = $defaults;
    }
```

------------------------------------------------------------------------

#### Thelia {#thelia-classes-toomanyinjections}

`too-many-injections`{.interpreted-text role="ref"}, in
core/lib/Thelia/Core/Event/Delivery/DeliveryPostageEvent.php:58.

Classic address class, with every details. May be even shorter than
expected.

``` {.php}
//class DeliveryPostageEvent extends ActionEvent
    public function __construct(
        DeliveryModuleInterface $module,
        Cart $cart,
        Address $address = null,
        Country $country = null,
        State $state = null
    ) {
        $this->module = $module;
        $this->cart = $cart;
        $this->address = $address;
        $this->country = $country;
        $this->state = $state;
    }
```

### @ Operator

#### Phinx {#phinx-structures-noscream}

`@-operator`{.interpreted-text role="ref"}, in
src/Phinx/Util/Util.php:239.

fopen() may be tested for existence, readability before using it.
Although, it actually emits some errors on Windows, with network
volumes.

``` {.php}
$isReadable = @\fopen($filePath, 'r') !== false;

        if (!$filePath || !$isReadable) {
            throw new \Exception(sprintf(Cannot open file %s \n, $filename));
        }
```

------------------------------------------------------------------------

#### PhpIPAM {#phpipam-structures-noscream}

`@-operator`{.interpreted-text role="ref"}, in
functions/classes/class.Log.php:322.

Variable and index existence should always be tested with isset() : it
is faster than using `@`.

``` {.php}
$_SESSION['ipamusername']
```

### Avoid Optional Properties

#### ChurchCRM {#churchcrm-classes-avoidoptionalproperties}

`avoid-optional-properties`{.interpreted-text role="ref"}, in
src/ChurchCRM/BackupManager.php:401.

Backuptype is initialized with null, and yet, it isn\'t checked for any
invalid valid values, in particular in switch() structures.

``` {.php}
// BackupType is initialized with null
  class JobBase
  {
      /**
        *
        * @var BackupType
        */
      protected $BackupType;

// In the child class BackupJob, BackupType may be of any type      
  class BackupJob extends JobBase
  {
      /**
       *
       * @param String $BaseName
       * @param BackupType $BackupType
       * @param Boolean $IncludeExtraneousFiles
       */
      public function __construct($BaseName, $BackupType, $IncludeExtraneousFiles, $EncryptBackup, $BackupPassword)
      {
          $this->BackupType = $BackupType;


// Later, Backtype is not checked with all values : 
          try {
              $this->DecryptBackup();
              switch ($this->BackupType) {
              case BackupType::SQL:
                $this->RestoreSQLBackup($this->RestoreFile);
                break;
              case BackupType::GZSQL:
                $this->RestoreGZSQL();
                break;
              case BackupType::FullBackup:
                $this->RestoreFullBackup();
                break;
// Note  : no default case here
            }
```

------------------------------------------------------------------------

#### Dolibarr {#dolibarr-classes-avoidoptionalproperties}

`avoid-optional-properties`{.interpreted-text role="ref"}, in
htdocs/product/stock/class/productlot.class.php:149.

\$this-\>fk\_product is tested for value 11 times while being used in
this class. All detected situations were checking the presence of the
property before usage.

``` {.php}
class Productlot extends CommonObject
{
// more code
    /**
     * @var int ID
     */
    public $fk_product;

// Checked usage of fk_product
// line 341
        $sql .= ' fk_product = '.(isset($this->fk_product) ? $this->fk_product : "null").',';
```

### Mismatched Ternary Alternatives

#### phpadsnew {#phpadsnew-structures-mismatchedternary}

`mismatched-ternary-alternatives`{.interpreted-text role="ref"}, in
phpAdsNew-2.0/admin/lib-misc-stats.inc.php:219.

This is an unusual way to apply a condition. \$bgcolor is \'\#FFFFFF\'
by default, and if \$i % 2, then \$bcolor is \'\#F6F6F6\';. A more
readable ternary option would be \'\$bgcolor = = \$i % 2 ? \"\#FFFFFF\"
: \"\#F6F6F6\";\', and make a matched alternative branches.

``` {.php}
$bgcolor = #FFFFFF;
    $i % 2 ? 0 : $bgcolor = #F6F6F6;
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-structures-mismatchedternary}

`mismatched-ternary-alternatives`{.interpreted-text role="ref"}, in
portal/messaging/messages.php:132.

IS\_DASHBOARD is defined as a boolean or a string. Later, it is tested
as a boolean, and displayed as a integer, which will be cast to string
by echo. Lots of transtyping are happening here.

``` {.php}
// In two distinct if/then branch
l:29) define('IS_DASHBOARD', false);
l:41) define('IS_DASHBOARD', $_SESSION['authUser']);

l:132) echo IS_DASHBOARD ? IS_DASHBOARD : 0;
?>
```

### Mismatched Default Arguments

#### SPIP {#spip-functions-mismatcheddefaultarguments}

`mismatched-default-arguments`{.interpreted-text role="ref"}, in
ecrire/inc/lien.php:160.

generer\_url\_entite() takes \$connect in, with a default value of empty
string. Later, generer\_url\_entite() receives that value, but uses null
as a default value. This forces the ternary test on \$connect, to turn
it into a null before shipping it to the next function, and having it
processed accordingly.

``` {.php}
// http://code.spip.net/@traiter_lien_implicite
function traiter_lien_implicite($ref, $texte = '', $pour = 'url', $connect = '') {

    // some code was edited here

    if (is_array($url)) {
        @list($type, $id) = $url;
        $url = generer_url_entite($id, $type, $args, $ancre, $connect ? $connect : null);
    }
```

### Mismatched Typehint

#### WordPress {#wordpress-functions-mismatchedtypehint}

`mismatched-typehint`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### Scalar Or Object Property

#### SugarCrm {#sugarcrm-classes-scalarorobjectproperty}

`scalar-or-object-property`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/data/Link.php:54.

The \_relationship property starts its life as a string, and becomes an
object later.

``` {.php}
class Link {

    /* Private variables.*/
    var $_log;
    var $_relationship_name; //relationship this attribute is tied to.
    var $_bean; //stores a copy of the bean.
    var $_relationship= '';

/// More code..... 

// line 92
        $this->_relationship=new Relationship();
```

### Assign With And Precedence

#### xataface {#xataface-php-assignand}

`assign-with-and-precedence`{.interpreted-text role="ref"}, in
Dataface/LanguageTool.php:265.

The usage of \'and\' here is a workaround for PHP version that have no
support for the coalesce. \$autosubmit receives the value of
\$params\[\'autosubmit\'\] only if the latter is set. Yet, with = having
higher precedence over \'and\', \$autosubmit is mistaken with the
existence of \$params\[\'autosubmit\'\] : its value is actually omitted.

``` {.php}
$autosubmit = isset($params['autosubmit']) and $params['autosubmit'];
```

### Logical To in\_array

#### Zencart {#zencart-performances-logicaltoinarray}

`logical-to-in\_array`{.interpreted-text role="ref"}, in
admin/users.php:32.

Long list of == are harder to read. Using an in\_array() call gathers
all the strings together, in an array. In turn, this helps readability
and possibility, reusability by making that list an constant.

``` {.php}
// if needed, check that a valid user id has been passed
if (($action == 'update' || $action == 'reset') && isset($_POST['user']))
{
  $user = $_POST['user'];
}
elseif (($action == 'edit' || $action == 'password' || $action == 'delete' || $action == 'delete_confirm') && $_GET['user'])
{
  $user = $_GET['user'];
}
elseif(($action=='delete' || $action=='delete_confirm') && isset($_POST['user']))
{
  $user = $_POST['user'];
}
```

### Pathinfo() Returns May Vary

#### NextCloud {#nextcloud-php-pathinforeturns}

`pathinfo()-returns-may-vary`{.interpreted-text role="ref"}, in
lib/private/Preview/Office.php:56.

\$absPath is build with the toTmpFile() method, which may return a
boolean (false) in case of error. Error situations include the inability
to create the temporary file.

``` {.php}
$absPath = $fileview->toTmpFile($path);

// More code

            list($dirname, , , $filename) = array_values(pathinfo($absPath));
            $pngPreview = $dirname . '/' . $filename . '.png';
```

### Multiple Type Variable

#### Typo3 {#typo3-structures-multipletypevariable}

`multiple-type-variable`{.interpreted-text role="ref"}, in
typo3/sysext/backend/Classes/Form/Element/InputDateTimeElement.php:270.

\$fullElement is an array most of the time, but finally ends up being a
string. Since the array is not the final state, it may be interesting to
make it a class, which collects the various variables, and export the
final string. Such class would be usefull in several places in this
repository.

``` {.php}
$fullElement = [];
            $fullElement[] = '<div class=checkbox t3js-form-field-eval-null-placeholder-checkbox>';
            $fullElement[] =     '<label for= . $nullControlNameEscaped . >';
            $fullElement[] =         '<input type=hidden name= . $nullControlNameEscaped .  value= . $fallbackValue .  />';
            $fullElement[] =         '<input type=checkbox name= . $nullControlNameEscaped .  id= . $nullControlNameEscaped .  value=1' . $checked . $disabled . ' />';
            $fullElement[] =         $overrideLabel;
            $fullElement[] =     '</label>';
            $fullElement[] = '</div>';
            $fullElement[] = '<div class=t3js-formengine-placeholder-placeholder>';
            $fullElement[] =    '<div class=form-control-wrap style=max-width: . $width . px>';
            $fullElement[] =        '<input type=text class=form-control disabled=disabled value= . $shortenedPlaceholder .  />';
            $fullElement[] =    '</div>';
            $fullElement[] = '</div>';
            $fullElement[] = '<div class=t3js-formengine-placeholder-formfield>';
            $fullElement[] =    $expansionHtml;
            $fullElement[] = '</div>';
            $fullElement = implode(LF, $fullElement);
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-structures-multipletypevariable}

`multiple-type-variable`{.interpreted-text role="ref"}, in
library/core/functions.general.php:1427.

Here, \$value may be of different type. The if() structures merges all
the incoming format into one standard type (int). This is actually the
contrary of this analysis, and is a false positive.

``` {.php}
if (is_array($value)) {
                        $value = count($value);
                    } elseif (stringEndsWith($field, 'UserID', true)) {
                        $value = 1;
                    }
```

### Is Actually Zero

#### Dolibarr {#dolibarr-structures-iszero}

`is-actually-zero`{.interpreted-text role="ref"}, in
htdocs/compta/ajaxpayment.php:99.

Here, the \$amountToBreakDown is either \$currentRemain or \$result.

``` {.php}
$amountToBreakdown = ($result - $currentRemain >= 0 ?
                                        $currentRemain :                                // Remain can be fully paid
                                        $currentRemain + ($result - $currentRemain));   // Remain can only partially be paid
```

------------------------------------------------------------------------

#### SuiteCrm {#suitecrm-structures-iszero}

`is-actually-zero`{.interpreted-text role="ref"}, in
modules/AOR\_Charts/lib/pChart/class/pDraw.class.php:523.

\$Xa may only amount to \$iX2, though the expression looks weird.

``` {.php}
if ( $X > $iX2 ) { $Xa = $X-($X-$iX2); $Ya = $iY1+($X-$iX2); } else { $Xa = $X; $Ya = $iY1; }
```

### Unconditional Break In Loop

#### LiveZilla {#livezilla-structures-unconditionloopbreak}

`unconditional-break-in-loop`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

Only one row is read from the DBManager, and the rest is ignored. The
result has no more than one result, basedd on the [LIMIT 1]{.title-ref}
clause in the SQL. The while loop may be removed.

``` {.php}
$result = DBManager::Execute(true, "SELECT * FROM `" . DB_PREFIX . DATABASE_STATS_AGGS . "` WHERE `month`>0 AND ((`year`='" . DBManager::RealEscape(date("Y")) . "' AND `month`<'" . DBManager::RealEscape(date("n")) . "') OR (`year`<'" . DBManager::RealEscape(date("Y")) . "')) AND (`aggregated`=0 OR `aggregated`>" . (time() - 300) . ") AND `day`=0 ORDER BY `year` ASC,`month` ASC LIMIT 1;");
        if ($result)
            while ($row = DBManager::FetchArray($result)) {
                if (empty($row["aggregated"])) {
                    DBManager::Execute(true, "UPDATE `" . DB_PREFIX . DATABASE_STATS_AGGS . "` SET `aggregated`=" . time() . " WHERE `year`=" . $row["year"] . " AND `month`=" . $row["month"] . " AND `day`=0 LIMIT 1;");
                    $this->AggregateMonth($row["year"], $row["month"]);
                }
                return false;
            }
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-structures-unconditionloopbreak}

`unconditional-break-in-loop`{.interpreted-text role="ref"}, in
includes/htmlform/HTMLFormField.php:138.

The final break is useless : the execution has already reached the end
of the loop.

``` {.php}
for ( $i = count( $thisKeys ) - 1; $i >= 0; $i-- ) {
            $keys = array_merge( array_slice( $thisKeys, 0, $i ), $nameKeys );
            $data = $alldata;
            foreach ( $keys as $key ) {
                if ( !is_array( $data ) || !array_key_exists( $key, $data ) ) {
                    continue 2;
                }
                $data = $data[$key];
            }
            $testValue = (string)$data;
            break;
        }
```

### Could Be Else

#### SugarCrm {#sugarcrm-structures-couldbeelse}

`could-be-else`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/modules/Emails/ListViewGroup.php:79.

The first condition makes different checks if \'query\' is in
\$\_REQUEST or not. The second only applies to \$\_REQUEST\[\'query\'\],
as there is no else. There is also no visible sign that the first
condition may change \$\_REQUEST or not

``` {.php}
if(!isset($_REQUEST['query'])){
    //_pp('loading: '.$currentModule.'Group');
    //_pp($current_user->user_preferences[$currentModule.'GroupQ']);
    $storeQuery->loadQuery($currentModule.'Group');
    $storeQuery->populateRequest();
} else {
    //_pp($current_user->user_preferences[$currentModule.'GroupQ']);
    //_pp('saving: '.$currentModule.'Group');
    $storeQuery->saveFromGet($currentModule.'Group');
}

if(isset($_REQUEST['query'])) {
    // we have a query
    if(isset($_REQUEST['email_type']))              $email_type = $_REQUEST['email_type'];
    if(isset($_REQUEST['assigned_to']))             $assigned_to = $_REQUEST['assigned_to'];
    if(isset($_REQUEST['status']))                  $status = $_REQUEST['status'];
    // More code
}
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-structures-couldbeelse}

`could-be-else`{.interpreted-text role="ref"}, in library/log.inc:653.

Those two if structure may definitely merged into one single
instruction.

``` {.php}
$success = 1;
    $checksum = ;
    if ($outcome === false) {
        $success = 0;
    }

    if ($outcome !== false) {
        // Should use the $statement rather than the processed
        // variables, which includes the binded stuff. If do
        // indeed need the binded values, then will need
        // to include this as a separate array.

        //error_log(STATEMENT: .$statement,0);
        //error_log(BINDS: .$processed_binds,0);
        $checksum = sql_checksum_of_modified_row($statement);
        //error_log(CHECKSUM: .$checksum,0);
    }
```

### Next Month Trap

#### Contao {#contao-structures-nextmonthtrap}

`next-month-trap`{.interpreted-text role="ref"}, in
system/modules/calendar/classes/Events.php:515.

This code is wrong on August 29,th 30th and 31rst : 6 months before is
caculated here as February 31rst, so march 2. Of course, this depends on
the leap years.

``` {.php}
case 'past_180':
                return array(strtotime('-6 months'), time(), $GLOBALS['TL_LANG']['MSC']['cal_empty']);
```

------------------------------------------------------------------------

#### Edusoho {#edusoho-structures-nextmonthtrap}

`next-month-trap`{.interpreted-text role="ref"}, in
src/AppBundle/Controller/Admin/AnalysisController.php:1426.

The last month is wrong 8 times a year : on 31rst, and by the end of
March.

``` {.php}
'lastMonthStart' => date('Y-m-d', strtotime(date('Y-m', strtotime('-1 month')))),
            'lastMonthEnd' => date('Y-m-d', strtotime(date('Y-m', time())) - 24 * 3600),
            'lastThreeMonthsStart' => date('Y-m-d', strtotime(date('Y-m', strtotime('-2 month')))),
```

### Printf Number Of Arguments

#### PhpIPAM {#phpipam-structures-printfarguments}

`printf-number-of-arguments`{.interpreted-text role="ref"}, in
functions/classes/class.Common.php:1174.

16 will not be displayed.

``` {.php}
sprintf('%032s', gmp_strval(gmp_init($ipv6long, 10), 16);
```

### Don\'t Send \$this In Constructor

#### Woocommerce {#woocommerce-classes-dontsendthisinconstructor}

`don't-send-$this-in-constructor`{.interpreted-text role="ref"}, in
includes/class-wc-cart.php:107.

WC\_Cart\_Session and WC\_Cart\_Fees receives \$this, the current
object, at a moment where it is not consistent : for example,
tax\_display\_cart hasn\'t been set yet. Although it may be unexpected
to have an object called WC\_Cart being called by the session or the
fees, this is still a temporary inconsistence.

``` {.php}
/**
     * Constructor for the cart class. Loads options and hooks in the init method.
     */
    public function __construct() {
        $this->session          = new WC_Cart_Session( $this );
        $this->fees_api         = new WC_Cart_Fees( $this );
        $this->tax_display_cart = $this->is_tax_displayed();

        // Register hooks for the objects.
        $this->session->init();
```

------------------------------------------------------------------------

#### Contao {#contao-classes-dontsendthisinconstructor}

`don't-send-$this-in-constructor`{.interpreted-text role="ref"}, in
system/modules/core/library/Contao/Model.php:110.

\$this is send to \$objRegistry. \$objRegistry is obtained with a
factory, ModelRegistry::getInstance(). It is probably fully prepared at
that point. Yet, \$objRegistry is called and used to fill \$this
properties with full values. At some point, \$objRegistry return values
without having a handle on a fully designed object.

``` {.php}
/**
     * Load the relations and optionally process a result set
     *
     * @param \Database\Result $objResult An optional database result
     */
    public function __construct(\Database\Result $objResult=null)
    {
        // Some code was removed 
            $objRegistry = \Model\Registry::getInstance();

            $this->setRow($arrData); // see #5439
            $objRegistry->register($this);

        // More code below
        // $this-> are set
        // $objRegistry is called 
    }
```

### Parent First

#### shopware {#shopware-classes-parentfirst}

`parent-first`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

Here, the parent is called last. Givent that \$title is defined in the
same class, it seems that \$name may be defined in the BaseContainer
class. In fact, it is not, and BasecContainer and FieldSet are fairly
independant classes. Thus, the parent::\_\_construct call could be first
here, though more as a coding convention.

``` {.php}
/**
 * Class FieldSet
 */
class FieldSet extends BaseContainer
{
    /**
     * @var string
     */
    protected $title;

    /**
     * @param string $name
     * @param string $title
     */
    public function __construct($name, $title)
    {
        $this->title = $title;
        $this->name = $name;
        parent::__construct();
    }
```

------------------------------------------------------------------------

#### PrestaShop {#prestashop-classes-parentfirst}

`parent-first`{.interpreted-text role="ref"}, in
controllers/admin/AdminPatternsController.php:30.

A good number of properties are set in the current object even before
the parent AdminController(Core) is called. \'table\' and \'lang\' acts
as default values for the parent class, as it (the parent class) would
set them to another default value. Many properties are used, but not
defined in the current class, nor its parent. This approach prevents the
constructor from requesting too many arguments. Yet, as such, it is
difficult to follow which of the initial values are transmitted via
protected/public properties rather than using the \_\_construct() call.

``` {.php}
class AdminPatternsControllerCore extends AdminController
{
    public $name = 'patterns';

    public function __construct()
    {
        $this->bootstrap = true;
        $this->show_toolbar = false;
        $this->context = Context::getContext();

        parent::__construct();
    }
```

### Invalid Regex

#### SugarCrm {#sugarcrm-structures-invalidregex}

`invalid-regex`{.interpreted-text role="ref"}, in
SugarCE-Full-6.5.26/include/utils/file\_utils.php:513.

This yields an error at execution time :
`Compilation failed: invalid range in character class at offset 4`.

``` {.php}
preg_replace('/[^\w-._]+/i', '', $name)
```

### Use Named Boolean In Argument Definition

#### phpMyAdmin {#phpmyadmin-functions-avoidbooleanargument}

`use-named-boolean-in-argument-definition`{.interpreted-text
role="ref"}, in /libraries/classes/Util.php:1929.

\$request is an option to [checkParameters]{.title-ref}, although it is
not visibile with is its actual role.

``` {.php}
public static function checkParameters($params, $request = false) { 
    /**/ 
}
```

------------------------------------------------------------------------

#### Cleverstyle {#cleverstyle-functions-avoidbooleanargument}

`use-named-boolean-in-argument-definition`{.interpreted-text
role="ref"}, in /core/classes/Response.php:129.

\$httponly is an option to [cookie]{.title-ref}, and true/false makes it
readable. There may be other situations, like fallback, or forcedd
usage, so the boolean may be misleading. Note also the [\$expire =
0]{.title-ref}, which may be a date, or a special value. We need to read
the documentation to understand this.

``` {.php}
public function cookie($name, $value, $expire = 0, $httponly = false) { /**/ }   { 
    /**/ 
}
```

### Never Used Parameter

#### Piwigo {#piwigo-functions-neverusedparameter}

`never-used-parameter`{.interpreted-text role="ref"}, in
include/functions\_html.inc.php:329.

\$alternate\_url is never explicitely passed to bad\_request() : this
doesn\'t show in this extract. It could be dropped from this code.

``` {.php}
function bad_request($msg, $alternate_url=null)
{
  set_status_header(400);
  if ($alternate_url==null)
    $alternate_url = make_index_url();
  redirect_html( $alternate_url,
    '<div style="text-align:left; margin-left:5em;margin-bottom:5em;">
<h1 style="text-align:left; font-size:36px;">'.l10n('Bad request').'</h1><br>'
.$msg.'</div>',
    5 );
}
```

### Identical On Both Sides

#### phpMyAdmin {#phpmyadmin-structures-identicalonbothsides}

`identical-on-both-sides`{.interpreted-text role="ref"}, in
libraries/classes/DatabaseInterface.php:323.

This code looks like
`($options & DatabaseInterface::QUERY_STORE) == DatabaseInterface::QUERY_STORE`,
which would make sense. But PHP precedence is actually executing
`$options & (DatabaseInterface::QUERY_STORE == DatabaseInterface::QUERY_STORE)`,
which then doesn\'t depends on QUERY\_STORE but only on \$options.

``` {.php}
if ($options & DatabaseInterface::QUERY_STORE == DatabaseInterface::QUERY_STORE) {
    $tmp = $this->_extension->realQuery('
        SHOW COUNT(*) WARNINGS', $this->_links[$link], DatabaseInterface::QUERY_STORE
    );
    $warnings = $this->fetchRow($tmp);
} else {
    $warnings = 0;
}
```

------------------------------------------------------------------------

#### HuMo-Gen {#humo-gen-structures-identicalonbothsides}

`identical-on-both-sides`{.interpreted-text role="ref"}, in
include/person\_cls.php:73.

In that long logical expression, \$personDb-\>pers\_cal\_date is tested
twice

``` {.php}
// *** Filter person's WITHOUT any date's ***
            if ($user[group_filter_date]=='j'){
                if ($personDb->pers_birth_date=='' AND $personDb->pers_bapt_date==''
                AND $personDb->pers_death_date=='' AND $personDb->pers_buried_date==''
                AND $personDb->pers_cal_date=='' AND $personDb->pers_cal_date==''
                ){
                    $privacy_person='';
                }
            }
```

### No Reference For Ternary

#### phpadsnew {#phpadsnew-php-noreferenceforternary}

`no-reference-for-ternary`{.interpreted-text role="ref"}, in
lib/OA/Admin/Menu/Section.php334:334.

The reference should be removed from the function definition. Either
this method returns null, which is never a reference, or it returns
\$this, which is always a reference, or the results of a methodcall. The
latter may or may not be a reference, but the Ternary operator will drop
it and return by value.

``` {.php}
function &getParentOrSelf($type)
    {
        if ($this->type == $type) {
            return $this;
        }
        else {
            return $this->parentSection != null ? $this->parentSection->getParentOrSelf($type) : null;
        }
    }
```

### Unused Inherited Variable In Closure

#### shopware {#shopware-functions-unusedinheritedvariable}

`unused-inherited-variable-in-closure`{.interpreted-text role="ref"}, in
recovery/update/src/app.php:129.

In the first closuree, \$containere is used as the root for the method
calls, but \$app is not used. It may be dropped. In fact, some of the
following calls to \$app-\>map() only request one inherited,
\$container.

``` {.php}
$app->map('/applyMigrations', function () use ($app, $container) {
    $container->get('controller.batch')->applyMigrations();
})->via('GET', 'POST')->name('applyMigrations');

$app->map('/importSnippets', function () use ($container) {
    $container->get('controller.batch')->importSnippets();
})->via('GET', 'POST')->name('importSnippets');
```

------------------------------------------------------------------------

#### Mautic {#mautic-functions-unusedinheritedvariable}

`unused-inherited-variable-in-closure`{.interpreted-text role="ref"}, in
MauticCrmBundle/Tests/Integration/SalesforceIntegrationTest.php:1202.

\$max is relayed to getLeadsToCreate(), while \$restart is omitted. It
may be dropped, along with its reference.

``` {.php}
function () use (&$restart, $max) {
                    $args = func_get_args();

                    if (false === $args[2]) {
                        return $max;
                    }

                    $createLeads = $this->getLeadsToCreate($args[2], $max);

                    // determine whether to return a count or records
                    if (false === $args[2]) {
                        return count($createLeads);
                    }

                    return $createLeads;
                }
```

### Useless Referenced Argument

#### Woocommerce {#woocommerce-functions-uselessreferenceargument}

`useless-referenced-argument`{.interpreted-text role="ref"}, in
includes/data-stores/class-wc-product-variation-data-store-cpt.php:414.

\$product is defined with a reference in the method signature, but it is
also used as an object with a dynamical property. As such, the reference
in the argument definition is too much.

``` {.php}
public function update_post_meta( &$product, $force = false ) {
        $meta_key_to_props = array(
            '_variation_description' => 'description',
        );

        $props_to_update = $force ? $meta_key_to_props : $this->get_props_to_update( $product, $meta_key_to_props );

        foreach ( $props_to_update as $meta_key => $prop ) {
                    $value   = $product->{get_$prop}( 'edit' );
                    $updated = update_post_meta( $product->get_id(), $meta_key, $value );
            if ( $updated ) {
                $this->updated_props[] = $prop;
            }
        }

        parent::update_post_meta( $product, $force );
```

------------------------------------------------------------------------

#### Magento {#magento-functions-uselessreferenceargument}

`useless-referenced-argument`{.interpreted-text role="ref"}, in
setup/src/Magento/Setup/Module/Di/Compiler/Config/Chain/PreferencesResolving.php:63.

\$value is defined with a reference. In the following code, it is only
read and never written : for index search, or by itself. In fact,
\$preferences is also only read, and never written. As such, both could
be removed.

``` {.php}
private function resolvePreferenceRecursive(&$value, &$preferences)
    {
        return isset($preferences[$value])
            ? $this->resolvePreferenceRecursive($preferences[$value], $preferences)
            : $value;
    }
```

### Useless Catch

#### Zurmo {#zurmo-exceptions-uselesscatch}

`useless-catch`{.interpreted-text role="ref"}, in
app/protected/modules/workflows/forms/attributes/ExplicitReadWriteModelPermissionsWorkflowActionAttributeForm.php:99.

Catch the exception, then return. At least, the comment is honest.

``` {.php}
try
                {
                    $group = Group::getById((int)$this->type);
                    $explicitReadWriteModelPermissions->addReadWritePermitable($group);
                }
                catch (NotFoundException $e)
                {
                    //todo: handle exception better
                    return;
                }
```

------------------------------------------------------------------------

#### PrestaShop {#prestashop-exceptions-uselesscatch}

`useless-catch`{.interpreted-text role="ref"}, in
src/Core/Addon/Module/ModuleManagerBuilder.php:170.

Here, the catch clause will intercept a IO problem while writing element
on the disk, and will return false. Since this is a constructor, the
returned value will be ignored and the object will be left in a wrong
state, since it was not totally inited.

``` {.php}
private function __construct()
    {
    // More code......
            try {
                $filesystem = new Filesystem();
                $filesystem->dumpFile($phpConfigFile, '<?php return ' . var_export($config, true) . ';' . \n);
            } catch (IOException $e) {
                return false;
            }
        }
```

### Test Then Cast

#### Dolphin {#dolphin-structures-testthencast}

`test-then-cast`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

\$aLimits\[\'per\_page\'\] is tested for existence and not false. Later,
it is cast from string to int : yet, a \'0.1\' string value would pass
the test, and end up filling \$aLimits\[\'per\_page\'\] with 0.

``` {.php}
if (isset($aLimits['per_page']) && $aLimits['per_page'] !== false)
            $this->aCurrent['paginate']['perPage'] = (int)$aLimits['per_page'];
```

------------------------------------------------------------------------

#### SuiteCrm {#suitecrm-structures-testthencast}

`test-then-cast`{.interpreted-text role="ref"}, in
modules/jjwg\_Maps/controller.php:1035.

\$marker\[\'lat\'\] is compared to the string \'0\', which actually
transtype it to integer, then it is cast to string for
map\_marker\_data\_points() needs and finally, it is cast to float, in
case of a correction. It would be safer to test it in its string type,
since floats are not used as array indices.

``` {.php}
if ($marker['lat'] != '0' && $marker['lng'] != '0') {

            // Check to see if marker point already exists and apply offset if needed
            // This often occurs when an address is only defined by city, state, zip.
            $i = 0;
            while (isset($this->map_marker_data_points[(string) $marker['lat']][(string) $marker['lng']]) &&
            $i < $this->settings['map_markers_limit']) {
                $marker['lat'] = (float) $marker['lat'] + (float) $this->settings['map_duplicate_marker_adjustment'];
                $marker['lng'] = (float) $marker['lng'] + (float) $this->settings['map_duplicate_marker_adjustment'];
                $i++;
            }
```

### Property Could Be Local

#### Mautic {#mautic-classes-propertycouldbelocal}

`property-could-be-local`{.interpreted-text role="ref"}, in
app/bundles/EmailBundle/Model/SendEmailToContact.php:47.

\$translator is a private property, provided at construction time. It is
private, and only used in the processBadEmails() method. \$translator
may be turned into a parameter for processBadEmails(), and make the
class slimmer.

``` {.php}
class SendEmailToContact
{
    /**
     * @var TranslatorInterface
     */
    private $translator;

// Skipped code 

    /**
     * SendEmailToContact constructor.
     *
     * @param MailHelper          $mailer
     * @param StatRepository      $statRepository
     * @param DoNotContact        $dncModel
     * @param TranslatorInterface $translator
     */
    public function __construct(MailHelper $mailer, StatHelper $statHelper, DoNotContact $dncModel, TranslatorInterface $translator)
    {
        $this->mailer     = $mailer;
        $this->statHelper = $statHelper;
        $this->dncModel   = $dncModel;
        $this->translator = $translator;
    }

// Skipped code 

    /**
     * Add DNC entries for bad emails to get them out of the queue permanently.
     */
    protected function processBadEmails()
    {
        // Update bad emails as bounces
        if (count($this->badEmails)) {
            foreach ($this->badEmails as $contactId => $contactEmail) {
                $this->dncModel->addDncForContact(
                    $contactId,
                    ['email' => $this->emailEntityId],
                    DNC::BOUNCED,
                    $this->translator->trans('mautic.email.bounce.reason.bad_email'),
                    true,
                    false
                );
            }
        }
    }
```

------------------------------------------------------------------------

#### Typo3 {#typo3-classes-propertycouldbelocal}

`property-could-be-local`{.interpreted-text role="ref"}, in
typo3/sysext/install/Classes/Updates/MigrateUrlTypesInPagesUpdate.php:28.

\$urltypes is a private property, with a list of protocols for
communicationss. It acts as a constant, being only read in the
executeUpdate() method : constants may hold arrays. If this property has
to evolve in the future, an accessor to update it will be necessary.
Until then, this list may be hardcoded in the method.

``` {.php}
/**
 * Merge URLs divided in pages.urltype and pages.url into pages.url
 * @internal This class is only meant to be used within EXT:install and is not part of the TYPO3 Core API.
 */
class MigrateUrlTypesInPagesUpdate implements UpgradeWizardInterface
{
    private $urltypes = ['', 'http://', 'ftp://', 'mailto:', 'https://'];

// Skipped code

    /**
     * Moves data from pages.urltype to pages.url
     *
     * @return bool
     */
    public function executeUpdate(): bool
    {
        foreach ($this->databaseTables as $databaseTable) {
            $connection = GeneralUtility::makeInstance(ConnectionPool::class)
                ->getConnectionForTable($databaseTable);

            // Process records that have entries in pages.urltype
            $queryBuilder = $connection->createQueryBuilder();
            $queryBuilder->getRestrictions()->removeAll();
            $statement = $queryBuilder->select('uid', 'urltype', 'url')
                ->from($databaseTable)
                ->where(
                    $queryBuilder->expr()->neq('urltype', 0),
                    $queryBuilder->expr()->neq('url', $queryBuilder->createPositionalParameter(''))
                )
                ->execute();

            while ($row = $statement->fetch()) {
                $url = $this->urltypes[(int)$row['urltype']] . $row['url'];
                $updateQueryBuilder = $connection->createQueryBuilder();
                $updateQueryBuilder
                    ->update($databaseTable)
                    ->where(
                        $updateQueryBuilder->expr()->eq(
                            'uid',
                            $updateQueryBuilder->createNamedParameter($row['uid'], \PDO::PARAM_INT)
                        )
                    )
                    ->set('url', $updateQueryBuilder->createNamedParameter($url), false)
                    ->set('urltype', 0);
                $updateQueryBuilder->execute();
            }
        }
        return true;
    }
```

### Too Many Native Calls

#### SPIP {#spip-php-toomanynativecalls}

`too-many-native-calls`{.interpreted-text role="ref"}, in
/ecrire/xml/analyser\_dtd.php:58.

This expression counts 4 usages of count(), which is more than the
default level of 3 PHP calls in one expression.

``` {.php}
spip_log("Analyser DTD $avail $grammaire (" . spip_timer('dtd') . ") " . count($dtc->macros) . ' macros, ' . count($dtc->elements) . ' elements, ' . count($dtc->attributs) . " listes d'attributs, " . count($dtc->entites) . " entites")
```

### Redefined Private Property

#### Zurmo {#zurmo-classes-redefinedprivateproperty}

`redefined-private-property`{.interpreted-text role="ref"}, in
app/protected/modules/zurmo/models/OwnedCustomField.php:51.

The class OwnedCustomField is part of a large class tree :
OwnedCustomField extends CustomField, CustomField extends
BaseCustomField, BaseCustomField extends RedBeanModel, RedBeanModel
extends BeanModel.

Since \$canHaveBean is distinct in BeanModel and in OwnedCustomField,
the public method getCanHaveBean() also had to be overloaded.

``` {.php}
class OwnedCustomField extends CustomField
    {
        /**
         * OwnedCustomField does not need to have a bean because it stores no attributes and has no relations
         * @see RedBeanModel::canHaveBean();
         * @var boolean
         */
        private static $canHaveBean = false;

/..../

        /**
         * @see RedBeanModel::getHasBean()
         */
        public static function getCanHaveBean()
        {
            if (get_called_class() == 'OwnedCustomField')
            {
                return self::$canHaveBean;
            }
            return parent::getCanHaveBean();
        }
```

### Don\'t Unset Properties

#### Vanilla {#vanilla-classes-dontunsetproperties}

`don't-unset-properties`{.interpreted-text role="ref"}, in
applications/dashboard/models/class.activitymodel.php:1073.

The \_NotificationQueue property, in this class, is defined as an array.
Here, it is destroyed, then recreated. The unset() is too much, as the
assignation is sufficient to reset the array

``` {.php}
/**
     * Clear notification queue.
     *
     * @since 2.0.17
     * @access public
     */
    public function clearNotificationQueue() {
        unset($this->_NotificationQueue);
        $this->_NotificationQueue = [];
    }
```

------------------------------------------------------------------------

#### Typo3 {#typo3-classes-dontunsetproperties}

`don't-unset-properties`{.interpreted-text role="ref"}, in
typo3/sysext/linkvalidator/Classes/Linktype/InternalLinktype.php:73.

The property errorParams is emptied by unsetting it. The property is
actually defined in the above class, as an array. Until the next error
is added to this list, any access to the error list has to be checked
with isset(), or yield an \'Undefined\' warning.

``` {.php}
public function checkLink($url, $softRefEntry, $reference)
    {
        $anchor = '';
        $this->responseContent = true;
        // Might already contain values - empty it
        unset($this->errorParams);
//....

abstract class AbstractLinktype implements LinktypeInterface
{
    /**
     * Contains parameters needed for the rendering of the error message
     *
     * @var array
     */
    protected $errorParams = [];
```

### Strtr Arguments

#### SuiteCrm {#suitecrm-php-strtrarguments}

`strtr-arguments`{.interpreted-text role="ref"}, in
includes/vCard.php:221.

This code prepares incoming \'\$values\' for extraction. The keys are
cleaned then split with explode(). The \'=\' sign would stay, as strtr()
can\'t remove it. This means that such keys won\'t be recognized later
in the code, and gets omitted.

``` {.php}
$values = explode(';', $value);
                    $key = strtoupper($keyvalue[0]);
                    $key = strtr($key, '=', '');
                    $key = strtr($key, ',', ';');
                    $keys = explode(';', $key);
```

### Callback Function Needs Return

#### Contao {#contao-functions-callbackneedsreturn}

`callback-function-needs-return`{.interpreted-text role="ref"}, in
core-bundle/src/Resources/contao/modules/ModuleQuicklink.php:91.

The empty closure returns [null]{.title-ref}. The array\_flip() array
has now all its values set to null, and reset, as intended. A better
alternative is to use the array\_fill\_keys() function, which set a
default value to every element of an array, once provided with the
expected keys.

``` {.php}
$arrPages = array_map(function () {}, array_flip($tmp));
```

------------------------------------------------------------------------

#### Phpdocumentor {#phpdocumentor-functions-callbackneedsreturn}

`callback-function-needs-return`{.interpreted-text role="ref"}, in
src/phpDocumentor/Plugin/ServiceProvider.php:24.

The array\_walk() function is called on the plugin\'s list. Each element
is registered with the application, but is not used directly : this is
for later. The error mechanism is to throw an exception : this is the
only expected feedback. As such, no return is expected. May be a
\'foreach\' loop would be more appropriate here, but this is syntactic
sugar.

``` {.php}
array_walk(
            $plugins,
            function ($plugin) use ($app) {
                /** @var Plugin $plugin */
                $provider = (strpos($plugin->getClassName(), '\') === false)
                    ? sprintf('phpDocumentor\Plugin\%s\ServiceProvider', $plugin->getClassName())
                    : $plugin->getClassName();
                if (!class_exists($provider)) {
                    throw new \RuntimeException('Loading Service Provider for ' . $provider . ' failed.');
                }

                try {
                    $app->register(new $provider($plugin));
                } catch (\InvalidArgumentException $e) {
                    throw new \RuntimeException($e->getMessage());
                }
            }
        );
```

### Wrong Range Check

#### Dolibarr {#dolibarr-structures-wrongrange}

`wrong-range-check`{.interpreted-text role="ref"}, in
htdocs/includes/phpoffice/PhpSpreadsheet/Spreadsheet.php:1484.

When \$tabRatio is 1001, then the condition is valid, and the ratio
accepted. The right part of the condition is not executed.

``` {.php}
public function setTabRatio($tabRatio)
    {
        if ($tabRatio >= 0 || $tabRatio <= 1000) {
            $this->tabRatio = (int) $tabRatio;
        } else {
            throw new Exception('Tab ratio must be between 0 and 1000.');
        }
    }
```

------------------------------------------------------------------------

#### WordPress {#wordpress-structures-wrongrange}

`wrong-range-check`{.interpreted-text role="ref"}, in
wp-includes/formatting.php:3634.

This condition may be easier to read as [\$diff \>= WEEK\_IN\_SECONDS &&
\$diff \< MONTH\_IN\_SECONDS]{.title-ref}. When testing for outside this
interval, using not is also more readable : [!(\$diff \>=
WEEK\_IN\_SECONDS && \$diff \< MONTH\_IN\_SECONDS)]{.title-ref}.

``` {.php}
} elseif ( $diff < MONTH_IN_SECONDS && $diff >= WEEK_IN_SECONDS ) {
        $weeks = round( $diff / WEEK_IN_SECONDS );
        if ( $weeks <= 1 ) {
            $weeks = 1;
        }
        /* translators: Time difference between two dates, in weeks. %s: Number of weeks */
        $since = sprintf( _n( '%s week', '%s weeks', $weeks ), $weeks );
```

### Cant Instantiate Class

#### WordPress {#wordpress-classes-cantinstantiateclass}

`cant-instantiate-class`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### strpos() Too Much

#### WordPress {#wordpress-performances-strpostoomuch}

`strpos()-too-much`{.interpreted-text role="ref"}, in
core/traits/Request/Server.php:127.

Instead of searching for `HTTP_`, it is faster to compare the first 5
chars to the literal `HTTP_`. In case of absence, this solution returns
faster.

``` {.php}
if (strpos($header, 'HTTP_') === 0) {
                $header = substr($header, 5);
            } elseif (strpos($header, 'CONTENT_') !== 0) {
                continue;
            }
```

### Weak Typing

#### TeamPass {#teampass-classes-weaktype}

`weak-typing`{.interpreted-text role="ref"}, in
includes/libraries/Tree/NestedTree/NestedTree.php:100.

The is\_null() test detects a special situation, that requires usage of
default values. The \'else\' handles every other situations, including
when the \$node is an object, or anything else. \$this-\>getNode() will
gain from having typehints : it may be NULL, or the results of
mysqli\_fetch\_object() : a stdClass object. The expected properties of
nleft and nright are not certain to be available.

``` {.php}
public function getDescendants($id = 0, $includeSelf = false, $childrenOnly = false, $unique_id_list = false)
    {
        global $link;
        $idField = $this->fields['id'];

        $node = $this->getNode($id);
        if (is_null($node)) {
            $nleft = 0;
            $nright = 0;
            $parent_id = 0;
            $personal_folder = 0;
        } else {
            $nleft = $node->nleft;
            $nright = $node->nright;
            $parent_id = $node->$idField;
            $personal_folder = $node->personal_folder;
        }
```

### Check JSON

#### Woocommerce {#woocommerce-structures-checkjson}

`check-json`{.interpreted-text role="ref"}, in
includes/admin/helper/class-wc-helper-plugin-info.php:66.

In case the body is an empty string, this will be correctly decoded, but
will yield an object with an empty-named property.

``` {.php}
$results = json_decode( wp_remote_retrieve_body( $request ), true );
        if ( ! empty( $results ) ) {
            $response = (object) $results;
        }

        return $response;
```

### Bad Constants Names

#### PrestaShop {#prestashop-constants-badconstantnames}

`bad-constants-names`{.interpreted-text role="ref"}, in
src/PrestaShopBundle/Install/Upgrade.php:214.

INSTALL\_PATH is a valid name for a constant. \_\_PS\_BASE\_URI\_\_ is
not a valid name.

``` {.php}
require_once(INSTALL_PATH . 'install_version.php');
            // needed for upgrade before 1.5
            if (!defined('__PS_BASE_URI__')) {
                define('__PS_BASE_URI__', str_replace('//', '/', '/'.trim(preg_replace('#/(install(-dev)?/upgrade)$#', '/', str_replace('\', '/', dirname($_SERVER['REQUEST_URI']))), '/').'/'));
            }
```

------------------------------------------------------------------------

#### Zencart {#zencart-constants-badconstantnames}

`bad-constants-names`{.interpreted-text role="ref"}, in
zc\_install/ajaxTestDBConnection.php:10.

A case where PHP needs help : if the PHP version is older than 5.3, then
it is valid to compensate. Though, this \_\_DIR\_\_ has a fixed value,
wherever it is used, while the official \_\_DIR\_\_ change from dir to
dir.

``` {.php}
if (!defined('__DIR__')) define('__DIR__', dirname(__FILE__));
```

### Dont Mix ++

#### Contao {#contao-structures-dontmixplusplus}

`dont-mix-++`{.interpreted-text role="ref"}, in
core-bundle/src/Resources/contao/drivers/DC\_Table.php:1272.

Incrementing and multiplying at the same time.

``` {.php}
$this->Database->prepare("UPDATE " . $this->strTable . " SET sorting=? WHERE id=?")
           ->execute(($count++ * 128), $objNewSorting->id);
```

------------------------------------------------------------------------

#### Typo3 {#typo3-structures-dontmixplusplus}

`dont-mix-++`{.interpreted-text role="ref"}, in
typo3/sysext/backend/Classes/Controller/SiteConfigurationController.php:74.

The post-increment is not readable at first glance.

``` {.php}
foreach ($row['rootline'] as &$record) {
                $record['margin'] = $i++ * 20;
            }
```

### Abstract Or Implements

#### Zurmo {#zurmo-classes-abstractorimplements}

`abstract-or-implements`{.interpreted-text role="ref"}, in
app/protected/extensions/zurmoinc/framework/views/MassEditProgressView.php:30.

The class MassEditProgressView extends ProgressView, which is an
abstract class. That class defines one abstract method : abstract
protected function headerLabelPrefixContent(). Yet, the class
MassEditProgressView doesn\'t implements this method. This means that
the class can\'t be instatiated, and indeed, it isn\'t. The class
MassEditProgressView is subclassed, by the class
MarketingListMembersMassSubscribeProgressView, which implements the
method headerLabelPrefixContent(). As such, MassEditProgressView should
be marked abstract, so as to prevent any instantiation attempt.

``` {.php}
class MassEditProgressView extends ProgressView { 
    /**/ 
}
```

### Incompatible Signature Methods

#### SuiteCrm {#suitecrm-classes-incompatiblesignature}

`incompatible-signature-methods`{.interpreted-text role="ref"}, in
modules/Home/Dashlets/RSSDashlet/RSSDashlet.php:138.

The class in the RSSDashlet.php file has an \'array\' typehint which is
not in the parent Dashlet class. While both files compile separately,
they yield a PHP warning when running : typehinting mismatch only yields
a warning.

``` {.php}
// File /modules/Home/Dashlets/RSSDashlet/RSSDashlet.php
    public function saveOptions(
        array $req
        )
    {

// File /include/Dashlets/Dashlets.php
    public function saveOptions( $req ) {
```

### Ambiguous Visibilities

#### Typo3 {#typo3-classes-ambiguousvisibilities}

`ambiguous-visibilities`{.interpreted-text role="ref"}, in
typo3/sysext/backend/Classes/Controller/NewRecordController.php:90.

\$allowedNewTables is declared once protected and once public.
\$allowedNewTables is rare : 2 occurences. This may lead to confusion
about access to this property.

``` {.php}
class NewRecordController
{
/.. many lines../
    /**
     * @var array
     */
    protected $allowedNewTables;

class DatabaseRecordList
{
/..../ 
    /**
     * Used to indicate which tables (values in the array) that can have a
     * create-new-record link. If the array is empty, all tables are allowed.
     *
     * @var string[]
     */
    public $allowedNewTables = [];
```

### Could Be Abstract Class

#### Edusoho {#edusoho-classes-couldbeabstractclass}

`could-be-abstract-class`{.interpreted-text role="ref"}, in
src/Biz/Task/Strategy/BaseStrategy.php:14.

BaseStrategy is extended by NormalStrategy, DefaultStrategy (Not shown
here), but it is not instantiated itself.

``` {.php}
class BaseStrategy { 
    // Class code
}
```

------------------------------------------------------------------------

#### shopware {#shopware-classes-couldbeabstractclass}

`could-be-abstract-class`{.interpreted-text role="ref"}, in
engine/Shopware/Plugins/Default/Core/PaymentMethods/Components/GenericPaymentMethod.php:31.

A \'Generic\' class sounds like a class that could be \'abstract\'.

``` {.php}
class GenericPaymentMethod extends BasePaymentMethod { 
    // More class code
}
```

### Continue Is For Loop

#### XOOPS {#xoops-structures-continueisforloop}

`continue-is-for-loop`{.interpreted-text role="ref"}, in
htdocs/kernel/object.php:711.

break is used here for cases, unless the case includes a if/then
structures, in which it becomes a continue. It really should be a break.

``` {.php}
foreach ($this->vars as $k => $v) {
            $cleanv = $v['value'];
            if (!$v['changed']) {
            } else {
                $cleanv = is_string($cleanv) ? trim($cleanv) : $cleanv;
                switch ($v['data_type']) {
                    case XOBJ_DTYPE_TIMESTAMP:
                        $cleanv = !is_string($cleanv) && is_numeric($cleanv) ? date(_DBTIMESTAMPSTRING, $cleanv) : date(_DBTIMESTAMPSTRING, strtotime($cleanv));
                        break;
                    case XOBJ_DTYPE_TIME:
                        $cleanv = !is_string($cleanv) && is_numeric($cleanv) ? date(_DBTIMESTRING, $cleanv) : date(_DBTIMESTRING, strtotime($cleanv));
                        break;
                    case XOBJ_DTYPE_DATE:
                        $cleanv = !is_string($cleanv) && is_numeric($cleanv) ? date(_DBDATESTRING, $cleanv) : date(_DBDATESTRING, strtotime($cleanv));
                        break;
                    case XOBJ_DTYPE_TXTBOX:
                        if ($v['required'] && $cleanv != '0' && $cleanv == '') {
                            $this->setErrors(sprintf(_XOBJ_ERR_REQUIRED, $k));
                            continue 2;
                        }
                        if (isset($v['maxlength']) && strlen($cleanv) > (int)$v['maxlength']) {
                            $this->setErrors(sprintf(_XOBJ_ERR_SHORTERTHAN, $k, (int)$v['maxlength']));
                            continue 2;
                        }
```

### Wrong Access Style to Property

#### HuMo-Gen {#humo-gen-classes-undeclaredstaticproperty}

`wrong-access-style-to-property`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

lame\_binary\_path is a static property, but it is accessed as a normal
property in the exception call, while it is checked with a valid syntax.

``` {.php}
protected function wavToMp3($data)
    {
        if (!file_exists(self::$lame_binary_path) || !is_executable(self::$lame_binary_path)) {
            throw new Exception('Lame binary  . $this->lame_binary_path .  does not exist or is not executable');
        }
```

### Method Could Be Static

#### FuelCMS {#fuelcms-classes-couldbestatic}

`method-could-be-static`{.interpreted-text role="ref"}, in
fuel/modules/fuel/models/Fuel\_assets\_model.php:240.

This method makes no usage of \$this : it only works on the incoming
argument, \$file. This may even be a function.

``` {.php}
public function get_file($file)
    {
        // if no extension is provided, then we determine that it needs to be decoded
        if (strpos($file, '.') === FALSE)
        {
            $file = uri_safe_decode($file);
        }
        return $file;
    }
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-classes-couldbestatic}

`method-could-be-static`{.interpreted-text role="ref"}, in
system/ee/legacy/libraries/Upload.ph:859.

This method returns the list of mime type, by using a hidden global
value : ee() is a functioncall that give access to the external storage
of values.

``` {.php}
/**
     * List of Mime Types
     *
     * This is a list of mime types.  We use it to validate
     * the allowed types set by the developer
     *
     * @param   string
     * @return  string
     */
    public function mimes_types($mime)
    {
        ee()->load->library('mime_type');
        return ee()->mime_type->isSafeForUpload($mime);
    }
```

### Possible Missing Subpattern

#### phpMyAdmin {#phpmyadmin-php-missingsubpattern}

`possible-missing-subpattern`{.interpreted-text role="ref"}, in
libraries/classes/Advisor.php:557.

The last capturing subpattern is `( \[(.*)\])?` and it is optional.
Indeed, when the pattern succeed, the captured values are stored in
`$match`. Yet, the code checks for the existence of `$match[3]` before
using it.

``` {.php}
if (preg_match("/rule\s'(.*)'( \[(.*)\])?$/", $line, $match)) {
                    $ruleLine = 1;
                    $ruleNo++;
                    $rules[$ruleNo] = ['name' => $match[1]];
                    $lines[$ruleNo] = ['name' => $i + 1];
                    if (isset($match[3])) {
                        $rules[$ruleNo]['precondition'] = $match[3];
                        $lines[$ruleNo]['precondition'] = $i + 1;
                    }
```

------------------------------------------------------------------------

#### SPIP {#spip-php-missingsubpattern}

`possible-missing-subpattern`{.interpreted-text role="ref"}, in
ecrire/inc/filtres\_dates.php:73.

This code avoid the PHP notice by padding the resulting array (see
comment in French : eviter === avoid)

``` {.php}
if (preg_match("#^([12][0-9]{3}[-/][01]?[0-9])([-/]00)?( [-0-9:]+)?$#", $date, $regs)) {
                $regs = array_pad($regs, 4, null); // eviter notice php
                $date = preg_replace("@/@", "-", $regs[1]) . "-00" . $regs[3];
            } else {
                $date = date("Y-m-d H:i:s", strtotime($date));
            }
```

### Overwritten Source And Value

#### ChurchCRM {#churchcrm-structures-foreachsourcevalue}

`overwritten-source-and-value`{.interpreted-text role="ref"}, in
edusoho/vendor/symfony/symfony/src/Symfony/Component/VarDumper/Dumper/CliDumper.php:194.

\$str is actually processed as an array (string of characters), and it
is also modified along the way.

``` {.php}
foreach ($str as $str) {
                if ($i < $m) {
                    $str .= \n;
                }
                if (0 < $this->maxStringWidth && $this->maxStringWidth < $len = mb_strlen($str, 'UTF-8')) {
                    $str = mb_substr($str, 0, $this->maxStringWidth, 'UTF-8');
                    $lineCut = $len - $this->maxStringWidth;
                }
                //.... More code
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-structures-foreachsourcevalue}

`overwritten-source-and-value`{.interpreted-text role="ref"}, in
system/ee/EllisLab/ExpressionEngine/Service/Theme/ThemeInstaller.php:595.

Looping over \$filename.

``` {.php}
foreach (directory_map($to_dir) as $directory => $filename)
            {
                if (is_string($directory))
                {
                    foreach ($filename as $filename)
                    {
                        unlink($to_dir.$directory.'/'.$filename);
                    }

                    @rmdir($to_dir.$directory);
                }
                else
                {
                    unlink($to_dir.$filename);
                }
            }
```

### Incompatible Signature Methods With Covariance

#### SuiteCrm {#suitecrm-classes-incompatiblesignature74}

`incompatible-signature-methods-with-covariance`{.interpreted-text
role="ref"}, in modules/Home/Dashlets/RSSDashlet/RSSDashlet.php:138.

The class in the RSSDashlet.php file has an \'array\' typehint which is
not in the parent Dashlet class. While both files compile separately,
they yield a PHP warning when running : typehinting mismatch only yields
a warning.

``` {.php}
// File /modules/Home/Dashlets/RSSDashlet/RSSDashlet.php
    public function saveOptions(
        array $req
        )
    {

// File /include/Dashlets/Dashlets.php
    public function saveOptions( $req ) {
```

### Could Be Private Class Constant

#### Phinx {#phinx-classes-couldbeprivateconstante}

`could-be-private-class-constant`{.interpreted-text role="ref"}, in
src/Phinx/Db/Adapter/MysqlAdapter.php:46.

The code includes a fair number of class constants. The one listed here
are only used to define TEXT columns in MySQL, with their maximal size.
Since they are only intented to be used by the MySQL driver, they may be
private.

``` {.php}
class MysqlAdapter extends PdoAdapter implements AdapterInterface
{

//.....
    const TEXT_SMALL   = 255;
    const TEXT_REGULAR = 65535;
    const TEXT_MEDIUM  = 16777215;
    const TEXT_LONG    = 4294967295;
```

### Disconnected Classes

#### WordPress {#wordpress-classes-disconnectedclasses}

`disconnected-classes`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### Wrong Class Name Case

#### WordPress {#wordpress-classes-wrongcase}

`wrong-class-name-case`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### One Letter Functions

#### ThinkPHP {#thinkphp-functions-oneletterfunctions}

`one-letter-functions`{.interpreted-text role="ref"}, in
ThinkPHP/Mode/Api/functions.php:859.

There are also the functions C, E, G\... The applications is written in
a foreign language, which may be a base for non-significant function
names.

``` {.php}
function F($name, $value = '', $path = DATA_PATH)
```

------------------------------------------------------------------------

#### Cleverstyle {#cleverstyle-functions-oneletterfunctions}

`one-letter-functions`{.interpreted-text role="ref"}, in
core/drivers/DB/PostgreSQL.php:71.

There is also function f(). Those are actually overwritten methods. From
the documentation, q() is for query, and f() is for fetch. Those are
short names for frequently used functions.

``` {.php}
public function q ($query, ...$params) {
```

------------------------------------------------------------------------

#### Dolibarr {#dolibarr-php-debuginfousage}

`\_\_debuginfo()-usage`{.interpreted-text role="ref"}, in
htdocs/includes/stripe/lib/StripeObject.php:108.

\_values is a private property from the Stripe Class. The class contains
other objects, but only \_values are displayed with var\_dump.

``` {.php}
// Magic method for var_dump output. Only works with PHP >= 5.6
    public function __debugInfo()
    {
        return $this->_values;
    }
```

### PHP7 Dirname

#### OpenConf {#openconf-structures-php7dirname}

`php7-dirname`{.interpreted-text role="ref"}, in include.php:61.

Since PHP 7.0, dirname( , 2); does the job.

``` {.php}
$OC_basepath = dirname(dirname($_SERVER['PHP_SELF']));
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-structures-php7dirname}

`php7-dirname`{.interpreted-text role="ref"}, in
includes/installer/Installer.php:1173.

Since PHP 7.0, dirname( , 2); does the job.

``` {.php}
protected function envPrepPath() {
        global $IP;
        $IP = dirname( dirname( __DIR__ ) );
        $this->setVar( 'IP', $IP );
    }
```

### Avoid set\_error\_handler \$context Argument

#### shopware {#shopware-php-avoidseterrorhandlercontextarg}

`avoid-set\_error\_handler-$context-argument`{.interpreted-text
role="ref"}, in
engine/Shopware/Plugins/Default/Core/ErrorHandler/Bootstrap.php:162.

The registered handler is a local method, called `errorHandler`, which
has 6 arguments, and relays those 6 arguments to set\_error\_handler().

``` {.php}
public function registerErrorHandler($errorLevel = E_ALL)
    {
        // Only register once.  Avoids loop issues if it gets registered twice.
        if (self::$_registeredErrorHandler) {
            set_error_handler([$this, 'errorHandler'], $errorLevel);

            return $this;
        }

        self::$_origErrorHandler = set_error_handler([$this, 'errorHandler'], $errorLevel);
        self::$_registeredErrorHandler = true;

        return $this;
    }
```

------------------------------------------------------------------------

#### Vanilla {#vanilla-php-avoidseterrorhandlercontextarg}

`avoid-set\_error\_handler-$context-argument`{.interpreted-text
role="ref"}, in library/core/functions.error.php:747.

Gdn\_ErrorHandler is a function that requires 6 arguments.

``` {.php}
set_error_handler('Gdn_ErrorHandler', E_ALL & ~E_STRICT)
```

### Unused Private Properties

#### OpenEMR {#openemr-classes-unusedprivateproperty}

`unused-private-properties`{.interpreted-text role="ref"}, in
entities/User.php:46.

This class has a long list of private properties. It also has an equally
long (minus one) list of accessors, and a \_\_toString() method which
exposes all of them. \$oNotes is the only one never mentionned anywhere.

``` {.php}
class User
{
    /**
     * @Column(name=id, type=integer)
     * @GeneratedValue(strategy=AUTO)
     */
    private $id;

    /**
     * @OneToMany(targetEntity=ONote, mappedBy=user)
     */
    private $oNotes;
```

------------------------------------------------------------------------

#### phpadsnew {#phpadsnew-classes-unusedprivateproperty}

`unused-private-properties`{.interpreted-text role="ref"}, in
lib/OA/Admin/UI/component/Form.php:23.

\$dispatcher is never used anywhere.

``` {.php}
class OA_Admin_UI_Component_Form
    extends HTML_QuickForm
{
    private $dispatcher;
```

### Unused Functions

#### Woocommerce {#woocommerce-functions-unusedfunctions}

`unused-functions`{.interpreted-text role="ref"}, in
includes/wc-core-functions.php:2124.

wc\_is\_external\_resource() is unused. This is not obvious immediately,
since there is a call from wc\_get\_relative\_url(). Yet since
wc\_get\_relative\_url() itself is never used, then it is a dead
function. As such, since wc\_is\_external\_resource() is only called by
this first function, it also dies, even though it is called in the code.

``` {.php}
/**
 * Make a URL relative, if possible.
 *
 * @since 3.2.0
 * @param string $url URL to make relative.
 * @return string
 */
function wc_get_relative_url( $url ) {
    return wc_is_external_resource( $url ) ? $url : str_replace( array( 'http://', 'https://' ), '//', $url );
}

/**
 * See if a resource is remote.
 *
 * @since 3.2.0
 * @param string $url URL to check.
 * @return bool
 */
function wc_is_external_resource( $url ) {
    $wp_base = str_replace( array( 'http://', 'https://' ), '//', get_home_url( null, '/', 'http' ) );

    return strstr( $url, '://' ) && ! strstr( $url, $wp_base );
}
```

------------------------------------------------------------------------

#### Piwigo {#piwigo-functions-unusedfunctions}

`unused-functions`{.interpreted-text role="ref"}, in
admin/include/functions.php:2167.

get\_user\_access\_level\_html\_options() is unused and can\'t be find
in the code.

``` {.php}
/**
 * Returns access levels as array used on template with html_options functions.
 *
 * @param int $MinLevelAccess
 * @param int $MaxLevelAccess
 * @return array
 */
function get_user_access_level_html_options($MinLevelAccess = ACCESS_FREE, $MaxLevelAccess = ACCESS_CLOSED)
{
  $tpl_options = array();
  for ($level = $MinLevelAccess; $level <= $MaxLevelAccess; $level++)
  {
    $tpl_options[$level] = l10n(sprintf('ACCESS_%d', $level));
  }
  return $tpl_options;
}
```

### Unused Interfaces

#### Tine20 {#tine20-interfaces-unusedinterfaces}

`unused-interfaces`{.interpreted-text role="ref"}, in
tine20/Tinebase/User/LdapPlugin/Interface.php:20.

Tinebase\_User\_LdapPlugin\_Interface is mentioned as a type for a
property, in a php doc document. Typehinted properties are available
since PHP 7.4

``` {.php}
interface Tinebase_User_LdapPlugin_Interface {

//----------
// in tine20/Tinebase/User/ActiveDirectory.php
/** @var Tinebase_User_LdapPlugin_Interface $plugin */
```

### Exception Order

#### Woocommerce {#woocommerce-exceptions-alreadycaught}

`exception-order`{.interpreted-text role="ref"}, in
includes/api/v1/class-wc-rest-products-controller.php:787.

This try/catch expression is able to catch both WC\_Data\_Exception and
WC\_REST\_Exception.

In another file, /includes/api/class-wc-rest-exception.php, we find that
WC\_REST\_Exception extends WC\_Data\_Exception (class
WC\_REST\_Exception extends WC\_Data\_Exception {}). So
WC\_Data\_Exception is more general, and a WC\_REST\_Exception exception
is caught with WC\_Data\_Exception Exception. The second catch should be
put in first.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
try {
            $product_id = $this->save_product( $request );
            $post       = get_post( $product_id );
            $this->update_additional_fields_for_object( $post, $request );
            $this->update_post_meta_fields( $post, $request );

            /**
             * Fires after a single item is created or updated via the REST API.
             *
             * @param WP_Post         $post      Post data.
             * @param WP_REST_Request $request   Request object.
             * @param boolean         $creating  True when creating item, false when updating.
             */
            do_action( 'woocommerce_rest_insert_product', $post, $request, false );
            $request->set_param( 'context', 'edit' );
            $response = $this->prepare_item_for_response( $post, $request );

            return rest_ensure_response( $response );
        } catch ( WC_Data_Exception $e ) {
            return new WP_Error( $e->getErrorCode(), $e->getMessage(), $e->getErrorData() );
        } catch ( WC_REST_Exception $e ) {
            return new WP_Error( $e->getErrorCode(), $e->getMessage(), array( 'status' => $e->getCode() ) );
        }
```

### Rethrown Exceptions

#### PrestaShop {#prestashop-exceptions-rethrown}

`rethrown-exceptions`{.interpreted-text role="ref"}, in
classes/webservice/WebserviceOutputBuilder.php:731.

The setSpecificField method catches a WebserviceException, representing
an issue with the call to the webservice. However, that piece of
information is lost, and the exception is rethrown immediately, without
any action.

``` {.php}
public function setSpecificField($object, $method, $field_name, $entity_name)
    {
        try {
            $this->validateObjectAndMethod($object, $method);
        } catch (WebserviceException $e) {
            throw $e;
        }

        $this->specificFields[$field_name] = array('entity'=>$entity_name, 'object' => $object, 'method' => $method, 'type' => gettype($object));
        return $this;
    }
```

### Slow Functions

#### ChurchCRM {#churchcrm-performances-slowfunctions}

`slow-functions`{.interpreted-text role="ref"}, in
src/Reports/PrintDeposit.php:35.

You may replace this with a isset() : \$\_POST can\'t contain a NULL
value, unless it was set by the script itself.

``` {.php}
array_key_exists("report_type", $_POST);
```

------------------------------------------------------------------------

#### SuiteCrm {#suitecrm-performances-slowfunctions}

`slow-functions`{.interpreted-text role="ref"}, in
include/json\_config.php:242.

This is a equivalent for nl2br()

``` {.php}
preg_replace("/\r\n/", "<BR>", $focus->$field)
```

### Joining file()

#### WordPress {#wordpress-performances-joinfile}

`joining-file()`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

------------------------------------------------------------------------

#### SPIP {#spip-performances-joinfile}

`joining-file()`{.interpreted-text role="ref"}, in
ecrire/inc/install.php:109.

When the file is not accessible, file() returns null, and can\'t be
processed by join().

``` {.php}
$s = @join('', file($file));
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-performances-joinfile}

`joining-file()`{.interpreted-text role="ref"}, in
ExpressionEngine\_Core2.9.2/system/expressionengine/libraries/simplepie/idn/idna\_convert.class.php:100.

join(\'\', ) is used as a replacement for file\_get\_contents(), which
was introduced in PHP 4.3.0.

``` {.php}
if (function_exists('file_get_contents')) {
    $this->NP = unserialize(file_get_contents(dirname(__FILE__).'/npdata.ser'));
} else {
    $this->NP = unserialize(join('', file(dirname(__FILE__).'/npdata.ser')));
}
```

------------------------------------------------------------------------

#### PrestaShop {#prestashop-performances-joinfile}

`joining-file()`{.interpreted-text role="ref"}, in
classes/module/Module.php:2972.

implode(\'\', ) is probably not the slowest part in these lines.

``` {.php}
$override_file = file($override_path);

eval(preg_replace(array('#^\s*<\?(?:php)?#', '#class\s+'.$classname.'\s+extends\s+([a-z0-9_]+)(\s+implements\s+([a-z0-9_]+))?#i'), array(' ', 'class '.$classname.'OverrideOriginal_remove'.$uniq), implode('', $override_file)));
$override_class = new ReflectionClass($classname.'OverrideOriginal_remove'.$uniq);

$module_file = file($this->getLocalPath().'override/'.$path);
eval(preg_replace(array('#^\s*<\?(?:php)?#', '#class\s+'.$classname.'(\s+extends\s+([a-z0-9_]+)(\s+implements\s+([a-z0-9_]+))?)?#i'), array(' ', 'class '.$classname.'Override_remove'.$uniq), implode('', $module_file)));
```

### Simplify Regex

#### Zurmo {#zurmo-structures-simplepreg}

`simplify-regex`{.interpreted-text role="ref"}, in
app/protected/core/components/Browser.php:73.

Here, strpos() or stripos() is a valid replacement.

``` {.php}
preg_match('/opera/', $userAgent)
```

------------------------------------------------------------------------

#### OpenConf {#openconf-structures-simplepreg}

`simplify-regex`{.interpreted-text role="ref"}, in
openconf/include.php:964.

[%e]{.title-ref} is not a special char for PCRE regex, although it look
like it. It is a special char for date() or printf(). This
preg\_replace() may be upgraded to str\_replace()

``` {.php}
$conv = iconv($cp, 'utf-8', strftime(preg_replace("/\%e/", '%#d', $format), $time));
```

### Make One Call With Array

#### HuMo-Gen {#humo-gen-performances-makeonecall}

`make-one-call-with-array`{.interpreted-text role="ref"}, in
admin/include/kcfinder/lib/helper\_text.php:47.

The three calls to str\_replace() could be replaced by one, using array
arguments. Nesting the calls doesn\'t reduce the number of calls.

``` {.php}
static function jsValue($string) {
        return
            preg_replace('/\r?\n/', "\n",
            str_replace('"', "\\"",
            str_replace("'", "\'",
            str_replace("\", "\\",
        $string))));
    }
```

------------------------------------------------------------------------

#### Edusoho {#edusoho-performances-makeonecall}

`make-one-call-with-array`{.interpreted-text role="ref"}, in
src/AppBundle/Common/StringToolkit.php:55.

Since str\_replace is already using an array, the second argument must
also be an array, with repeated empty strings. That syntax allows adding
the \'&nbsp;\' and \' \' to those arrays. Note also that trim() should
be be called early, but since some of the replacing may generate
terminal spaces, it should be kept as is.

``` {.php}
$text = strip_tags($text);

        $text = str_replace(array(\n, \r, \t), '', $text);
        $text = str_replace('&nbsp;', ' ', $text);
        $text = trim($text);
```

### No Count With 0

#### Contao {#contao-performances-notcountnull}

`no-count-with-0`{.interpreted-text role="ref"}, in
system/modules/repository/classes/RepositoryManager.php:1148.

If \$elist contains at least one element, then it is not empty().

``` {.php}
$ext->found = count($elist)>0;
```

------------------------------------------------------------------------

#### WordPress {#wordpress-performances-notcountnull}

`no-count-with-0`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

\$build or \$signature are empty at that point, no need to calculate
their respective length.

``` {.php}
// Check for zero length, although unlikely here
    if (strlen($built) == 0 || strlen($signature) == 0) {
      return false;
    }
```

### time() Vs strtotime()

#### Woocommerce {#woocommerce-performances-timevsstrtotime}

`time()-vs-strtotime()`{.interpreted-text role="ref"}, in
includes/class-wc-webhook.php:384.

time() would be faster here, as an entropy generator. Yet, it would
still be better to use an actual secure entropy generator, like
random\_byte or random\_int. In case of older version, microtime() would
yield better entropy.

``` {.php}
public function get_new_delivery_id() {
        // Since we no longer use comments to store delivery logs, we generate a unique hash instead based on current time and webhook ID.
        return wp_hash( $this->get_id() . strtotime( 'now' ) );
    }
```

### Getting Last Element

#### Thelia {#thelia-arrays-gettinglastelement}

`getting-last-element`{.interpreted-text role="ref"}, in
/core/lib/Thelia/Core/Security/AccessManager.php:61.

This code extract the last element with array\_slice (position -1) as an
array, then get the element in the array with current().

``` {.php}
current(\array_slice(self::$accessPows, -1, 1, true))
```

### Avoid glob() Usage

#### Phinx {#phinx-performances-noglob}

`avoid-glob()-usage`{.interpreted-text role="ref"}, in
src/Phinx/Migration/Manager.php:362.

glob() searches for a list of files in the migration folder. Those files
are not known, but they have a format, as checked later with the regex :
a combinaison of `FilesystemIterator` and `RegexIterator` would do the
trick too.

``` {.php}
$phpFiles = glob($config->getMigrationPath() . DIRECTORY_SEPARATOR . '*.php');

            // filter the files to only get the ones that match our naming scheme
            $fileNames = array();
            /** @var AbstractMigration[] $versions */
            $versions = array();

            foreach ($phpFiles as $filePath) {
                if (preg_match('/([0-9]+)_([_a-z0-9]*).php/', basename($filePath))) {
```

------------------------------------------------------------------------

#### NextCloud {#nextcloud-performances-noglob}

`avoid-glob()-usage`{.interpreted-text role="ref"}, in
lib/private/legacy/helper.php:185.

Recursive copy of folders, based on scandir(). `DirectoryIterator` and
`FilesystemIterator` would do the same without the recursion.

``` {.php}
static function copyr($src, $dest) {
        if (is_dir($src)) {
            if (!is_dir($dest)) {
                mkdir($dest);
            }
            $files = scandir($src);
            foreach ($files as $file) {
                if ($file != "." && $file != "..") {
                    self::copyr("$src/$file", "$dest/$file");
                }
            }
        } elseif (file_exists($src) && !\OC\Files\Filesystem::isFileBlacklisted($src)) {
            copy($src, $dest);
        }
    }
```

### Avoid Concat In Loop

#### SuiteCrm {#suitecrm-performances-noconcatinloop}

`avoid-concat-in-loop`{.interpreted-text role="ref"}, in
include/export\_utils.php:433.

\$line is build in several steps, then then final version is added to
\$content. It would be much faster to make \$content an array, and
implode it once after the loop.

``` {.php}
foreach($records as $record)
        {
            $line = implode("\"" . getDelimiter() . "\"", $record);
            $line = "\"" . $line;
            $line .= "\"\r\n";
            $line = parseRelateFields($line, $record, $customRelateFields);
            $content .= $line;
        }
```

------------------------------------------------------------------------

#### ThinkPHP {#thinkphp-performances-noconcatinloop}

`avoid-concat-in-loop`{.interpreted-text role="ref"}, in
ThinkPHP/Common/functions.php:720.

The foreach loop appends the \$name and builds a fully qualified name.

``` {.php}
if (!C('APP_USE_NAMESPACE')) {
        $class = parse_name($name, 1);
        import($module . '/' . $layer . '/' . $class . $layer);
    } else {
        $class = $module . '\' . $layer;
        foreach ($array as $name) {
            $class .= '\' . parse_name($name, 1);
        }
        // 导入资源类库
        if ($extend) {
            // 扩展资源
            $class = $extend . '\' . $class;
        }
    }
    return $class . $layer;
```

### Use pathinfo() Arguments

#### Zend-Config {#zend-config-php-usepathinfoargs}

`use-pathinfo()-arguments`{.interpreted-text role="ref"}, in
src/Factory.php:74:90.

The [\$filepath]{.title-ref} is broken into pieces, and then, only the
\'extension\' part is used. With the PATHINFO\_EXTENSION constant used
as a second argument, only this value could be returned.

``` {.php}
$pathinfo = pathinfo($filepath);

        if (! isset($pathinfo['extension'])) {
            throw new Exception\RuntimeException(sprintf(
                'Filename "%s" is missing an extension and cannot be auto-detected',
                $filename
            ));
        }

        $extension = strtolower($pathinfo['extension']);
        // Only $extension is used beyond that point
```

------------------------------------------------------------------------

#### ThinkPHP {#thinkphp-php-usepathinfoargs}

`use-pathinfo()-arguments`{.interpreted-text role="ref"}, in
ThinkPHP/Extend/Library/ORG/Net/UploadFile.class.php:508.

Without any other check, pathinfo() could be used with
PATHINFO\_EXTENSION.

``` {.php}
private function getExt($filename) {
        $pathinfo = pathinfo($filename);
        return $pathinfo['extension'];
    }
```

### Substring First

#### SPIP {#spip-performances-substrfirst}

`substring-first`{.interpreted-text role="ref"}, in
ecrire/inc/filtres.php:1694.

The code first makes everything uppercase, including the leading and
trailing spaces, and then, removes them : it would be best to swap those
operations. Note that spip\_substr() is not considered in this analysis,
but with SPIP knowledge, it could be moved inside the calls.

``` {.php}
function filtre_initiale($nom) {
    return spip_substr(trim(strtoupper(extraire_multi($nom))), 0, 1);
}
```

------------------------------------------------------------------------

#### PrestaShop {#prestashop-performances-substrfirst}

`substring-first`{.interpreted-text role="ref"}, in
admin-dev/filemanager/include/utils.php:197.

dirname() reduces the string (or at least, keeps it the same size), so
it more efficient to have it first.

``` {.php}
dirname(str_replace(' ', '~', $str))
```

### Slice Arrays First

#### WordPress {#wordpress-arrays-slicefirst}

`slice-arrays-first`{.interpreted-text role="ref"}, in
modules/InboundEmail/InboundEmail.php:1080.

Instead of reading ALL the keys, and then, keeping only the first fifty,
why not read the 50 first items from the array, and then extract the
keys?

``` {.php}
$results = array_slice(array_keys($diff), 0 ,50);
```

### Double array\_flip()

#### NextCloud {#nextcloud-performances-doublearrayflip}

`double-array\_flip()`{.interpreted-text role="ref"}, in
lib/public/AppFramework/Http/EmptyContentSecurityPolicy.php:372.

The array \$allowedScriptDomains is flipped, to unset \'self\', then,
unflipped (or flipped again), to restore its initial state. Using
array\_keys() or array\_search() would yield the needed keys for
unsetting, at a lower cost.

``` {.php}
if(is_string($this->useJsNonce)) {
                $policy .= '\'nonce-'.base64_encode($this->useJsNonce).'\'';
                $allowedScriptDomains = array_flip($this->allowedScriptDomains);
                unset($allowedScriptDomains['\'self\'']);
                $this->allowedScriptDomains = array_flip($allowedScriptDomains);
                if(count($allowedScriptDomains) !== 0) {
                    $policy .= ' ';
                }
            }
```

### Closure Could Be A Callback

#### Tine20 {#tine20-functions-closure2string}

`closure-could-be-a-callback`{.interpreted-text role="ref"}, in
tine20/Tinebase/Convert/Json.php:318.

is\_scalar() is sufficient here.

``` {.php}
$value = array_filter($value, function ($val) { return is_scalar($val); });
```

------------------------------------------------------------------------

#### NextCloud {#nextcloud-functions-closure2string}

`closure-could-be-a-callback`{.interpreted-text role="ref"}, in
apps/files\_sharing/lib/ShareBackend/Folder.php:114.

\$qb is the object for the methodcall, passed via use. The closure may
have been replaced with array(\$qb, \'createNamedParameter\').

``` {.php}
$parents = array_map(function($parent) use ($qb) {
                return $qb->createNamedParameter($parent);
            }, $parents);
```

### Isset() On The Whole Array

#### Tine20 {#tine20-performances-issetwholearray}

`isset()-on-the-whole-array`{.interpreted-text role="ref"}, in
tine20/Crm/Model/Lead.php:208.

Only the second call is necessary : it also includes the first one.

``` {.php}
isset($relation['related_record']) && isset($relation['related_record']['n_fileas'])
```

------------------------------------------------------------------------

#### ExpressionEngine {#expressionengine-performances-issetwholearray}

`isset()-on-the-whole-array`{.interpreted-text role="ref"}, in
system/ee/legacy/libraries/Form\_validation.php:1487.

This is equivalent to [isset(\$this-\>\_field\_data\[\$field\],
\$this-\>\_field\_data\[\$field\]\[\'postdata\'\])]{.title-ref}, and the
second call may be skipped.

``` {.php}
!isset($this->_field_data[$field]) OR !isset($this->_field_data[$field]['postdata'])
```

### Compare Hash

#### Traq {#traq-security-comparehash}

`compare-hash`{.interpreted-text role="ref"}, in
src/Models/User.php:105.

This code should also avoid using SHA1.

``` {.php}
sha1($password) == $this->password
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-security-comparehash}

`compare-hash`{.interpreted-text role="ref"}, in
livezilla/\_lib/objects.global.users.inc.php:1391.

This code is using the stronger SHA256 but compares it to another
string. \$\_token may be non-empty, and still be comparable to 0.

``` {.php}
function IsValidToken($_token)
{
    if(!empty($_token))
        if(hash("sha256",$this->Token) == $_token)
            return true;
    return false;
}
```

### Register Globals

#### TeamPass {#teampass-security-registerglobals}

`register-globals`{.interpreted-text role="ref"}, in api/index.php:25.

The API starts with security features, such as the whitelist(). The
whitelist applies to IP addresses, so the query string is not sanitized.
Then, the QUERY\_STRING is parsed, and creates a lot of new global
variables.

``` {.php}
teampass_whitelist();

parse_str($_SERVER['QUERY_STRING']);
$method = $_SERVER['REQUEST_METHOD'];
$request = explode("/", substr(@$_SERVER['PATH_INFO'], 1));
```

------------------------------------------------------------------------

#### XOOPS {#xoops-security-registerglobals}

`register-globals`{.interpreted-text role="ref"}, in
htdocs/modules/system/admin/images/main.php:33:33.

This code only exports the POST variables as globals. And it does clean
incoming variables, but not all of them.

``` {.php}
// Check users rights
if (!is_object($xoopsUser) || !is_object($xoopsModule) || !$xoopsUser->isAdmin($xoopsModule->mid())) {
    exit(_NOPERM);
}

//  Check is active
if (!xoops_getModuleOption('active_images', 'system')) {
    redirect_header('admin.php', 2, _AM_SYSTEM_NOTACTIVE);
}

if (isset($_POST)) {
    foreach ($_POST as $k => $v) {
        ${$k} = $v;
    }
}

// Get Action type
$op = system_CleanVars($_REQUEST, 'op', 'list', 'string');
```

### Safe Curl Options

#### OpenConf {#openconf-security-curloptions}

`safe-curl-options`{.interpreted-text role="ref"}, in
openconf/include.php:703.

The function that holds that code is only used to call openconf.com,
over http, while openconf.com is hosted on https, nowadays. This may be
a sign of hard to access certificates.

``` {.php}
$ch = curl_init();
            curl_setopt($ch, CURLOPT_URL, $f);
            curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
            curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);       
            curl_setopt($ch, CURLOPT_AUTOREFERER, true);       
            curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);       
            curl_setopt($ch, CURLOPT_MAXREDIRS, 5);       
            curl_setopt($ch, CURLOPT_HEADER, false);       
            $s = curl_exec($ch);
            curl_close($ch);
            return($s);
```

### Unserialize Second Arg

#### Piwigo {#piwigo-security-unserializesecondarg}

`unserialize-second-arg`{.interpreted-text role="ref"}, in
admin/configuration.php:491.

unserialize() extracts information from the \$conf variable : this
variable is read from a configuration file. It is later tested to be an
array, whose index may not be all set (@\$disabled\[\$type\];). It would
be safer to make \$disabled an object, add the class to unserialize, and
set default values to the needed properties/index.

``` {.php}
$disabled = @unserialize(@$conf['disabled_derivatives']);
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-security-unserializesecondarg}

`unserialize-second-arg`{.interpreted-text role="ref"}, in
livezilla/\_lib/objects.global.inc.php:2600.

unserialize() only extract a non-empty value here. But its content is
not checked. It is later used as an array, with multiple index.

``` {.php}
$this->Customs = (!empty($_row["customs"])) ? @unserialize($_row["customs"]) : array();
```

### Encoded Simple Letters

#### Zurmo {#zurmo-security-encodedletters}

`encoded-simple-letters`{.interpreted-text role="ref"}, in
yii/framework/web/CClientScript.php:783.

This actually decodes into a copyright notice.

\'function cleanAndSanitizeScriptHeader(& \$output)

:   

    {

    :   \$requiredOne = \<span\>Copyright &\#169; Zurmo Inc., 2013. All
        rights reserved.;\....\'

``` {.php}
eval(\x66\x75\x6e\x63\x74\x69\x6f\x6e\x20\x63\x6c\x65\x61\x6e\x41\x6e\x64\x53\x61\x6e\x69\x74\x69\x7a\x65\x53\x63\x72 .
     \x69\x70\x74\x48\x65\x61\x64\x65\x72\x28\x26\x20\x24\x6f\x75\x74\x70\x75\x74\x29\x0d\x0a\x20\x20\x20\x20\x20\x20 .
     \x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x7b\x0d\x0a\x20\x20\x20\x20\x20\x20\x20 .
     \x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x24\x72\x65\x71\x75\x69\x72 .
     // several more lines like that
```

### Mkdir Default

#### Mautic {#mautic-security-mkdirdefault}

`mkdir-default`{.interpreted-text role="ref"}, in
app/bundles/CoreBundle/Helper/AssetGenerationHelper.php:120.

This code is creating some directories for Javascript or CSS (from the
directories names) : those require universal reading access, but
probably no execution nor writing access. 0711 would be sufficient in
this case.

``` {.php}
//combine the files into their corresponding name and put in the root media folder
                if ($env == 'prod') {
                    $checkPaths = [
                        $assetsFullPath,
                        $assetsFullPath/css,
                        $assetsFullPath/js,
                    ];
                    array_walk($checkPaths, function ($path) {
                        if (!file_exists($path)) {
                            mkdir($path);
                        }
                    });
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-security-mkdirdefault}

`mkdir-default`{.interpreted-text role="ref"}, in
interface/main/backuplog.php:27.

If \$BACKUP\_EVENTLOG\_DIR is a backup for an event log, this should be
stored out of the web server reach, with low rights, beside the current
user. This is part of a CLI PHP script.

``` {.php}
mkdir($BACKUP_EVENTLOG_DIR)
```

### Phpinfo

#### Dolphin {#dolphin-structures-phpinfousage}

`phpinfo`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/install/exec.php:4.

An actual phpinfo(), available during installation. Note that the
phpinfo() is actually triggered by a hidden POST variable.

``` {.php}
<?php

    if (!empty($_POST['phpinfo']))
        phpinfo();
    elseif (!empty($_POST['gdinfo']))
        echo '<pre>' . print_r(gd_info(), true) . '</pre>';

?>
<center>

    <form method=post>
        <input type=submit name=phpinfo value="PHP Info">
    </form>
    <form method=post>
        <input type=submit name=gdinfo value="GD Info">
    </form>

</center>
```

### Configure Extract

#### Zurmo {#zurmo-security-configureextract}

`configure-extract`{.interpreted-text role="ref"}, in
app/protected/modules/marketing/utils/GlobalMarketingFooterUtil.php:127.

This code intent to overwrite [\$hash]{.title-ref} and
[\$preview]{.title-ref} : it is even literally in the code. The
overwrite is intended too, and could even skip the initialisation of the
variables. Although the compact()/extract() combinaison is safe as now,
it could be safer to only relay the array index, instead of extracting
the variables here.

``` {.php}
public static function resolveManageSubscriptionsUrlByArray(array $queryStringArray, $preview = false)
        {
            $hash = $preview = null;
            extract(static::resolvePreviewAndHashFromArray($queryStringArray));
            return static::resolveManageSubscriptionsUrl($hash, $preview);
        }

// Also with : 
        protected static function resolvePreviewAndHashFromArray(array $queryStringArray)
        {
            $preview    = static::resolvePreviewFromArray($queryStringArray);
            $hash       = static::resolveHashByArray($queryStringArray);
            return compact('hash', 'preview');
        }
```

------------------------------------------------------------------------

#### Dolibarr {#dolibarr-security-configureextract}

`configure-extract`{.interpreted-text role="ref"}, in
htdocs/includes/restler/framework/Luracast/Restler/Format/HtmlFormat.php:224.

The extract() has been cleverly set in a closure, with a limited scope.
The potential overwrite may impact existing variables, such as
[\$\_]{.title-ref}, [\$nav]{.title-ref}, [\$form]{.title-ref}, and
[\$data]{.title-ref} itself. This may impact the following including.
Using EXTR\_SKIP would give existing variables priority, and avoid
interference.

``` {.php}
$template = function ($view) use ($data, $path) {
            $form = function () {
                return call_user_func_array(
                    'Luracast\Restler\UI\Forms::get',
                    func_get_args()
                );
            };
            if (!isset($data['form']))
                $data['form'] = $form;
            $nav = function () {
                return call_user_func_array(
                    'Luracast\Restler\UI\Nav::get',
                    func_get_args()
                );
            };
            if (!isset($data['nav']))
                $data['nav'] = $nav;

            $_ = function () use ($data, $path) {
                extract($data);
                $args = func_get_args();
                $task = array_shift($args);
                switch ($task) {
                    case 'require':
                    case 'include':
                        $file = $path . $args[0];
                        if (is_readable($file)) {
                            if (
                                isset($args[1]) &&
                                ($arrays = Util::nestedValue($data, $args[1]))
                            ) {
                                $str = '';
                                foreach ($arrays as $arr) {
                                    extract($arr);
                                    $str .= include $file;
                                }
                                return $str;
                            } else {
                                return include $file;
                            }
                        }
                        break;
                    case 'if':
                        if (count($args) < 2)
                            $args[1] = '';
                        if (count($args) < 3)
                            $args[2] = '';
                        return $args[0] ? $args[1] : $args[2];
                        break;
                    default:
                        if (isset($data[$task]) && is_callable($data[$task]))
                            return call_user_func_array($data[$task], $args);
                }
                return '';
            };
            extract($data);
            return @include $view;
        };
```

### Property Variable Confusion

#### PhpIPAM {#phpipam-structures-propertyvariableconfusion}

`property-variable-confusion`{.interpreted-text role="ref"}, in
functions/classes/class.Admin.php:16.

There is a property called \'\$users\'. It is easy to mistake
\$this-\>users and \$users. Also, it seems that \$this-\>users may be
used as a cache system, yet it is not employed here.

``` {.php}
/**
     * (array of objects) to store users, user id is array index
     *
     * @var mixed
     * @access public
     */
    public $users;

////////////

    /**
     * Fetches all users that are in group
     *
     * @access public
     * @return array of user ids
     */
    public function group_fetch_users ($group_id) {
        $out = array ();
        # get all users
        $users = $this->fetch_all_objects(users);
        # check if $gid in array
        if($users!==false) {
            foreach($users as $u) {
                $group_array = json_decode($u->groups, true);
                $group_array = $this->groups_parse($group_array);

                if(sizeof($group_array)>0) {
                    foreach($group_array as $group) {
                        if(in_array($group_id, $group)) {
                            $out[] = $u->id;
                        }
                    }
                }
            }
        }
        # return
        return isset($out) ? $out : array();
    }
```

### Use session\_start() Options

#### WordPress {#wordpress-php-usesessionstartoptions}

`use-session\_start()-options`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### Isset Multiple Arguments

#### ThinkPHP {#thinkphp-php-issetmultipleargs}

`isset-multiple-arguments`{.interpreted-text role="ref"}, in
library/think/Request.php:1187.

This may be shortened with isset(\$sub), \$array\[\$name\]\[\$sub\])

``` {.php}
isset($sub) && isset($array[$name][$sub])
```

------------------------------------------------------------------------

#### LiveZilla {#livezilla-php-issetmultipleargs}

`isset-multiple-arguments`{.interpreted-text role="ref"}, in
livezilla/\_lib/trdp/pchart/class/pDraw.class.php:3852.

This is the equivalent of
!(isset(\$Data\[\"Series\"\]\[\$SerieA\]\[\"Data\"\]) &&
isset(\$Data\[\"Series\"\]\[\$SerieB\]\[\"Data\"\])), and then,
!(isset(\$Data\[\"Series\"\]\[\$SerieA\]\[\"Data\"\],
\$Data\[\"Series\"\]\[\$SerieB\]\[\"Data\"\]))

``` {.php}
!isset($Data["Series"][$SerieA]["Data"]) || !isset($Data["Series"][$SerieB]["Data"])
```

### Unitialized Properties

#### SPIP {#spip-classes-unitializedproperties}

`unitialized-properties`{.interpreted-text role="ref"}, in
ecrire/public/interfaces.php:584.

The class Critere (Criteria) has no method at all. When using a class as
an array, to capture values, one of the advantage of the class is in the
default values for the properties. In particular, the last property
here, called \$not, should be initialized with a false.

``` {.php}
/**
 * Description d'un critère de boucle
 *
 * Sous-noeud de Boucle
 *
 * @package SPIP\Core\Compilateur\AST
 **/
class Critere {
    /**
     * Type de noeud
     *
     * @var string
     */
    public $type = 'critere';

    /**
     * Opérateur (>, <, >=, IN, ...)
     *
     * @var null|string
     */
    public $op;

    /**
     * Présence d'une négation (truc !op valeur)
     *
     * @var null|string
     */
    public $not;
```

### Use List With Foreach

#### MediaWiki {#mediawiki-structures-uselistwithforeach}

`use-list-with-foreach`{.interpreted-text role="ref"}, in
includes/parser/LinkHolderArray.php:372.

This foreach reads each element from \$entries into entry. \$entry, in
turn, is written into \$pdbk, \$title and \$displayText for easier
reuse. 5 elements are read from \$entry, and they could be set in their
respective variable in the foreach() with a list call. The only on that
can\'t be set is \'query\' which has to be tested.

``` {.php}
foreach ( $entries as $index => $entry ) {
                $pdbk = $entry['pdbk'];
                $title = $entry['title'];
                $query = isset( $entry['query'] ) ? $entry['query'] : [];
                $key = "$ns:$index";
                $searchkey = "<!--LINK'\" $key-->";
                $displayText = $entry['text'];
                if ( isset( $entry['selflink'] ) ) {
                    $replacePairs[$searchkey] = Linker::makeSelfLinkObj( $title, $displayText, $query );
                    continue;
                }
                if ( $displayText === '' ) {
                    $displayText = null;
                } else {
                    $displayText = new HtmlArmor( $displayText );
                }
                if ( !isset( $colours[$pdbk] ) ) {
                    $colours[$pdbk] = 'new';
                }
                $attribs = [];
                if ( $colours[$pdbk] == 'new' ) {
                    $linkCache->addBadLinkObj( $title );
                    $output->addLink( $title, 0 );
                    $link = $linkRenderer->makeBrokenLink(
                        $title, $displayText, $attribs, $query
                    );
                } else {
                    $link = $linkRenderer->makePreloadedLink(
                        $title, $displayText, $colours[$pdbk], $attribs, $query
                    );
                }

                $replacePairs[$searchkey] = $link;
            }
```

### Empty With Expression

#### HuMo-Gen {#humo-gen-structures-emptywithexpression}

`empty-with-expression`{.interpreted-text role="ref"}, in
fanchart.php:297.

The test on \$pid may be directly done on \$treeid\[\$sosa\]\[0\]. The
distance between the assignation and the empty() makes it hard to spot.

``` {.php}
$pid=$treeid[$sosa][0];
            $birthyr=$treeid[$sosa][1];
            $deathyr=$treeid[$sosa][4];
            $fontpx=$fontsize;
            if($sosa>=16 AND $fandeg==180) { $fontpx=$fontsize-1; }
            if($sosa>=32 AND $fandeg!=180) { $fontpx=$fontsize-1; }
            if (!empty($pid)) {
```

### Should Use array\_filter()

#### xataface {#xataface-php-shouldusearrayfilter}

`should-use-array\_filter()`{.interpreted-text role="ref"}, in
actions/manage\_build\_index.php:38.

This selection process has three tests : the two first are exclusive,
and the third is inclusive. They could fit in one or several closures.

``` {.php}
$indexable = array();
        foreach ( $tables as $key=>$table ){
            if ( preg_match('/^dataface__/', $table) ){
                continue;
            }
            if ( preg_match('/^_/', $table) ){
                continue;
            }

            if ( $index->isTableIndexable($table) ){
                $indexable[] = $table;
                //unset($tables[$key]);
            }

        }
```

------------------------------------------------------------------------

#### shopware {#shopware-php-shouldusearrayfilter}

`should-use-array\_filter()`{.interpreted-text role="ref"}, in
engine/Shopware/Bundle/StoreFrontBundle/Service/Core/VariantCoverService.php:71.

Closure would be the best here, since \$covers has to be injected in the
array\_filter callback.

``` {.php}
$covers = $this->variantMediaGateway->getCovers(
            $products,
            $context
        );

        $fallback = [];
        foreach ($products as $product) {
            if (!array_key_exists($product->getNumber(), $covers)) {
                $fallback[] = $product;
            }
        }
```

### \*\* For Exponent

#### Traq {#traq-php-newexponent}

`**-for-exponent`{.interpreted-text role="ref"}, in
src/views/layouts/\_footer.phtm:5.

pow(1024, 2) could be (1023 \*\* 2), to convert bytes into Mb.

``` {.php}
<?=round((microtime(true) - START_TIME), 2); ?>s, <?php echo round((memory_get_peak_usage() - START_MEM) / pow(1024, 2), 3)?>mb
```

------------------------------------------------------------------------

#### TeamPass {#teampass-php-newexponent}

`**-for-exponent`{.interpreted-text role="ref"}, in
includes/libraries/Authentication/phpseclib/Math/BigInteger.php:286.

pow(2, 62) could also be hard coded with 0x4000000000000000.

``` {.php}
pow(2, 62)
```

### Should Use Math

#### OpenEMR {#openemr-structures-shouldusemath}

`should-use-math`{.interpreted-text role="ref"}, in
controllers/C\_Prescription.class.php:638.

\$pdf-\>ez\[\'leftMargin\'\] is now 0.

``` {.php}
function multiprint_body(& $pdf, $p)
    {
        $pdf->ez['leftMargin'] += $pdf->ez['leftMargin'];
        $pdf->ez['rightMargin'] += $pdf->ez['rightMargin'];
        $d = $this->get_prescription_body_text($p);
        if ($pdf->ezText($d, 10, array(), 1)) {
            $pdf->ez['leftMargin'] -= $pdf->ez['leftMargin'];
            $pdf->ez['rightMargin'] -= $pdf->ez['rightMargin'];
            $this->multiprint_footer($pdf);
            $pdf->ezNewPage();
            $this->multiprint_header($pdf, $p);
```

### Could Use Compact

#### WordPress {#wordpress-structures-couldusecompact}

`could-use-compact`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

### Could Use array\_fill\_keys

#### ChurchCRM {#churchcrm-structures-couldusearrayfillkeys}

`could-use-array\_fill\_keys`{.interpreted-text role="ref"}, in
src/ManageEnvelopes.php:107.

There are two initialisations at the same time here : that should make
two call to array\_fill\_keys().

``` {.php}
foreach ($familyArray as $fam_ID => $fam_Data) {
        $envelopesByFamID[$fam_ID] = 0;
        $envelopesToWrite[$fam_ID] = 0;
    }
```

------------------------------------------------------------------------

#### PhpIPAM {#phpipam-structures-couldusearrayfillkeys}

`could-use-array\_fill\_keys`{.interpreted-text role="ref"}, in
functions/scripts/merge\_databases.php:418.

Even when the initialization is mixed with other operations, it is a
good idea to extract it from the loop and give it to
array\_fill\_keys().

``` {.php}
$arr_new = array();
                foreach ($arr as $type=>$objects) {
                    $arr_new[$type] = array();
                    if(sizeof($objects)>0) {
                        foreach($objects as $ok=>$object) {
                            $arr_new[$type][] = $highest_ids_append[$type] + $object;
                        }
                    }
                }
```

### preg\_match\_all() Flag

#### FuelCMS {#fuelcms-php-pregmatchallflag}

`preg\_match\_all()-flag`{.interpreted-text role="ref"}, in
fuel/modules/fuel/helpers/MY\_array\_helper.php:205.

Using PREG\_SET\_ORDER will remove the usage of the `$key`variable.

``` {.php}
function parse_string_to_array($str)
    {
        preg_match_all('#(\w+)=([\'"])(.*)\2#U', $str, $matches);
        $params = array();
        foreach($matches[1] as $key => $val)
        {
            if (!empty($matches[3]))
            {
                $params[$val] = $matches[3][$key];
            }
        }
        return $params;
    }
```

### Use Count Recursive

#### WordPress {#wordpress-structures-usecountrecursive}

`use-count-recursive`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

This code actually loads the file, join it, then split it again. file()
would be sufficient.

``` {.php}
$markerdata = explode( "\n", implode( '', file( $filename ) ) );
```

------------------------------------------------------------------------

#### PrestaShop {#prestashop-structures-usecountrecursive}

`use-count-recursive`{.interpreted-text role="ref"}, in
controllers/admin/AdminSearchController.php:342.

This could be improved with count() recursive and a array\_filter call,
to remove empty \$list.

``` {.php}
$nb_results = 0;
            foreach ($this->_list as $list) {
                if ($list != false) {
                    $nb_results += count($list);
                }
            }
```

### Should Use Foreach

#### ExpressionEngine {#expressionengine-structures-shoulduseforeach}

`should-use-foreach`{.interpreted-text role="ref"}, in
system/ee/EllisLab/ExpressionEngine/Service/Model/Query/Builder.php:241.

This code could turn the string into an array, with the explode()
function, and use foreach(), instead of calculating the length()
initially, and then building the loop.

``` {.php}
$length = strlen($str);
        $words = array();

        $word = '';
        $quote = '';
        $quoted = FALSE;

        for ($i = 0; $i < $length; $i++)
        {
            $char = $str[$i];

            if (($quoted == FALSE && $char == ' ') || ($quoted == TRUE && $char == $quote))
            {
                if (strlen($word) > 2)
                {
                    $words[] = $word;
                }

                $quoted = FALSE;
                $quote = '';
                $word = '';

                continue;
            }

            if ($quoted == FALSE && ($char == ' || $char == ") && ($word === '' || $word == '-'))
            {
                $quoted = TRUE;
                $quote = $char;
                continue;
            }

            $word .= $char;
        }
```

------------------------------------------------------------------------

#### Woocommerce {#woocommerce-structures-shoulduseforeach}

`should-use-foreach`{.interpreted-text role="ref"}, in
includes/libraries/class-wc-eval-math.php:84.

This loops reviews the \'stack\' and updates its elements. The same loop
may leverage foreach and references for more efficient code.

``` {.php}
$stack_size = count( $stack );
                for ( $i = 0; $i < $stack_size; $i++ ) { // freeze the state of the non-argument variables
                    $token = $stack[ $i ];
                    if ( preg_match( '/^[a-z]\w*$/', $token ) and ! in_array( $token, $args ) ) {
                        if ( array_key_exists( $token, self::$v ) ) {
                            $stack[ $i ] = self::$v[ $token ];
                        } else {
                            return self::trigger( "undefined variable '$token' in function definition" );
                        }
                    }
                }
```

### Too Many Parameters

#### WordPress {#wordpress-functions-toomanyparameters}

`too-many-parameters`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

11 parameters is a lot for a function. Note that it is more than the
default configuration, and reported there. This may be configured.

``` {.php}
/**
 * [identifyUserRights description]
 * @param  string $groupesVisiblesUser  [description]
 * @param  string $groupesInterditsUser [description]
 * @param  string $isAdmin              [description]
 * @param  string $idFonctions          [description]
 * @return string                       [description]
 */
function identifyUserRights(
    $groupesVisiblesUser,
    $groupesInterditsUser,
    $isAdmin,
    $idFonctions,
    $server,
    $user,
    $pass,
    $database,
    $port,
    $encoding,
    $SETTINGS
) {
```

------------------------------------------------------------------------

#### ChurchCRM {#churchcrm-functions-toomanyparameters}

`too-many-parameters`{.interpreted-text role="ref"}, in
src/Reports/ReminderReport.php:192.

10 parameters is a lot for a function. Here, we may also identify a
family (ID, Name), and a full address (Address1, Address2, State, Zip,
Country), which may be turned into an object.

``` {.php}
public function StartNewPage($fam_ID, $fam_Name, $fam_Address1, $fam_Address2, $fam_City, $fam_State, $fam_Zip, $fam_Country, $fundOnlyString, $iFYID) 
{
```

### Should Preprocess Chr()

#### phpadsnew {#phpadsnew-php-shouldpreprocess}

`should-preprocess-chr()`{.interpreted-text role="ref"}, in
phpAdsNew-2.0/adview.php:302.

Each call to chr() may be done before. First, chr() may be replace with
the hexadecimal sequence \"0x3B\"; Secondly, 0x3b is a rather long
replacement for a simple semi-colon. The whole pragraph could be stored
in a separate file, for easier modifications.

``` {.php}
echo chr(0x47).chr(0x49).chr(0x46).chr(0x38).chr(0x39).chr(0x61).chr(0x01).chr(0x00).
             chr(0x01).chr(0x00).chr(0x80).chr(0x00).chr(0x00).chr(0x04).chr(0x02).chr(0x04).
             chr(0x00).chr(0x00).chr(0x00).chr(0x21).chr(0xF9).chr(0x04).chr(0x01).chr(0x00).
             chr(0x00).chr(0x00).chr(0x00).chr(0x2C).chr(0x00).chr(0x00).chr(0x00).chr(0x00).
             chr(0x01).chr(0x00).chr(0x01).chr(0x00).chr(0x00).chr(0x02).chr(0x02).chr(0x44).
             chr(0x01).chr(0x00).chr(0x3B);
```

### Drop Substr Last Arg

#### SuiteCrm {#suitecrm-structures-substrlastarg}

`drop-substr-last-arg`{.interpreted-text role="ref"}, in
modules/UpgradeWizard/uw\_utils.php:2422.

substr() is even trying to go beyond the end of the string.

``` {.php}
substr($relativeFile, 1, strlen($relativeFile))
```

------------------------------------------------------------------------

#### Tine20 {#tine20-structures-substrlastarg}

`drop-substr-last-arg`{.interpreted-text role="ref"}, in
tine20/Calendar/Frontend/Cli.php:95.

Omitting the last character would yield the same result.

``` {.php}
substr($opt, 18, strlen($opt))
```

### Possible Increment

#### Zurmo {#zurmo-structures-possibleincrement}

`possible-increment`{.interpreted-text role="ref"}, in
app/protected/modules/workflows/utils/SavedWorkflowsUtil.php:196.

There are suspicious extra spaces around the +, that give the hint that
there used to be something else, like a constant, there. From the name
of the methods, it seems that this code was refactored from an addition
to a simple method call.

``` {.php}
$timeStamp =  + $workflow->getTimeTrigger()->resolveNewTimeStampForDuration(time());
```

------------------------------------------------------------------------

#### MediaWiki {#mediawiki-structures-possibleincrement}

`possible-increment`{.interpreted-text role="ref"}, in
includes/filerepo/file/LocalFile.php:613.

That is a useless assignation, except for the transtyping to integer
that PHP does silently. May be that should be a +=, or completely
dropped.

``` {.php}
$decoded[$field] = +$decoded[$field]
```

### One If Is Sufficient

#### Tikiwiki {#tikiwiki-structures-oneifissufficient}

`one-if-is-sufficient`{.interpreted-text role="ref"}, in
lib/wiki-plugins/wikiplugin\_trade.php:152.

empty(\$params\[\'inputtitle\'\]) should have priority over
\$params\[\'wanted\'\] == \'n\'.

``` {.php}
if ($params['wanted'] == 'n') {
        if (empty($params['inputtitle'])) {
            $params['inputtitle'] = 'Payment of %0 %1 from user %2 to %3';
        }
    } else {
        if (empty($params['inputtitle'])) {
            $params['inputtitle'] = 'Request payment of %0 %1 to user %2 from %3';
        }
    }
```

### Could Use array\_unique

#### Dolibarr {#dolibarr-structures-couldusearrayunique}

`could-use-array\_unique`{.interpreted-text role="ref"}, in
htdocs/includes/restler/framework/Luracast/Restler/Format/XmlFormat.php:250.

This loop has two distinct operations : the first collect keys and keep
them unique. A combinaison of array\_keys() and array\_unique() would do
that job, while saving the in\_array() lookup, and the configuration
check with \'static::\$importSettingsFromXml\'. The second operation is
distinct, and could be done with array\_map().

``` {.php}
$attributes = $xml->attributes();
            foreach ($attributes as $key => $value) {
                if (static::$importSettingsFromXml
                    && !in_array($key, static::$attributeNames)
                ) {
                    static::$attributeNames[] = $key;
                }
                $r[$key] = static::setType((string)$value);
            }
```

------------------------------------------------------------------------

#### OpenEMR {#openemr-structures-couldusearrayunique}

`could-use-array\_unique`{.interpreted-text role="ref"}, in
gacl/gacl\_api.class.php:441:441.

This loop is quite complex : it collects \$aro\_value in
\$acl\_array\[\'aro\'\]\[\$aro\_section\_value\], but also creates the
array in \$acl\_array\[\'aro\'\]\[\$aro\_section\_value\], and report
errors in the debug log. array\_unique() could replace the collection,
while the debug would have to be done somewhere else.

``` {.php}
foreach ($aro_value_array as $aro_value) {
                    if ( count($acl_array['aro'][$aro_section_value]) != 0 ) {
                        if (!in_array($aro_value, $acl_array['aro'][$aro_section_value])) {
                            $this->debug_text("append_acl(): ARO Section Value: $aro_section_value ARO VALUE: $aro_value");
                            $acl_array['aro'][$aro_section_value][] = $aro_value;
                            $update=1;
                        } else {
                            $this->debug_text("append_acl(): Duplicate ARO, ignoring... ");
                        }
                    } else { //Array is empty so add this aro value.
                        $acl_array['aro'][$aro_section_value][] = $aro_value;
                        $update = 1;
                    }
                }
```

### Too Many Children

#### Typo3 {#typo3-classes-toomanychildren}

`too-many-children`{.interpreted-text role="ref"}, in
typo3/sysext/backend/Classes/Form/AbstractNode.php:26.

More than 15 children for this class : 15 is the default configuration.

``` {.php}
abstract class AbstractNode implements NodeInterface, LoggerAwareInterface {
```

------------------------------------------------------------------------

#### Woocommerce {#woocommerce-classes-toomanychildren}

`too-many-children`{.interpreted-text role="ref"}, in
includes/abstracts/abstract-wc-rest-controller.php:30.

This class is extended 22 times, more than the default configuration of
15.

``` {.php}
class WC_REST_Controller extends WP_REST_Controller {
```

### Should Use Operator

#### Zencart {#zencart-structures-shoulduseoperator}

`should-use-operator`{.interpreted-text role="ref"}, in
includes/modules/payment/paypal/paypal\_curl.php:378.

Here, \$options is merged with \$values if it is an array. If it is not
an array, it is probably a null value, and may be ignored. Adding a
\'array\' typehint will strengthen the code an catch situations where
TransactionSearch() is called with a string, leading to clearer code.

``` {.php}
function TransactionSearch($startdate, $txnID = '', $email = '', $options) {
    // several lines of code, no mention of $options
      if (is_array($options)) $values = array_merge($values, $options);
    }
    return $this->_request($values, 'TransactionSearch');
  }
```

------------------------------------------------------------------------

#### SugarCrm {#sugarcrm-structures-shoulduseoperator}

`should-use-operator`{.interpreted-text role="ref"}, in
include/utils.php:2093:464.

\$override should an an array : if not, it is actually set by default to
empty array. Here, a typehint with a default value of \'array()\' would
offset the parameter validation to the calling method.

``` {.php}
function sugar_config_union( $default, $override ){
    // a little different then array_merge and array_merge_recursive.  we want
    // the second array to override the first array if the same value exists,
    // otherwise merge the unique keys.  it handles arrays of arrays recursively
    // might be suitable for a generic array_union
    if( !is_array( $override ) ){
        $override = array();
    }
    foreach( $default as $key => $value ){
        if( !array_key_exists($key, $override) ){
            $override[$key] = $value;
        }
        else if( is_array( $key ) ){
            $override[$key] = sugar_config_union( $value, $override[$key] );
        }
    }
    return( $override );
}
```

### Could Be Static Closure

#### Piwigo {#piwigo-functions-couldbestaticclosure}

`could-be-static-closure`{.interpreted-text role="ref"}, in
include/ws\_core.inc.php:620.

The closure function(\$m) makes no usage of the current object : using
static prevents \$this to be forwarded with the closure.

``` {.php}
/**
   * WS reflection method implementation: lists all available methods
   */
  static function ws_getMethodList($params, &$service)
  {
    $methods = array_filter($service->_methods,
      function($m) { return empty($m["options"]["hidden"]) || !$m["options"]["hidden"];} );
    return array('methods' => new PwgNamedArray( array_keys($methods),'method' ) );
  }
```

### Add Default Value

#### Zurmo {#zurmo-functions-adddefaultvalue}

`add-default-value`{.interpreted-text role="ref"}, in
wp-admin/includes/misc.php:74.

Default values may be a literal (1, \'abc\', \...), or a constant :
global or class. Here,
MissionsListConfigurationForm::LIST\_TYPE\_AVAILABLE may be used
directly in the signature of the method

``` {.php}
public function getMetadataFilteredByOption($option)
        {
            if ($option == null)
            {
                $option = MissionsListConfigurationForm::LIST_TYPE_AVAILABLE;
            }
```

------------------------------------------------------------------------

#### Typo3 {#typo3-functions-adddefaultvalue}

`add-default-value`{.interpreted-text role="ref"}, in
typo3/sysext/indexed\_search/Classes/FileContentParser.php:821.

\$extension could get a default value to handle default situations : for
example, a file is htm format by default, unless better known. Also, the
if/then structure could get a \'else\' clause, to handle unknown
situations : those are situations where the extension is provided but
not known, in particular when the icon is missing in the storage folder.

``` {.php}
public function getIcon($extension)
    {
        if ($extension === 'htm') {
            $extension = 'html';
        } elseif ($extension === 'jpeg') {
            $extension = 'jpg';
        }
        return 'EXT:indexed_search/Resources/Public/Icons/FileTypes/' . $extension . '.gif';
    }
```

### Named Regex

#### Phinx {#phinx-structures-namedregex}

`named-regex`{.interpreted-text role="ref"}, in
src/Phinx/Util/Util.php:127.

\$matches\[1\] could be renamed by \$matches\[\'filename\'\], if the
capturing subpattern was named \'filename\'.

``` {.php}
const MIGRATION_FILE_NAME_PATTERN = '/^\d+_([\w_]+).php$/i';
//.... More code with class definition
    public static function mapFileNameToClassName($fileName)
    {
        $matches = [];
        if (preg_match(static::MIGRATION_FILE_NAME_PATTERN, $fileName, $matches)) {
            $fileName = $matches[1];
        }

        return str_replace(' ', '', ucwords(str_replace('_', ' ', $fileName)));
    }
```

------------------------------------------------------------------------

#### shopware {#shopware-structures-namedregex}

`named-regex`{.interpreted-text role="ref"}, in
engine/Library/Enlight/Components/Snippet/Resource.php:207.

\$\_match\[3\] is actually extracted two preg\_match() before : by the
time we read its usage, the first regex has been forgotten. A named
subpattern would be useful here to remember what was captured.

``` {.php}
if (!preg_match("!(.?)(name=)(.*?)(?=(\s|$))!", $_block_args, $_match) && empty($_block_default)) {
                throw new SmartyException('"' . $_block_tag . '" missing name attribute');
            }
            $_block_force = (bool) preg_match('#[\s]force#', $_block_args);
            $_block_json = (bool) preg_match('#[\s]json=["\']true["\']\W#', $_block_args);
            $_block_name = !empty($_match[3]) ? trim($_match[3], '\'"') : $_block_default;
```

### Could Use Try

#### Mautic {#mautic-exceptions-couldusetry}

`could-use-try`{.interpreted-text role="ref"}, in
app/bundles/StageBundle/Controller/StageController.php:78.

\$limit is read as a session variable or a default value. There are no
check here that \$limit is not null, before using it in a division. It
is easy to imagine this is done elsewhere, yet a try/catch could help
intercept unwanted situations.

``` {.php}
//set limits
        $limit = $this->get('session')->get(
            'mautic.stage.limit',
            $this->coreParametersHelper->getParameter('default_pagelimit')
        );
/... Code where $limit is read but not modified /
        $count = count($stages);
        if ($count && $count < ($start + 1)) {
            $lastPage = ($count === 1) ? 1 : (ceil($count / $limit)) ?: 1;
```

### Use Basename Suffix

#### NextCloud {#nextcloud-structures-basenamesuffix}

`use-basename-suffix`{.interpreted-text role="ref"}, in
lib/private/URLGenerator.php:176.

This code removes the 4 last letters from the images. It may be \'png\',
\'jpg\' or \'txt\'.

``` {.php}
substr(basename($image), 0, -4)
```

------------------------------------------------------------------------

#### Dolibarr {#dolibarr-structures-basenamesuffix}

`use-basename-suffix`{.interpreted-text role="ref"}, in
htdocs/core/website.inc.php:42.

The extension \'.tpl.php\' is dropped from the file name, unless it
appears somewhere else in the \$websitepagefile variable.

``` {.php}
str_replace(array('.tpl.php', 'page'), array('', ''), basename($websitepagefile))
```

### Don\'t Loop On Yield

#### Dolibarr {#dolibarr-structures-dontlooponyield}

`don't-loop-on-yield`{.interpreted-text role="ref"}, in
htdocs/includes/sabre/sabre/dav/lib/DAV/Server.php:912.

Yield from is a straight replacement here.

``` {.php}
if (($newDepth === self::DEPTH_INFINITY || $newDepth >= 1) && $childNode instanceof ICollection) {
    foreach ($this->generatePathNodes($subPropFind) as $subItem) {
        yield $subItem;
    }
}
```

------------------------------------------------------------------------

#### Tikiwiki {#tikiwiki-structures-dontlooponyield}

`don't-loop-on-yield`{.interpreted-text role="ref"}, in
lib/goal/goallib.php:944.

The replacement with `yield from`is not straigthforward here. Yield is
only called when \$user hasn\'t been `$done` : this is a unicity check.
So, the double loop may produce a fully merged array, that may be
reduced further by array\_unique(). The final array, then, can be used
with yield from.

``` {.php}
$done = [];

foreach ($goal['eligible'] as $groupName) {
    foreach ($userlib->get_group_users($groupName) as $user) {
        if (! isset($done[$user])) {
            yield ['user' => $user, 'group' => null];
            $done[$user] = true;
        }
    }
}
```

### Multiple Usage Of Same Trait

#### NextCloud {#nextcloud-traits-multipleusage}

`multiple-usage-of-same-trait`{.interpreted-text role="ref"}, in
build/integration/features/bootstrap/WebDav.php:41.

WebDav uses Sharing, and Sharing uses Webdav. Once using the other is
sufficient.

``` {.php}
trait WebDav { 
    use Sharing;

}
//Trait Sharing is in /build/integration/features/bootstrap/Sharing.php:36
```

### Function Subscripting, Old Style

#### OpenConf {#openconf-structures-functionpresubscripting}

`function-subscripting,-old-style`{.interpreted-text role="ref"}, in
openconf/include.php:1469.

Here, \$advocateid may be directly read from ocsql\_fetch\_assoc(),
although, checking for the existence of \'advocateid\' before accessing
it would make the code more robust

``` {.php}
$advocateid = false;
    if (isset($GLOBALS['OC_configAR']['OC_paperAdvocates']) && $GLOBALS['OC_configAR']['OC_paperAdvocates']) {
        $ar = ocsql_query(SELECT `advocateid` FROM ` . OCC_TABLE_PAPERADVOCATE . ` WHERE `paperid`=' . safeSQLstr($pid) . ') or err('Unable to retrieve advocate');
        if (ocsql_num_rows($ar) == 1) {
            $al = ocsql_fetch_assoc($ar);
            $advocateid = $al['advocateid'];
        }
    }
```

### No Class As Typehint

#### Vanilla {#vanilla-functions-noclassastypehint}

`no-class-as-typehint`{.interpreted-text role="ref"}, in
library/Vanilla/Formatting/Formats/RichFormat.php:51.

All three typehints are based on classes. When Parser or Renderer are
changed, for testing, versioning or moduling reasons, they must subclass
the original class.

``` {.php}
public function __construct(Quill\Parser $parser, Quill\Renderer $renderer, Quill\Filterer $filterer) {
        $this->parser = $parser;
        $this->renderer = $renderer;
        $this->filterer = $filterer;
    }
```

------------------------------------------------------------------------

#### phpMyAdmin {#phpmyadmin-functions-noclassastypehint}

`no-class-as-typehint`{.interpreted-text role="ref"}, in
libraries/classes/CreateAddField.php:29.

Although the class is named \'DatabaseInterface\', it is a class.

``` {.php}
public function __construct(DatabaseInterface $dbi)
    {
        $this->dbi = $dbi;
    }
```

### Argument Should Be Typehinted

#### Dolphin {#dolphin-functions-shouldbetypehinted}

`argument-should-be-typehinted`{.interpreted-text role="ref"}, in
Dolphin-v.7.3.5/plugins/intervention-image/Intervention/Image/Gd/Commands/WidenCommand.php:20.

This closures make immediate use of the \$constraint argument, and calls
its method aspectRatio. No check is made on this argument, and it may
easily be mistaken with another class, or a null. Adding a typehint here
will ensure a more verbose development error and help detect misuse of
the closure.

``` {.php}
$this->arguments[2] = function ($constraint) use ($additionalConstraints) {
            $constraint->aspectRatio();
            if(is_callable($additionalConstraints)) 
                $additionalConstraints($constraint);
        };
```

------------------------------------------------------------------------

#### Mautic {#mautic-functions-shouldbetypehinted}

`argument-should-be-typehinted`{.interpreted-text role="ref"}, in
app/bundles/PluginBundle/Helper/IntegrationHelper.php:374.

This piece of code inside a 275 lines method. Besides, there are 11
classes that offer a \'getPriority\' method, although \$returnServices
could help to semantically reduce the number of possible classes. Here,
typehints on \$a and \$b help using the wrong kind of object.

``` {.php}
if (empty($alphabetical)) {
            // Sort by priority
            uasort($returnServices, function ($a, $b) {
                $aP = (int) $a->getPriority();
                $bP = (int) $b->getPriority();

                if ($aP === $bP) {
                    return 0;
                }

                return ($aP < $bP) ? -1 : 1;
            });
```
