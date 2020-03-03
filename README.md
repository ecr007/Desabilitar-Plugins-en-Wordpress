# Desabilitar-Plugins-en-Wordpress

```php
/**
 * 
 * Desactive plugin in x pages DESABILITADO
 * 
 */
function desactive_plugin($plugins){
	
	if(session_id() == 'cabba9d1f399869080751a2824c151b4'){

		$request_uri = parse_url( $_SERVER['REQUEST_URI'], PHP_URL_PATH );

		$is_admin = strpos( $request_uri, '/wp-admin/' );

		if( false === $is_admin ){

			$disableInHome = [
				'classic-editor/classic-editor.php',
				'disqus-comment-system/disqus.php',
			];

			if ($request_uri == "/") {

				foreach ($plugins as $key => $value) {
					if(in_array($value, $disableInHome)) unset($plugins[$key]);
				}
			}
		}
	}

	if (isset($_GET['jc_view_plugins']) && $_GET['jc_view_plugins'] == 1) {
		echo "<pre>";
			print_r($plugins);
		echo "</pre>";
	}

	return $plugins;
}

add_filter( 'option_active_plugins', 'desactive_plugin' );
```
