# API használata és paraméterezése

A statisztika kihasználja a `cache_get` és `cache_set` Drupal függvényeket, hogy az oldal betöltését gyorsabbá tegye.

## Függvényhívás:

```php
user_statistics_get_statistics($type, $variables = array())
```

Paraméterek:

- `$type` az adott lekérdezés típusa.
- `$variables` tömb, amely a típus változó paraméterezést végzi el.

## Típusok és paramétereik

### Minden felhasználó száma

```php
user_statistics_get_statistics('total_users')
```

### Online felhasználók száma

```php
user_statistics_get_statistics('online_users')
```

### Szerpkör lekérdezése

Példa:

```php
user_statistics_get_statistics('roles_by_rid', array('rid' => 3))
```

Változó paraméter:

- `rid` az adott szerepkör azonosítója. 3-as általában az adminisztrátorokat jelenti.

### Mező értékszerinti lekérdezése

Példa:

```php
user_statistics_get_statistics(
  'fields_by_value',
  array(
    'field_name'  => 'field_nem',
    'field_value' => 'nő',
  )
)
```

Változó paraméter:

- `field_name` a mező neve, ahogy az entity-ben szerepel.
- `field_value` a keresett, mezőhöz hozzárendelt érték.


## Példa form a használatra

![Example](https://raw.github.com/janoka/user_statistics/master/images/user_statistics_example.png)

```php
/**
 * Display global statistics with 'Refresh' button to clear the cache.
 */
function user_statistics_site_statistics_form($form, &$form_state) {
  $items = array(
    'title' => 'Results',
    'items' => array(
      t('Total Users: %data', array('%data' => user_statistics_get_statistics('total_users'))),
      t('Online Users: %data', array('%data' => user_statistics_get_statistics('online_users'))),
      t('Administrators: %data', array('%data' => user_statistics_get_statistics('roles_by_rid', array('rid' => 3)))),
      t('Females: %data', array(
        '%data' => user_statistics_get_statistics('fields_by_value',
          array(
            'field_name'  => 'field_nem',
            'field_value' => 'nő',
          )
        ),
      )),
      t('Males: %data', array(
        '%data' => user_statistics_get_statistics('fields_by_value',
          array(
            'field_name'  => 'field_nem',
            'field_value' => 'férfi',
          )
        ),
      )),
    ),
  );

  // Display form.
  $form = array();
  $form['statistics'] = array(
    '#title'  => 'Statistics',
    '#markup' => theme('item_list', $items),
  );
  $form['submit'] = array(
    '#type' => 'submit',
    '#value' => t('Refresh'),
  );
  return $form;
}
```
