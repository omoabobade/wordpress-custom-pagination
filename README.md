# wordpress-custom-pagination

Core of the code : 
<pre><code>
  $customPagHTML     = "";
  $query             = "SELECT * FROM custom_table";
  $total_query     = "SELECT COUNT(1) FROM (${query}) AS combined_table";
  $total             = $wpdb->get_var( $total_query );
  $items_per_page = 4;
  $page             = isset( $_GET['cpage'] ) ? abs( (int) $_GET['cpage'] ) : 1;
  $offset         = ( $page * $items_per_page ) - $items_per_page;
  $result         = $wpdb->get_results( $query . " ORDER BY field DESC LIMIT ${offset}, ${items_per_page}" );
  $totalPage         = ceil($total / $items_per_page);
</code></pre>
For Page display :
<pre><code>
  if($totalPage > 1){
    $customPagHTML     =  '<div><span>Page '.$page.' of '.$totalPage.'</span>'.paginate_links( array(
    'base' => add_query_arg( 'cpage', '%#%' ),
    'format' => '',
    'prev_text' => __('&laquo;'),
    'next_text' => __('&raquo;'),
    'total' => $totalPage,
    'current' => $page
    )).'</div>';
  }
  </code>
</pre>
To display the pagination on the page:
<pre><code>
  echo $customPagHTML;  
  </code>
  </pre>
