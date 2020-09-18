# Upgrade-wordpress-to-php-7.3
Possible warning and errors to be solved when migrating from lower version of php to 7.3

# issue 1
Deprecated: Function create_function() is deprecated in functions/theme-functions.php on line 604

	Old Line
	add_filter( 'loop_shop_columns', create_function( false, 'return 3;' ) );

	New Line
	add_filter( 'loop_shop_columns', function(false) {return 3;});

	Old Line
	add_filter( 'loop_shop_per_page', create_function( '$cols', 'return 12;' ), 20 );

	New Line
	add_filter( 'loop_shop_per_page', function($cols) {return 12;}, 20);

# solution link : https://stackoverflow.com/questions/50181382/deprecated-function-create-function-is-deprecated-php-7-2
