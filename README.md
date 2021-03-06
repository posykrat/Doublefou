# Doublefou

## PHP components

### Breadcrumb

```php
use Doublefou\Components\Breadcrumb;
use Doublefou\Components\BreadcrumbLink;
$breadcrumb = new Breadcrumb();
$newLink = new BreadcrumbLink(
	'http://www.google.fr', //Link target
	'Link name', //Link name
	false //Is current ?
);
$breadcrumb->addLink(
	$newLink, //Link to add
	null //Link position 
);
$breadcrumbLinks = $breadcrumb->getBreadCrumb();
foreach ($breadcrumbLinks as $breadcrumbLink) {
	echo $breadcrumbLink->link;
	echo $breadcrumbLink->current;
	echo $breadcrumbLink->title;
}
```

### CustomMenuCollection

```php
use Doublefou\Components\CustomMenuCollection;
use Doublefou\Components\CustomMenuItem;
$menuCollection = new CustomMenuCollection(
	'menu-header' //Menu slug
);
$menuItems = $menuCollection->getItems();
foreach($menuItems as $menuItem){
	echo $menuItem->getPermalink().'<br>';
	echo $menuItem->getTitle().'<br>';
	echo $menuItem->getParentID().'<br>';
	echo $menuItem->getID().'<br>';
	echo '<hr>';
	if($menuItem->hasChildren()){
		$submenuItems = $menuItem->getCustomMenuCollection()->getItems();
		foreach($submenuItems as $submenuItem){
			echo $submenuItem->getPermalink().'<br>';
			echo $submenuItem->getTitle().'<br>';
			echo $submenuItem->getParentID().'<br>';
			echo $submenuItem->getID().'<br>';
			echo '<hr>';
		}
	}
}
```

### Summary

Construction d'un sommaire automatique à partir des titres <hx> d'un post content
```php
use Doublefou\Components\Summary;
$summaryBuilder = new Summary(
	'2-4', //Title levels, exemple : 1-5
	null //By default watching current post content, you can setup other content like acf fields
);
$summaryItems = $summaryBuilder->getSummary();
if(count($summaryItems) > 0)
{
	foreach($summaryItems as $summaryItem){
		echo $summaryItem->getLevel();
		echo $summaryItem->getID();
		echo $summaryItem->getTitle();
	}
}
```

## PHP Helpers

### CustomPostColumnsManager

Gestion des colonnes de la liste d'un CPT en administration. 
```php
use Doublefou\Helper\CustomPostColumnsManager;
$test = new CustomPostColumnsManager('recette');
$test->addACFColumn('Type','taxonomy','recette_type',true,'15%');
$test->addACFColumn('Note','select','recette_stars',true,'10%');
$test->addACFColumn('Date de parution','default','recette_date',true,'10%');
$test->addACFColumn('Miniature','image','recette_miniature',false,'15%');
$test->removeColumn('date');
```