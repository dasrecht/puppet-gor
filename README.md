# gor

Puppet module for [Gor](https://github.com/buger/gor/).

Installs Gor, configures an upstart job with the appropriate arguments, and
starts the service. You will need to provide your own `gor` package.

## Example usage

Pass some arguments:
```puppet
class { 'gor':
  args => {
    '-input-raw'             => 'localhost:7999',
    '-output-http-header'    => 'User-Agent: gor',
    '-output-http'           => 'https://staging.example.com',
    '-output-http-redirects' => 2,
    '-output-http-timeout'   => '120s'
  },
}
```

The same argument can be specified multiple times by passing an array:
```puppet
class { 'gor':
  args => {
    …
    '-output-http-method' => [
      'GET', 'HEAD', 'OPTIONS'
    ],
  },
}
```

To install a specific version of the Gor package:
check https://github.com/buger/gor/releases
```puppet
class { 'gor':
  version       => '0.10.1',
  digest_string => '6d7a23e5ae97edec6fa389cdee9546be',
  digest_type   => 'md5',
  …
}
```

To prevent the service from starting:
```puppet
class { 'gor':
  service_ensure => 'stopped',
  …
}
```

To install only the Gor package without having a gor service running:
```puppet
class { 'gor':
  version       => '0.10.1',
  digest_string => '6d7a23e5ae97edec6fa389cdee9546be',
  digest_type   => 'md5'
}
```

To install the Gor package with a gor service but that can only be started manually:
```puppet
class { 'gor':
  version       => '0.10.1',
  digest_string => '6d7a23e5ae97edec6fa389cdee9546be',
  digest_type   => 'md5',
  service_ensure => 'stopped',
  args => {
    '-input-raw'             => 'localhost:7999',
    '-output-http-header'    => 'User-Agent: gor',
    '-output-http'           => 'https://staging.example.com',
    '-output-http-redirects' => 2,
    '-output-http-timeout'   => '120s'
  },
}
```

To install the Gor package with a gor service running that always send requests to https://staging.example.com
```puppet
class { 'gor':
  version       => '0.10.1',
  digest_string => '6d7a23e5ae97edec6fa389cdee9546be',
  digest_type   => 'md5',
  args => {
    '-input-raw'             => 'localhost:7999',
    '-output-http-header'    => 'User-Agent: gor',
    '-output-http'           => 'https://staging.example.com',
    '-output-http-redirects' => 2,
    '-output-http-timeout'   => '120s'
  },
}
```

## License

See [LICENSE](LICENSE) file.
