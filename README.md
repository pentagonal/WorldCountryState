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
│   ├── Country.json        [Sql Data for country]
│   └── StateAndCountry.sql [Sql Data for country & state]
│
└── State/
    └── ... state|separate|country|code.json
        [list of all state separate by country code (eg: EN.json) uppercase country code]
```
### License
GPL or [Follow The LICENSE](LICENSE)
