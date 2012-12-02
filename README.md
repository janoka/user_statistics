# API használata és paraméterezése

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
