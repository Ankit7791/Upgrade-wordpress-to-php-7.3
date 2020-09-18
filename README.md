# Upgrade-wordpress-to-php-7.3
Possible warning and errors to be solved when migrating from lower version of php to 7.3

First things first, if you are able to login into wp-admin try updating wordpress and plugins to newer version which will reduce the error solving..

# issue 1
	Deprecated: Function create_function() is deprecated in functions/theme-functions.php on line 604

	Old Line
	add_filter( 'loop_shop_columns', create_function( false, 'return 3;' ) );

	New Line
	add_filter( 'loop_shop_columns', function() {return 3;});

	Old Line
	add_filter( 'loop_shop_per_page', create_function( '$cols', 'return 12;' ), 20 );

	New Line
	add_filter( 'loop_shop_per_page', function($cols) {return 12;}, 20);

	# solution link : https://stackoverflow.com/questions/50181382/deprecated-function-create-function-is-deprecated-php-7-2

# issue 2
	Deprecated: The called constructor method for WP_Widget in Mfn_Company_Widget is deprecated since version 4.3.0! Use 
	
	Find Mfn_Company_Widget class file in your themes folder (This is reference same can be done for all errors of this kind)
	
	Old Line 
	Previously we used to have the same name of the constructor as the class name 
	
	So, function classname(){
	   //this will be the constructor
	}
	
	But in newer php version it is recommended to __construct(),
	
	So, function __construct(){
	   //this will the be the new constructor function now	
	}
	
	If still the above issue persists than, goto wp-includes > functions.php
		 * @param bool $trigger Whether to trigger the error for deprecated functions. Default true.
	 */
	if ( WP_DEBUG && apply_filters( 'deprecated_constructor_trigger_error', true ) ) 
	
	change the if condition to 
	
	if ( WP_DEBUG && apply_filters( 'deprecated_constructor_trigger_error', false ) ) 
	
# issue 3
	Fatal error: Uncaught Error: [] operator not supported for strings
	
	You can fix this PHP error by first initializing $data[] as an array:

	$data = [];
	$data[] = '<script type="text/javascript">' . NL;

	A second method is to use the older style using array():

	$data = array();
	$data[] = '<script type="text/javascript">' . NL;
	
	Old Code
	
	$section_style 		= '';
	$section_style[] 	= 'padding-top:'. intval( $section['attr']['padding_top'] ) .'px';
	$section_style[] 	= 'padding-bottom:'. intval( $section['attr']['padding_bottom'] ) .'px';
	$section_style[] 	= 'background-color:'. $section['attr']['bg_color'];
	
	New Code
	
	$section_style 		= []; or array();
	$section_style[] 	= 'padding-top:'. intval( $section['attr']['padding_top'] ) .'px';
	$section_style[] 	= 'padding-bottom:'. intval( $section['attr']['padding_bottom'] ) .'px';
	$section_style[] 	= 'background-color:'. $section['attr']['bg_color'];
	
	Solution link : https://www.saotn.org/fatal-error-operator-not-supported-strings-php-71/
