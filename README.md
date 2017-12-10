# WorldCountryState
World List All Country And State on `json` format


### What is this?

This a repository for list of all country & state / county / province.
The content is separate by `json` files.

### Terms

```
The Repository does not guarantee 100% accurate.
All contents that contained in this repository taken from several sources.
Therefore,
the repository owner has not responsible for the accuracy of the contents of all existing things.
```

### Structure

```
Src/
├── All/
│   ├── Country.json            [list of all countries (without state array key use Country Code)]
│   ├── State.json              [list of all state / province / county (array key use default array inheritance)]
│   ├── StateAndCountry.json    [list of all state & countries (with state array key use Country Code and state on key subdivision)]
│   └── StateByCountryCode.json [list of all state separate by country code (array key use country code and sub array use key as fips_code of state)]
│
├── Country/
│   └── ... country and state |separate|country|code.json
│       [list of all country and state separate by country code (eg: EN.json) uppercase country code]
│
├── CountryNoState/
│   └── ... country|separate|country|code.json
│       [list of all country without state separate by country code (eg: EN.json) uppercase country code]
│
├── SQL/
│   ├── State.sql           [Sql Data for state]
│   ├── Country.sql         [Sql Data for country]
│   └── StateAndCountry.sql [Sql Data for country & state]
│
└── State/
    └── ... state|separate|country|code.json
        [list of all state separate by country code (eg: EN.json) uppercase country code]
```

### Helper

For some reason html output wil be invalid on some browser with certain Character set,
To make sure the text / contents displaying properly, this php function helper to entity the string contents.

```php
/**
 * Entities the Multibytes string
 *  Iconv must be enable to use this function work properly
 *
 * @param string $string the string to detect multibytes
 * @param boolean $entities  true if want to entity the output
 * @return string
 */
function multibyteEntities($string, $entities = true)
{
    static $iconv = null;
    if (!isset($iconv)) {
        // safe resouce check multiple call
        $iconv = function_exists('iconv');
    }

    if (is_array($string)) {
        foreach ($string as $key => $value) {
            $string[$key] = multibyteEntities($value, $entities);
        }
        return $string;
    }

    if (is_object($string)) {
        foreach (get_object_vars($string) as $key => $value) {
            $string->{$key} = multibyteEntities($value, $entities);
        }
        return $string;
    }

    if (!$iconv) { // add \n\r\t as ASCII
        return $entities ? htmlentities(html_entity_decode($string)) : $string;
    }
    /**
     * Work Safe with Parse 4096 Bit | 4KB data split for regex callback & safe memory usage
     * that maybe fail on very long string
     */
    if (strlen($string) >= 4096) {
        return implode('', multibyteEntities(str_split($string, 4096), $entities));
    }
    return preg_replace_callback('/[\x{80}-\x{10FFFF}]/u', function ($m) {
        $char = current($m);
        $utf  = iconv('UTF-8', 'UCS-4//IGNORE', $char);
        return sprintf("&#x%s;", ltrim(strtolower(bin2hex($utf)), "0"));
    }, ($entities ? htmlentities(html_entity_decode($string)) : $string));
}
```

### License
GPL or [Follow The LICENSE](LICENSE)
