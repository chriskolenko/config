config
======

a simple configuration package for Go applications capable of loading
configuration data from [TOML](https://github.com/mojombo/toml) files
and/or environment variables. The package is a simple wrapper around the
[`flag.FlagSet`](http://golang.org/pkg/flag/) package, and can be used
in pretty much the same way.

Credit
------

This is an adaptation of [go-toml-config](https://github.com/stvp/go-toml-config).
Thanks to the original authors for their work.

Example
--------

With `my_app.conf`:

```toml
country = "USA"

[atlanta]
enabled = true
population = 432427
temperature = 99.6
```

Use:

```go
import "github.com/drone/config"

var (
  country            = config.String("country", "Unknown")
  atlantaEnabled     = config.Bool("atlanta-enabled", false)
  alantaPopulation   = config.Int("atlanta-population", 0)
  atlantaTemperature = config.Float("atlanta-temperature", 0)
)

func main() {
  config.SetPrefix("MY_APP_")
  config.Parse("/path/to/my_app.conf")
}
```

By setting the prefix `MY_APP_` you can set or override configuration
with environment variables. For example, `MY_APP_COUNTRY=FR`