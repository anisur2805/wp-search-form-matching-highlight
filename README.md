# wp-search-form-matching-highlight

``` 
<form role="search" id="tfsb_form" action="" method="post">
	<label>
		<span class="screen-reader-text"><?php echo _x( 'Search for:', 'label' ) ?></span>
		<input type="search" class="title search-field"
			placeholder="<?php echo esc_attr_x( 'Search post here...', 'placeholder' ) ?>"
			value="<?php echo get_search_query() ?>" name="s"
			title="<?php echo esc_attr_x( 'Search for:', 'label' ) ?>" />
	</label>
	<input type="submit" name="submit" class="search-submit"
		value="<?php echo esc_attr_x( 'Search', 'submit button' ) ?>" />
    
    /* if you want to search specific post type only - just pass the post type as value or default is 'post'
       <input type="hidden" name="post_type" value="tf-service-bookings" /> */ 
        
</form>

*OR you can simply use 'get_search_form();'*

/**
 * Highlight search keyword\s
 */

add_filter( 'the_title', 'tfsb_highlight_search_keyword', 10, 1 );
add_filter( 'the_excerpt', 'tfsb_highlight_search_keyword', 10, 1 );
add_filter( 'the_content', 'tfsb_highlight_search_keyword', 10, 1 );
 
function tfsb_highlight_search_keyword( $text ) {

    if( $is_search ) {
        $pattern = '/('. join('|', explode(' ', get_search_query())).')/i';
        $text = preg_replace( $pattern, '<span class="tfsb_highligh_keyword">\0</span>', $text);
    }
    
    return $text;
} 

```
