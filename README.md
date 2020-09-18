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
